<template>
    <button class="btn">
        <slot></slot>
    </button>
</template>

<script>
    export default{

    }
</script>

<style scoped>
    .btn{
        padding: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #fff;
        background-color: #39B54A;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
</style>