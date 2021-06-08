<template>
  <div class="all-dropdown-container">
    <Dropdown
      v-for="(dropdown, index) in dropdowns"
      :ref="`dropdown-${index}`"
      @selected="(data) => seleteData(data, index)"
      :defaultSelected="'ab'"
      :options="dropdown"
      :key="index"
    />
  </div>
</template>

<script>
import Dropdown from "./components/Dropdown.vue";

export default {
  name: "App",
  components: {
    Dropdown,
  },
  data() {
    return {
      years: [
        {
          name: "1996",
          id: "1996",
        },
        {
          name: "1997",
          id: "1997",
        },
        {
          name: "1998",
          id: "1998",
        },
        {
          name: "1999",
          id: "1999",
        },
        {
          name: "2000",
          id: "2000",
        },
        {
          name: "2001",
          id: "2001",
        },
        {
          name: "2002",
          id: "2002",
        },
      ],
      Make: [
        {
          name: "Honda",
          id: "Honda",
        },
        {
          name: "Toyota",
          id: "Toyota",
        },
        {
          name: "Yamaha",
          id: "Yamaha",
        },
        {
          name: "Mecerdes",
          id: "Mecerdes",
        },
        {
          name: "Porsche",
          id: "Porsche",
        },
        {
          name: "Audi",
          id: "Audi",
        },
        {
          name: "Aucura",
          id: "Aucura",
        },
      ],
    };
  },
  computed: {
    dropdowns() {
      return [this.years, this.Make];
    },
  },
  methods: {
    seleteData(data, index) {
      console.log(data);
      this.$refs[`dropdown-${index + 1}`] &&
        this.$refs[`dropdown-${index + 1}`].showOptions();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.all-dropdown-container {
  display: flex;
  flex-wrap: wrap;
}
</style>
