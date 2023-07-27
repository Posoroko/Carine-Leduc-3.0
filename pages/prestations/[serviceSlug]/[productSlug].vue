<script setup>

const route = useRoute();

const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
const directusItems = appConfig.directus.items;

const fetchOptions = {
    server: true,
    params: {
        fields: '*.*',
    }
}

const { data: product } = await useAsyncData(
    `product-${route.params.productSlug}`,
    async () => {
        const items = await $fetch(`${directusItems}Products?filter[slug][_eq]=${route.params.productSlug}`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: true }
)
</script>

<template>
    <PageMain v-if="product">
        <template #header>
            <PageHeaderImage v-if="product.headerImage" :imageId="product.headerImage.id" size="small" />

            <PageTitle :text="product.name" />
        </template>

        <template #main>
            <section class="fullWidthBox">
                <p>product.name</p>
                <p>product.price</p>
                    <PageParagraph v-for="para in product.paragraphs" :key="para.id" :title="para.title" :text="para.content" />
            </section>
        </template>
    </PageMain>
</template>

<style scoped>

</style>