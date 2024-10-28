<script lang="ts">
    import { slide, fade } from 'svelte/transition';
    import { cubicOut } from 'svelte/easing';
  
    let isOpen = false;
  
    const routes = [
      { name: "Home", path: "/" },
      { name: "Photos", path: "/photos" },
      { name: "Add Photos", path: "/add-photos" },
      { name: "About", path: "/about" },
    ];
  
    function toggleMenu() {
      isOpen = !isOpen;
    }
  </script>
  
  <header class="sticky top-0 z-50 w-full bg-gradient-to-r from-purple-400 via-pink-500 to-red-500 text-white shadow-lg">
    <div class="container mx-auto px-4 py-2 flex items-center justify-between">
      <a href="/" class="text-2xl font-bold tracking-tight hover:text-yellow-300 transition-colors duration-300">
        Private Photo Store
      </a>
      <nav class="hidden md:flex space-x-6 text-sm font-medium">
        {#each routes as route}
          <a
            href={route.path}
            class="relative overflow-hidden group py-2"
          >
            <span class="relative z-10 transition-colors duration-300 group-hover:text-yellow-300">{route.name}</span>
            <span class="absolute inset-x-0 bottom-0 h-0.5 bg-yellow-300 transform scale-x-0 group-hover:scale-x-100 transition-transform duration-300 ease-out"></span>
          </a>
        {/each}
      </nav>
      <button
        on:click={toggleMenu}
        class="md:hidden p-2 rounded-full hover:bg-white/20 transition-colors duration-300"
        aria-label="Toggle menu"
      >
        {#if isOpen}
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="h-6 w-6"><path d="M18 6 6 18"/><path d="m6 6 12 12"/></svg>
        {:else}
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="h-6 w-6"><line x1="4" x2="20" y1="12" y2="12"/><line x1="4" x2="20" y1="6" y2="6"/><line x1="4" x2="20" y1="18" y2="18"/></svg>
        {/if}
      </button>
    </div>
  </header>
  
  {#if isOpen}
    <button
      transition:fade={{ duration: 200, easing: cubicOut }}
      class="fixed inset-0 z-40 bg-black/50 backdrop-blur-sm"
      on:click={toggleMenu}
      aria-label="Close menu"
      
    ></button>
    <nav
      transition:slide={{ duration: 300, easing: cubicOut }}
      class="fixed inset-y-0 right-0 z-50 w-64 bg-gradient-to-b from-purple-600 to-pink-600 p-6 shadow-xl"
    >
      <div class="flex flex-col space-y-6">
        {#each routes as route}
          <a
            href={route.path}
            class="text-white text-lg font-medium hover:text-yellow-300 transition-colors duration-300"
            on:click={toggleMenu}
          >
            {route.name}
          </a>
        {/each}
      </div>
    </nav>
  {/if}