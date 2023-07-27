<script setup>

</script>

<template class="relative">
    <header class="">
        <NavBarMain />
        <slot name="header">


        </slot>

    
    </header>

    <main class="">
        <slot name="main">

        </slot>
    </main>
</template>

<style>
header {
    width: 100%;
    position: relative;

}
header .headerImage_large {
    width: 100%;
    /* height: calc(100vh - var(--navBarHeight)); */
    object-fit: cover;
}
header .headerImage_small {
    width: 100%;
    /* height: calc(60vh - var(--navBarHeight)); */
    object-fit: cover;
    object-position: center;
}
/* .headerImage_large,
.headerImage_small {
    margin-bottom: 50px;
} */
</style>

<style scoped>

main {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: clamp(20px, 5vw, 50px);
    z-index: 0;
}
/* main * {
    padding-left: clamp(5px, 2vw, 10px);
    padding-right: clamp(5px, 2vw, 10px); 
} */
</style>