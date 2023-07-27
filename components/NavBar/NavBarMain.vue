<template>
    <nav class="navBar w100">
        <!-- <div class="logoBar flex alignCenter justifyCenter">
            <NuxtLink class="carine pointer" to="/">
                <WidgetAnimatedLogo />
            </NuxtLink>
        </div> -->

        <div class="tabBar flex justifyCenter w100">
            <NuxtLink class="tab pointer" to="/prestations">Prestations</NuxtLink>
            <NuxtLink class="tab pointer" to="/a-propos">À propos</NuxtLink>
            <NuxtLink class="tab pointer" to="/agenda">Agenda</NuxtLink>
        </div>
    </nav>
</template>

<style scoped>

.tabBar {
    /* border-bottom: 2px solid rgba(0, 0, 0, 0.168);
    box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.286); */
    background-color: var(--background-color);
    position: sticky;
    top: 0px;
}
.carine {
    font-family: var(--brand-font);
    font-size: clamp(28px, 4vw + 1px, 50px);
    font-weight: 700;
    font-style: unset;

    padding: 10px 0 0 0;
    border: 1px solid black;
    display: block;
}
.navBar {

    z-index: 10000;

}
/* .navBar {
    background-color: var(--brand-color-1);
}
.navBar * {
    color: var(--basic-light-color);
} */
.tabBar {
    padding: 15px 0 3px 0;
    margin-bottom: 10px;
}
.tab {
    font-family: var(--text-font);
    font-size: clamp(1.8rem, 2vw + 0.1rem, 2.2rem);
    text-transform: uppercase;
    padding: 3px 8px;
    border-top: 1px solid transparent;
    border-bottom: 1px solid transparent;
    transition: 300ms ease;
}
.tab:hover {
    border-top: 1px solid var(--brand-color-1);
    border-bottom: 1px solid var(--brand-color-1);
    transition: 300ms ease;
}
</style>