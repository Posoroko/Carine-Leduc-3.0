<script setup>

const props = defineProps({
    schedule: String,
})

</script>

<template>
    <div class="scheduleBox narrowWidth">
        <h2 class="bodySubtitle">Heures d'ouverture du cabinet :</h2>
        <p class="scheduleText bodyText2 marTop20">
            {{ schedule }}
        </p>
    </div>
</template>

<style scoped>

    .scheduleText {
        white-space: pre-line;
    }
</style>