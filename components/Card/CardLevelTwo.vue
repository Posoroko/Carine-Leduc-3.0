<script setup>
const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;

const props = defineProps({
    title: String,
    text: String,
    url: String,
    imageId: String,
    imageAlt: String,
    price: String,
    length: String
})
</script>

<template>
    <div class="container relative flex alignCenter rightArrowHover">
        <div class="halfMandalaBox">
            <DecoHalfMandala1 />
        </div>

        <NuxtLink :to="url" class="card flex wrap pointer relative">
            <div class="textBox flex column justifyBetween lightText">
                <div class="inline spaceBetween gap50">
                    <h2 class="cardTitle">{{ title }}</h2>

                    <span class="bodyText1">{{ price }}€ - {{ length }}</span>
                </div>

                <p class="cardTeaser">{{ text }}</p>

                <WidgetRightArrow class="marTop20" />
            </div>

            

            <div class="cardFrame">
                <img class="cardImage" :src="`${directusAssets}${imageId}`" :alt="imageAlt">
            </div>
        </NuxtLink>
    </div>
</template>

<style scoped>
.halfMandalaBox {
    height: 200px;
    opacity: 0.3;
    transform: translateX(50%);
    transition: 300ms ease;
    z-index: -1;
}
.container:hover .halfMandalaBox {
    transform: translateX(25%);
    transition: 1200ms 150ms cubic-bezier(.08,.85,.35,.98);
}

.card {
    border: 4px solid var(--brand-color-2);
    border-radius: 5px;
    margin: auto;
    box-shadow: 0px 0px 10px 0 rgba(0, 0, 0, 0.433);
    transition: 300ms ease;
}
.card:hover {
    box-shadow: 2px 2px 10px 0 rgba(0, 0, 0, 0.83);
    transition: 300ms ease;
}
.card:hover .textBox{
    background-color: var(--brand-color-2-hover);
        transition: 300ms ease;
}
.card:hover .cardImage {
    box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.927);
    transform: scale(1.02);
    transition: 300ms ease-in;
}
.textBox {
    width: 60%;
    background-color: var(--brand-color-2);
    padding: 50px 70px 20px 30px;
    transition: 300ms ease;
    display: flex;
    flex-direction: column;
    gap: 20px;
}


.cardTitle {
    font-family: var(--title-font);
    font-size: clamp(3rem, 4vw + 0.1rem, 4.5rem);
    font-weight: 700;
    color: var(--basic-light-color);
    line-height: 1.2;
}
.cardTeaser {
    font-family: var(--text-font);
    font-size: clamp(1.8rem, 2vw + 0.1rem, 2.8rem);
    font-weight: 300;
    color: var(--basic-light-color);
    line-height: 1.4;
    white-space: pre-wrap;
}
.cardFrame {
    width: 40%;
    padding: 20px 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-end;
}
.cardImage {
    width: 110%;
    aspect-ratio: 5/3;
    object-fit: cover;
    object-position: center;
    border-radius: 5px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.559);
    transition: 300ms ease;
}


@media (max-width: 900px) {
    .cardFrame {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-end;
    }
    .cardImage {
        width: 120%;
        border-top-left-radius: 5px;
        border-bottom-left-radius: 5px;
    }

}
@media (max-width: 620px) {
    .textBox, .cardFrame {
        width: 100%;
    }
    .cardFrame {
        padding: 0;
        display: block;
    }
    .cardImage {
        width: 100%;
        aspect-ratio: 5/4;
        border-radius: 0;
        
    }

    .halfMandalaBox {
        display: none;
    }
}
</style>