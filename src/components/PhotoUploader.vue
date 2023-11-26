<template>
    <div class="uploader">
        <input type="file" @change="handleFileChange" accept="image/*">
        <img class="loaded-img" v-if="imageUrl" :src="imageUrl" alt="Selected Image">
        <button class="send-btn" @click="uploadFile">Отправить фото</button>
    </div>
</template>

<script>
import axios from "axios";

export default {
    props: {
        author_id: {
            type: Number,
            required: true
        }
    },
    data() {
        return {
            imageUrl: null,
            file: null,
            author_id: 1
        };
    },
    methods: {
        handleFileChange(event) {
            const file = event.target.files[0];
            if (file) {
                this.file = file;
                this.imageUrl = URL.createObjectURL(file);
            }
        },
        uploadFile() {
            if (this.file) {
                const formData = new FormData();
                formData.append('file', this.file);
                formData.append('order', this.order);
                formData.append('author_id', this.author_id);

                axios.post('http://91.107.35.153:3001/api/orders', formData)
                    .then(response => {
                        console.log('File uploaded successfully', response);
                        // Дополнительная логика после успешной загрузки
                    })
                    .catch(error => {
                        console.error('Error uploading file', error);
                        // Обработка ошибок
                    });
            } else {
                console.warn('No file selected');
            }
        }
    }
};
</script>

<style scoped>

.uploader {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    align-content: center;
    flex-direction: column;

}

.loaded-img {
    margin-top: 10px;
    max-width: 30vw;
    margin-bottom: 10px;
}
</style>
