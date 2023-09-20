<script setup>

const route = useRoute();

const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
const directusItems = appConfig.directus.items;

const fetchOptions = {
    server: true,
    params: {
        fields: '*.*',
    }
}

const { data: product } = await useAsyncData(
    `product-${route.params.productSlug}`,
    async () => {
        const items = await $fetch(`${directusItems}Products?filter[slug][_eq]=${route.params.productSlug}`, fetchOptions)

        return items.data[0]
    }
    ,
    { server: true }
)
</script>

<template>
    <PageMain v-if="product">
        <template #header>
            <PageHeaderImage v-if="product.headerImage" :imageId="product.headerImage.id" size="small" />

            <PageTitle :text="product.name" />

            <div class="narrowWidth">
                <p>{{ product.price }}€</p>
                <!-- <p>{{ product.length }}</p> -->
            </div>

            <PageIntroText :text="product.teaser" />

            <div class="goalsBox narrowWidth">
                <h2 class="bodyTitle lightText">
                    A quoi s'attendre ?
                </h2>

                <ul class="goals">
                    <li  v-for="(goal, index) in product.goals" key="index">
                        {{ goal.content }}
                    </li>
                </ul>
            </div>
            
        </template>

        <template #main>
            <section class="fullWidthBox">
                <PageParagraph v-for="para in product.paragraphs" :key="para.id" :title="para.title" :text="para.content" />
            </section>
        </template>
    </PageMain>
</template>

<style scoped>
.goalsBox{
    background-color: var(--brand-color-1);
    padding: 40px;
    margin-bottom: 120px;
    border-radius: 10px;
    box-shadow: 3px 3px 10px black;
}
.goals {
    color: var(--basic-light-color);
    margin-top: 30px;
    list-style: disc;
    padding-left: 40px;
    
    
}
.goals li {
    font-family: var(--body-text-family);
    font-size : clamp(1.8rem, 3.5vw + 0.1rem, 2.8rem);
    font-weight: 500;
    line-height: 1.7em;
}
</style>