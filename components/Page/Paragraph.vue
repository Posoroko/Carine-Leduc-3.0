<script setup>
const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;

const props = defineProps({
    text: {
        type: String,
        required: true
    },
    title: {
        type: String,
        required: false
    },
    imageId: {
        type: String,
        required: false
    },
    imageAlt: {
        type: String,
        required: false
    },
})
</script>

<template>
    <div class="box narrowWidth marTop50">
        <div class="imageBox w100" v-if="imageId">
            <WidgetImageAndModal :imageId="imageId" :imageAlt="imageAlt" objectFit="contain" />

            <!-- <img class="paragraphImage" :src="`${directusAssets}${imageId}?key=300px`" :alt="imageAlt"> -->
        </div>

        <h2 class="title" v-if="title">{{ title }}</h2>

        <p class="content bodyText2 w100" v-if="text">
            <span class="firstLetter">{{ text[0] }}</span>
            {{ text.slice(1, 10000) }}
        </p>
    </div>
</template>

<style scoped>
.imageBox {
    /*height: 300px;*/
}
.title {
    font-family: var(--title-font);
    font-size: clamp(2rem, 2vw + 0.1rem, 3.2rem);
    font-weight: 700;
    color: var(--text-color);
    margin-top: 75px;
}
.paragraphImage {
    width: 300px;
}
.content {
    width: 100%;
    color: var(--text-color);
    padding-bottom: 40px;
    border-bottom: 1px solid var(--brand-color-2);
    margin-top: 40px;
    margin-bottom: 120px;
    text-align: justify;
    columns: 2;
    gap: 40px;
}

@media (max-width: 768px) {
    .content {
        columns: 1;
    }

}

.firstLetter {
    color: var(--brand-color-2);
    font-size: 100px;
    line-height: 0.5;
    float: left;
    display: block;
    padding: 10px 5px 0 0;
    /* height: 100px; */
}
</style>
