<template>
  <div class="main-page">
    <PeriodicTable
      :periodic-table-data="periodicJson"
      :invertedRowOrder="invertedRowOrder"
    />
    <button class="invert-button" @click="invertedRowOrder = !invertedRowOrder">
      INVERT
    </button>
  </div>
</template>

<script>
import PeriodicTable from "./components/PeriodicTable.vue";
import periodicJson from "@/assets/periodic-table-data.json";

export default {
  name: "App",
  components: {
    PeriodicTable,
  },
  data() {
    return {
      invertedRowOrder: false,
      periodicJson,
    };
  },
};
</script>

<style>
html,
body,
#app {
  height: 100%;
}
.main-page {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  flex-direction: column;
  height: 100%;
}
.invert-button {
  height: 10%;
  width: 20%;
  font-size: 2rem;
}
</style>
