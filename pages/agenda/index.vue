<script setup>

const route = useRoute();

const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
const directusItems = appConfig.directus.items;

const fetchOptions = {
    server: true,
    params: {
        // fields: 'type, type.name, *.*',
    }
}
const { data: pageData } = await useAsyncData(
    `agendaPageData`,
    async () => {
        const items = await $fetch(`${directusItems}Pages?filter[id][_eq]=agenda`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: true }
)

const { data: agenda } = await useAsyncData(
    `agenda`,
    async () => {
        const items = await $fetch(`${directusItems}Agenda`, fetchOptions)

        return items.data
    }
    ,
    { server: true }
)

</script>

<template>
    <PageMain v-if="pageData && agenda">
        <template #header>
            <PageHeaderImage :imageId="pageData.headerImage" size="small" />

            <PageTitle :text="pageData.title" />

            <PageIntroText :text="pageData.introText" />
        </template>

        <template #main>
            <section class="fullWidthBox">
                <div class="mainWidth productsBoard flex column gap20">
                    <NuxtLink class="card pointer" :to="`/agenda/${date.slug}`"
                        v-for="date in agenda" :key="date.id">
                        <p class="cardTitle"> {{ date.title }}</p>
                    </NuxtLink>
                </div>
            </section>
        </template>
    </PageMain>
</template>

<style scoped>
.productsBoard {}
</style>