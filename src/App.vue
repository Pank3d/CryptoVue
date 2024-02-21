<template>
  <div>
    <h1>CRYPTO</h1>
    <p v-if="error !== ''">{{ error }}</p>
    <p v-if="errorToAdd !== ''">{{ errorToAdd }}</p>
    <p v-if="result !== 0" className="input">
      {{ result + ` ${this.cryptoSecond}` }}
    </p>
    <Input
      :changeAmount="changeAmount"
      :convert="convert"
      :favourite="favourite"
    />
    <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs" />

    <div className="selectors">
      <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
      <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
    </div>
  </div>
</template>

<script>
import Input from "./components/Input.vue";
import Selector from "./components/Selector.vue";
import CryptoConvert from "crypto-convert";
import Favourite from "./components/Favourite.vue";

const convert = new CryptoConvert();

export default {
  components: { Input, Selector, Favourite },
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      favs: [],
      errorToAdd: "",
    };
  },
  methods: {
    changeAmount(val) {
      this.amount = val;
    },
    getFromFavs(index) {
      this.cryptoFirst = this.favs[index].from;
      this.cryptoSecond = this.favs[index].to;
    },

    setCryptoFirst(val) {
      this.cryptoFirst = val;
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val;
    },
    async convert() {
      if (this.amount <= 0) {
        this.error = "error zdes";
        return;
      } else if (this.cryptoFirst === this.cryptoSecond) {
        this.error = "error nelzya tak ";
        return;
      } else if (
        this.cryptoFirst === "" ||
        this.cryptoSecond === "" ||
        (this.cryptoSecond === "" && this.cryptoFirst === "")
      ) {
        this.error = "error suka nelzya tak";
        return;
      }

      this.error = "";
      await convert.ready();
      if (this.cryptoFirst === "BTC" && this.cryptoSecond === "ETH") {
        this.result = convert.BTC.ETH(this.amount);
      } else if (this.cryptoFirst === "BTC" && this.cryptoSecond === "USDT") {
        this.result = convert.BTC.USDT(this.amount);
      } else if (this.cryptoFirst === "ETH" && this.cryptoSecond === "USDT") {
        this.result = convert.ETH.USDT(this.amount);
      } else if (this.cryptoFirst === "ETH" && this.cryptoSecond === "BTC") {
        this.result = convert.ETH.BTC(this.amount);
      } else if (this.cryptoFirst === "USDT" && this.cryptoSecond === "BTC") {
        this.result = convert.USDT.BTC(this.amount);
      } else if (this.cryptoFirst === "USDT" && this.cryptoSecond === "ETH") {
        this.result = convert.USDT.ETH(this.amount);
      }
    },
    favourite() {
      if (this.cryptoFirst !== this.cryptoSecond) {
        this.favs.push({
          from: this.cryptoFirst,
          to: this.cryptoSecond,
        });
      } else {
        this.errorToAdd = "Так нельзя";
      }
    },
  },
};
</script>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 700px;
  margin: 0 auto;
}

.input {
  display: block;
  width: 100%;
  height: calc(2.25rem + 2px);
  padding: 0.375rem 0.75rem;
  font-family: inherit;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #bdbdbd;
  border-radius: 0.25rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
</style>
