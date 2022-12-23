<script setup lang="ts">
import { ref, computed } from "vue";
import socksGreenImage from "./assets/images/socks_green.jpeg";
import socksBlueImage from "./assets/images/socks_blue.jpeg";

const selectedVariant = ref(0);
const product = ref("Socks");
const brand = ref("Vue Mastery");

const details = ref(["50% cotton", "30% wool", "20% polyester"]);
const variants = ref([
  { id: 2234, color: "green", image: socksGreenImage, quantity: 50 },
  { id: 2235, color: "blue", image: socksBlueImage, quantity: 0},
]);

const cart = ref(0);

const title = computed(() => {
  return `${brand.value} - ${product.value}`;
});

const image = computed(() => {
  return variants.value[selectedVariant.value].image;
});

const inStock = computed(() => {
  return variants.value[selectedVariant.value].quantity > 0;
});

const addToCart = () => {
  cart.value += 1;
};

const updateVariant = (index: number) => {
  selectedVariant.value = index;
};
</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart">
    <p>Cart({{ cart }})</p>
  </div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img v-bind:src="image" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-html="detail" v-for="detail in details"></li>
        </ul>
        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          class="color-circle"
          :style="{ backgroundColor: variant.color }"
          @mouseover="updateVariant(index)"
        ></div>
        <button
          class="button"
          :class="{ disabledButton: !inStock }"
          v-on:click="addToCart"
          :disabled="!inStock"
        >
          Add to Cart
        </button>
      </div>
    </div>
  </div>
</template>
