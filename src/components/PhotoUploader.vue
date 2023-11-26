<template>
    <div class="wrapper">
        <div class="background"></div>
          <div class="content-wrapper">
            <div class="text-info">
                <h1 class="name-tag">ДИЗАЙН-КОД<br>ЕКАТЕРИНБУРГ</h1>
                <p>Добро пожаловать на сайт Екатеринбурга, где дизайн-код — ключевой элемент развития нашего города. </p>
                <p><mark>Дизайн-код</mark> — это набор правил проектирования, требований и рекомендаций, с помощью которых можно сформировать стилистически единую, комфортную и безопасную городскую среду или другое физическое пространство.</p>
                <p><mark>Загрузите фотографию объекта </mark> и мы покажем, как он будет выглядеть. </p>
            </div>
            <div class="uploader">
                <input class="custom-file-input" type="file" @change="handleFileChange" accept="image/*">
                <img class="loaded-img" v-if="imageUrl" :src="imageUrl" alt="Selected Image">
                <button class="send-btn" @click="uploadFile">Отправить фото</button>
            </div>
          </div>
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
            author_id: 1,
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

                        // Вызываем событие upload-complete
                        this.$emit('upload-complete');
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
* {
    margin: 0;
    padding: 0;
    display: inline-block;
}

body {
    margin: 0;
    padding: 0;
    display: inline-block;
}

.wrapper {
    display: contents;
}

.background {
    background-image: url(src/components/background/background.jpg);
    background-position: left;
    background-repeat: no-repeat;
    background-size: cover;
    width: 65vw;
    height: 98vh;
    position: relative;
}

.uploader {
    display: flex;
    flex-direction: column;
    padding-top: 24px;
    align-items: flex-end;
}

.custom-file-input {
    color: transparent;
}

.custom-file-input::-webkit-file-upload-button {
    visibility: hidden;
}

.custom-file-input::before {
    content: 'Нажмите, чтобы добавить фото';
    color: black;
    display: inline-block;
    background: #D9D9D9;
    border: none;
    border-radius: 60px;
    padding: 30px;
    outline: none;
    white-space: nowrap;
    -webkit-user-select: none;
    cursor: pointer;
    font-weight: 700;
    font-size: 12px;
}

.custom-file-input:hover::before {
    border-color: black;
}

.custom-file-input:active {
    outline: 0;
}

.custom-file-input:active::before {
    background: -webkit-linear-gradient(top, #e3e3e3, #f9f9f9);
}

.loaded-img {
    padding-top: 20px;
    width: 100%;
    height: 200px;
}

.text-info {
    font-family: 'Montserrat', sans-serif;
    font-weight: bold;
    text-align: right;
    font-size: 30px;
    padding-top: 48px;
}

.text-info p {
    font-family: 'Montserrat', sans-serif;
    font-weight: 500;
    font-size: 18px;
    padding-top: 20px;
}

.content-wrapper {
    position: absolute;
    display: flex;
    flex-wrap: nowrap;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-end;
    padding-left: 40vw;
    padding-right: 110px;
}

.send-btn {
    padding: 20px;
    background-color: #CEFF65;
    border: none;
    border-radius: 95px;
    font-size: 15px;
    margin-top: 20px;
    cursor: pointer;
}

</style>
