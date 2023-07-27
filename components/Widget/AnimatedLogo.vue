<template>
    <div class="box flex alignEnd">
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
    </div>
</template>

<style>
:root {
    --delay: 25ms;
}
</style>

<style scoped>

.letter {
    display: flex;
    align-items: center;
    line-height: 1;
    position: relative;
    display: inline-block;
    animation-duration: 1s;
    animation-iteration-count: 1;
    animation-timing-function: ease-in-out;
}
.box:hover .letter {
    animation-name: jump 
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

@keyframes jump {
    0% {transform: translateY(0px);}
    15% {transform: translateY(-5px);}
    50% {transform: translateY(0px);}
}
</style>