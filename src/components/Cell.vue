<template>
  <a
    class="cell"
    tabindex="0"
    :id="id"
    :ref="`i${customRef}`"
    element-type="cell"
    :href="`${url}`"
    >{{ name }}
    <!-- @focus="logger"
    <a :url="url" tabindex="-1"></a> -->
  </a>
</template>

<script>
export default {
  // inject: ["setFocused"],
  props: ["id", "url", "name", "customRef"],
  data() {
    return {
      uiType: "verticalList", // puede ser verticalList horizontalList o grid
    };
  },
  methods: {
    customKeydown(event) {
      console.log(event);
      console.log(this.$emit);
      this.$emit("customKeydown");
    },
    logger() {
      console.log("me focuseearon!");
    },
  },
};
</script>

<style scoped>
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

.cell:focus {
  background-color: tomato;
  border: none;
  border-radius: 1px;
  outline: none;
  box-shadow: -4px 5px 29px 6px #ff9900;
}
</style>
