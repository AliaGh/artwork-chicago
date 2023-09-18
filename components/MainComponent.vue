<template>
    <div class="relative container mx-auto">
        <SearchBar @searchArtWork="setFilter" />
        <Toast v-if="noResults" :message="message" :is-visible="noResults" />
        <ArtworkContainer :images="images" :configUrl="configUrl" :currentPage="currentPage" :hasMore="hasMore"
            @loadMore="fetchMoreData" />

    </div>
</template>
  
<script>
import ArtworkContainer from './ArtworkContainer.vue';
import SearchBar from './SearchBar.vue';
import Toast from './Toast.vue';

export default {
    name: "App",
    components: { ArtworkContainer, SearchBar, Toast },

    data() {
        return {
            images: [],
            currentPage: 1,
            hasMore: true,
            configUrl: "",
            filter: "",
            noResults: false,
            lastQuery: '',
            message: ''
        }
    },
    // fetch data during SSR and assign the response to the images array
    async fetch() {
        await this.fetchData()
    },
    methods: {
        // send an API call after checking if there is a query or the current query is not equal to the last query
        async setFilter(text) {
            if (this.lastQuery !== text) {
                this.filter = text
                this.lastQuery = this.filter
                this.currentPage = 1
                this.images = []
                this.hasMore = false
                await this.fetchData()

            }
        },
        // fetch the data from the API and set the images array value 
        async fetchData() {
            let res = null
            const params = [`page=${this.currentPage}`, "limit=6"]

            if (this.filter) {
                params.push(`q=${this.filter}`)
            }

            try {
                res = await (await fetch(`https://api.artic.edu/api/v1/artworks/search?fields=id,title,thumbnail,image_id&${params.join('&')}`)).json()

                if (res) {
                    if (res.data.length > 0) {
                        this.noResults = false
                        this.images.push(...res.data)
                        this.configUrl = res.config.iiif_url
                        this.hasMore = res.pagination.current_page < res.pagination.total_pages
                    } else {
                        this.noResults = true
                        this.message = "There is no matching results for your search"
                    }
                }

            }
            catch {
                this.noResults = true
                this.message = "An error occurred while fetching the data"
            }

        },
        // fetch more data after checking the current page and compare it to the total pages (hasMore)
        async fetchMoreData() {
            if (this.hasMore) {
                this.currentPage++
                await this.fetchData()
            }

        }
    },
}
</script>
  