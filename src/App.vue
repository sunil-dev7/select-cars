<template>
  <div class="app">
    <img style="margin-bottom: 20px" :src="'./2.jpg'" />
    <MultipleDropdown @complete="isDone = true" />
    <div><button @click="moveToNext">Search Part</button></div>
    <img style="margin-top: 20px" class="bottom-image" :src="'./1.jpg'" />
  </div>
</template>

<script>
import MultipleDropdown from "./components/MultipleDropdown.vue";

export default {
  name: "App",
  components: {
    MultipleDropdown,
  },
  data() {
    return {
      isDone: false,
    };
  },

  methods: {
    moveToNext() {
      if (this.isDone) {
        window.location.href =
          "https://www.partsgeek.com/ymm/2020/autocar_llc-dt-/xpeditor.html";
      } else {
        alert("Please complete the flow");
      }
    },
  },
};
</script>

<style scoped>
.app {
  background: white;
}
button {
  color: #fff;
  background-color: #ef6f1a;
  border-color: #ef6f1a;
  font-weight: 700;
  font-size: 1.75rem;
  width: 300px;
  border-radius: 10px;
  border: 0;
  height: 70px;
  margin-top: 20px;
}
button:hover {
  cursor: pointer;
}
</style>
