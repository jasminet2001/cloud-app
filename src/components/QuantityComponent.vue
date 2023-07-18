<template>
  <v-sheet style="margin-left: 0em">
    <v-card
      width="283px"
      height="334px"
      class="my-4 pa-8 sticky"
      elevation="12"
      rounded
    >
      <v-row class="d-flex justify-center my-2"
        ><p>instance quantity:</p></v-row
      >
      <v-row class="d-flex justify-center">
        <div>
          <button @click="decrement" class="btn">-</button>
          <input
            type="number"
            class="input"
            id="stepper"
            :value="count"
            min="0"
            max="100"
            step="2"
            readonly
          />
          <button @click="increment" class="btn">+</button>
        </div>
      </v-row>
      <v-row class="d-flex justify-center">
        <v-checkbox v-model="checkbox" label="Enable IPv4"></v-checkbox>
      </v-row>
      <v-row class="d-flex justify-center"> <v-divider></v-divider></v-row>
      <v-row class="d-flex justify-center">
        <h2 class="my-2">Total ${{ total }}/month</h2>
      </v-row>
      <v-row class="d-flex justify-center">
        <!-- <span v-if="togglebutton">
        <v-btn color="success">Deploy Now</v-btn>
      </span>
      <span v-else>
        <v-btn @click="toggle" disabled color="success">Deploy Now</v-btn>
      </span> -->
        <!-- :disabled="togglebutton" -->
        <!-- @click.self="toggle" -->
        <v-btn
          color="#00CD82"
          class="white--text px-12"
          @click="showInfo"
          :disabled="isAddButtonDisabled"
          >Deploy Now</v-btn
        >
      </v-row>
    </v-card>
  </v-sheet>
</template>

<script>
export default {
  name: "QuantityComponent",
  props: ["message"],
  data() {
    return {
      count: 0,
      checkbox: false,
      total: 0,
      togglebutton: true,
      userInfo: "",
    };
  },
  methods: {
    increment() {
      this.count++;
    },
    decrement() {
      if (this.count > 0) {
        this.count--;
      }
    },
    toggle() {
      this.togglebutton = !this.togglebutton;
      console.log("dfdf");
    },
    async showInfo() {
      let axios = require("axios");
      let config = {
        method: "get",
        url: "https://assignment.abrnoc.com/user-info",
        headers: {
          Accept: "application/json",
        },
      };
      let that = this;
      await axios(config)
        .then(function (response) {
          that.userInfo = response.data;
          that.$toast.success("Plan Successfully Purchased!");
        })
        .catch(() => {
          that.$toast.error("Please Fill in the information Correctly.");
        });

      //prints user information here
      console.log(this.message);
      console.log(this.userInfo);
      console.log("Enable IPV4: " + this.checkbox);
      console.log("Instance Quantity: " + this.count);
    },
    async totalCost() {
      let that = this;
      //total cost based on monthly price
      console.log(that.message.plan.price.replace("$", ""));
      this.total = that.count * that.message.plan.price.replace("$", "");
    },
  },
  updated() {
    this.totalCost();
  },
  computed: {
    // isAddButtonDisabled() {
    //   console.log(this.total);
    //   if (this.total <= this.userInfo.balance) {
    //     return false;
    //   } else {
    //     return true;
    //   }
    // },
  },
};
</script>

<style scoped>
[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  height: auto;
}
.input {
  width: 8em;
  height: 100%;
  text-align: center;
  border: 0;
  background: transparent;
  color: #000;
}
.btn {
  width: 2em;
  font-weight: 300;
  height: 2em;
  line-height: 0.1em;
  font-size: 1.4em;
  padding: 0em !important;
  background: #eee;
  color: #333;
  border: none;
}
.sticky {
  position: -webkit-sticky;
  position: fixed;
  top: 200px;
  right: 80px;
  padding: 5px;
}
</style>