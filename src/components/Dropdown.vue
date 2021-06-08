<template>
  <div class="dropdown" v-if="options">
    <!-- Dropdown Input -->
    <input
      class="dropdown-input"
      :name="name"
      inputmode="none"
      @focus.prevent="showOptions"
      @blur="exit"
      @keyup="keyMonitor"
      v-model="searchFilter"
      :disabled="disabled"
      :placeholder="placeholder"
    />

    <!-- Dropdown Menu -->
    <div class="dropdown-items-container" v-show="optionsShown">
      <ul
        class="dropdown-content"
        v-for="(collumn, index) in numberOfCollumn"
        :key="index"
      >
        <li
          class="dropdown-item"
          @mousedown="selectOption(option)"
          v-for="(option, cIndex) in getCollumnNth(index)"
          :key="'cIndex' + cIndex"
        >
          {{ option.name || option.id || "-" }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Dropdown",
  template: "Dropdown",
  props: {
    name: {
      type: String,
      required: false,
      default: "dropdown",
      note: "Input name",
    },
    options: {
      type: Array,
      required: true,
      default: () => [],
      note: "Options of dropdown. An array of options with id and name",
    },
    placeholder: {
      type: String,
      required: false,
      default: "Please select an option",
      note: "Placeholder of dropdown",
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false,
      note: "Disable the dropdown",
    },
    maxItem: {
      type: Number,
      required: false,
      default: -1,
      note: "Max items showing, if max items < 0 => Show all",
    },
    defaultSelected: {
      type: String,
      default: "",
      note: "default selected Value at first time",
    },
    maxItemPercolumn: {
      type: Number,
      default: 2,
      note: "Number of item per collumn",
    },
  },
  data() {
    return {
      selected: null,
      optionsShown: false,
      searchFilter: "", // current Search keyword
      oldSearchFilter: "", // old Search keyword
    };
  },
  computed: {
    // Filtered List
    filteredOptions() {
      const filtered = [];
      const regOption = new RegExp(this.searchFilter, "ig");
      for (const option of this.options) {
        if (this.searchFilter.length < 1 || option.name.match(regOption)) {
          if (this.maxItem < 0 || filtered.length < this.maxItem)
            filtered.push(option);
        }
      }
      return filtered;
    },
    numberOfCollumn() {
      return Math.ceil(this.filteredOptions.length / this.maxItemPercolumn);
    },
  },
  created() {
    this.initDefaultValue();
  },
  methods: {
    // Default value passing from parent
    initDefaultValue() {
      const defaultSelect = this.options.find(
        (_) => _.name === this.defaultSelected
      );
      this.selected = defaultSelect
        ? this.selectOption(defaultSelect, false)
        : this.selected;
    },
    selectOption(option, doTriggerEvent = true) {
      this.selected = option;
      this.optionsShown = false;
      this.searchFilter = this.selected.name;
      this.oldSearchFilter = this.searchFilter;
      doTriggerEvent && this.$emit("selected", this.selected);
    },
    showOptions() {
      if (!this.disabled) {
        this.searchFilter = "";
        this.optionsShown = true;
      }
    },
    // Separate list to multiple collumn
    getCollumnNth(index) {
      const startIndex = index * this.maxItemPercolumn;
      const endIndex =
        startIndex + this.maxItemPercolumn > this.filteredOptions.length
          ? this.filteredOptions.length
          : startIndex + this.maxItemPercolumn;
      return this.filteredOptions.slice(startIndex, endIndex);
    },
    exit() {
      this.selected = null;
      this.searchFilter = this.oldSearchFilter;
      this.optionsShown = false;
    },
    // Selecting first one when pressing Enter
    keyMonitor: function(event) {
      if (event.key === "Enter" && this.filteredOptions[0]) {
        const selectOption = this.options.find(
          (_) => _.name === this.searchFilter
        );
        if (selectOption) {
          this.selectOption();
        }
      }
    },
  },
  watch: {
    searchFilter() {
      // Search keyword change
      this.$emit("filter", this.searchFilter);
    },
  },
};
</script>

<style lang="scss" scoped>
.dropdown {
  position: relative;
  display: block;
  margin: auto;
  .dropdown-input {
    background: #fff;
    cursor: pointer;
    border: 1px solid #e7ecf5;
    border-radius: 3px;
    color: #333;
    display: block;
    font-size: 0.8em;
    padding: 6px;
    min-width: 250px;
    max-width: 250px;
    &:hover {
      background: #f8f8fa;
    }
  }
  .dropdown-items-container {
    position: absolute;
    background-color: #fff;
    min-width: 248px;
    // max-width: 248px;
    // max-height: 248px;
    border: 1px solid #e7ecf5;
    box-shadow: 0px -8px 34px 0px rgba(0, 0, 0, 0.05);
    overflow: auto;
    z-index: 1;
    list-style-type: none;
    display: flex;
    padding: 2px 4px 2px 8px;
    @media screen and (max-width: 640px) {
      display: block;
    }
    .dropdown-content {
      list-style-type: none;
      min-width: 100px;
      padding: 0;
      margin: 0;
      .dropdown-item {
        color: black;
        font-size: 0.7em;
        line-height: 1em;
        padding: 8px;
        text-decoration: none;
        display: block;
        cursor: pointer;
        &:hover {
          background-color: #e7ecf5;
        }
      }
    }
  }
  .dropdown:hover .dropdowncontent {
    display: block;
  }
}
</style>
