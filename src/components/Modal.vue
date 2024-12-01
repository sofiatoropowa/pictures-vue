<template>
  <div v-if="isVisible" class="modal-overlay" @click.self="close">
    <div class="modal-content">
      <button class="close-button" @click="close">×</button>

      <h3 class="modal-title">{{ title }}</h3>

      <swiper :slides-per-view="1" loop>
        <swiper-slide v-for="(img, index) in images" :key="index">
          <img class="slide-img" :src="img" alt="image" />
        </swiper-slide>
      </swiper>

      <div class="modal-description">{{ description }}</div>

      <div class="modal-bottom">
        <div class="price-before">{{ beforeDiscount }}</div>
        <div class="price">{{ price }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { Swiper, SwiperSlide } from "swiper-vue2";
import "swiper/swiper-bundle.css";

export default {
  name: "Modal",
  components: {
    Swiper,
    SwiperSlide,
  },
  props: {
    isVisible: {
      type: Boolean,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      default: "",
    },
    beforeDiscount: {
      type: Number,
    },
    price: {
      type: Number,
      required: true,
    },
    images: {
      type: Array,
    },
  },
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  max-width: 600px;
  width: 100%;
  position: relative;
}

.modal-title {
  margin-top: 0;
}

.modal-description,
.modal-bottom {
  margin-top: 20px;
}

.slide-img {
  width: 100%;
  object-fit: contain;
  max-height: 200px;
  margin: 0 auto;
}

.price-before {
  font-size: 14px;
  color: #a0a0a0;
  text-decoration: line-through;
}

.price {
  font-size: 16px;
  font-weight: 700;
  color: #343030;
}

.close-button {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 40px;
  position: absolute;
  right: 10px;
  top: 2px;
}
</style>
