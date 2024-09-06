<template>
    <div>
        <table class="mt-4">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Price</th>
                    <th>Vooraad</th>
                    <th>Categorie</th>
                    <th>Sold Out</th>
                    <th>SKU</th>
                    <th>Description</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="product in products" :key="product.id">
                    <td>{{ product.id }}</td>
                    <td>{{ product.name }}</td>
                    <td>{{ product.price }}</td>
                    <td>{{ product.vooraad }}</td>
                    <td>{{ product.categorie }}</td>
                    <td>{{ product.soldOut ? 'Yes' : 'No' }}</td>
                    <td>{{ product.sku }}</td>
                    <td>{{ product.description }}</td>
                    <td>
                        <button @click="addToCart(product.id)"
                            class="bg-green-500 hover:bg-green-700 text-white font-bold py-1 px-2 rounded">Add to Cart</button>
                    </td>
                </tr>
            </tbody>
        </table>
        <p>Total products: {{ products.length }}</p>
        <br>
        <button @click="toggleCart()"
            class="mt-4 bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">Show Cart</button>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    products: Array,
    addToCart: Function,
    toggleCart: Function
});
</script>

<style scoped>
/* Add any additional styles here */
</style>