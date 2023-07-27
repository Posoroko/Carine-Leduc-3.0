<script setup>

const props = defineProps({
    text: {
        type: String,
        required: true
    },
    size: {
        type: String,
        default: "large"
    }
})

</script>

<template>
    <div class="fullWidthBox">
        <p class="introText mainTextColor" :class="size">
            {{ text }}
        </p>
    </div>
</template>

<style scoped>
.introText {
    width: min(100%, 500px);
    margin: auto;
    font-family: var(--text-font);
    font-size: clamp(1.6rem, 2.5vw, 2.4rem);
    font-weight: 500;
    line-height: 1.5;
    white-space: pre-wrap;
    
}
.introText.large {
    padding: 150px 0;
}
.introText.small {
    padding: 150px 0;
}
</style>