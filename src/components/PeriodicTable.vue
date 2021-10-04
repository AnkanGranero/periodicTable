<template>
  <table class="table">
    <td
      v-for="element in periodicTableData"
      :key="element.atomicNumber"
      class="element block"
      :style="{
        'grid-column': element.column,
        'grid-row': customRowOrder(element.row),
      }"
      :class="selectedGroup === element.block ? [active, element.block] : ''"
      @click="clickOnBlock(element.block)"
    >
      <span> {{ element.atomicNumber }}</span>
      <span>{{ element.symbol }}</span>
      <span> {{ element.name }}</span>
    </td>
  </table>
</template>

<script>
export default {
  name: "Periodic-table",
  props: {
    periodicTableData: {
      type: Object,
      required: true,
    },
    invertedRowOrder: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      selectedGroup: "",
    };
  },
  methods: {
    customRowOrder(row) {
      if (this.invertedRowOrder) {
        return this.numberOfRows - row + 1;
      }
      return row;
    },
    clickOnBlock(block) {
      this.selectedGroup = this.selectedGroup !== block ? block : "";
    },
  },
  computed: {
    numberOfRows() {
      let arrayOfRows = this.periodicTableData.map((element) => element.row);
      return Math.max(...arrayOfRows);
    },
  },
};
</script>
<style>
.table {
  display: inline-grid;
  grid-template-columns: repeat(18, 7%);
  grid-template-rows: repeat(9, auto);
  justify-content: center;
}
.element {
  border: 1px solid black;
  font-size: 0.8vw;
}
.block {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.s {
  background: red;
}
.p {
  background: yellow;
}
.d {
  background: rgb(103, 191, 255);
}
.f {
  background: rgb(149, 210, 149);
}
</style>