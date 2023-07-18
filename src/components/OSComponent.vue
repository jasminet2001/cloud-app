<template>
  <v-sheet>
    <v-row style="margin-top: 4em">
      <h2>Operating System</h2>
    </v-row>
    <v-row style="margin-top: 3em">
      <v-col
        v-for="item in osItems"
        :key="item.family"
        cols="12"
        sm="6"
        md="4"
        lg="4"
        class="mb-8"
      >
        <v-card elevation="12" width="226px" height="133px">
          <v-row class="d-flex justify-center ml-2">
            <v-col cols="4">
              <v-img :src="item.img" style="height: 40px; width: 40px" />
            </v-col>
            <v-col cols="8" class="d-flex align-center">
              <strong>{{ item.family }}</strong>
            </v-col>
          </v-row>
          <v-row>
            <v-select
              class="mx-8"
              clearable
              label="Select"
              :items="item.versions"
              outlined
              v-model="operatingsystem"
              v-on:change="saveData"
            ></v-select>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-sheet>
</template>

<script>
export default {
  name: "OSComponent",
  data() {
    return {
      osItems: [
        {
          family: "Windows",
          img: "../assets/windows.png",
          versions: [],
        },
        { family: "Ubuntu", img: "../assets/Ubuntu-old.png", versions: [] },
        { family: "CentOS", img: "../assets/centos.png", versions: [] },
        { family: "Debian", img: "../assets/debian.png", versions: [] },
        { family: "Fedora", img: "../assets/fedora.png", versions: [] },
        { family: "FreeBSD", img: "../assets/freebsd.png", versions: [] },
        { family: "Rocky", img: "../assets/rocky.png", versions: [] },
      ],
      operatingsystem: "",
    };
  },
  methods: {
    async Plans() {
      let axios = require("axios");
      let config = {
        method: "get",
        url: "https://assignment.abrnoc.com/operating_systems",
        headers: {
          Accept: "application/json",
        },
      };
      let that = this;
      await axios(config)
        .then(function (response) {
          response.data.forEach((item) => {
            let osItem = that.osItems.find(
              (os) => os.family.toLowerCase() === item.family.toLowerCase()
            );
            if (osItem) {
              osItem.versions.push(item.version);
            }
          });
        })
        .catch(() => {});
    },
    async saveData() {
      this.$emit("os", this.operatingsystem);
    },
  },
  async mounted() {
    await this.Plans();
  },
};
</script>

