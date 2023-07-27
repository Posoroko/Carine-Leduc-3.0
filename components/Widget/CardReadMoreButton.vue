<script setup>
const props = defineProps({
    url: {
        type: String,
        required: true
    }
})
</script>

<template>
    <div class="buttonBox full flex justifyEnd">
        <NuxtLink class="button flex alignCenter" :to="url">
            <span class="lightText bodyText1">lire</span> 
            <span class="chevronBox"><WidgetChevron direction="right" /></span>
        </NuxtLink>
    </div>
</template>

<style scoped>
.buttonBox {
    padding-right: 30px;
}
.button {
    height: 100%;
    transition: 300ms ease;
}

.card:hover .button .chevronBox{
    transition: 300ms ease;

}

@media (hover: hover) {
    .chevronBox{
        opacity: 0;
        transform: translateX(-50px);
    }

    .card:hover .button .chevronBox{
        opacity: 1;
        transform: translateX(0px);
        transition: 300ms ease;
    }
}
</style>