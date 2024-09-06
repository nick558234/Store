<template>
  <div class="flex flex-col items-center">
    <h1 class="text-3xl font-bold mb-6">Winkelwagen</h1>
    <ul class="w-full max-w-2xl">
      <li v-for="product in cart" :key="product.id" class="flex justify-between items-center p-4 border-b ">
        <div>
          <h2 class="text-xl font-semibold">{{ product.name }}</h2>
          <p class="text-gray-600">{{ product.description }}</p>
        </div>
        <div class="text-right">
          <p class="text-lg font-bold">{{ product.price }}</p>
          <p class="text-sm text-gray-500">SKU: {{ product.sku }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const cart = ref([]);

// Load cart from localStorage when the component is mounted
onMounted(() => {
  const storedCart = localStorage.getItem('cart');
  if (storedCart) {
    cart.value = JSON.parse(storedCart);
  }
});
</script>

<style scoped>
/* Add any additional styles here */
</style>