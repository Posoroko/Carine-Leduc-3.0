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
const { data: pageData } = await useAsyncData(
    "pageData",
    async () => {
        const items = await $fetch(`${directusItems}Pages?filter[id][_eq]=services`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: true }
)

const { data: services } = await useAsyncData(
    "services",
    async () => {
        const items = await $fetch(`${directusItems}Services`, fetchOptions)
        
        return items.data
    }
    ,
    { server: true }
)
</script>

<template>
    <PageMain v-if="pageData && services">
        <template #header>
            <PageHeaderImage :imageId="pageData.headerImage" size="small" />
        
            <PageTitle :text="pageData.title" />
        
            <PageIntroText :text="pageData.introText" />
        </template>

        <template #main>
            <ul class="fullWidthBox flex column gap50">
                <li class="mainWidth serviceBox" v-for="service in services" :key="service.id">
                    <CardLevelOne  :title="service.name" 
                            :text="service.teaser"
                            :imageId="service.cardImage"
                            :imageAlt="`${service.name} avec Carine Leduc, thérapeute énergétitienne.`"
                            :url="`/prestations/${service.slug}`"/>
                </li>
            </ul>
        </template>
    </PageMain>
</template>

<style scoped>

</style>