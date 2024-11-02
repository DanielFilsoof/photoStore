<script lang="ts">
    import { onMount } from 'svelte';
    import { fade } from 'svelte/transition';
    import { cubicOut } from 'svelte/easing';
  
    let photos: { id: number; url: string; title: string }[] = [];
    let loading = true;
    let error = null;
  
    async function fetchPhotos() {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/photos?_limit=20');
        if (!response.ok) throw new Error('Failed to fetch photos');
        const data = await response.json();
        photos = data.map(photo => ({
          id: photo.id,
          url: photo.url,
          title: photo.title
        }));
      } catch (e) {
        error = e.message;
      } finally {
        loading = false;
      }
    }
  
    onMount(fetchPhotos);
  </script>
  
  <main class="min-h-screen bg-gradient-to-br from-purple-100 to-pink-100 p-4 md:p-8">
    <div class="max-w-6xl mx-auto">
      <h1 class="text-3xl font-bold mb-6 text-center text-transparent bg-clip-text bg-gradient-to-r from-purple-400 via-pink-500 to-red-500">
        Your Photo Gallery
      </h1>
  
      {#if loading}
        <div class="flex justify-center items-center h-64">
          <div class="animate-spin rounded-full h-16 w-16 border-t-2 border-b-2 border-purple-500"></div>
        </div>
      {:else if error}
        <div class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative" role="alert">
          <strong class="font-bold">Error:</strong>
          <span class="block sm:inline">{error}</span>
        </div>
      {:else}
        <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4" in:fade={{ duration: 300, easing: cubicOut }}>
          {#each photos as photo (photo.id)}
            <div class="relative group overflow-hidden rounded-lg shadow-md transition-transform duration-300 hover:scale-105 focus-within:ring-4 focus-within:ring-yellow-300">
              <img 
                src={photo.url} 
                alt={photo.title} 
                class="w-full h-48 object-cover"
                loading="lazy"
              />
              <div class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-end p-4">
                <p class="text-white text-sm font-medium truncate">{photo.title}</p>
              </div>
              <button class="sr-only focus:not-sr-only focus:absolute focus:z-10 focus:top-2 focus:left-2 bg-white text-purple-600 px-2 py-1 rounded text-sm">
                View {photo.title}
              </button>
            </div>
          {/each}
        </div>
      {/if}
    </div>
  </main>
  
  <style>
    /* Custom styles to match the gradient text with the app's theme */
    :global(.dark) {
      --gradient-from: theme('colors.purple.400');
      --gradient-via: theme('colors.pink.500');
      --gradient-to: theme('colors.red.500');
    }
  </style>