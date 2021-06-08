<template>
  <div class="all-dropdown-container">
    <div
      class="dropdown-with-label"
      v-for="(dropdown, index) in dropdowns"
      :key="index"
      v-show="dropdown.isShow"
    >
      <div class="dropdown-label">
        <span>Choose {{ dropdown.label }}:</span>
        <div class="arrow">
          <div class="line"></div>
          <div class="point"></div>
        </div>
      </div>
      <Dropdown
        class="dropdown-container"
        :ref="`dropdown-${index}`"
        @selected="(data) => seleteData(data, index)"
        :defaultSelected="'ab'"
        :options="dropdown.options"
      />
    </div>
  </div>
</template>

<script>
import Dropdown from "./Dropdown.vue";

const years = [
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
];

const make = [
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
];

const model = [
  {
    name: "accor",
    id: "accor",
  },
  {
    name: "civic",
    id: "civic",
  },
  {
    name: "city",
    id: "city",
  },
];

export default {
  name: "App",
  components: {
    Dropdown,
  },
  data() {
    return {
      dropdowns: [
        {
          label: "Year",
          options: years,
          isShow: true,
        },
        {
          label: "Make",
          options: make,
          isShow: false,
        },
        {
          label: "Model",
          options: model,
          isShow: false,
        },
      ],
    };
  },
  computed: {},
  methods: {
    seleteData(data, index) {
      console.log(data);
      if (this.dropdowns[index + 1]) {
        this.dropdowns[index + 1].isShow = true;
      } else {
        this.$emit("complete");
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.all-dropdown-container {
  margin: auto;
  .dropdown-with-label {
    display: flex;
    margin-top: 10px;
    justify-content: center;
    .dropdown-label {
      vertical-align: middle;
      line-height: 29px;
      margin-right: 20px;
      width: 280px;
      span:nth-child(1) {
        margin-right: 20px;
      }
      .arrow {
        width: 120px;
        display: inline-block;
        vertical-align: middle;
      }

      .line {
        margin-top: 10px;
        width: 100px;
        background: #ef6f1a;
        height: 10px;
        float: left;
      }

      .point {
        width: 0;
        height: 0;
        border-top: 15px solid transparent;
        border-bottom: 15px solid transparent;
        border-left: 20px solid #ef6f1a;
        float: right;
      }
    }
    .dropdown-container {
      vertical-align: middle;
    }
  }
}
</style>
