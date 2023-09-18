<template>
  <div class="mb-5 w-full col-span-1 md:col-span-2 lg:col-span-3">
    <div class="relative w-full">
      <input id="search" v-model="searchArt" type="text"
        class="outline-none bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-red-200 focus:border-red-200  w-full pl-4 p-2.5"
        placeholder="Search artworks..." required @keyup.enter="filter($event.target.value)">
      <div class="absolute top-3 right-3 items-center pr-2 cursor-pointer" @click="filter(searchArt)">
        <img class="text-red-500" src="/search.svg" alt="Search" />
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: "SearchBar",
  data() {
    return {
      searchArt: ''
    }
  },
  methods: {
    filter(value) {
      this.$emit('searchArtWork', value.trim());
    },
  },



}
</script>