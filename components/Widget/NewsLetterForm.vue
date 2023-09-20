<script setup>
const appConfig = useAppConfig();
const directusItems = appConfig.directus.items;
const newsLetterCollection = directusItems + 'mail';
console.log(newsLetterCollection)

const submitPending = ref(false)

const htmlForm = ref(null)

const formData = ref({
    email: '',
});

const errors = ref({
    email: null,
});
const messages = ref({})

const validateForm = () => {


    // Validate email field using a regular expression
    const emailRegex = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
    if (!emailRegex.test(formData.value.email) || formData.value.email.length > 320 || formData.value.email.length < 5) {
        errors.value.email = 'Votre adresse mail doit contenir entre 5 et 320 caractères et être au bon format "';
    } else {
        errors.value.email = null;
    }

    if (errors.value.email) {
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
        const response = await fetch(newsLetterCollection, {
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
    messages.value.success = "J'ai bien noté votre adresse mail, merci !"
    formData.value.name = ''
    formData.value.email = ''
    formData.value.message = ''
    submitPending.value = false
};
</script>

<template>
    <div class="box narrowWidth centered marTop100 ">
        <p class="formIntroText lightText centered">Inscrivez-vous à ma news letter <br> pour rester informé !</p>

        <form :ref="htmlForm" @subit.prevent class=" lightText flex column marTop20 w100">

            <div class="formRow marTop20 w100">
                <label class=" titleFont" for="email">Adresse mail:</label>

                <input class=" bodyText2 w100 lightText marTop20" type="email " id="email" v-model="formData.email" />
            </div>

            <div class="w100 centered pad20">
                <p class="errorMessage" v-if="errors.email">{{ errors.email }}</p>

                <p class="successMessage " v-if="messages.success">{{ messages.success }}</p>
            </div>

            <button @click.prevent="submitForm" class="formButton BGC_Brand2_Hoverable lightText bodyText2"
                v-if="!submitPending">envoyer</button>
            <button class="formButton BGC_Brand2_Hoverable lightText bodyText2" v-if="submitPending" disabled>patientez</button>
        </form>
    </div>
</template>

<style scoped>
.box {
    background-color: var(--brand-color-1);
    padding: 50px;
    border-radius: 10px;
    box-shadow: 2px 2px 6px rgba(0, 0, 0, 0.341);
}
.formIntroText {

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

textarea,
input {
    background-color: transparent;
    border-radius: 10px;
    padding: 20px;
    border: 2px solid var(--basic-light-color);
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
    color: var(--basic-light-color);
}</style>