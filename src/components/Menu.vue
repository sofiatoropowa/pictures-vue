<template>
  <ul class="menu">
    <li class="menu-item">
      <a href="/">Каталог</a>
    </li>
    <li class="menu-item">
      <a href="/">Доставка</a>
    </li>
    <li class="menu-item">
      <a href="/">Оплата</a>
    </li>
    <li class="menu-item">
      <a href="/">Контакты</a>
    </li>
    <li class="menu-item">
      <a href="/">О компании</a>
    </li>
  </ul>
</template>

<script>
export default {
  name: "Menu",
};
</script>

<style scoped>
.menu {
  display: flex;
  gap: 48px;
  padding-left: 96px;
}

.menu-item {
  list-style: none;
  font-size: 14px;
}

.menu-item a {
  text-decoration: none;
  color: #343030;
  transition: .2s;
}

.menu-item a:hover {
  opacity: .7;
}

@media (max-width: 1440px) {
  .menu {
    gap: 14px;
    padding-left: 0;
  }
}

@media (max-width: 768px) {
  .menu-item {
    font-size: 10px;
  }
}
</style>
