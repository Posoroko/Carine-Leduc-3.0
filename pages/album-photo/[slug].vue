<script setup>
const route = useRoute()

const appConfig = useAppConfig();
const directusAssets = appConfig.directus.assets;
const directusItems = appConfig.directus.items;

// const fetchOptions = {
//     server: true,
//     params: {
//         fields: 'id, title, images, images.*, description, slug, headerImage',
//     }
// }

// const { data: album } = await useAsyncData(
//     "album",
//     async () => {
//         const items = await $fetch(`${directusItems}Albums?filter[slug][_eq]=${route.params.slug}`, fetchOptions)

//         return items.data[0]
//     }
//     ,
//     { server: true }
// )

// const selectedImageIndex = ref(null)

// const modalIsOpen = ref(false)

// function handleImageclick(e) {
//     selectedImageIndex.value = e.target.dataset.index
//     modalIsOpen.value = true
// }
// function closeModal() {
//     modalIsOpen.value = false
// }

// function navigate(direction) {
//     console.log(selectedImageIndex.value)
//     if (direction === 'left' && selectedImageIndex.value > 0) {
//         selectedImageIndex.value--
//     } else if (direction === 'right' && selectedImageIndex.value < album.value.images.length - 1) {
//         selectedImageIndex.value++
//     }
// }

</script>

<template>
    <PageMain v-if="album">
        <template #headerImage>
            <img class="headerImage_small" :src="`${directusAssets}${album.headerImage}`" alt="">

            <div class="mainWidth">
                <SectionTitle :title="`Album : ${album.title}`" />
            </div>
        </template>

        <template #main>

            <p class="bodyText1 lightText mainWidth marTop50">
                {{ album.description }}
            </p>

            <div class="galeryBox mainWidth">
                <img class="galeryImage" v-for="(image, index) in album.images" :src="`${directusAssets}${image.directus_files_id}`"
                    :alt="`${image.alt}`" :data-index="index" @click="handleImageclick">
            </div>

            <div class="modal" v-if="modalIsOpen">
                <div class="modalContent centered pad20">
                    <span class="close lightText" @click="closeModal">&times;</span>

                    <img class="objectFitContain" :src="`${directusAssets}${album.images[selectedImageIndex].directus_files_id}`"
                        alt="compagnie Singe Diesel">

                    <WidgetLeftRightNavigation @navigate="navigate" />
                </div>
            </div>
        </template>

    </PageMain>
</template>

<style scoped>
.galeryBox {
    min-height: 80vh;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 20px;
}

.galeryImage {
    width: auto;
    height: auto;
    max-width: 200px;
    max-height: 200px;
    object-fit: contain;
    object-position: center;
    border-radius: 5px;
    box-shadow: 2px 2x 10px hsl(0, 0%, 0%);
    overflow: visible;
    cursor: pointer;
    transition: 150ms ease;
}

.galeryImage:hover {
    scale: 1.025;
}

.galeryImage:nth-child(2n+1):hover {
    rotate: 2deg;
    transition: 150ms ease;
}

.galeryImage:nth-child(2n+2):hover {
    rotate: -2deg;
    transition: 150ms ease;
}

.modal {
    position: fixed;
    width: 100vw;
    height: 100vh;
    top: 0;
    left: 0;
    padding: max(5vw, 10px);
    background-color: #0000005d;
    backdrop-filter: blur(5px);
}

.modalContent {
    width: 100%;
    height: 100%;
    background-color: var(--background);
    border-radius: 10px;
    box-shadow: 1px 1px 10px #00000097;
    position: relative;
}

.close {
    width: 48px;
    height: 48px;
    font-size: 40px;
    line-height: 1;
    cursor: pointer;
    position: absolute;
    top: 10px;
    right: 10px;
    display: grid;
    place-items: center;
}

.close:hover {
    rotate: 360deg;
    transition: 300ms ease;
}</style>