<template>
     <div class="buttonBox w100 flex justifyEnd">
        <span class="icon ligntText east">east</span>
    </div>
</template>

<style scoped>
.rightArrowHover:hover .east {
    opacity: 1;
    transform: translateX(20px);
    transition: 900ms cubic-bezier(.01,.96,.04,.96);
}
.east {
    font-size: clamp(3rem, 4.5vw + 0.1rem, 5rem);
    color: var(--basic-light-color); 
    transition: 900ms cubic-bezier(.01,.96,.04,.96);
}
@media (hover: hover ) {
    .east {
        opacity: 0.5;
    }
}
</style>