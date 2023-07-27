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
function toFrenchFormat(date) {
    let _date = new Date(date)
    let day = _date.getDate();
    let month = _date.getMonth() + 1;
    let year = _date.getFullYear();

    return `${day}/${month}/${year}`;
}

let drawer = ref(null)
let offset = ref(0)
let drawerClass = computed(() => {
    return `translateX(${offset.value}px)`
})

function navigate(way) {
    if(way == "left") {
        offset.value -= cardWidth;
        return
    }
    if(offset.value < 0) {
        offset.value += cardWidth;
    }
}


let cardWidth = 265;

</script>

<template>
    <PageMain v-if="pageData && agenda">
        <template #header>
            <PageHeaderImage :imageId="pageData.headerImage" size="small" />

            <PageTitle :text="pageData.title" />

            <PageIntroText :text="pageData.introText" />
        </template>

        <template #main>
            <section class="fullWidthBox relative">
                <div class="drawer flex gap20 relative" ref="drawer">
                    <NuxtLink class="card pointer flex column justifyBetween BGC_Brand2_Hoverable rightArrowHover" :to="`/agenda/${date.slug}`" v-for="date in agenda" :key="date.id">
                        <div>
                            <p class="date">{{ toFrenchFormat(date.date) }}</p>
                
                            <p class="where">{{ date.where }}</p>
                
                            <p class="cardTitle marTop50"> {{ date.title }}</p>
                        </div>

                        <p class="cardText bodyText2 marTop50">{{ date.description.slice(0, 100) }} ...</p>

                        <WidgetRightArrow />
                    </NuxtLink>
                </div>

                <WidgetLeftRightNavigation @navigate="navigate" />
            </section>
        </template>
    </PageMain>
</template>

<style scoped>
.drawer {
    transform: v-bind("drawerClass");
    transition: 300ms ease;
}
* {
    font-family: "EB Garamond", sans-serif;
    color: var(--basic-light-color);
}
.card {
    width: 265px;
    padding: 40px;
    border-radius: 10px;

}
.date {
    font-size: clamp(2rem, 2.5vw, 2.8rem);
}
.cardTitle {
    font-family: var(--title-font);
    font-size: clamp(2.4rem, 3vw, 3.5rem);
    font-weight: 700;
}
.cardText {
    /* height: 4em; */
}
</style>