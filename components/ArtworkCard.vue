<template>
    <div class="bg-white rounded-lg shadow-md overflow-hidden">
        <div 
class="bg-center bg-cover bg-grey-500"
            :style="imageInfo.thumbnail.lqip ? { backgroundImage: `url('${imageInfo.thumbnail.lqip}')` } : { backgroundColor: '#E5E7EB' }">
            <a :href="imagePath" target="_blank">
                <img
:src="imagePath" :alt="imageInfo.thumbnail.alt_text || ''"
                    :placeholder="imageInfo.thumbnail.alt_text || ''"
                    class="w-full h-56 object-center object-cover aspect-square"
                    :loading="currentPage > 1 ? 'lazy' : 'eager'" />
            </a>
        </div>
        <div class="pt-4 h-20">
            <p class="flex items-center justify-center text-gray-600 max-h-16 overflow-auto"> {{ imageInfo.title }}</p>
        </div>
    </div>
</template>
  
<script>


export default {
    name: "ArtworkCard",
    props: {
        imageInfo: {
            type: Object,
            required: true
        },
        configUrl: {
            type: String,
            required: true
        },
        currentPage: {
            type: Number,
            required: true
        },

    },
    data() {
        return {
        }
    },
    computed: {
        imagePath() {
            return `${this.configUrl}/${this.imageInfo.image_id}/full/843,/0/default.jpg`
        }
    }

}
</script>