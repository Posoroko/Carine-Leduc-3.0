<script setup>

const route = useRoute();

const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
const directusItems = appConfig.directus.items;

const fetchOptions = {
    server: true,
    params: {
        fields: 'type, type.name, *.*',
    }
}
const { data: service } = await useAsyncData(
    `service-${route.params.slug}`,
    async () => {
        const items = await $fetch(`${directusItems}Services?filter[slug][_eq]=${route.params.serviceSlug}`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: true }
)

const { data: products } = await useAsyncData(
    `products-${route.params.serviceSlug}`,
    async () => {
        const items = await $fetch(`${directusItems}Products?filter[type][slug][_eq]=${route.params.serviceSlug}`, fetchOptions)
        console.log(route.params.serviceSlug)
        
        return items.data
    }
    ,
    { server: true }
)
</script>

<template>
    
    <PageMain v-if="service && products">
        <template #header>
            
            <PageHeaderImage :imageId="service.headerImage.id" size="small" />

            <PageTitle :text="service.name" />

            <PageIntroText :text="service.introText" />
        </template>

        <template #main>
            <section class="fullWidthBox">
                <div class="mainWidth productsBoard flex column gap20">
                    <p>Voici mes {{ products.length }} propositions de {{ service.name }}.</p>

                    <ul class="flex column gap50">
                        <li v-for="prod in products" :key="prod.id">
                            <CardLevelTwo 
                                :title="prod.name"
                                :text="prod.teaser"
                                :url="`/prestation/${route.params.serviceSlug}/${prod.slug}`"
                                :imageId="prod.cardImage.id"
                                :imageAlt="`${prod.name}, par Carine Leduc, thérapeute énergétitienne.`"/>
                        </li>
                    </ul>
                </div>
            </section>
        </template>
    </PageMain>
</template>

<style scoped>

</style>