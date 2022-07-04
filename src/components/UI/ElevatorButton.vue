<template lang="">
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: 'elevator-button'
}
</script>

<style scoped>
.btn {
    align-self: flex-end;
    padding: 10px 15px;
    background: none;
    color: blue;
    border: 1px solid blue;
    border-radius: 50%;
}
</style>