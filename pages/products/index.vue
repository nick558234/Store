<template>
  <div class="flex h-screen">
    <Aside :toggleCart="toggleCart" />
    <div class="flex-1 flex flex-col">
      <Header />
      <div class="p-5">
        <ProductForm @product-added="handleProductAdded" />
        <ProductView
          :products="products"
          :addToCart="addToCart"
          :toggleCart="toggleCart"
        />

        <!-- Clear buttons -->
        <div class="mt-4 flex space-x-4">
          <button
            @click="clearProducts()"
            class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded"
          >
            Clear Products
          </button>
          <button
            @click="clearCart()"
            class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded"
          >
            Clear Cart
          </button>
        </div>
        <!-- Popup Modal for Cart -->
        <div
          v-if="showCart"
          class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 overflow-y-auto"
        >
          <div
            class="bg-white p-8 rounded-lg shadow-lg w-full max-w-lg overflow-y-auto"
          >
                      <button
              @click="toggleCart()"
              class="absolute top-4 right-4 text-gray-600 hover:text-gray-900 bg-transparent p-2 rounded-full focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500"
              aria-label="Close"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-6 w-6"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
                stroke-width="2"
                color="red"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M6 18L18 6M6 6l12 12"
                />
              </svg>
            </button>
            <Cart />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>

const products = ref([]);
const cart = ref([]);
const showCart = ref(false);

onMounted(() => {
  const storedProducts = localStorage.getItem("products");
  if (storedProducts) products.value = JSON.parse(storedProducts);

  const storedCart = localStorage.getItem("cart");
  if (storedCart) cart.value = JSON.parse(storedCart);
});

// Handlers
const handleProductAdded = (newProduct) => {
  products.value.push(newProduct);
  localStorage.setItem("products", JSON.stringify(products.value));
};

const addToCart = (productId) => {
  const product = products.value.find((p) => p.id === productId);
  if (product) {
    cart.value.push(product);
    localStorage.setItem("cart", JSON.stringify(cart.value));
  }
};

const toggleCart = () => {
  // Toggle the visibility of the cart modal
  showCart.value = !showCart.value;
};

const clearProducts = () => {
  // remove all products from the list
  products.value = [];
  localStorage.removeItem("products");
};

const clearCart = () => {
  // remove all products from the cart
  cart.value = [];
  localStorage.removeItem("cart");
};

// Ensure the page uses the 'default' layout
definePageMeta({
  layout: "default",
});
</script>

<style scoped>
/* Add any additional styles here */
</style>
