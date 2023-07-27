<script setup>

const route = useRoute();

const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
const directusItems = appConfig.directus.items;

const fetchOptions = {
    server: true,
    params: {
        // fields: 'id, title, subtitle, content, image, imageAlt, moreInfo, date_created, file, fileName',
    }
}

const { data: contact } = await useAsyncData(
    "contactData",
    async () => {
        const items = await $fetch(`${directusItems}Contact`, fetchOptions)

        return items.data
    }
    ,
    { server: true }
)
</script>

<template>
    <PageMain>
            <template #headerImage>
                
            </template>

            <template #main>
                <div class="mainWidth marTop150 flex alignCenter">
                    <PageTitle text="Mentions légales" />
                </div>

                <div class="mainWidth flex column gap30">
                    <h2 class="mentionsTitle">Ce site internet est la propriété de  </h2>

                    <address class="contactBox mentionsText flex column gap20 alignStart">
                        <b class="name ">{{ contact.name }}</b>

                        <p class="address contactInfoFont">{{ contact.address }}</p>

                 
                    </address>

                    <p class="mentionsText">Directeur de publication : <b>{{ contact.name }}</b></p>

                    <div>
                        <h3 class="mentionsTitle">Design et Développement</h3>
                        <address class="mentionsText marTop20">
                            Monsieur Edgar, un service de Studio Posoro<br>
                            24, rue de Kerven – 29270 Carhaix​<br>
                            06 95 07 12 64<br>
                            eric@posoroko.com<br>
                            <a class="underline pointer" href="https://www.posoroko.com" target="_blank">https://www.posoroko.com</a><br>
                        </address>
                    </div>

                    <div>
                        <h2 class="mentionsTitle">DROITS DE REPRODUCTION </h2>
                        <p class="mentionsText">
                            Ce site est protégé par la législation française et internationale par le droit d’auteur et la propriété intellectuelle. Toute copie, représentation, adaptation, diffusion, intégrale ou partielle, du contenu du site est illicite à l’exception d’une unique copie réservée à l’usage privé de l’utilisateur. Les informations contenues dans ce site sont présentées à titre purement informatif et sont non contractuelles. <b>{{ contact.name }}</b> ne saurait être tenue responsable pour toute erreur ou omission dans les textes et illustrations du site. Toute représentation et/ou reproduction et/ou exploitation partielle ou totale de ce site, par quelques procédés que ce soit, sans l’autorisation expresse et préalable de <b>{{ contact.name }}</b> sont interdites et constitueraient une contrefaçon au sens des articles L 335-2 et suivants du code de la propriété intellectuelle.
                        </p>
                    </div>

                    <div>
                        <h2 class="mentionsTitle">PROTECTION DES DONNÉES PERSONNELLES </h2>
                        <p class="mentionsText">
                            Conformément au Règlement (UE) 2016/679 relatif à la protection des données à caractère personnel et à
                            la loi n°78/17 du 6 janvier 1978
                            modifiée, vous disposez des droits suivants sur vos données personnelles, et notamment : le droit
                            d’accéder, et de faire rectifier vos données,
                            le droit à l’effacement, à la limitation du traitement, et le droit de vous opposer à tout moment au
                            traitement de vos données pour des motifs
                            tenant à votre situation particulière. Pour exercer vos droits, merci d’adresser votre demande à :
                            <b>{{ contact.email }}</b>
                        </p>
                    </div>

                    <div>
                        <h2 class="mentionsTitle">ABSENCE DE GARANTIE</h2>
                        <p class="mentionsText">
                            Nous mettons en place tous les moyens nécessaires pour vous apporter une information fiable et
                            actualisée. Cependant, malgré le soin que nous apportons à la mise à jour de ce site, des erreurs ou omissions peuvent être présentes. En
                            conséquence, l’éditeur ne peut être tenu responsable. Nous ne garantissons pas le contenu des sites Internet vers lesquels nous pointons.
                        </p>
                    </div>

                    <div>
                        <h2 class="mentionsTitle">LIEN </h2>

                        <p class="mentionsText">
                            Certaines pages peuvent contenir des liens vers des sites externes à ce site. <b>{{ contact.name }}</b> ne
                            réalise pas de contrôle sur ces sites, par conséquent, elle n’assume aucune responsabilité quant à la disponibilité de ces sites, leurs
                            contenus, publicités, produits ou services disponibles à partir de ces sites. L’accès à d’autres sites externes au site
                            <b>carine-leduc.com</b> se fait donc sous l’entière responsabilité de l’utilisateur qui les consulte.
                        </p>
                    </div>
                </div>
            </template>
        </PageMain>
</template>

<style scoped>
* {
    color: var(--text-color);
}
.mentionsTitle {
    font-family: 'Montserrat', sans-serif;
    font-size: clamp(2rem, 2.5vw, 3rem);
}
.mentionsText{
    font-family: 'Montserrat', sans-serif;
    font-size: clamp(1.6rem, 2vw, 2.2rem);
    margin-top: 20px;
}
.mentionsTitle1 {
    margin-top: 10px;
}
.address {
    white-space: pre-wrap;
}
</style>