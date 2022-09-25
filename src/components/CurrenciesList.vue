<template>
  <div class="container">
    <div class="currencies">
      <label class="label currencies-find" for="find">
        найти валюту:<br />
        <input class="clickable" type="search" name="find" v-model="search" />
      </label>
      <label class="label currencies-choice" for="current-valute"
        >текущая валюта:<br />
        <select
          class="clickable select"
          name="current-valute"
          id="select-id"
          v-model="selectedCurrency"
        >
          <option
            v-for="currency in currencies"
            :key="currency.ID"
            :value="currency"
          >
            {{ currency.CharCode }}
          </option>
        </select>
        <br />
        {{ selectedCurrency.Name }}
      </label>
    </div>
    <div class="list-wrapper">
      <ul class="list">
        <li
          class="list-item"
          v-for="item in sortCurrenciesByName"
          :key="item.ID"
        >
          <div class="currency-name">
            {{ item.Name }}<br />
            <small>({{ item.CharCode }})</small>
          </div>
          <div class="currency-value">
            {{ (item.Value / selectedCurrency.Value).toFixed(4) }}
            {{ selectedCurrency.CharCode }}
          </div>
          <div class="change">
            {{
              (
                item.Value / selectedCurrency.Value -
                item.Previous / selectedCurrency.Previous
              ).toFixed(4)
            }}
          </div>
          <NegativeArrow
            v-if="
              item.Value / selectedCurrency.Value >
              item.Previous / selectedCurrency.Previous
            "
          />
          <PositiveArrow v-else />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import NegativeArrow from './NegativeArrow.vue';
import PositiveArrow from './PositiveArrow.vue';
import { mapActions, mapGetters } from 'vuex';

export default {
  components: { NegativeArrow, PositiveArrow },
  mounted() {
    this.fetchCurrencies();
  },

  data() {
    return {
      search: '',
      selectedCurrency: {
        CharCode: 'RUB',
        Value: 1,
        Name: 'Российских рублей',
        Previous: 1,
      },
    };
  },

  computed: {
    ...mapGetters(['currencies']),
    sortCurrenciesByName() {
      const query = this.search.toLowerCase();
      const selectedCurrency = this.selectedCurrency;
      return this.currencies.filter(
        (element) =>
          element !== selectedCurrency &&
          (element.Name.toLowerCase().includes(query) ||
            element.CharCode.toLowerCase().includes(query))
      );
    },
  },
  methods: {
    ...mapActions(['fetchCurrencies']),
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 800px;
  margin: 0px auto;
}
.currencies {
  display: grid;
  grid-template-columns: 1fr 1fr;
  width: 100%;
}

.list-item {
  list-style: none;
  display: flex;
  align-items: center;
  margin-bottom: 15px;
  border-bottom: 2px solid rgb(224, 146, 56);
}
.list {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  column-gap: 80px;
}
.currency-name {
  width: 200px;
}
.currency-value {
  margin-left: 40px;
  margin-right: 40px;
  text-align: center;
  width: 50px;
}
.label {
  font-size: 1.5rem;
}
.clickable {
  width: 140px;
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
.select {
  cursor: pointer;
  padding-left: 1rem;
}
</style>
