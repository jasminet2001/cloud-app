<template>
  <div>
    <v-row class="mb-4"><h2>Region</h2></v-row>
    <v-row>
      <div class="d-flex flex-row">
        <v-card
          elevation="12"
          class="d-flex flex-row mx-4"
          width="226px"
          height="72px"
        >
          <v-col cols="3">
            <img
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
        >
          <v-col cols="3">
            <img
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
          class="d-flex flex-row mx-4 card"
          width="226px"
          height="72px"
        >
          <v-col cols="3" class="d-flex align-center">
            <img
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
  </div>
</template>

<script>
export default {
  name: "RegionComponent",
  data() {
    return {
      items: [
        { id: 1, image: "sg.png", country: "Singapore", color: "normal" },
        { id: 2, image: "grey-sg.png", country: "Singapore", color: "grey" },
        { id: 3, image: "usa.jpg", country: "Los Angeles", color: "normal" },
        { id: 4, image: "grey-usa.png", country: "Los Angeles", color: "grey" },
        { id: 5, image: "germany.png", country: "Germany", color: "normal" },
      ],
      showContent: false,
    };
  },
  methods: {
    getImageUrl(image) {
      return require(`@/assets/${image}`);
    },
    toggleContent() {
      this.showContent = !this.showContent;
    },
  },
};
</script>

<style scoped>
.card {
  background-color: #f1f9fe;
}
</style>