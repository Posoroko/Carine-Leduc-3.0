<script setup>
const props = defineProps({
    text: {
        type: String,
        required: true
    }
})
</script>

<template>
    <p class="content bodyText2">
        <span class="firstLetter">{{ text[0] }}</span>
        {{ text.slice(1, 10000) }}
    </p>
</template>

<style scoped>
.content {
    width: min(100%, 80ch);
    text-align: justify;
    padding: 30px;
    columns: 2;
    gap: 60px;
    margin: 0 auto;
}
@media (max-width: 768px) {
    .bodyText2 {
        columns: 1;
    }
}
.firstLetter {
    color: var(--brand-color-2);
    font-size: 100px;
    line-height: 0.5;
    float: left;
    display: block;
    padding: 10px 5px 0 0 ;
    /* height: 100px; */
}
</style>