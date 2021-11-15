<template>
  <div
    @keydown.down.capture="handleDownArrow"
    @keydown.up.capture="handleUpArrow"
    @focus="handleRowFocus"
    ref="globalContainer"
  >
    <Row
      :data="data1"
      id="firstRow"
      tabindex="0"
      element-type="row"
      lastFocused="getLastFocused"
    />
    <Row
      :data="data2"
      id="secondRow"
      tabindex="0"
      element-type="row"
      lastFocused="getLastFocused"
    />
    <Row
      :data="data3"
      id="lastRow"
      ref="lastRow"
      tabindex="0"
      element-type="row"
      lastFocused="getLastFocused"
    />
  </div>
</template>

<script>
import Row from "./components/Row.vue";

export default {
  components: {
    Row,
  },
  data() {
    return {
      data1: [
        { name: "Google", id: "google", url: "www.google.com" },
        { name: "Bing", id: "bing", url: "www.bing.com" },
        { name: "Vuejs", id: "vuejs", url: "vuejs.org" },
        { name: "Ole", id: "ole", url: "www.ole.com" },
      ],
      data2: [
        { name: "Google", id: "2google", url: "www.google.com" },
        { name: "Bing", id: "2bing", url: "www.bing.com" },
        { name: "Vuejs", id: "2vuejs", url: "vuejs.org" },
        { name: "Ole", id: "2ole", url: "www.ole.com" },
      ],
      data3: [
        { name: "Google", id: "3google", url: "www.google.com" },
        { name: "Bing", id: "3bing", url: "www.bing.com" },
        { name: "Vuejs", id: "3vuejs", url: "vuejs.org" },
        { name: "Ole", id: "3ole", url: "www.ole.com" },
      ],
      container: null,
      firstRow: null,
      lastRow: null,
    };
  },
  computed: {
    nextTarget() {
      return (
        this.focused?.nextElementSibling ||
        this.$refs.container.firstElementChild
      );
    },
    prevTarget() {
      return (
        this.focused?.previousElementSibling ||
        this.$refs.container.lastElementChild
      );
    },
  },
  methods: {
    handleDownArrow(e) {
      let elType = e.target.getAttribute("element-type");
      if (elType === "cell") {
        // ? la fila actual tiene una siguiente fila?
        if (e.target?.parentElement?.nextElementSibling) {
          e.target?.parentElement?.nextElementSibling?.focus();
        } else {
          this.firstRow.focus();
        }
      } else if (elType === "row") {
        if (e.target?.nextElementSibling) {
          e.target?.nextElementSibling?.focus();
        } else {
          this.firstRow.focus();
        }
      } else {
        console.log("no es row ni cell");
      }
    },
    handleUpArrow(e) {
      let elType = e.target.getAttribute("element-type");
      if (elType === "cell") {
        // ? la fila actual tiene una siguiente fila?
        if (e.target?.parentElement?.previousElementSibling) {
          e.target?.parentElement?.previousElementSibling?.focus();
        } else {
          this.lastRow.focus();
        }
      } else if (elType === "row") {
        if (e.target?.previousElementSibling) {
          e.target?.previousElementSibling?.focus();
        } else {
          this.lastRow.focus();
        }
      } else {
        console.log("no es row ni cell");
      }
    },
    handleRowFocus(e) {
      console.log("Row focused: ", e.target.id);
    },
    logChange(event) {
      console.log(event);
    },
  },
  mounted() {
    this.container = this.$refs.globalContainer;
    this.firstRow = this.$refs.globalContainer.firstElementChild;
    this.lastRow = this.$refs.globalContainer.lastElementChild;
    this.$refs.globalContainer.firstElementChild.firstElementChild.focus();
  },
};
</script>
