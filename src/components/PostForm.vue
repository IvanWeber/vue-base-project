<template>
    <form @submit.prevent>
            <h4>Создание поста</h4>
            <my-input 
                v-model="post.title"
                type="text" 
                placeholder="Название"
            />
            <my-input 
                v-model="post.body"
                type="text" 
                placeholder="Описание"
            />
            <my-button 
                class="btn"
                style="margin-top: 15px" 
                @click="createPost"
            >
                Создать
            </my-button>
        </form>
</template>
<script>
import MyButton from '@/components/UI/MyButton';
import MyInput from '@/components/UI/MyInput';
import { handleError } from 'vue';

export default {
    components: {MyButton, MyInput},
    data() {
        return {
            post: {
                title: '',
                body: ''
            }
        }
    },
    methods: {
        createPost() {
            this.post.id= Date.now();
            this.$emit('create', this.post, 'second param', '3 param');
            this.post = {
                title: '',
                body: ''
            }
            
        }
    },
}
</script>
<style scoped>
form {
    display: flex;
    flex-direction: column;
}
</style>