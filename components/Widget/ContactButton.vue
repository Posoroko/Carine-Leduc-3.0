<template>
    <NuxtLink to="/contact/formulaire-de-contact" class="button flex alignCenter titleFont lightText BGC_Brand2_Hoverable">

        <svg class="" xmlns="http://www.w3.org/2000/svg" height="24" viewBox="0 -960 960 960" width="24"><path d="M360-300q-42 0-71-29t-29-71q0-42 29-71t71-29q42 0 71 29t29 71q0 42-29 71t-71 29ZM200-80q-33 0-56.5-23.5T120-160v-560q0-33 23.5-56.5T200-800h40v-80h80v80h320v-80h80v80h40q33 0 56.5 23.5T840-720v560q0 33-23.5 56.5T760-80H200Zm0-80h560v-400H200v400Zm0-480h560v-80H200v80Zm0 0v-80 80Z"/></svg>


        <div>
            demander un <br> rendez-vous !
        </div>
    </NuxtLink>
</template>

<style scoped>
.button {
    position: fixed;
    bottom: 20px;
    right: 20px;

    color: var(--basic-light-color);
    padding: 10px ;
    border-radius: 5px;

    font-size: clamp(1.6rem, 2vw + 0.1rem, 2.6rem);
    cursor: pointer;
    transition: 150ms;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.488);
    gap: 10px;
}
.button:hover {
    transition: 150ms;
    box-shadow: 2px 2px 6px rgba(0, 0, 0, 0.488);
}
svg {
    width: 50px;
    height: 50px;
    fill: var(--basic-light-color);
}
</style>