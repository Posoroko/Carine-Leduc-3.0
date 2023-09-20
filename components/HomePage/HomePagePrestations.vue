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
    <section class="fullWidthBox">
        <PageTitle text="Prestations" color="var(--basic-dark-color)"/>

        <div class="cardsBox flex justifyCenter wrap">

            <NuxtLink :to="`/prestations/${service.slug}`" class="card rightArrowHover relative flex column  pointer" v-for="service in services" :key="service.id">
                <div class="frame" >
                    <img class="cardImage" v-if="service.cardImage" :src="`${directusAssets}${service.cardImage}?key=350px`" alt="Soins énergétique par Carine Leduc">
                </div>

                <div class="textBox flex column justifyBetween">

                    <div>
                        <p class="cardTitle lightText">{{ service.name }}</p>

                        <p class="cardTeaser lightText">
                            {{ service.teaser }}
                        </p>
                    </div>

                    <WidgetRightArrow />
                </div>
            </NuxtLink>
        </div>
    </section>
</template>

<style>
:root {
    --card-width: 350px;
}
</style>

<style scoped>

.cardsBox {
    width: min(100%, calc(var(--card-width) * 3.5));
    padding: 40px 20px;
    /* border: 4px solid var(--brand-color-1);
    outline: 2px solid var(--brand-color-1); */
    outline-offset: -8px;
    margin: 50px auto;
    align-items: stretch;
    gap: 50px;
    /* box-shadow: 1px 1px 5px 0px rgba(0, 0, 0, 0.351); */
}
.card {
    width: min(95vw, var(--card-width));
    background-color: var(--brand-color-1);
    border-radius: 5px;
    transition: 300ms ease;
    box-shadow: 1px 1px 10px 0px rgba(0,0,0,0.75);
}
.card:hover {
    transform: scale(1.02);
    transition: 300ms ease;
}
.frame {
    width: 100%;
    aspect-ratio: 1/1;
    overflow: hidden;
}
.cardImage{
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
}
.textBox {
    width: 100%;
    padding: 20px;
    flex-grow: 1;
}
.cardTitle {
    font-family: var(--title-font);
    font-size: clamp(2.8rem, 4.5vw + 0.1rem, 3.5rem);
    font-weight: 700;
    color: var(--basic-light-color);
    line-height: 1.2;
    white-space: pre-wrap;
}
.cardTeaser {
    font-family: var(--text-font);
    font-size: 24px;
    font-weight: 300;
    color: var(--basic-light-color);
    line-height: 1.3;
    white-space: pre-wrap;
    margin-top: 30px;
}
</style>