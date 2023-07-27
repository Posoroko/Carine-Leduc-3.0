<script setup>
const props = defineProps({
    text: {
        type: String,
        required: true
    },
    color: String

})
</script>

<template>
    <div class="fullWidthBox marTop50">
        <div class="flex justifyCenter alignCenter">
            <WidgetTitleFlower color="dark" direction="left" />
        
            <h2 class="mainWidth bodyTitle">{{ text }}</h2>

            <WidgetTitleFlower color="dark" direction="right" />
        </div>
    </div>
</template>

<style scoped>
h2 {
    text-align: center;
    color: v-bind(color);
}
</style>