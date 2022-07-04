<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <div class="app__btns">
            <my-button
                @click="showDialog"
            >
                Создать пост
            </my-button>
            <my-select
                v-model="selectedSort"
                :options="sortOptions"
            />
        </div>
        
        <my-dialog v-model:show="dialogVisible">
            <post-form 
                @create="createPost"
            />
        </my-dialog>
        
        <post-list 
            :posts="posts"
            @remove="removePost"
            v-if="!isPostsLoading"
        />
        <div v-else>Идёт загрузка...</div>
        <div>
            <elevator-emulator
                :floorCount="floorCount"
                :elevatorCount="elevatorCount"
            />
        </div>
    </div>
</template>


<script>

import PostForm from "./components/PostForm";
import PostList from "@/components/PostList";
import ElevatorEmulator from "@/components/ElevatorEmulator";
import MyDialog from '@/components/UI/MyDialog';
import MyButton from '@/components/UI/MyButton';
import MySelect from '@/components/UI/MySelect';
import axios from 'axios';

export default {

    components: {
        PostList, PostForm, MyDialog, MyButton, MySelect, ElevatorEmulator
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostsLoading: false,
            selectedSort: '',
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По содержимому'}
            ],
            floorCount: 5,
            elevatorCount: 3,

        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },
        async fetchPosts() {
            try {
                this.isPostsLoading = true;
                const response = await axios.get(`https://jsonplaceholder.typicode.com/posts?_limit=10`);
                this.posts = response.data;
            } catch (e) {
                alert('Ошибка')
            } finally {
                this.isPostsLoading = false;
            }
        }
    },
    mounted() {
        this.fetchPosts();
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => {
                return post1[newValue]?.localeCompare(post2[newValue])
            })
        }
    },
    watch: {
        selectedSort(newValue) {
            this.posts.sort((post1, post2) => {
                return post1[newValue]?.localeCompare(post2[newValue])
            })
        },
    }
}

</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    padding: 20px;
}

.app__btns {
    display: flex;
    justify-content: space-between;
    margin: 15px 0;
}

</style>