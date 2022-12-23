<script setup lang="ts">
import { ref, computed } from "vue";
import socksGreenImage from "./assets/images/socks_green.jpeg";
import socksBlueImage from "./assets/images/socks_blue.jpeg";

const product = ref("Socks");
const brand = ref("Vue Mastery");
const image = ref(socksGreenImage);
const inStock = ref(true);

const details = ref(["50% cotton", "30% wool", "20% polyester"]);
const variants = ref([
  { id: 2234, color: "green", image: socksGreenImage },
  { id: 2235, color: "blue", image: socksBlueImage },
]);

const cart = ref(0);

const title = computed(() => {
  return `${brand.value} - ${product.value}`;
})

const addToCart = () => {
  cart.value += 1;
};

const updateImage = (variantImage: string) => {
  image.value = variantImage;
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
        <h1>{{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-html="detail" v-for="detail in details"></li>
        </ul>
        <div
          v-for="variant in variants"
          :key="variant.id"
          class="color-circle"
          :style="{ backgroundColor: variant.color }"
          v-on:mouseover="updateImage(variant.image)"
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
