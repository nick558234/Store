<template>
 <ul class="mt-4">
      <li v-for="product in products" :key="product.id" class="mt-2">
        {{ product.name }} - {{ product.price }}
        <button @click="addToCart(product.id)" class="ml-4 bg-green-500 hover:bg-green-700 text-white font-bold py-1 px-2 rounded">Add to Cart</button>
      </li>
    </ul>
</template>
<script setup>

</script>
