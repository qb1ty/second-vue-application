<template>
    <h2 class="h2">Варианты в избранном</h2>
    <div v-for="(el, index) in favs" @click="getFavEl(index)" :key="index" class="div">
        <span class="span">{{ el.from }}</span>
        <span class="span">{{ el.to }}</span>
    </div>
</template>

<script>
export default {
    props: {
        favs: {
            type: Array,
            required: true
        },
        getFavEl: {
            type: Function,
            required: true
        }
    }
}
</script>

<style setup>
.h2 {
    margin-top: 10px;
    color: #fff;
}

.div {
    display: flex;
    justify-content: space-between;
    width: 500px;
    margin: 10px auto;
    transition: all .5s ease;
}

.span {
    padding: 10px 15px;
    background-color: #8c00ff;
    color: #fff;
}

.div:hover {
    opacity: .7;
    transform: scale(1.1);
    cursor: pointer;
}
</style>