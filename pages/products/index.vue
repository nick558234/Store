<template>
    <div>
        <h1>Producten beheer</h1>
        <div>
            <label for="name">Name</label>
            <input id="name" placeholder="Naam" v-model="productData.name" />
            <button @click="addProduct()">Product toevoegen</button>
        </div>
        <ul>
            <li v-for="product in products" :key="product.id">
                {{ productData }}
            </li>
        </ul>
    </div>
</template>

<script setup>
import { ref } from 'vue';

useHead({
    title: 'Producten beheer'
});

const productData = ref({ name: '' });
const products = ref([]);

const addProduct = () => {
    products.value.push({
        id: products.value.length + 1,
        name: productData.name
    });
};
</script>