<template>
    <ul>
        <li @click="setCrypto('BTC')" :class="crypto === 'BTC' ? 'active' : '' ">Bitcoin</li>
        <li @click="setCrypto('ETH')" :class="crypto === 'ETH' ? 'active' : '' ">ETH</li>
        <li @click="setCrypto('USDT')" :class="crypto === 'USDT' ? 'active' : '' ">USDT</li>
    </ul>
</template>

<script>
export default {
    data() {
        return {
            current: ''
        }
    },
    props: {
        setCrypto: {
            type: Function,
            required: true
        },
        crypto: {
            type: String,
            required: true
        }
    }
}
</script>

<style setup>
    ul {
        list-style: none;
        width: 200px;
        padding: 0;
        border-radius: 3px;
        border: 3px solid #000;
        margin-top: 30px;
    }

    li {
        display: block;
        background: #1A032D;
        color: #fff;
        padding: 20px 0;
    }

    li:hover, li.active {
        background-color: #24043e;
        cursor: pointer;
    }
</style>