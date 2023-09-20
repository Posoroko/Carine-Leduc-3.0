<template>
    <footer class="flex alignCenter justifyCenter flex gap20 chicFont">
        <div class="footerLinkBox flex justifyCenter gap20 wrap">
            <NuxtLink class="footerLink" to="/contact">                
                <span>contact</span>    
            </NuxtLink>

            <NuxtLink class="footerLink" to="/mentions-legales">
                <span>mentions légales</span>
            </NuxtLink>

            <a class="footerLink" href="https://monsieuredgar.com">
                <span>monsieuredgar.com</span>
            </a>

            <a class="footerLink" href="https://posoroko.com">
                <span>posoroko.com</span>
            </a>
        </div>
    </footer>
</template>

<style scoped>
footer {
    
    background-color: var(--brand-color-1 );
    padding: 100px 20px 100px 20px;
    margin-top: 50px;
}
.footerLink{
    font-family: var(--body-font);
    font-size: clamp(1.6rem, 2.5vw + 0.1rem, 1.8rem);
    font-weight: 200;
    color: var(--basic-light-color);
    cursor: pointer;
}
</style>