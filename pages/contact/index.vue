<script setup>

const route = useRoute();

const appConfig = useAppConfig();
const directusItems = appConfig.directus.items;

const fetchOptions = {
    server: true,
    params: {
        // fields: 'id, title, subtitle, content, image, imageAlt, moreInfo, date_created, file, fileName',
    }
}

const { data: contact } = await useAsyncData(
    "contactData",
    async () => {
        const items = await $fetch(`${directusItems}Contact`, fetchOptions)

        return items.data
    }
    ,
    { server: true }
)

</script>

<template>
    <PageMain>
        <template #headerImage>
            <SectionTitle title="Contact" />
        </template>

        <template #main>
            <div class="narrowWidth lightText bodyTitle centered">
                <NuxtLink class="formulaireLink BGC_Brand2_Hoverable pointer" to="/contact/formulaire-de-contact">formulaire de contact</NuxtLink>
            </div>

            <WidgetSchedule v-if="contact" :schedule="contact.schedule" />

            <div class="narrowWidth marTop20">
                <address class="contactBox flex column gap20 alignStart">
                    <p class="name ">{{ contact.name }}</p>

                    <div class="flex alignCenter wrap gap50">
                        <p class="address contactInfoFont">{{ contact.address }}</p>

                        <a class="mapLink pointer address flex alignCenter gap10"
                            :href="`http://maps.google.com/?q=${contact.address}`" target="_blank">
                            <span>repérer sur la carte</span> <span class="icon">search</span>
                        </a>
                    </div>

                    <div class="flex column gap20">
                        <p class="contactInfoFont">informations :</p>

                        <a :href="`mailto:${contact.email}`" class="contactInfoFont pointer">{{ contact.email }}</a>

                        <a :href="`tel:${contact.telFixe}`" class="contactInfoFont pointer flex alignCenter gap10"><span
                                class="icon">call</span> fixe: {{ contact.telFixe }}</a>

                        <a :href="`tel:${contact.telPortable}`" class="contactInfoFont pointer flex alignCenter gap10"><span
                                class="icon">call</span> portable:{{ contact.telPortable }}</a>
                    </div>
                </address>
            </div>
        </template>
    </PageMain>
</template>
<style scoped>
.formulaireLink {
    padding: 10px 30px;
    border-radius: 10px;
}
.contactInfoFont {
    color: var(--text-color);
    font-family: "Montserrat", sans-serif;
    font-size: clamp(2rem, 2.5vw, 3rem);
}

.name {
    font-family: var(--title-font), sans-serif;
    font-size: 30px;
    font-weight: 700;
}

.address {
    white-space: pre-wrap;
}

.mapLink {
    font-family: "Montserrat", sans-serif;
    font-size: 20px;
    font-weight: 700;
    color: var(--basic-light-color);
    background-color: var(--brand-color-2);
    padding: 10px 15px;
    border: 1px solid var(--brand-color-2);
    border-radius: 100px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.407);
    transition: 100ms ease;
}

.mapLink:hover {
    background-color: var(--brand-color-2-hover);
    box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.816);
    transition: 100ms ease;
}

.mapLink:hover .icon {
    transform: rotateZ(360deg);
    transition: 1000ms ease;
}

a.mapLink {
    background-color: var(--brand-color-2-hover);

}

.narrowWidth {
    padding: 50px;
    border: 1px solid var(--brand-color-1);
}</style>