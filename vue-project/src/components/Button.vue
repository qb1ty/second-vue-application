<template>
    <button @click="convert()">Конвертировать</button>
</template>


<script>
export default {
    props: {
        convert: {
            type: Function,
            required: true
        }
    }
}
</script>

<style setup>
    button {
        position: relative;
        top: 20px;
        padding: 15px 20px;
        margin-bottom: 10px;
        border: 0;
        border-radius: 5px;
        cursor: pointer;
        background-color: #1a032d;
        color: #fff;
        transition: transform .3s ease;
    }

    button:hover {
        transform: scale(1.1) translateY(-2px);
    }
</style>