<template>
  <div class="mobile-menu__wrap">
    <ul class="mobile-menu">
      <li class="mobile-menu__item">
        <a href="/">Каталог</a>
      </li>
      <li class="mobile-menu__item">
        <a href="/">Доставка</a>
      </li>
      <li class="mobile-menu__item">
        <a href="/">Оплата</a>
      </li>
      <li class="mobile-menu__item">
        <a href="/">Контакты</a>
      </li>
      <li class="mobile-menu__item">
        <a href="/">О компании</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MobileMenu",
};
</script>

<style scoped>
.mobile-menu {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
}

.mobile-menu__wrap {
    position: absolute;
    top: 80px;
    right: 0;
    background: #fff;
    padding: 20px 10px;
    width: 100%;
    height: 100vh;
}

.mobile-menu__item {
    list-style: none;
    font-size: 14px;
}

.mobile-menu__item a {
  text-decoration: none;
  color: #343030;
  transition: .2s;
}
</style>

