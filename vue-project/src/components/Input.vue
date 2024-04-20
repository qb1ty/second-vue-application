<template>
    <input type="number" min="0" @input="changeAmount($event.target.value)" placeholder="Введите число">  
</template>

<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            required: true
        }
    }
}
</script>

<style setup>
    input {
        border: 0;
        outline: none;
        border-radius: 3px;
        padding: 10px 15px;
        background-color: #fafafa;
        color: #333;
        width: 525px;
        font-size: 1.25em;
    }
</style>