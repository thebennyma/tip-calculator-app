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
          <button disabled>Custom</button>
        </div>
      </div>
      <div class="tip__put-tip__number-people">
        <label>Number of People</label>
        <input type="number" v-model="numberPeople" placeholder="0" />
      </div>
    </div>
    <div class="tip__amount">
      <div class="tip__amount__div">
        <div class="tip__amount__div__tip">
          <label>Tip Amount</label><label>/person</label>
          <label v-if="!tipAmountComputed"> $0 </label>
          <label v-else> ${{ tipAmountComputed }}</label>
        </div>
        <div class="tip__amount__div__total">
          <label>Total</label><label>/person</label
          ><label v-if="!tipAmountComputed"> $0 </label>
          <label v-else> ${{ totalAmountComputed }}</label>
        </div>
      </div>
      <button class="tip__amount__reset" @click="resetTip()">RESET</button>
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
        ? ((this.bill * this.perTipValue) / this.numberPeople).toFixed(2)
        : (0).toFixed(2);
    },
    totalAmountComputed() {
      return this.billComputed != "" &&
        this.numberPersonComputed != "" &&
        this.amountTipComputed != ""
        ? (this.bill * this.perTipValue).toFixed(2)
        : (0).toFixed(2);
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

  @media only screen and (max-width: 800px) {
    grid-template-columns: 1fr;
    grid-row-gap: 2rem;
    padding: 2rem;
  }
  &__put-tip {
    display: grid;
    grid-row-gap: 1rem;
    &__tip {
      display: grid;
      grid-row-gap: 0.2rem;
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
        @media only screen and (max-width: 800px) {
          grid-template-columns: 1fr 1fr;
          button {
            padding: 0.6rem 1rem;
          }
        }
      }
    }
    &__bill,
    &__number-people {
      display: grid;
      grid-row-gap: 0.2rem;
      input[type="number"]::-webkit-inner-spin-button,
      input[type="number"]::-webkit-outer-spin-button {
        -webkit-appearance: none;
        margin: 0;
      }
      input[type="number"]:focus {
        outline: none;
        border: 2px solid hsl(172, 67%, 45%);
        box-shadow: none;
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
    grid-row-gap: 2rem;
    background: hsl(183, 100%, 15%);
    border-radius: 1rem;
    padding: 2rem;
    width: 30vh;
    &__div {
      &__tip,
      &__total {
        display: grid;
        grid-column-gap: 1rem;
        grid-template-areas: "tip amount" "person amount";
        label:first-child {
          color: hsl(189, 41%, 97%);
          grid-area: tip;
          font-size: 1rem;
        }
        label:nth-child(2n) {
          color: white;
          grid-area: person;
          font-size: 0.7rem;
          width: 100px;
          color: hsl(184, 14%, 56%);
        }
        label:last-child {
          color: hsl(172, 67%, 45%);
          grid-area: amount;
          font-size: 2.5rem;
          text-align: right;
          @media only screen and (max-width: 800px) {
            font-size: 1.5rem;
          }
        }
      }
    }
    button {
      font-weight: bold;
      font-family: "Space Mono", monospace;
      font-size: 1.3rem;
      border-radius: 0.5rem;
      border: none;
      padding: 0.8rem 0.3rem;
      color: hsl(183, 100%, 15%);
      background: hsl(172, 67%, 45%);
      cursor: pointer;
    }
  }
}
</style>
