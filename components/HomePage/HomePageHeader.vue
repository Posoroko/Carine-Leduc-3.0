<script setup>
const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
const directusItems = appConfig.directus.items;

const props = defineProps({
    imageId: {
        type: String,
        required: true
    }
})
</script>

<template>
    <div class="box relative">
        <img :src="`${directusAssets}${imageId}?key=header-1920-750`" alt="Carine Leduc, thérapeute énergéticienne en Centre-Bretagne.">

        <div class="absoluteFull flex column justifyEnd alignStart">
            <div class="flex column">
                <h1 class="lightText">
                    <span class="letter">C</span>
                    <span class="letter">a</span>
                    <span class="letter">r</span>
                    <span class="letter">i</span>
                    <span class="letter">n</span>
                    <span class="letter">e</span>
                    <span class="letter">&nbsp</span>
                    <span class="letter">L</span>
                    <span class="letter">e</span>
                    <span class="letter">d</span>
                    <span class="letter">u</span>
                    <span class="letter">c</span>
                </h1>
            
                <h2 class="">Thérapeute énergéticienne</h2>
            </div>
        </div>
    </div>
</template>

<style scoped>
.box {
    height: 75vh;
    
}
.absoluteFull {
    padding-bottom: 30px;
}
h1, h2 {
    
    padding-left: max(2.5vw, 10px);
}
h1 {
    font-family: var(--brand-font);
    font-size: clamp(4.8rem, 12vw + 0.1rem, 15rem);
    line-height: 0.5;
    color: var(--basic-light-color);
    text-shadow: 0 0 10px black;
}
h2 {
    font-family: 'Montserrat';
    font-size: clamp(1.8rem, 3vw + 1px, 4rem);
    font-weight: 200;
    line-height: 1.8;
    color: var(--basic-light-color);
    margin-left: auto;
    text-shadow: 0 0 10px black;
}
.h1 {
    animation-name: slideIn;
    animation-duration: 3s;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
    animation-timing-function: cubic-bezier(0.075, 0.82, 0.165, 1);
}
.letter:nth-child(1) { animation-delay: var(--delay); }
.letter:nth-child(2) { animation-delay: calc(var(--delay) * 2); }
.letter:nth-child(3) { animation-delay: calc(var(--delay) * 3); }
.letter:nth-child(4) { animation-delay: calc(var(--delay) * 4); }
.letter:nth-child(5) { animation-delay: calc(var(--delay) * 5); }
.letter:nth-child(6) { animation-delay: calc(var(--delay) * 6); }
.letter:nth-child(7) { animation-delay: calc(var(--delay) * 7); }
.letter:nth-child(8) { animation-delay: calc(var(--delay) * 8); }
.letter:nth-child(9) { animation-delay: calc(var(--delay) * 9); }
.letter:nth-child(10) { animation-delay: calc(var(--delay) * 10); }
.letter:nth-child(11) { animation-delay: calc(var(--delay) * 11); }
.letter:nth-child(12) { animation-delay: calc(var(--delay) * 12); }

@keyframes slideIn {
    from {
        transform: translateX(100px);
    }
    to {
        transform: translateX(0px);
    }
}

img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    filter: brightness(0.89);
}
</style>