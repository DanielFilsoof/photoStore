<script lang="ts">
    import { fade } from 'svelte/transition';
    import { cubicOut } from 'svelte/easing';
  </script>
  
  <main class="h-[75vh] bg-gradient-to-br from-purple-100 to-pink-100 flex items-center justify-center p-4">
    <div class="w-full max-w-4xl grid gap-8 md:grid-cols-2">
      <a
        href="/photos"
        class="group relative overflow-hidden rounded-2xl shadow-lg transition-transform duration-300 hover:scale-105 focus:outline-none focus:ring-4 focus:ring-yellow-300"
        transition:fade={{ duration: 300, easing: cubicOut }}
      >
        <div class="absolute inset-0 bg-gradient-to-r from-purple-400 via-pink-500 to-red-500 opacity-90 transition-opacity duration-300 group-hover:opacity-100"></div>
        <div class="relative z-10 flex flex-col items-center justify-center p-8 text-white h-64">
          <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mb-4"><rect width="18" height="18" x="3" y="3" rx="2" ry="2"/><circle cx="9" cy="9" r="2"/><path d="m21 15-3.086-3.086a2 2 0 0 0-2.828 0L6 21"/></svg>
          <span class="text-2xl font-bold tracking-tight group-hover:text-yellow-300 transition-colors duration-300">View Photo Gallery</span>
        </div>
      </a>
      
      <a
        href="/add-photos"
        class="group relative overflow-hidden rounded-2xl shadow-lg transition-transform duration-300 hover:scale-105 focus:outline-none focus:ring-4 focus:ring-yellow-300"
        transition:fade={{ duration: 300, easing: cubicOut, delay: 150 }}
      >
        <div class="absolute inset-0 bg-gradient-to-r from-purple-400 via-pink-500 to-red-500 opacity-90 transition-opacity duration-300 group-hover:opacity-100"></div>
        <div class="relative z-10 flex flex-col items-center justify-center p-8 text-white h-64">
          <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mb-4"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" x2="12" y1="3" y2="15"/></svg>
          <span class="text-2xl font-bold tracking-tight group-hover:text-yellow-300 transition-colors duration-300">Upload Pictures</span>
        </div>
      </a>
    </div>
  </main>