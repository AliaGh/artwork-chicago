<template>
    <div class="m-3">
        <HeaderComponent />
        <MainComponent />
    </div>
</template>
  
<script>
import HeaderComponent from '~/components/HeaderComponent.vue';
import MainComponent from '~/components/MainComponent.vue';

export default {
    name: "App",
    components: { HeaderComponent, MainComponent },
    mounted() {
        window.scrollTo(0, 0)
    }
}
</script>
  