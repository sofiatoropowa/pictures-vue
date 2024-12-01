<template>
  <div class="header-wrap">
    <div class="container">
      <div class="header">
        <button class="burger" @click="toggleMenu">
          <span v-if="!isMenuOpen">
            <svg width="20px" height="20px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M4 18L20 18" stroke="#000000" stroke-width="2" stroke-linecap="round"/>
            <path d="M4 12L20 12" stroke="#000000" stroke-width="2" stroke-linecap="round"/>
            <path d="M4 6L20 6" stroke="#000000" stroke-width="2" stroke-linecap="round"/>
            </svg>
          </span>
          <span v-else>×</span>
        </button>
        <MobileMenu v-if="isMenuOpen"></MobileMenu>
        <Menu class="menu"></Menu>
        <Search class="search" @search="onSearch" />
      </div>
    </div>
  </div>
</template>

<script>
import Menu from "./Menu.vue";
import MobileMenu from "./MobileMenu.vue";
import Search from "./Search.vue";

export default {
  name: "Header",
  components: {
    MobileMenu,
    Menu,
    Search,
  },
  data() {
    return {
      isMenuOpen: false,
    };
  },
  methods: {
    onSearch(query) {
      this.$emit("search", query);
    },
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    }
  }
};
</script>

<style scoped>
.header-wrap {
  padding: 24px 0;
  border-bottom: 1px solid #e1e1e1;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.burger {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  font-size: 30px;
}

@media (max-width: 768px) {
  .header-wrap {
    padding: 10px 0;
  }

  .header {
    flex-direction: column;
    align-items: end;
    gap: 10px;
  }

  .burger {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .search {
    display: none;
  }

  .menu {
    display: none;
  }
}
</style>
