<template>
  <div
    @keydown.left="focusHandler"
    @keydown.right="focusHandler"
    @keydown.enter="logEnter"
    ref="container"
    @focus.capture="setFocused"
    :id="id"
  >
    <Cell
      v-for="(item, index) in data"
      :key="index + item.id"
      :firstChild="index === 0"
      :lastChild="index === data.length - 1"
      :id="item.id"
      :name="item.name"
      :url="item.url"
      :custom-ref="index"
    />
  </div>
</template>

<script>
import Cell from "./Cell.vue";
export default {
  props: ["data", "id"],
  data: function () {
    return {
      focused: "",
    };
  },
  components: {
    Cell,
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
    setFocused(e) {
      let elType = e.target.getAttribute("element-type");
      if (elType === "row") {
        this.focused?.focus();
      } else if (elType === "cell") {
        this.focused = e.target;
        this.focused.focus();
      }
    },
    logEnter(e) {
      console.log(e.target.id);
    },
    focusHandler(event) {
      switch (event.key) {
        case "ArrowLeft":
          return this.prevTarget.focus();
        case "ArrowRight":
          return this.nextTarget.focus();
        default:
      }
    },
  },
  mounted() {
    this.focused = this.$refs.container.firstElementChild;
  },
};
</script>

<style>
div.row {
  display: flex;
}
</style>
