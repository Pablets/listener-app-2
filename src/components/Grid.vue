<template>
  <div
    ref="globalContainer"
    :tabindex="focusable ? 0 : -1"
    @keydown.down="handleDownArrow"
    @keydown.up.capture="handleUpArrow"
    @keydown.right.capture="handleRightArrow"
    @keydown.left.capture="handleLeftArrow"
  >
    <div
      class="gridWrapper"
      v-for="(row, rowIndex) in contentData"
      :key="rowIndex + 1"
      :data="`data${rowIndex + 1}`"
      element-type="row"
      :rowNumber="rowIndex"
      :rowData="computedData(rowIndex)"
      :ref="`r${rowIndex}`"
      tabindex="0"
    >
      <template>
        <div class="row">
          <a
            class="cell"
            v-for="(item, colIndex) in contentData[rowIndex]"
            :key="colIndex + item.id"
            :id="item.id"
            :name="item.name"
            :url="item.url"
            :cellRowNumber="rowIndex"
            :cellColNumber="colIndex"
            :cellRef="`r${rowIndex}c${colIndex}`"
            :ref="`r${rowIndex}c${colIndex}`"
            tabindex="0"
          >
            {{ item.name }}
          </a>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  props: ["contentData", "focusable", "type"],
  data() {
    return {
      rowNumber: -1,
      colNumber: -1,
      rows: "",
      currentFocused: "r0c0",
    };
  },
  methods: {
    handleRowNumber(row) {
      this.rowNumber = row;
      console.log("row", row);
    },
    handleDownArrow() {
      console.log("handleDownArrow");
      let modifier = this.currentFocused.split("");
      let prevModifier = Number(modifier[1]) + 1;
      if (prevModifier < this.rows.length) {
        modifier.splice(1, 1, prevModifier.toString());
      } else {
        modifier.splice(1, 1, "0");
      }
      let postModifier = modifier.join("");
      this.currentFocused = postModifier;
      this.$refs[postModifier][0].focus();
    },
    handleUpArrow() {
      let modifier = this.currentFocused.split("");
      let prevModifier = Number(modifier[1]) - 1;
      if (prevModifier >= 0) {
        modifier.splice(1, 1, prevModifier.toString());
      } else {
        modifier.splice(1, 1, this.rows.length - 1);
      }
      let postModifier = modifier.join("");
      this.currentFocused = postModifier;
      this.$refs[postModifier][0].focus();
    },
    handleRightArrow() {
      let modifier = this.currentFocused.split("");
      let currentRow = modifier[1];
      let cModifier = Number(modifier[3]) + 1;
      if (cModifier < this.contentData[currentRow].length) {
        modifier.splice(3, 1, cModifier.toString());
      } else {
        modifier.splice(3, 1, 0);
      }
      let postModifier = modifier.join("");
      this.currentFocused = postModifier;
      this.$refs[postModifier][0].focus();
    },
    handleLeftArrow() {
      let modifier = this.currentFocused.split("");
      let prevModifier = Number(modifier[3]) - 1;
      if (prevModifier >= 0) {
        modifier.splice(3, 1, prevModifier.toString());
      } else {
        modifier.splice(3, 1, this.contentDataLenght - 1);
      }
      let postModifier = modifier.join("");
      this.currentFocused = postModifier;
      this.$refs[postModifier][0].focus();
    },
    computedData(row) {
      this.contentDataLenght = this.contentData[row].length;
      return this.contentData[row];
    },
    logChange(event) {
      console.log(event);
    },
  },
  mounted() {
    // ? esto es para computar la cantidad de rows a mostrar
    this.rows = Array.from({ length: this.contentData.length }, (v, i) => i + 1);
    // ? especifico el primer elemento a hacer focus
    this.currentFocused = "r0c0";
    // ? hago focus sobre el elemento
    // this.$refs.r0c0[0].focus();

    // let a = this.$children.map((child) => {
    //   return child;
    // });
    // console.log('dentro de "grid"', this);
  },
};
</script>

<style scoped>
div.gridWrapper {
  color: black;
  border: 1px solid black;
  overflow: hidden;
  width: 100%;
}
div.row {
  width: 100vw;
}
div.banner {
  width: 100vw;
}

div.row {
  display: flex;
}
.cell {
  text-decoration: none;
  color: black;
  display: inline-block;
  padding: 0px 10px;
  background-color: coral;
  margin: 10px;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-size: 20px;
  border-radius: 1px;
  outline: none;
  width: 100px;
}

*:focus {
  background-color: tomato;
  border: none;
  border-radius: 1px;
  outline: none;
  box-shadow: -4px 5px 29px 6px #ff9900;
}
</style>
