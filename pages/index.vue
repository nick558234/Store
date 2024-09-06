<template>
  <div class="flex h-screen">
    <!-- Sidebar -->
    <Aside />

    <!-- Main Content -->
    <div class="flex-1 flex flex-col">
      <!-- Header -->
      <header class="bg-gray-200 p-4 flex justify-between items-center">
        <h1 class="text-3xl font-bold">Winkelvooraadbeheer</h1>
      </header>

      <!-- Content -->
      <main class="flex-1 p-4 overflow-y-auto">
        <slot></slot>
        <div>
          <!-- Select for choosing user role -->
          <label for="userRole" class="block mb-2">Select User Role:</label>
          <select id="userRole" v-model="userRole" class="border rounded-md p-2 mb-4">
            <option value="admin">Admin</option>
            <option value="editor">Editor</option>
            <option value="viewer">Viewer</option>
          </select>

          <!-- Display content based on user role -->
          <div v-if="userRoleContent">
            {{ userRoleContent }}
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import Aside from '~/components/Aside.vue';

// Set the page title
useHead({
  title: 'Winkelvooraadbeheer'
});

// Example user role
const userRole = ref('admin'); // Default role

// Computed property to determine content based on user role
const userRoleContent = computed(() => {
  switch (userRole.value) {
    case 'admin':
      return 'Welcome, Admin! You have full access to the system.';
    case 'editor':
      return 'Welcome, Editor! You can edit content.';
    case 'viewer':
      return 'Welcome, Viewer! You can view content.';
    default:
      return 'Welcome! Please select a role.';
  }
});
</script>

<style scoped>
/* Add any additional styles here */
</style>