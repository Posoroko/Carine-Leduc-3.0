<template>
    <NuxtLink to="/contact/formulaire-de-contact" class="button titleFont lightText BGC_Brand2_Hoverable">
        demander un rendez-vous
    </NuxtLink>
</template>

<style scoped>
.button {
    display: block;
    position: fixed;
    bottom: 20px;
    right: 20px;

    color: var(--basic-light-color);
    padding: 10px 20px;
    border-radius: 5px;

    font-size: clamp(1.8rem, 2vw + 0.1rem, 2.8rem);
    cursor: pointer;
    transition: 150ms;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.488);
}
.button:hover {
    transition: 150ms;
    box-shadow: 2px 2px 6px rgba(0, 0, 0, 0.488);
}
</style>