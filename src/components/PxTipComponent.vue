<template>
  <div class="tip">
    <div class="tip__put-tip">
      <div class="tip__put-tip__bill" :class="{ isActiveBeZero: bill === '0' }">
        <label>Bill</label>
        <label class="be-zero" :class="{ isActive: bill === '0' }"
          >Cant't be zero</label
        >
        <input
          type="number"
          placeholder="0"
          :class="{ isBeZero: bill === '0' }"
          :value="bill"
          @input="updateValueBill"
        />
        <img src="@/assets/icon-dollar.svg" alt="" />
      </div>
      <div class="tip__put-tip__tip">
        <label>Select tip</label>
        <div>
          <button
            @click="amountTip(0.05)"
            :class="{ isActive: perTipValue == 0.05 }"
          >
            5%
          </button>
          <button
            @click="amountTip(0.1)"
            :class="{ isActive: perTipValue == 0.1 }"
          >
            10%
          </button>
          <button
            @click="amountTip(0.15)"
            :class="{ isActive: perTipValue == 0.15 }"
          >
            15%
          </button>
          <button
            @click="amountTip(0.25)"
            :class="{ isActive: perTipValue == 0.25 }"
          >
            25%
          </button>
          <button
            @click="amountTip(0.5)"
            :class="{ isActive: perTipValue == 0.5 }"
          >
            50%
          </button>
          <button v-if="customIsActive" class="custom" @click="activeCustom()">
            Custom
          </button>
          <input
            v-else
            type="number"
            name=""
            placeholder="0"
            :value="custom"
            @input="updateValuePercentage"
            min="0"
          />
        </div>
      </div>
      <div
        class="tip__put-tip__number-people"
        :class="{ isActiveBeZero: numberPeople === '0' }"
      >
        <label>Number of People</label>
        <label class="be-zero" :class="{ isActive: numberPeople === '0' }"
          >Cant't be zero</label
        >
        <input
          type="number"
          placeholder="0"
          :class="{ isBeZero: numberPeople === '0' }"
          :value="numberPeople"
          @input="updateValuePerson"
          min="0"
        />
        <img src="@/assets/icon-person.svg" alt="" />
      </div>
    </div>
    <div class="tip__amount">
      <div class="tip__amount__div">
        <div
          class="tip__amount__div__tip"
          :class="{ isActiveBeZero: numberPeople === '0' }"
        >
          <label>Tip Amount</label><label>/ person</label>
          <label v-if="!tipAmountComputed"> $0 </label>
          <label v-else> ${{ tipAmountComputed }}</label>
        </div>
        <div class="tip__amount__div__total">
          <label>Total</label><label>/ person</label
          ><label v-if="!tipAmountComputed"> $0 </label>
          <label v-else> ${{ totalAmountComputed }}</label>
        </div>
      </div>
      <button
        class="tip__amount__reset"
        :class="{
          isActive: totalAmountComputed > 0,
        }"
        @click="resetTip()"
        :disabled="totalAmountComputed > 0"
      >
        RESET
      </button>
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
      custom: "",
      customIsActive: true,
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
      return this.customIsActive == false
        ? this.convertPercentage
        : this.perTipValue;
    },
    convertPercentage() {
      return this.custom / 100;
    },
    tipAmountComputed() {
      return this.billComputed > 0 &&
        this.numberPersonComputed > 0 &&
        this.amountTipComputed > 0
        ? (
            (this.bill *
              (this.customIsActive == false
                ? this.convertPercentage
                : this.perTipValue)) /
            this.numberPeople
          ).toFixed(2)
        : (0).toFixed(2);
    },
    totalAmountComputed() {
      return this.billComputed > 0 &&
        this.numberPersonComputed > 0 &&
        this.amountTipComputed > 0
        ? (
            this.bill *
            (this.customIsActive == false
              ? this.convertPercentage
              : this.perTipValue)
          ).toFixed(2)
        : (0).toFixed(2);
    },
  },
  methods: {
    amountTip(tip, index) {
      this.perTipValue = tip;
      this.customIsActive = true;
    },
    resetTip() {
      this.bill = "";
      this.perTipValue = "";
      this.numberPeople = "";
      this.customIsActive = true;
      this.custom = "";
    },
    activeCustom() {
      this.customIsActive = false;
      this.perTipValue = "";
    },
    updateValueBill(event) {
      const value = event.target.value;
      if (String(value).length <= 5) {
        this.bill = value;
      }
      this.$forceUpdate();
    },
    updateValuePerson(event) {
      const value = event.target.value;
      if (String(value).length <= 5) {
        this.numberPeople = value;
      }
      this.$forceUpdate();
    },
    updateValuePercentage(event) {
      const value = event.target.value;
      if (String(value).length <= 3) {
        this.custom = value;
      }
      this.$forceUpdate();
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
          font-size: 1.3rem;
          border-radius: 0.5rem;
          border: none;
          padding: 0.5rem 0.5rem;
          color: hsl(189, 41%, 97%);
          background: hsl(183, 100%, 15%);
          cursor: pointer;
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
          width: 83%;
          @media only screen and (max-width: 800px) {
            width: 88%;
          }
        }
        input[type="number"]::-webkit-inner-spin-button,
        input[type="number"]::-webkit-outer-spin-button {
          -webkit-appearance: none;
          margin: 0;
        }
        input[type="number"]:focus {
          outline: none;
          border: 1px solid hsl(172, 67%, 45%);
          box-shadow: none;
        }
        .isActive {
          color: hsl(183, 100%, 15%);
          background: hsl(172, 67%, 45%);
        }
        .custom {
          color: hsl(183, 100%, 15%);
          background: hsl(185, 41%, 84%);
          opacity: 0.6;
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
      .be-zero {
        display: none;
      }
      .isActive {
        display: grid;
        color: red;
        opacity: 0.8;
      }
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
      .isBeZero[type="number"]:focus {
        border: 2px solid red;
      }
      .isBeZero {
        border: 2px solid red;
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
      img {
        position: absolute;
        padding-top: 2rem;
        padding-left: 1rem;
      }
    }
    .isActiveBeZero {
      display: grid;
      grid-template-areas: "a a" "c c";
      label:first-child {
        grid-area: a;
      }
      label:nth-child(2n) {
        grid-area: a;
        text-align: right;
      }
      label:last-child {
        grid-area: c;
      }
    }
  }
  &__amount {
    display: grid;
    grid-row-gap: 3rem;
    background: hsl(183, 100%, 15%);
    border-radius: 1rem;
    padding: 2rem;
    width: 30vh;
    @media only screen and (max-width: 800px) {
      width: 80%;
    }
    &__div {
      display: grid;
      grid-row-gap: 1.5rem;
      &__tip,
      &__total {
        display: grid;
        grid-column-gap: 1rem;
        grid-template-areas: "tip amount" "person amount";
        label:first-child {
          color: hsl(189, 41%, 97%);
          grid-area: tip;
          font-size: 1rem;
          padding-bottom: 4px;
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
          font-size: 1.8rem;
          text-align: right;
          @media only screen and (max-width: 800px) {
            font-size: 1.5rem;
          }
        }
      }
    }
    button {
      cursor: not-allowed;
      opacity: 0.2;
    }
    button,
    .isActive {
      font-weight: bold;
      font-family: "Space Mono", monospace;
      font-size: 1.3rem;
      border-radius: 0.5rem;
      border: none;
      padding: 0.8rem 0.3rem;
      color: hsl(183, 100%, 15%);
      background: hsl(172, 67%, 45%);
    }
    .isActive {
      cursor: pointer;
      opacity: 1;
    }
  }
}
</style>
