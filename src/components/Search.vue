<template>
  <div class="input-wrap">
    <input
      class="input"
      type="text"
      placeholder="Поиск по названию картины"
      v-model="searchQuery"
      @input="onSearch"
    />
    <button class="button" @click="onSearch">Найти</button>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      searchQuery: "",
    };
  },
  methods: {
    onSearch() {
      this.$emit("search", this.searchQuery);
    },
  },
};
</script>

<style scoped>
.input-wrap {
  display: flex;
  gap: 0;
}

.input {
  width: 290px;
  height: 48px;
  padding: 14px;
  background: transparent;
  border: 1px solid #e1e1e1;
}

.input::placeholder {
  color: #9f9f9f;
  font-size: 14px;
}

.button {
  border: none;
  font-size: 14px;
  color: #f4f6f9;
  background: #382e2b;
  padding: 14px 30px;
  height: 48px;
  cursor: pointer;
}

@media (max-width: 1200px) {
  .input {
    width: 120px;
  }
}

@media (max-width: 768px) {
}
</style>
