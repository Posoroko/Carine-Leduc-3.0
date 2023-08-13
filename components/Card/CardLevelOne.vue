<script setup>
const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;

const props = defineProps({
    title: String,
    text: String,
    url: String,
    imageId: String,
    imageAlt: String,
})

</script>

<template>
    <article class="mainWidth cardBox rightArrowHover">
        <NuxtLink :to="url" class="card relative block pointer flex">
            <div class="leftBox">

            </div>

            <div class="frame centered">
                <img class="cardImage" :src="`${directusAssets}${imageId}?key=220px`" :alt="imageAlt">
            </div>

            <div class="textBox flex column justifyBetween">
                <h2 class="cardTitle lightText">{{ title }}</h2>

                <p class="cardText lightText">{{ text }}</p>

                <WidgetRightArrow />
            </div>
        </NuxtLink>
    </article>
</template>

<style scoped>
.card {
    isolation: isolate;
    
}

.leftBox,
.textBox,
.frame{
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.493);
    transition: 300ms ease;
}
.cardBox:hover .leftBox,
.cardBox:hover .textBox,
.cardBox:hover .frame{
    background-color: var(--brand-color-1-hover);
    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.788);
    transition: 300ms ease;
}
.cardBox:hover .cardImage{
    transform: scale(1.02);
    transition: 300ms ease;
    z-index: 1;
}

.leftBox {
    width: min(10%, 60px);
    background-color: var(--brand-color-1);
    margin: 20px 0px 20px 20px;
}
.frame {
    width: 20%;
    /* min-height: 250px; */
    aspect-ratio: 1/1;
    border-radius: 5px;
    overflow: hidden;
}
.cardImage {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    transition: 300ms ease;
}
.textBox {
    width: 65%;
    background-color: var(--brand-color-1);
    margin: 20px 20px 20px 0;
    padding: 40px 40px 20px 40px;
    flex-grow: 1;
    z-index: -1;
}
.cardTitle {
    font-family: var(--title-font);
    font-size: clamp(3rem, 4vw + 0.1rem, 4rem);
}
.cardText {
    font-family: var(--text-font);
    font-size: clamp(2rem, 2.5vw + 0.1rem, 2.8rem);
    margin-top: 25px;
}

@media (max-width: 760px) {
    .card {
        flex-wrap: wrap;
    }

    .leftBox {
        display: none;
    }
}
@media (max-width: 600px) {
    .card {
        flex-direction: column;
    }
    .frame {
        width: 100%;
        height: 250px;
    }
    .textBox {
        width: 100%;
        margin-top: 0;
    }
 
}

</style>