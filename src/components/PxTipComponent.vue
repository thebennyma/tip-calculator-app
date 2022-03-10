<template>
  <div>
    <div>
      <div>
        <label>Bill</label>
        <input type="number" v-model="bill" placeholder="0" />
      </div>
      <div>
        <label>Select tip %</label>
        <button @click="amountTip(0.05)">5%</button>
        <button @click="amountTip(0.1)">10%</button>
        <button @click="amountTip(0.15)">15%</button>
        <button @click="amountTip(0.25)">25%</button>
        <button @click="amountTip(0.5)">50%</button>
        <button disabled>Custom</button>
      </div>
      <div>
        <label>Number of People</label>
        <input type="number" v-model="numberPeople" placeholder="0" />
      </div>
    </div>
    <div>
      <div>
        <label>Tip Amount</label><label>/person</label
        ><label>{{ tipAmountComputed }}</label>
      </div>
      <div>
        <label>Total</label><label>/person</label
        ><label> {{ totalAmountComputed }}</label>
      </div>
      <button @click="resetTip()">Reset</button>
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

<style></style>
