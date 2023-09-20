<script setup>
const appConfig = useAppConfig();
const directusItems = appConfig.directus.items;
const mailCollection = directusItems + 'mail';
console.log(mailCollection)

const submitPending = ref(false)

const htmlForm = ref(null)

const formData = ref({
    name: '',
    email: '',
    message: '',
});

const errors = ref({
    name: null,
    email: null,
    message: null,
});
const messages = ref({})

const validateForm = () => {

    // Validate name field
    if (formData.value.name.length > 50 || formData.value.name.length < 2) {
        errors.value.name = 'Votre nom doit contenir entre 2 et 50 caractères';
    } else {
        errors.value.name = null;
    }

    // Validate email field using a regular expression
    const emailRegex = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
    if (!emailRegex.test(formData.value.email) || formData.value.email.length > 320 || formData.value.email.length < 5) {
        errors.value.email = 'Votre adresse mail doit contenir entre 5 et 320 caractères et être au bon format "';
    } else {
        errors.value.email = null;
    }

    // Validate message field
    if (formData.value.message.length > 500 || formData.value.message.length < 25) {
        errors.value.message = 'Votre message doit contenir entre 25 et 500 caractères';
    } else {
        errors.value.message = null;
    }

    if(errors.value.name || errors.value.email || errors.value.message) {
        return false
    } else {
        return true
    }
};

const submitForm = async () => {
    submitPending.value = true

    const validationErrors = errors.value

    if (!validateForm()) {
        // Handle form validation errors (e.g., display error messages)
        console.error('Form validation errors:', validationErrors);

        submitPending.value = false
        return;
    }

    try {
        const response = await fetch(mailCollection, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(formData.value),
        });

        if (response.ok) {
            const responseData = await response.json();
            // Handle the response data as needed
            console.log(responseData);
        } else {
            // Handle HTTP error
            console.error('HTTP Error:', response.status);
        }
    } catch (error) {
        // Handle any errors that occur during the request
        console.error(error);
    }
    messages.value.success = 'Votre message a bien été envoyé, je vous recontacterai très rapidement.'
    formData.value.name = ''
    formData.value.email = ''
    formData.value.message = ''
    submitPending.value = false
};
</script>

<template>
    <p class="formIntroText">Pour demander un <b>rendez-vous</b> ou simplement poser une question écrivez moi un petit message et je reviendrai vers vous très rapidement.</p>

    <form :ref="htmlForm" @subit.prevent class="flex column marTop20">
        <div class="formRow marTop20">
          <label class="darkText titleFont" for="name">Nom:</label>

          <input class="darkText bodyText2" type="text" id="name" v-model="formData.name" />
        </div>

        <div class="formRow marTop20">
          <label class="darkText titleFont" for="email">Adresse mail:</label>

          <input class="darkText bodyText2" type="email " id="email" v-model="formData.email" />
        </div>

        <div class="formRow marTop20">
            <label class="darkText titleFont" for="message">Votre message</label>

            <textarea class="darkText bodyText2" rows="6" id="message" v-model="formData.message"></textarea>
        </div>

        <div class="w100 centered pad20">
            <p class="errorMessage" v-if="errors.name">{{ errors.name }}</p>
            <p class="errorMessage" v-if="errors.email">{{ errors.email }}</p>
            <p class="errorMessage" v-if="errors.message">{{ errors.message }}</p>
            <p class="successMessage" v-if="messages.success">{{ messages.success }}</p>
        </div>
    
        <button @click.prevent="submitForm" class="formButton BGC_Brand2_Hoverable lightText bodyText2" v-if="!submitPending">envoyer</button>
        <button class="formButton BGC_Brand2_Hoverable lightText bodyText2" v-if="submitPending" disabled>patientez</button>
    </form>
</template>

<style scoped>
.formIntroText {
    color: var(--text-color);
    font-family: "Montserrat", sans-serif;
    font-size: clamp(2rem, 2.5vw, 3rem);
}
.formRow {
    width: 100%;
    display: flex;
    flex-direction: column;
}
label {
    font-size: clamp(1.8rem, 2vw + 0.1rem, 2.8rem);
    padding-left: 20px;
}
textarea, input {
    background-color: transparent;
    border-radius: 10px;
    padding: 20px;
    border: 2px solid rgba(53, 71, 53, 0.304);
    resize: vertical;
}
button {
    padding: 2px 12px;
    margin: 20px auto;
    border-radius: 5px;
    cursor: pointer;
    box-shadow: 2px 2px 5px black;
}
.errorMessage {
    font-size: clamp(1.4rem, 1.5vw + 0.1rem, 2.0rem);
    color: red;
}
.successMessage {
    font-size: clamp(1.4rem, 1.5vw + 0.1rem, 2.0rem);
    color: green;
}
</style>