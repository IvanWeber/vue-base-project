<template>
    <div class="post">
        <div>Пространство шахты</div>
        <shaft-space v-for="index in elevatorCount"/>
        Этаж
        <elevator-button
            @click="$emit('addCommand', floorNumber)"
        >
            Вызов лифта {{floorNumber}}
        </elevator-button>
    </div>
</template>

<script>
// import MyButton from '@/components/UI/MyButton.vue';
import ElevatorButton from '@/components/UI/ElevatorButton.vue';
import ShaftSpace from '@/components/ShaftSpace.vue';

export default {
    components: {ElevatorButton, ShaftSpace},
    props: {
        post: {
            type: Object,
            required: true
        },
        elevatorCount: {
            type: Number,
            required: true
        },
        floorNumber: {
            type: Number,
            required: true
        }
    }
}
</script>

<style scoped>
.post {
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

</style>