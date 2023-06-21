<script setup>
import VMenu from './components/VMenu.vue'
</script>
<template>
  <div class="flex h-screen w-screen items-center justify-center bg-gray-900">
    <div class="min-h-[300px] min-w-[500px] rounded bg-white p-5 text-center">
      <div class="flex h-[300px] w-full flex-col items-center justify-center">
        <v-menu>
          <button class="rounded bg-teal-500 px-4 py-2 text-white">Show menu</button>

          <ul class="mt-4 min-w-[150px] border px-4 py-2 text-left">
            <li>My menu</li>
            <li>Item 1</li>
            <li>Item 2</li>
            <li>Item 3</li>
          </ul>
        </v-menu>
      </div>
    </div>
  </div>
</template>
