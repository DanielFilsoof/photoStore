<script lang="ts">
    const currentYear = new Date().getFullYear();
  
    const footerLinks = [
      { name: "Terms of Service", path: "/terms" },
      { name: "Privacy Policy", path: "/privacy" },
      { name: "Contact Us", path: "/contact" },
    ];
  
    const socialLinks = [
      { name: "Facebook", icon: "facebook", url: "https://facebook.com" },
      { name: "Twitter", icon: "twitter", url: "https://twitter.com" },
      { name: "Instagram", icon: "instagram", url: "https://instagram.com" },
    ];
  </script>
  
  <footer class="bg-gradient-to-r from-purple-400 via-pink-500 to-red-500 text-white shadow-lg mt-auto">
    <div class="container mx-auto px-4 py-8">
      <div class="flex flex-col md:flex-row justify-between items-center">
        <div class="mb-4 md:mb-0">
          <a href="/" class="text-2xl font-bold tracking-tight hover:text-yellow-300 transition-colors duration-300">
            Private Photo Store
          </a>
          <p class="mt-2 text-sm">Privacy-first photo storage for peace of mind.</p>
        </div>
        <nav class="flex flex-wrap justify-center md:justify-end space-x-6 text-sm font-medium">
          {#each footerLinks as link}
            <a
              href={link.path}
              class="relative overflow-hidden group py-2"
            >
              <span class="relative z-10 transition-colors duration-300 group-hover:text-yellow-300">{link.name}</span>
              <span class="absolute inset-x-0 bottom-0 h-0.5 bg-yellow-300 transform scale-x-0 group-hover:scale-x-100 transition-transform duration-300 ease-out"></span>
            </a>
          {/each}
        </nav>
      </div>
      <div class="mt-8 flex flex-col md:flex-row justify-between items-center">
        <div class="flex space-x-6 mb-4 md:mb-0">
          {#each socialLinks as link}
            <a href={link.url} target="_blank" rel="noopener noreferrer" class="hover:text-yellow-300 transition-colors duration-300">
              <span class="sr-only">{link.name}</span>
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="h-6 w-6">
                {#if link.icon === 'facebook'}
                  <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path>
                {:else if link.icon === 'twitter'}
                  <path d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z"></path>
                {:else if link.icon === 'instagram'}
                  <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                  <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                  <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
                {/if}
              </svg>
            </a>
          {/each}
        </div>
        <p class="text-sm">&copy; {currentYear} Photo Store. All rights reserved.</p>
      </div>
    </div>
  </footer>
  
  <style>
    /* Add any additional styles here if needed */
  </style>