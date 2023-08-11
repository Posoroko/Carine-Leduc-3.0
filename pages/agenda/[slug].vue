<script setup>
const route = useRoute();

const appConfig = useAppConfig();
const directusItems = appConfig.directus.items;

const fetchOptions = {
    server: true,
    params: {
        // fields: 'type, type.name, *.*',
    }
}
const { data: date } = await useAsyncData(
    `agenda-${route.params.slug}`,
    async () => {
        const items = await $fetch(`${directusItems}Agenda?filter[slug][_eq]=${route.params.slug}`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: true }
)

function toFrenchFormat(date) {
    let months = ["Janvier", "Février", "Mars", "Avril", "Mai", "Juin", "Juillet", "Aout", "Septembre", "Octobre", "Novemebre", "Décembre"]
    let _date = new Date(date)
    let day = _date.getDate();
    let month = months[_date.getMonth()];
    let year = _date.getFullYear();

    return `${day} ${month} ${year}`;
}


let cardWidth = 265;

</script>

<template>
    <PageMain v-if="date">
        <template #header>
            <PageTitle :text="date.title" />
        </template>

        <template #main>
            <p class="date">{{ toFrenchFormat(date.date) }}</p>
            <p></p>
        </template>
    </PageMain>
</template>

<style scoped>
.drawer {
    width: auto;
    /* overflow: visible; */
    transform: v-bind("drawerClass");
    transition: 300ms ease;
    padding-left: 20px;
}

.agendaText {
    font-family: "EB Garamond", sans-serif;
    color: var(--basic-light-color);
}

.card {
    width: min(90vw, 300px);
    padding: 40px;
    border-radius: 10px;
    /* flex-shrink: 0; */
}

.date {
    font-size: clamp(2rem, 2.5vw, 2.8rem);
}

.cardTitle {
    font-family: var(--title-font);
    font-size: clamp(3rem, 4.5vw, 4rem);
    font-weight: 700;
}

.cardText {
    font-size: clamp(2rem, 2vw, 2.6rem);
    line-height: 1.5;
}</style>