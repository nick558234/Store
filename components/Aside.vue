<template>
  <aside class="w-64 bg-gray-800 text-white flex flex-col">
    <div class="p-4 text-2xl font-bold">Dashboard</div>
    <nav class="flex-1 p-4">
      <ul>
        <li class="mb-4">
          <NuxtLink :to="'/'" class="hover:bg-gray-700 p-2 rounded block">Home</NuxtLink>
        </li>
        <li class="mb-4">
          <NuxtLink :to="'/products'" class="hover:bg-gray-700 p-2 rounded block">Add products</NuxtLink>
        </li>
        <li class="mb-4">
          <button @click="toggleCart" class="hover:bg-gray-700 p-2 rounded block">Cart</button>
        </li>
      </ul>
    </nav>
  </aside>
</template>

<script setup>
defineProps({
  toggleCart: Function
});
</script>