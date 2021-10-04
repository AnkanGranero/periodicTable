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
      :class="[element.block, element.block === selectedGroup ? 'active' : '']"
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
<style lang="scss">
$red: #fa0000;
$yellow: #fbff00;
$blue: #67c0ff;
$green: #92dd92;

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
  background: rgba($red, 0.5);
  &.active {
    background: $red;
  }
}
.p {
  background: rgba($yellow, 0.5);
  &.active {
    background: $yellow;
  }
}
.d {
  background: rgba($blue, 0.5);
  &.active {
    background: $blue;
  }
}
.f {
  background: rgba($green, 0.5);
  &.active {
    background: $green;
  }
}
</style>