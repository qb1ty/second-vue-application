<template>
  <div>
    <h1>CRYPTO</h1>
    <Input :changeAmount="changeAmount"/><br />
    <Favourite :favs="favs" v-if="favs.length > 0" :getFavEl="getFavEl"/>
    <Button :convert="convert" />

    <button @click="favourite()" class="fav-button">добавить в избранные</button>
    <p v-if="error !== 'error'" class="error">{{ error }}</p>
    <p v-if="result !== 0" class="result">{{ result }}</p>
    <div class="selectors">
      <Selector :setCrypto="setCryptoFirst" :crypto="firstCrypto"/>
      <Selector :setCrypto="setCryptoSecond" :crypto="secondCrypto"/>
    </div>
  </div>
</template>

<script>
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import Button from './components/Button.vue';
import Favourite from './components/Favourite.vue';
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert()

export default {
  components: { Input, Selector, Button, CryptoConvert, Favourite },
  data() {
    return {
      amount: 0,
      firstCrypto: '',
      secondCrypto: '',
      error: '',
      result: 0,
      favs: []
    }
  },
  methods: {
    favourite() {
      if (this.firstCrypto === '' || this.secondCrypto === '') {
        this.error = 'Выберите валюту'
        return;
      } else if (this.firstCrypto === this.secondCrypto) {
        this.error = 'Выберите разную валюту'
        return;
      }

      this.error = ''
      
      if (this.firstCrypto.length || this.secondCrypto.length) {
        this.favs.push({
          from: this.firstCrypto,
          to: this.secondCrypto
        })
        return;
      }
    },
    getFavEl(index) {
      this.firstCrypto = this.favs[index].from
      this.secondCrypto = this.favs[index].to
    },
    changeAmount(value) {
      this.amount = value
    },
    setCryptoFirst(value) {
      this.firstCrypto = value
    },
    setCryptoSecond(value) {
      this.secondCrypto = value
    },
    async convert() {
      if (this.amount <= 0) {
        this.error = 'Введите число больше нуля'
        return;
      } else if (this.firstCrypto === '' || this.secondCrypto === '') {
        this.error = 'Выберите валюту'
        return;
      } else if (this.firstCrypto === this.secondCrypto) {
        this.error = 'Выберите разную валюту'
        return;
      }

      this.error = ''
      await convert.ready()

      if (this.firstCrypto === 'BTC' && this.secondCrypto === 'ETH') {
        this.result = convert.BTC.ETH(+this.amount);
        return;
      } else if (this.firstCrypto === 'BTC' && this.secondCrypto == 'USDT') {
        this.result = convert.BTC.USDT(+this.amount);
        return;
      } else if (this.firstCrypto === 'ETH' && this.secondCrypto == 'BTC') {
        this.result = convert.ETH.BTC(+this.amount);
        return;
      } else if (this.firstCrypto === 'ETH' && this.secondCrypto == 'USDT') {
        this.result = convert.ETH.USDT(+this.amount);
        return;
      } else if (this.firstCrypto === 'USDT' && this.secondCrypto == 'BTC') {
        this.result = convert.USDT.BTC(+this.amount);
        return;
      } else if (this.firstCrypto === 'USDT' && this.secondCrypto == 'ETH') {
        this.result = convert.USDT.ETH(+this.amount);
        return;
      }
    }
  }
}
</script>

<style setup>
  .selectors {
    display: flex;
    justify-content: space-around;
    width: 700px;
    margin: 0 auto;
  }
  .error {
    color: red;
    position: relative;
    top: 20px;
    margin-bottom: 10px
  }
  .result {
    color: #fff;
    position: relative;
    top: 20px;
    margin-bottom: 10px
  }
  .fav-button {
    margin-left: 20px;
  }
</style>