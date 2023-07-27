<template>
    <div class="flex column justifyBetween " id="appBox">

        <NuxtPage />

        <FooterMain />

        <div class="mandalaBox right">
            <DecoQuarterMandala />
        </div>

        <div class="mandalaBox left">
            <DecoQuarterMandala />
        </div>
    </div>
    
</template>

<style ccoped>
#appBox {
    /* width: 100vw; */
    min-height: 100vh;
    background-color: var(--background-color);
    position: relative;
    overflow: hidden;
    position: relative;
}
.mandalaBox {
    width: 18vw;
    aspect-ratio: 1;
    position: fixed;
    top: 0;
    right: 0;
    z-index: 10000;
    opacity: 0.7;
    pointer-events: none;
}
.mandalaBox.right {
    right: 0;
}
.mandalaBox.left {
    left: 0;
    rotate: -90deg;
}
</style>
