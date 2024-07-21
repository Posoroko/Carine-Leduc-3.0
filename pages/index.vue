<script setup>
const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
const directusItems = appConfig.directus.items;

const fetchOptions = {
    server: true,
    params: {
        // fields: 'id, title, subtitle, content, image, imageAlt, moreInfo, date_created, file, fileName',
    }
}

const { data: pageData } = await useAsyncData(
    "homepage",
    async () => {
        const items = await $fetch(`${directusItems}Pages?filter[id][_eq]=homepage`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: false }
)

</script>

<template>
    <PageMain v-if="pageData">

        <template #header>
            <HomePageHeader :imageId="pageData.headerImage" />
            
            <PageIntroText :text="pageData.introText" />
        </template>

        
        
        <template #main>
            <LazyHomePagePrestations />

            <LazyHomePageAbout />
        </template>
    </PageMain>
</template>

<style scoped>

</style>