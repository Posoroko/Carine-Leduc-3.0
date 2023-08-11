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
const { data: aboutPageData } = await useAsyncData(
    "aboutPageData",
    async () => {
        const items = await $fetch(`${directusItems}Pages?filter[id][_eq]=about`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: true }
)

const { data: aboutItems } = await useAsyncData(
    "homepageAbout",
    async () => {
        const items = await $fetch(`${directusItems}About`, fetchOptions)
        
        return items.data
    }
    ,
    { server: true }
)

</script>

<template>
    <section class="fullWidthBox" v-if="aboutPageData && aboutItems">
        
        
        <div class="about mainWidth flex column gap20 marTop50">
            <div class="cardBox ">
                <NuxtLink class="card rightArrowHover relative titleCard" to="/a-propos">
                    <img class="titleCardImage full objectFitCover" :src="`${directusAssets}${aboutPageData.headerImage}`" alt="">
                    
                    <span class="aboutTextBox block absoluteFull flex column justifyBetween">
                        <h2 class="aboutTitle">{{ aboutPageData.title }}</h2>

                        <p class="bodyText2 lightText introText">{{ aboutPageData.introText }}</p>

                        <WidgetRightArrow />
                    </span>
                </NuxtLink>
 
                <NuxtLink v-for="item in aboutItems" :key="item.id" :to="`a-propos/${item.slug}`" class="card rightArrowHover">
                    <div class="frame">
                        <img class="cardImage" :src="`${directusAssets}${item.cardImage}`" alt="">
                    </div>

                    <div class="textBox">
                        <p class="cardTitle">{{ item.title }}</p>

                        <p class="cardTeaser">{{ item.teaser }}</p>

                        <div class="arrowBox">
                            <WidgetRightArrow />
                        </div>
                    </div>
                </NuxtLink>
            </div>
        </div>
    </section>
</template>

<style scoped>
.cardBox {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 20px;
}
.card {
    width: calc(50% - 20px);
    border-radius: 7px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    cursor: pointer;
    box-shadow: 0 0 6px rgba(0, 0, 0, 0.682);
    transition: 300ms ease;

}
@media (max-width: 760px) {
    .card {
        width: min(100%, 450px);
    }
}
.card:hover {
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.775);
    transform: scale(1.01);
    transition: 300ms ease;
}
.titleCardImage {
    opacity: 0.7;
    filter: brightness(0.5) blur(2px) contrast(1.5);
}
.aboutTextBox {
    background-color: rgba(24, 64, 26, 0.455);
    padding: 50px;
    display: flex;
    flex-direction: column;
    justify-content: space-Evenly;
}
.aboutTitle {
    font-family: var(--title-font);
    font-size: clamp(3rem, 4vw, 5rem);
    color: var(--basic-light-color);
}
.frame {
    width: 100%;
    height: 300px;
}

img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
}
.textBox {
    background-color: var(--brand-color-1);
    padding: 30px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex-grow: 1;
}
.cardTitle {
    font-family: var(--title-font);
    font-size: clamp(2rem, 2.5vw, 4.5rem);
    color: var(--basic-light-color);
}
.cardTeaser {
    font-family: var(--text-font);
    font-size: clamp(1.8rem, 2vw, 2.4rem);
    color: var(--basic-light-color);
    margin-top: 20px;
}
.arrowBox {
    padding: 20px 10px 0 0;
}
</style>