<template>
  <div class="gridContainer" ref="gridContainer">
    <grid :contentData="contentData1" :focusable="true" type="grid" tabindex="0" @focus-next.capture="focusNextEl"></grid>
    <!-- <grid :contentData="contentData2" :focusable="true" type="grid" tabindex="0" @focus-next.capture="focusNextEl"></grid> -->
  </div>
</template>

<script>
import Grid from "./components/Grid.vue";
export default {
  components: {
    Grid,
  },
  data() {
    return {
      contentData2: [
        [
          { name: "Juan", id: "Juan", url: "www.Juan.com" },
          { name: "Pedro", id: "Pedro", url: "www.bing.com" },
          { name: "Martin", id: "Martin", url: "vuejs.org" },
          { name: "Andre", id: "Andre", url: "www.ole.com" },
        ],
        [
          { name: "Perro", id: "Perro", url: "www.google.com" },
          { name: "Gato", id: "Gato", url: "www.bing.com" },
          { name: "Algo", id: "Algo", url: "vuejs.org" },
          { name: "Ola", id: "Ola", url: "www.ole.com" },
        ],
      ],
      contentData1: [
        [
          { name: "Google", id: "google", url: "www.google.com" },
          { name: "Bing", id: "bing", url: "www.bing.com" },
          { name: "Vuejs", id: "vuejs", url: "vuejs.org" },
          { name: "Ole", id: "ole", url: "www.ole.com" },
          { name: "Juan", id: "Juan", url: "www.Juan.com" },
          { name: "Pedro", id: "Pedro", url: "www.bing.com" },
          { name: "Martin", id: "Martin", url: "vuejs.org" },
          { name: "Andre", id: "Andre", url: "www.ole.com" },
        ],
        [
          { name: "Googles", id: "2google", url: "www.google.com" },
          { name: "Bing", id: "2bing", url: "www.bing.com" },
          { name: "Vuejs", id: "2vuejs", url: "vuejs.org" },
          { name: "Ole", id: "2ole", url: "www.ole.com" },
          { name: "Juan", id: "2Juan", url: "www.Juan.com" },
          { name: "Pedro", id: "2Pedro", url: "www.bing.com" },
          { name: "Martin", id: "2Martin", url: "vuejs.org" },
          { name: "Andre", id: "2Andre", url: "www.ole.com" },
        ],
        [
          { name: "Googlee", id: "3google", url: "www.google.com" },
          { name: "Bing", id: "3bing", url: "www.bing.com" },
          { name: "Vuejs", id: "3vuejs", url: "vuejs.org" },
          { name: "Ole", id: "3ole", url: "www.ole.com" },
          { name: "Juan", id: "3Juan", url: "www.Juan.com" },
          { name: "Pedro", id: "3Pedro", url: "www.bing.com" },
          { name: "Martin", id: "3Martin", url: "vuejs.org" },
          { name: "Andre", id: "3Andre", url: "www.ole.com" },
        ],
        [
          { name: "Googlee", id: "4google", url: "www.google.com" },
          { name: "Bing", id: "4bing", url: "www.bing.com" },
          { name: "Vuejs", id: "4vuejs", url: "vuejs.org" },
          { name: "Ole", id: "4ole", url: "www.ole.com" },
          { name: "Juan", id: "4Juan", url: "www.Juan.com" },
          { name: "Pedro", id: "4Pedro", url: "www.bing.com" },
          { name: "Martin", id: "4Martin", url: "vuejs.org" },
          { name: "Andre", id: "4Andre", url: "www.ole.com" },
        ],
      ],
      gridIndex: 0,
      focusedElement: "",
    };
  },
  methods: {
    focusNextEl(target) {
      // console.log("asdasd");
      // console.log("focusNextEl", e.parentElement?.parentElement?.nextElementSibling);

      console.log(target);
      console.log(this.$root.$children[0].$children[0].$refs[target]);

      this.$root.$children[0].$children[1].$refs.r0c0[0].focus();

      // if (!e.target?.parentElement?.parentElement?.nextElementSibling) {
      //   // si hay otra grilla debajo
      //   if (e.target.parentElement?.parentElement?.parentElement?.nextElementSibling) {
      //     this.focusedElement = this.$root.$children[0].$children[1].$refs.r0c0[0];
      //   } else {
      //     this.focusedElement = this.$root.$children[0].$children[0].$refs.r0c0[0];
      //   }
      //   console.log(this.focusedElement);
      //   try {
      //     this.focusedElement.focus();
      //   } catch (error) {
      //     console.log(error);
      //   }
      // }
    },
    logChange(event) {
      console.log(event);
    },
    focusElement(target) {
      target.focus();
    },
  },
  mounted() {
    // console.dir(this.$children[0].$data);
    // let a = this.$children.map((child) => {
    //   return child.$el.tabIndex;
    // });
    // console.log(a);
    // console.log(this._uid);
    // console.dir(this.$refs.gridContainer)
    // console.log(this.$root.$children[0].$children[0].$el.firstElementChild);
    this.focusedElement = this.$root.$children[0].$children[0].$el.firstElementChild.firstElementChild.firstElementChild;
    this.focusedElement.focus();
    // this.$root.$children[0].$children[0].$children.$el.focus();
  },
  updated() {
    console.log("updated");
    this.focusedElement.focus();
  },
};
</script>

<style scoped>
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
