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

const { data: pageData } = await useAsyncData(
    "homepageAbout",
    async () => {
        const items = await $fetch(`${directusItems}About`, fetchOptions)
        const temp = {
            carine: null,
            techniques: null,
            cabinet: null
        }

        temp.carine = items.data.filter(item => item.id === 'carine')[0]
        temp.techniques = items.data.filter(item => item.id === 'techniques')[0]
        temp.cabinet = items.data.filter(item => item.id === 'cabinet')[0]

        console.log(temp)
        return temp
    }
    ,
    { server: true }
)

</script>

<template>
    <section class="fullWidthBox" v-if="pageData">
        
        
        <div class="about mainWidth flex column gap20 marTop50">
            <div class="cardBox ">
                <NuxtLink class="card relative titleCard" to="/a-propos">
                    <img class="titleCardImage full objectFitCover" :src="`${directusAssets}${aboutPageData.headerImage}`" alt="">
                    
                    <span class="aboutTextBox block absoluteFull flex column justifyBetween">
                        <h2 class="aboutTitle">{{ aboutPageData.title }}</h2>

                        <p class="bodyText2 lightText introText">{{ aboutPageData.introText }}</p>

                        <div class="buttonBox">
                            <p class="bodyText2 lightText">voir la page</p>
                        </div>
                    </span>
                </NuxtLink>
 
                <NuxtLink :to="`a-propos/${pageData.carine.slug}`" class="card">
                    <div class="frame">
                        <img class="cardImage" :src="`${directusAssets}${pageData.carine.cardImage}`" alt="">
                    </div>

                    <div class="textBox">
                        <p class="cardTitle">Moi</p>

                        <p class="cardTeaser">{{ pageData.cabinet.teaser }}</p>

                        <div class="buttonBox">
                            <WidgetCardReadMoreButton url="/a-propos/le-cabinet"/>
                        </div>
                    </div>
                </NuxtLink>
            </div>

            <div class="cardBox">
                <NuxtLink :to="`a-propos/${pageData.techniques.slug}`" class="card ">
                    <div class="frame">
                        <img class="" :src="`${directusAssets}${pageData.techniques.cardImage}`" alt="">
                    </div>

                    <div class="textBox">
                        <p class="cardTitle">Mes techniques</p>
                            
                        <p class="cardTeaser">{{ pageData.cabinet.teaser }}</p>

                        <div class="buttonBox">
                            <WidgetCardReadMoreButton url="/a-propos/le-cabinet"/>
                        </div>
                    </div>
                </NuxtLink>

                <NuxtLink :to="`a-propos/${pageData.cabinet.slug}`" class="card">
                    <div class="frame">
                        <img class="cardImage" :src="`${directusAssets}${pageData.cabinet.cardImage}`" alt="">
                    </div>

                    <div class="textBox">
                        <p class="cardTitle">Le cabinet</p>

                        <p class="cardTeaser">{{ pageData.cabinet.teaser }}</p>

                        <div class="buttonBox">
                            <WidgetCardReadMoreButton url="/a-propos/le-cabinet"/>
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
.buttonBox {
    margin-top: 20px;
    display: flex;
    justify-content: flex-end;
}
</style>