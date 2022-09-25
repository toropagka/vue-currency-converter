<template>
  <div class="containers">
    <label class="label"
      >выберите валюту<br />
      <select class="clickable" id="select" v-model="value">
        <option
          :value="currency"
          v-for="currency in currencies"
          :key="currency.ID"
        >
          {{ currency.CharCode }}
        </option>
      </select>
    </label>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';

export default {
  mounted() {
    this.fetchCurrencies();
  },
  props: {
    modelValue: Object,
  },
  emits: ['update:modelValue'],
  computed: {
    ...mapGetters(['currencies']),
    value: {
      get() {
        return this.modelValue;
      },
      set(value) {
        this.$emit('update:modelValue', value);
      },
    },
  },
  methods: {
    ...mapActions(['fetchCurrencies']),
  },
};
</script>

<style scoped>
.containers {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.label {
  font-size: 1.5rem;
}
.clickable {
  cursor: pointer;
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
</style>
