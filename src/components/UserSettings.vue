<template>
  <v-navigation-drawer class="settings-drawer" v-model="drawer" absolute temporary right>
    <v-subheader>Settings</v-subheader>
    <div class="switch-wrapper">
      <div>Fahrenheit</div>
      <v-switch
        @change="onUnitTypeChangeHandler"
        false-value="f"
        true-value="c"
        v-model="temperatureUnits"
      ></v-switch>
      <div>Celcius</div>
    </div>  
  </v-navigation-drawer>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  props: ["value"],
  computed: {
    ...mapGetters(["getUnits"])
  },
  created() {
    this.temperatureUnits = this.getUnits;
  },
  watch: {
    value() {
      this.drawer = this.value;
    },
    drawer() {
      this.$emit("input", this.drawer);
    }
  },
  data() {
    return {
      temperatureUnits: "",      
      drawer: this.value
    };
  },

  methods: {
    onUnitTypeChangeHandler() {
      this.$store.dispatch("setUnits", this.temperatureUnits);
    }
  }
};
</script>