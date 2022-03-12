<template>
  <div class="tip">
    <div class="tip__put-tip">
      <div class="tip__put-tip__bill">
        <label>Bill</label>
        <input type="number" v-model="bill" placeholder="0" />
      </div>
      <div class="tip__put-tip__tip">
        <label>Select tip</label>
        <div>
          <button @click="amountTip(0.05)">5%</button>
          <button @click="amountTip(0.1)">10%</button>
          <button @click="amountTip(0.15)">15%</button>
          <button @click="amountTip(0.25)">25%</button>
          <button @click="amountTip(0.5)">50%</button>
          <button @click="amountTip(1)">100%</button>
        </div>
      </div>
      <div class="tip__put-tip__number-people">
        <label>Number of People</label>
        <input type="number" v-model="numberPeople" placeholder="0" />
      </div>
    </div>
    <div class="tip__amount">
      <div class="tip__amount__tip">
        <label>Tip Amount</label><label>/person</label
        ><label>{{ tipAmountComputed }}</label>
      </div>
      <div class="tip__amount__total">
        <label>Total</label><label>/person</label
        ><label> {{ totalAmountComputed }}</label>
      </div>
      <button class="tip__amount__reset" @click="resetTip()">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "tip-component",
  data() {
    return {
      bill: "",
      perTipValue: "",
      numberPeople: "",
    };
  },
  computed: {
    billComputed() {
      return this.bill;
    },
    numberPersonComputed() {
      return this.numberPeople;
    },
    amountTipComputed() {
      return this.perTipValue;
    },
    tipAmountComputed() {
      return this.billComputed != "" &&
        this.numberPersonComputed != "" &&
        this.amountTipComputed != ""
        ? (this.bill * this.perTipValue) / this.numberPeople
        : null;
    },
    totalAmountComputed() {
      return this.billComputed != "" &&
        this.numberPersonComputed != "" &&
        this.amountTipComputed != ""
        ? this.bill * this.perTipValue
        : null;
    },
  },
  methods: {
    amountTip(tip, index) {
      this.perTipValue = tip;
    },
    resetTip() {
      this.bill = "";
      this.perTipValue = "";
      this.numberPeople = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.tip {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-column-gap: 2rem;
  background: hsl(0, 0%, 100%);
  padding: 2rem;
  border-radius: 1rem;
  font-family: "Space Mono", monospace;
  font-weight: bold;
  height: min-content;

  @media only screen and (max-width: 600px) {
    grid-template-columns: 1fr;
    grid-row-gap: 2rem;
    padding: 2rem;
  }
  &__put-tip {
    display: grid;
    grid-row-gap: 1rem;
    &__tip {
      label {
        color: hsl(186, 14%, 43%);
      }
      div {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-column-gap: 0.5rem;
        grid-row-gap: 0.5rem;
        button {
          font-family: "Space Mono", monospace;
          font-weight: bold;
          font-size: 1.5rem;
          border-radius: 0.5rem;
          border: none;
          padding: 0.3rem;
          color: hsl(189, 41%, 97%);
          background: hsl(183, 100%, 15%);
          cursor: pointer;
        }
      }
    }
    &__bill,
    &__number-people {
      input[type="number"]::-webkit-inner-spin-button,
      input[type="number"]::-webkit-outer-spin-button {
        -webkit-appearance: none;
        margin: 0;
      }
      label {
        color: hsl(186, 14%, 43%);
      }
      input {
        text-align: right;
        padding: 4px 0.5rem;
        color: hsl(183, 100%, 15%);
        font-family: "Space Mono", monospace;
        font-weight: bold;
        font-size: 1.5rem;
        border-radius: 0.5rem;
        border: none;
        background: hsl(189, 41%, 97%);
      }
    }
  }
  &__amount {
    display: grid;
    background: hsl(183, 100%, 15%);
  }
}
</style>
