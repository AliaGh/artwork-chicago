<template>
    <div class="container mx-auto">
        <div v-if="filteredImages.length > 0" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
            <div v-for="(imageInfo, imgIndx) in filteredImages" :key="imageInfo + imgIndx">
                <ArtworkCard :imageInfo="imageInfo" :configUrl="configUrl" :currentPage="currentPage" />
            </div>
        </div>
        <div ref="componentRef"></div>
    </div>
</template>

<script>
import ArtworkCard from './ArtworkCard.vue';

export default {
    name: "ArtworkContainer",
    components: { ArtworkCard },
    props: {
        images: {
            type: Array,
            required: true,
        },

        configUrl: {
            type: String,
            required: true,
        },
        currentPage: {
            type: Number,
            required: true,
        },
        hasMore: {
            type: Boolean,
            required: true
        }
    },
    computed: {
        // return an array of valid images by checking the image id
        filteredImages() {
            const filteredImages = this.images.filter(image => {
                return image.image_id
            })
            return filteredImages
        }
    },
    mounted() {
        const options = {
            threshold: 0.8 // percentage of the target's visibility the observer's callback should be executed.
        }
        const observer = new IntersectionObserver(this.handleIntersection, options)
        observer.observe(this.$refs.componentRef)

    },
    methods: {
        // trigger the fetchData method when the component enters the viewport
        handleIntersection(entries) {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    if (this.hasMore) {
                        this.$emit('loadMore');
                    }
                }
            })
        }
    },
}
</script>