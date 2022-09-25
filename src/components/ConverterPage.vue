<template>
  <div class="container">
    <div class="block">
      <CurrencySelectionBlock v-model="first" />
      <input
        class="clickable"
        type="number"
        v-model="howMuch"
        placeholder="введите сумму"
      />
      <span class="input-name"> {{ first.Name }}</span>
    </div>
    <button class="button" @click="reverseCurrency">
      <span class="reverse_arrow">&#128260;</span>
    </button>
    <div class="block">
      <CurrencySelectionBlock v-model="second" />
      <div class="output">
        <p>Вы получите:</p>
        <div class="output-sum">
          <p class="output-sum-text">
            {{ ((first.Value / second.Value) * howMuch).toFixed(4) }}
          </p>
        </div>
        <span class="output-name">{{ second.Name }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import CurrencySelectionBlock from './CurrencySelectionBlock.vue';

export default {
  components: { CurrencySelectionBlock },
  data() {
    return {
      howMuch: '',
      first: {
        'ID': 'R01235',
        'NumCode': '840',
        'CharCode': 'USD',
        'Nominal': 1,
        'Name': 'Доллар США',
        'Value': 58.1006,
        'Previous': 59.8318,
      },
      second: {
        'CharCode': 'RUB',
        'Value': 1,
        'Name': 'Российских рублей',
        'Previous': 1,
      },
    };
  },
  methods: {
    reverseCurrency() {
      [this.first, this.second] = [this.second, this.first];
    },
    firstEvent(value) {
      this.first = value;
    },
    secondEvent(value) {
      this.second = value;
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 1000px;
  margin: 0px auto;
}
.block {
  padding-top: 30px;
  height: 400px;
  width: 400px;
  background-color: aquamarine;
}
.button {
  height: 30px;
  width: 120px;
  cursor: pointer;
  padding: 0;
  border: none;
  background: none;
}
.button:hover {
  transform: scale(1.2, 1.2);
  transition: all 0.2s linear;
}
.clickable {
  margin-top: 70px;
  width: 280px;
  height: 40px;
  border: 1px solid rgb(102, 101, 101);
  box-shadow: 0 1px 0 1px rgba(0, 0, 0, 0.04);
  border-radius: 0.5em;
  background-color: rgb(219, 255, 243);
  font-family: sans-serif;
  font-size: 1.5rem;
  font-weight: 700;
  color: #444;
  line-height: 1.3;
}
.input-name {
  display: block;
  margin-top: 20px;
  font-size: 1.5rem;
}
.output {
  font-size: 1.5rem;
}
.output-sum-text {
  margin: 0 auto;
}
.output-sum {
  display: flex;
  align-items: center;
  text-align: center;
  margin-bottom: 20px;
  background-color: rgb(192, 238, 133);
  height: 40px;
  border-radius: 0.5em;
}
.reverse_arrow {
  margin: 0;
  padding: 0;
  font-size: 50px;
}
</style>
