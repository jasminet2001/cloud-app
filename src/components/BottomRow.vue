<template>
  <v-container style="margin-left: -3em; border: none; width: 87%">
    <v-row class="my-4"><h2>SSH Key (optional)</h2></v-row>
    <v-row no-gutters>
      <v-col order="first" class="pt-4" width="250px">
        <v-card width="226px" height="56px" @click="AddNew">
          <v-row class="px-2">
            <v-col cols="2"><v-icon>mdi-plus-circle-outline</v-icon></v-col>
            <v-col cols="10"><strong>Add New</strong></v-col>
          </v-row>
        </v-card>
      </v-col>

      <v-col
        sm="6"
        md="4"
        lg="4"
        cols="12"
        auto
        v-for="index in clickCount"
        :key="index"
      >
        <v-row v-if="add" no-gutters>
          <v-col no-gutters>
            <v-card width="226px" height="56px" class="mt-2">
              <v-row no-gutters>
                <v-col cols="3">
                  <v-checkbox
                    v-model="checkbox"
                    dense
                    class="mt-2 ml-2"
                  ></v-checkbox>
                </v-col>
                <v-col cols="6" class="mt-3">Key Name {{ index }}</v-col>
                <v-col cols="3">
                  <v-tooltip bottom>
                    <template v-slot:activator="{ on }">
                      <v-icon v-on="on" class="mt-3 mr-16"
                        >mdi-information-slab-circle-outline</v-icon
                      >
                    </template>
                    <span>username@hostname</span>
                  </v-tooltip>
                </v-col>
              </v-row>
            </v-card>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
    <v-row class="mb-2 mt-8"><h2>Hostname</h2></v-row>
    <v-row>
      <v-text-field
        :rules="[required]"
        clearable
        placeholder="Name 1"
        outlined
        v-model="hostname"
        style="padding-right: 30em"
        @click="toasts"
      ></v-text-field>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "BottomRow",
  data() {
    return {
      add: false,
      clickCount: 0,
      hostname: "",
      checkbox: false,
      successAlert: false,
      failAlert: false,
    };
  },
  methods: {
    AddNew() {
      this.add = true;
      this.clickCount = this.clickCount + 1;
    },
    required(v) {
      return !!v || "Field is required";
    },
    async toasts() {
      //checks if a string has characters $, or #, or@, or *, or & or any special characters
      const isValidHostname =
        /^(?!-)[A-Za-z0-9-]{1,63}(?<!-)(\.[A-Za-z0-9-]{1,63})*/;
      const isHostnameValid = isValidHostname.test(this.hostname);
      console.log(isHostnameValid);
      if (this.hostname == "") {
        this.$toast.error("Please Enter hostname.");
      }
      if (!isHostnameValid && this.hostname != "") {
        this.$toast.error("This field contains invalid characters.");
      }
      if (isHostnameValid && this.hostname != "") {
        this.$emit("host", this.hostname);
      }
    },
  },
};
</script>