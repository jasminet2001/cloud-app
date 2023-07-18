<template>
  <v-col cols="12">
    <v-card class="container" fluid elevation="1">
      <div div class="d-flex flex-row pa-4 align-center start">
        <p>Instances / New Instance</p>
      </div>
      <div class="d-flex flex-row pa-2 align-center end">
        <v-icon class="ma-2">mdi-bell-badge-outline</v-icon>
        <v-text-field
          v-model="numberValue"
          hide-details
          single-line
          class="ma-2"
          type="number"
        />
        <v-divider vertical class="ma-2"></v-divider>
        <v-icon class="ma-2">mdi-account-circle-outline</v-icon>
      </div>
    </v-card>
  </v-col>
</template>

<script>
export default {
  name: "TopRowComponent",
  data() {
    return {
      numberValue: 0,
    };
  },
  methods: {},
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  width: 100%;
  padding: 0 !important;
}
.end {
  justify-self: flex-end;
}
.start {
  justify-self: flex-start;
}
</style>