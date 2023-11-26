<script setup>
import { RouterLink, RouterView } from 'vue-router'
import PhotoUploader from './components/PhotoUploader.vue';

</script>

<template>
    <div id="app">
        <photo-uploader author_id="1" order="0"></photo-uploader>
    </div>
</template>

<style scoped>


@media (min-width: 1024px) {

}
</style>
