<template>
  <div :class="['card', { 'card--sold': sold }]">
    <img :class="[{ 'img-modal': !sold }]" :src="imageSrc" alt="picture" @click="openModal" />
    <div class="content">
      <h3 class="title">{{ title }}</h3>
      <div class="bottom">
        <div>
          <div class="price-before">{{ beforeDiscount }}</div>
          <div class="price">{{ price }}</div>
        </div>
        <button
          v-if="!sold"
          :class="[
            'button',
            { 'button--start': !isProcessing && !inCart },
            { 'button--loader': isProcessing },
            { 'button--in-cart': inCart },
          ]"
          @click="buy"
        >
          <span v-if="inCart && !isProcessing">
            <svg
              width="20"
              height="20"
              viewBox="0 0 20 20"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M16.5316 4.80934L7.63353 14.2369L3.34826 10.1923"
                stroke="#F4F6F9"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </span>
          {{
            isProcessing
              ? inCart
                ? "Удаляем..."
                : "Добавляем..."
              : inCart
              ? "В корзине"
              : "Купить"
          }}
        </button>
      </div>
    </div>

    <Modal
      v-if="!sold"
      :isVisible="isModalVisible"
      :title="title"
      :description="description"
      :beforeDiscount="beforeDiscount"
      :price="price"
      :images="images"
      @close="closeModal"
    />
  </div>
</template>

<script>
import Modal from "./Modal.vue";

export default {
  name: "Card",
  components: {
    Modal,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    beforeDiscount: {
      type: Number,
    },
    price: {
      type: Number,
      required: true,
    },
    imageSrc: {
      type: String,
      required: true,
    },
    sold: {
      type: Boolean,
      default: false,
    },
    description: {
      type: String,
      default: "",
    },
    images: {
      type: Array,
    },
  },
  data() {
    return {
      isProcessing: false,
      inCart: false,
      isModalVisible: false,
    };
  },
  created() {
    const cartItems = JSON.parse(localStorage.getItem("cartItems")) || [];
    this.inCart = cartItems.includes(this.title);
  },
  methods: {
    buy() {
      this.isProcessing = true;

      setTimeout(() => {
        const cartItems = JSON.parse(localStorage.getItem("cartItems")) || [];

        if (this.inCart) {
          const index = cartItems.indexOf(this.title);
          if (index > -1) {
            cartItems.splice(index, 1);
            this.inCart = false;
          }
        } else {
          cartItems.push(this.title);
          this.inCart = true;
        }

        localStorage.setItem("cartItems", JSON.stringify(cartItems));
        this.isProcessing = false;
      }, 2000);
    },

    openModal() {
      this.isModalVisible = true;
    },

    closeModal() {
      this.isModalVisible = false;
    },
  },
};
</script>

<style scoped>
.card {
  border: 1px solid #e1e1e1;
  max-width: 280px;
}

.card--sold {
  opacity: 0.5;
}

.img-modal {
  cursor: pointer;
}

.content {
  padding: 20px 24px 24px;
  min-height: 170px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.title {
  font-size: 18px;
  line-height: 27px;
  font-weight: 400;
  color: hsba(0, 8%, 20%, 1);
  margin: 0;
}

.bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 48px;
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

.button {
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  font-size: 14px;
  color: #f4f6f9;
  background: #382e2b;
  padding: 14px 1px;
  width: 118px;
  transition: 0.2s;
}

.button span {
  margin-right: 4px;
}

.button--loader {
  background: #c1b4b1;
}

.button--in-cart {
  background: #5b3a32;
}

.button--start:hover,
.button--in-cart:hover {
  cursor: pointer;
  background: #776763;
}

@media (max-width: 768px) {
  .content {
    padding: 10px 16px 20px;
    min-height: 140px;
  }

  .title {
    font-size: 14px;
  }
}
</style>
