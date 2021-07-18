<template>
  <div class="wrapper__search">
    <!-- Search -->
    <IconSearch class="search-icon" />
    <!-- Search input -->
    <input type="text" :placeholder="placeholder" v-model="search" />
  </div>
</template>


<script>
import IconSearch from "@/assets/svg/search.svg";

export default {
  components: {
    IconSearch,
  },

  props: {
    value: {
      type: String,
      required: true,
    },
    placeholder: {
      type: String,
      default: "Search",
    },
  },
  data() {
    return { search: this.value };
  },
  watch: {
    search(val) {
      this.$emit("search", val);
    },
  },
};
</script>


<style lang="scss" scoped>
svg {
  color: #e4e4e4;
}

/* Search */
.wrapper__search {
  position: relative;
}

.search-icon {
  top: 13px;
  left: 20px;
  position: absolute;
}

input {
  padding: 16px 16px 16px 56px !important;
  margin-bottom: 0px;
  border-radius: 30px;
  color: #909399;
  font-size: 16px;
  min-width: 400px;
  height: auto;
}
</style>


