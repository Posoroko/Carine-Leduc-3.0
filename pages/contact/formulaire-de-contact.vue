<script setup>

const route = useRoute();

const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
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

        <template #main>
            <PageTitle class="marTop50" text="Formulaire de contact" />

            <div class="narrowWidth marTop50">
                <WidgetContactForm />
            </div>

        </template>
    </PageMain>
</template>
<style scoped></style>