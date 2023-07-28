<script setup>

const route = useRoute();

const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
const directusItems = appConfig.directus.items;

const fetchOptions = {
    server: true,
    params: {
        fields: 'id, title, introText, cardImage, headerImage, paragraphs.*',
    }
}

const { data: pageData } = await useAsyncData(
    `about-${route.params.slug}`,
    async () => {
        const items = await $fetch(`${directusItems}About?filter[slug][_eq]=${route.params.slug}`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: true }
)
</script>

<template>
    <PageMain v-if="pageData">

            <template #header>
                <PageHeaderImage :imageId="pageData.headerImage" size="small" />
                
                <PageTitle :text="pageData.title" />
                
                <PageIntroText :text="pageData.introText" />
            </template>

            <template #main>
                <section class="fullWidthBox">
                    <PageParagraph v-for="para in pageData.paragraphs" :key="para.id" 
                        :title="para.title" 
                        :text="para.content" 
                        :imageId="para.image"
                        :imageAlt="para.imageAlt"/>
                </section>
            </template>
        </PageMain>
</template>

<style scoped>
.bodyText2 {
    width: min(100%, 80ch);
    text-align: justify;
    padding: 30px;
    columns: 2;
    gap: 60px;
    margin: 0 auto;
}
@media (max-width: 768px) {
    .bodyText2 {
        columns: 1;
    }
}
.firstLetter {
    color: var(--brand-color-2);
    font-size: 100px;
    line-height: 0.5;
    float: left;
    display: block;
    padding: 10px 5px 0 0 ;
    /* height: 100px; */
}
</style>