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
        const items = await $fetch(`${directusItems}About?filter[slug][_eq]=${route.params.slug}`, fetchOptions)
        console.log(items.data[0])
        return items.data[0]
    }
    ,
    { server: true }
)
</script>

<template>
    <PageMain v-if="pageData">

            <template #header>
                <PageHeaderImage :imageId="pageData.headerImage" size="large" />
                
                <PageTitle :text="pageData.title" />
                
                <PageIntroText :text="pageData.introText" />
            </template>

        
        
            <template #main>
                <section class="fullWidthBox">
                    <PageTwoColumnsParagraph v-if="pageData.paragraph1" :text="pageData.paragraph1" />

                    <p class="bodyText2" v-if="pageData.paragraph2">
                        <span class="firstLetter">{{ pageData.paragraph2[0] }}</span>
                        {{ pageData.paragraph2.slice(1, 10000) }}
                    </p>

                    <p class="bodyText2" v-if="pageData.paragraph3">
                        <span class="firstLetter">{{ pageData.paragraph3[0] }}</span>
                        {{ pageData.paragraph3.slice(1, 10000) }}
                    </p>
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