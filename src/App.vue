<template>
  <v-app class="wrapper">
    <v-row no-gutters>
      <v-col cols="2"></v-col>
      <v-col cols="10"> <top-row class="px-0 py-0"></top-row></v-col>
    </v-row>
    <navbar-component />
    <div class="container">
      <v-row>
        <v-col cols="12">
          <v-row class="d-flex justify-start">
            <Plan style="margin-top: 2em" @message="handleInfo"
          /></v-row>
          <v-row class="d-flex justify-start mt-8" style="margin-right: 20em">
            <OSComponent @os="handleOS"
          /></v-row>
          <v-row class="d-flex justify-start">
            <BottomRow @host="handleHost"
          /></v-row>
        </v-col>
      </v-row>
    </div>
    <v-col class="d-flex justify-start"
      ><QuantityComponent :message="information"
    /></v-col>
  </v-app>
</template>

<script>
import NavbarComponent from "./components/NavbarComponent.vue";
import TopRow from "./components/TopRow.vue";
import Plan from "./components/Plan.vue";
import OSComponent from "./components/OSComponent.vue";
import BottomRow from "./components/BottomRow.vue";
import QuantityComponent from "./components/QuantityComponent.vue";
export default {
  name: "App",
  components: {
    TopRow,
    NavbarComponent,
    Plan,
    OSComponent,
    BottomRow,
    QuantityComponent,
  },
  data: () => ({
    information: [
      {
        plan: Object,
        userinfo: Object,
        os: "",
        host: "",
      },
    ],
  }),
  methods: {
    handleInfo(msg) {
      this.information.plan = msg;
    },
    handleOS(os) {
      this.information.os = os;
    },
    handleHost(host) {
      this.information.host = host;
    },
  },
};
</script>

<style scoped>
.container {
  background-color: white;
  width: 80%;
  margin-left: 18em;
  margin-top: 4em;
  padding: 4em;
}
.wrapper {
  background-color: #f1f9fe;
}
</style>
