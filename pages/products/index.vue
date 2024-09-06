<template>
  <div class="flex flex-col items-center">
    <ProductForm @product-added="handleProductAdded" />
    <ul class="mt-4">
      <li v-for="product in products" :key="product.id" class="mt-2">
        {{ product.name }} - {{ product.price }}
        <button @click="addToCart(product.id)" class="ml-4 bg-green-500 hover:bg-green-700 text-white font-bold py-1 px-2 rounded">Add to Cart</button>
      </li>
    </ul>
    <button @click="toggleCart()" class="mt-4 bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">Show Cart</button>

    <!-- Popup Modal -->
    <div v-if="showCart" class="overflow fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 overflow-y-auto">
      <div class="bg-white p-8 rounded-lg shadow-lg w-full max-w-lg overflow-y-auto">
        <button @click="toggleCart()" class="absolute top-4 right-4 text-gray-600 hover:text-gray-900">
          x
        </button>
        <Cart />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';


const products = ref([]);
const cart = ref([]);
const showCart = ref(false);

// Load products and cart from localStorage when the component is mounted
onMounted(() => {
  // Retrieve the stored products from localStorage
  const storedProducts = localStorage.getItem('products');
  // If there are stored products, parse them and set the products array
  if (storedProducts) {
    products.value = JSON.parse(storedProducts);
  }

  // Retrieve the stored cart from localStorage
  const storedCart = localStorage.getItem('cart');
  // If there is a stored cart, parse it and set the cart array
  if (storedCart) {
    cart.value = JSON.parse(storedCart);
  }
});

const handleProductAdded = (newProduct) => {
  products.value.push(newProduct);
  // Save products to localStorage
  localStorage.setItem('products', JSON.stringify(products.value));
};

const addToCart = (productId) => {
  const product = products.value.find(p => p.id === productId);
  if (product) {
    cart.value.push(product);
    // Save cart to localStorage
    localStorage.setItem('cart', JSON.stringify(cart.value));
  }
};

const toggleCart = () => {
  showCart.value = !showCart.value;
};
</script>

<style scoped>
/* Add any additional styles here */
</style>