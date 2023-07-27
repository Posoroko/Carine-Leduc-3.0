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
    "aboutPageData",
    async () => {
        const items = await $fetch(`${directusItems}Pages?filter[id][_eq]=about`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: true }
)

const { data: aboutData } = await useAsyncData(
    "aboutData",
    async () => {
        const items = await $fetch(`${directusItems}About`, fetchOptions)

        return items.data
    }
    ,
    { server: true }
)
</script>

<template>
    <PageMain v-if="pageData">

            <template #header>
                <PageHeaderImage :imageId="pageData.headerImage" size="small" />

                <PageTitle text="A propos de moi ..." />
            
                <PageIntroText :text="pageData.introText" size="small" />
            </template>

            <template #main>
                <ul class="fullWidthBox flex column gap50 ">
                    <li v-for="item in aboutData" :key="item.id">
                        <CardLevelOne
                            :title="item.title"
                            :text="item.teaser"
                            :url="`a-propos/${item.slug}`"
                            :imageId="item.cardImage"
                            :imageAlt="`Carine Laduc, thérapeute énergétitienn, ${item.name}`"/>
                    </li>
                </ul>
            </template>
        </PageMain>
</template>

<style scoped>


</style>