<template>
  <v-app color="#dadada">
    <NavigationDrawer />
    <v-content>
      <v-toolbar 
        dark 
        :color="headerColor" 
      >
        <v-btn 
          class="ml-3 mr-3" 
          icon 
          @click="changeNavigationView" 
          href="#"
        >
          <v-icon v-if="expandOnHover">mdi-view-quilt</v-icon>
          <v-icon v-else>mdi-dots-vertical</v-icon>
        </v-btn>
        <div class="heading"> {{ currentRouteName }} </div>
        <v-spacer></v-spacer>
        <v-menu offset-y>
        <template v-slot:activator="{ on }">
          <v-btn
            v-on="on"
            icon
            href="#"
          >
            <v-icon>mdi-refresh mdi-spin</v-icon>
          </v-btn>
        </template>
        <v-color-picker
          v-model="color"
          hide-canvas 
          hide-inputs 
          show-swatches
          class="mx-auto"
        ></v-color-picker>
      </v-menu>
      </v-toolbar>
      <Loader />
      <router-view :class='showLoader ? "tw-hidden" : ""'></router-view>
    </v-content>
  </v-app>
</template>
<script>
import NavigationDrawer from '@/components/NavigationDrawer'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  components: {
    NavigationDrawer,
    Loader,
  },
  data: () => ({
    
  }),
  computed: {
    headerColor() {
      return this.$store.state.headerColor;
    },
    expandOnHover() {
      return this.$store.state.expandOnHover;
    },
    miniVariant() {
      return this.$store.state.miniVariant;
    },
    color: {
      get() {
        return this.$store.state.headerColor;
      },
      set(value) {
        this.$store.state.headerColor = value;   
      }
    },
    showLoader: {
      get() {
        return this.$store.state.showLoader;
      },
      set() {
        this.$store.state.showLoader = !this.$store.state.showLoader;   
      }
    },
    currentRouteName() {
      return this.$route.name;
    }
  },
  methods: {
    changeNavigationView() {
      this.$store.state.expandOnHover = !this.$store.state.expandOnHover;
      this.$store.state.miniVariant = !this.$store.state.miniVariant;
    }
  }
}
</script>
<style>
.logo-mini {
  float: left;
  text-align: center;
  margin-right: 15px;
}
</style>