<template>
  <v-card class="overflow-hidden" dir="rtl">
    <v-navigation-drawer
      permanent
      v-model="$data[$vuetify.breakpoint.smAndDown ? 'drawer' : 'value']"
      :value="true"
      fixed
      hide-overlay
      rail
      left
      dir="ltr"
    >
      <v-list dense nav>
        <v-list-item-group
          v-model="group"
          active-class="grey lighten-4--text text--accent-4"
        >
          <v-list-item class="py-2" link to="/user/dashboard">
            <v-list-item-icon>
              <img src="../assets/logo.svg" />
            </v-list-item-icon>
          </v-list-item>

          <v-divider></v-divider>

          <v-list-item class="py-2" link to="/user/dashboard">
            <v-list-item-icon>
              <v-icon>mdi-view-dashboard-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Dashboard</v-list-item-title>
          </v-list-item>

          <v-list-item
            class="py-2"
            link
            to="/user/editprofile"
            style="background-color: #2c5eff; color: white"
          >
            <v-list-item-icon>
              <v-icon color="white">mdi-plus-box-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Instances</v-list-item-title>
          </v-list-item>

          <v-list-item link to="/user/changepass">
            <v-list-item-icon>
              <v-icon>mdi-content-copy</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Snapshots</v-list-item-title>
          </v-list-item>

          <v-list-item class="py-2" link to="/user/bookmarks">
            <v-list-item-icon>
              <v-icon>mdi-key-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-title>SSH Keys</v-list-item-title>
          </v-list-item>

          <v-list-item class="py-2" link to="/user/subads" disabled>
            <v-list-item-icon>
              <v-icon>mdi-form-select</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Volume</v-list-item-title>
          </v-list-item>

          <v-divider></v-divider>

          <v-list-item class="py-2" link to="/user/upgrade">
            <v-list-item-icon>
              <v-icon>mdi-currency-usd</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Billing</v-list-item-title>
            <v-list-item-title>
              <v-icon v-bind="props">mdi-menu-down</v-icon>
            </v-list-item-title>
          </v-list-item>

          <v-list-item class="py-2" link to="payment">
            <v-list-item-icon>
              <v-icon>mdi-wifi</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Networking</v-list-item-title>
          </v-list-item>

          <v-list-item class="py-2" link to="/user/myads">
            <v-list-item-icon>
              <v-icon>mdi-file-chart-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Report</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>

      <v-list class="mx-4 my-12">
        <v-btn outlined color="#C5C5C5">
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-headphones</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Support</v-list-item-title>
          </v-list-item>
        </v-btn>
        <v-btn outlined color="#C5C5C5" class="pr-12 my-2">
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-help</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Help</v-list-item-title>
          </v-list-item>
        </v-btn>
      </v-list>
    </v-navigation-drawer>
  </v-card>
</template>

<script>
export default {
  name: "NavbarComponent",
};
</script>