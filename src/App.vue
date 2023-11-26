<script setup>
import PhotoUploader from './components/PhotoUploader.vue';
import LoadingStage from "@/components/LoadingStage.vue";
import { ref } from 'vue';

const showUploader = ref(true);

const handleUploadComplete = () => {
    // После завершения загрузки скрываем PhotoUploader и показываем LoadingStage
    showUploader.value = false;
};
</script>

<template>
    <div id="app">
        <PhotoUploader author_id="1" v-if="showUploader" @upload-complete="handleUploadComplete"></PhotoUploader>
        <LoadingStage v-else />
    </div>
</template>

<style scoped>
html, body {
    margin: 0;
    padding: 0;
}
* {
    margin: 0;
    padding: 0;
    display: flex;
}

body {
    margin: 0;
    padding: 0;
    display: inline-block;
}

@media (min-width: 1024px) {

}
@import url('https://fonts.googleapis.com/css2?family=Lato&family=Montserrat:wght@500;700&display=swap');
</style>
