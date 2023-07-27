<script setup>
const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;

const props = defineProps({
    imageId: {
        type: String,
        required: true
    },
    size: {
        type: String,
        required: true
    }
})
</script>

<template>
    <div class="headerImageFrame" :class="size">
        <img :src="`${directusAssets}${imageId}`" alt="Carine Leduc, thérapeute énergéticienne en Centre-Bretagne.">
    </div>
</template>


<style scoped>
.headerImageFrame.large {
    height: 75vh;
}
.headerImageFrame.small {
    height: 50vh;
}
img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
}
</style>