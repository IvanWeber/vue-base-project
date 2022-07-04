<template>
    <!-- <div v-if="posts.length > 0">
        <h3>Список постов</h3> -->
        <!-- <shaft-item 
            v-for="post in posts"
            :post="post"
            :key="post.id"
            @remove="$emit('remove', post)"
        /> -->
        <floor-item 
            v-for="index in floorCount"
            :elevatorCount="elevatorCount"
            :floorNumber="index"
            @addCommand="$emit('addCommand', floorNumber)"
        />
    <!-- </div> -->
    <!-- <h2 v-else style="color: red">
        Список постов пуст
    </h2> -->
</template>

<script>
import ShaftItem from "@/components/ShaftItem";
import FloorItem from "@/components/FloorItem";
// import { numberLiteralTypeAnnotation } from "@babel/types";
export default {
    components: {ShaftItem, FloorItem},
    props: {
        floorCount: {
            type: Number,
            required: true
        },
        elevatorCount: {
            type: Number,
            required: true
        },
        commandQueue: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>

</style>