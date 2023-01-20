<template>
  <div class="mapsSetings">
    <TypeMapSelector  :selectedTypeMap="typeMap" @TypeMapChange="updateLocalTypeMap" ></TypeMapSelector>
    <embedded-map :query="mapQuery" :zoom="areaZoom" :typemap="typeMap" ></embedded-map>
  </div>
</template>
<script>
import EmbeddedMap from "./EmbeddedMap.vue";
import TypeMapSelector from "./TypeMapSelector.vue";

export default {
  name: "CountryMap",
  components: { EmbeddedMap, TypeMapSelector },
  props: {
    country: {
      type: Object,
      default: null,
    },
    typeMap:{
      type: String,
      default: "m",
    }
  },
  computed: {
    mapQuery: function () {
      return this.country.name.common;
    },
    areaZoom() {
      const area = this.country.area;

      if (area >= 10000000) return 2;

      if (area >= 1000000) return 3;

      if (area >= 500000) return 4;

      if (area >= 100000) return 5;

      if (area >= 50000) return 6;

      return 9;
    },
  },
  methods: {
    updateLocalTypeMap(newTypeMap) {
        this.$emit("TypeMapChange", newTypeMap) ;
    },
  }
};
</script>

<style scoped>
  .mapsSetings {
    background-color: #ffffff;
  }
</style>