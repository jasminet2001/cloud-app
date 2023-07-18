<template>
  <v-sheet>
    <v-row class="mb-4"><h2>Region</h2></v-row>
    <v-row>
      <div class="d-flex flex-row">
        <v-card
          elevation="12"
          class="d-flex flex-row"
          width="226px"
          height="72px"
          @click="SelectCountry('Germany')"
        >
          <v-col cols="3">
            <img
              :style="imageStyle"
              @click="ChangeStyle('1')"
              src="../assets/germany.png"
              style="height: 40px; width: 40px; border-radius: 50%"
            />
          </v-col>
          <v-col cols="6" class="d-flex align-center justify-center">
            <strong>Germany</strong>
          </v-col>
        </v-card>
        <v-card
          elevation="12"
          class="d-flex flex-row mx-4"
          width="226px"
          height="72px"
          @click="SelectCountry('US')"
        >
          <v-col cols="3">
            <img
              :style="imageStyle"
              @click="ChangeStyle('2')"
              src="../assets/usa.jpg"
              style="height: 40px; width: 40px; border-radius: 50%"
            />
          </v-col>
          <v-col cols="6" class="d-flex align-center justify-center">
            <strong>Los Angeles</strong>
          </v-col>
        </v-card>
        <v-card
          elevation="12"
          class="d-flex flex-row mx-4"
          width="226px"
          height="72px"
          @click="SelectCountry('Japan')"
        >
          <v-col cols="3" class="d-flex align-center">
            <img
              :style="imageStyle"
              @click="ChangeStyle('3')"
              src="../assets/sg.png"
              style="height: 40px; width: 40px; border-radius: 50%"
            />
          </v-col>
          <v-col cols="6" class="d-flex align-center justify-center">
            <strong>Singapore</strong>
          </v-col>
        </v-card>
      </div>
    </v-row>

    <v-row class="mt-16 mb-8"><h2>Plan</h2></v-row>
    <v-row>
      <template>
        <v-data-table
          :headers="headers"
          :items="specs"
          :items-per-page="6"
          class="elevation-1"
        >
          <template slot="item.cpu" slot-scope="{ item }">
            <td>
              <!-- <v-radio-group>
                <v-radio
                  v-model="radioPlan"
                  value="success"
                  :label="item.cpu"
                ></v-radio>
              </v-radio-group> -->
              <input
                type="radio"
                name="cpu"
                id="cpuname"
                v-model="radioPlan"
                :value="item"
                checked
                v-on:change="checkPlan"
              />
              <label for="cpuname" style="margin: 1em">{{ item.cpu }}</label>
            </td>
          </template>
          <template slot="item.price" slot-scope="{ item }">
            <v-tooltip bottom>
              <template v-slot:activator="{ on }">
                <td class="custom-price-column">
                  {{ item.price }}
                  <v-icon v-on="on">mdi-information-slab-circle-outline</v-icon>
                </td>
              </template>
              <span>{{ item.hourly + "/hour" }}</span>
            </v-tooltip>
          </template>
          <template slot="item.memory" slot-scope="{ item }">
            <td>{{ item.memory }} GB</td>
          </template>
          <template slot="item.speed" slot-scope="{ item }">
            <td>{{ item.memory }} GB</td>
          </template>
        </v-data-table>
      </template>
    </v-row>
  </v-sheet>
</template>


<script>
export default {
  name: "PlanComponent",
  data() {
    return {
      headers: [
        {
          text: "CPU",
          align: "center",
          value: "cpu",
        },
        { text: "Memory", value: "memory", align: "center" },
        { text: "Connection Speed", value: "speed", align: "start" },
        { text: "Monthly Price", value: "price", align: "center" },
      ],
      specs: [
        {
          planID: 1,
          cpu: "",
          memory: "",
          speed: "",
          price: 0,
          hourly: 0,
          regionID: "",
        },
      ],
      country: "",
      grayscaleOne: true,
      grayscaleTwo: true,
      grayscaleThree: true,
      radioPlan: "",
    };
  },
  methods: {
    async PlanSelected() {
      let axios = require("axios");
      let config = {
        method: "get",
        url: "https://assignment.abrnoc.com/plans?region=" + this.country,
        headers: {
          Accept: "application/json",
        },
      };
      let that = this;
      await axios(config)
        .then(function (response) {
          that.specs = response.data.map((item) => {
            return {
              cpu: item.cpu_cores,
              memory: item.memory_size_in_GB,
              speed: item.connection_up_bound_speed,
              price: "$" + item.monthly_price,
              hourly: item.hourly_price,
              regionID: item.region_id,
            };
          });
        })
        .catch(() => {});
    },
    async SelectCountry(country) {
      this.country = country;
      this.PlanSelected();
    },
    async ChangeStyle(number) {
      if (number == "1") {
        this.grayscaleOne = !this.grayscaleOne;
      } else if (number == "2") {
        this.grayscaleTwo = !this.grayscaleTwo;
      } else {
        this.grayscaleThree = !this.grayscaleThree;
      }
      console.log("change");
    },
    // async radio() {
    //   this.radioPlan = false;
    // },
    checkPlan() {
      const info = this.radioPlan;

      if (this.radioPlan.cpu == 1) {
        this.$toast.warning("Plan is not available for selected region.");
        this.$emit("message", null);
      } else {
        this.$emit("message", info);
      }
    },
  },
  beforeMount() {
    this.SelectCountry("Germany");
  },
  computed: {
    imageStyle() {
      return {
        filter:
          !this.grayscaleOne || !this.grayscaleOne || !this.grayscaleThree
            ? "grayscale(0)"
            : "grayscale(100%)",
      };
    },
  },
};
</script>

<style scoped>
.thumbnail-image > img {
  width: 100%;
  height: auto;
  transition: all 250ms;
  filter: grayscale(100%);
}

.thumbnail-image:active > img {
  box-shadow: 2px 2px 6px 1px rgba(0, 0, 0, 0.5);
  visibility: hidden;
  filter: none;
}
</style>