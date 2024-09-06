<!-- ProductForm.vue -->
<template>
  <div class="">
    <label for="name" class="block">Name</label>
    <input id="name" placeholder="Naam" v-model="productData.name" class="border rounded-md p-2" />
    <label for="price" class="block mt-2">Price</label>
    <input id="price" type="number" placeholder="Prijs" v-model="productData.price" class="border rounded-md p-2" />
    <label for="vooraad" class="block mt-2">Vooraad</label>
    <input id="vooraad" type="number" placeholder="Vooraad" v-model="productData.vooraad" class="border rounded-md p-2" />
    <label for="categorie" class="block mt-2">Categorie</label>
    <input id="categorie" placeholder="Categorie" v-model="productData.categorie" class="border rounded-md p-2" />
    <label for="soldOut" class="block mt-2">Sold Out</label>
    <input id="soldOut" type="checkbox" v-if="productData.vooraad === 0 || productData.vooraad === null" v-model="isSoldOut" class="mt-1" />
    <label for="sku" class="block mt-2">SKU</label>
    <input id="sku" placeholder="SKU" v-model="productData.sku" class="border rounded-md p-2" />
    <label for="description" class="block mt-2">Description</label>
    <textarea id="description" placeholder="Beschrijving" v-model="productData.description" class="border rounded-md p-2"></textarea>
    <br>
    <button @click="addProduct" class="mt-4 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Product toevoegen</button>
  </div>
</template>

<script setup lang="ts">
import { ref, defineEmits, computed } from 'vue';

// Define the type for product data
interface ProductData {
  name: string;
  price: number;
  vooraad: number;
  categorie: string;
  soldOut: boolean;
  sku: string;
  description: string;
}

const emit = defineEmits(['product-added']);

const productData = ref<ProductData>({
  name: '',
  price: 0,
  vooraad: 0,
  categorie: '',
  soldOut: false,
  sku: '',
  description: ''
});

const isSoldOut = computed({
  get() {
    return productData.value.vooraad === '0' || productData.value.vooraad === null;
  },
  set(value) {
    productData.value.soldOut = value;
  }
});

const addProduct = () => {
  const newProduct = {
    id: Date.now(),
    ...productData.value
  };
  // Emit the new product to the parent component
  emit('product-added', newProduct);
  // Reset the form
  productData.value = {
    name: '',
    price: '',
    vooraad: '',
    categorie: '',
    soldOut: false,
    sku: '',
    description: ''
  };
};
</script>

<style scoped>
/* Add any additional styles here */
</style>