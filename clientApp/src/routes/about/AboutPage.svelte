<script lang="ts">
    import { fade } from 'svelte/transition';
    import { cubicOut } from 'svelte/easing';
  </script>
  
  <main 
    class="h-[75vh] bg-gradient-to-br from-purple-100 to-pink-100 flex items-center justify-center p-4"
    transition:fade={{ duration: 300, easing: cubicOut }}
  >
    <div class="w-full max-w-2xl">
      <div class="bg-white bg-opacity-90 rounded-2xl shadow-lg p-8">
        <h1 class="text-3xl font-bold mb-6 text-center text-transparent bg-clip-text bg-gradient-to-r from-purple-400 via-pink-500 to-red-500">
          About Private Photo Store
        </h1>
        <p class="text-lg text-gray-700 mb-4">
          Welcome to Private Photo Store, your secure haven for personal photo management.
        </p>
        <p class="text-lg text-gray-700 mb-4">
          Our application is designed with your privacy in mind. Here, you can upload and manage your photos privately, without the risk of them being used to train AI models or being accessed by unauthorized parties.
        </p>
        <p class="text-lg text-gray-700 mb-4">
          We understand the importance of your personal memories and the need to keep them safe. With Private Photo Store, you have full control over your images, ensuring they remain yours and yours alone.
        </p>
        <p class="text-lg text-gray-700">
          Enjoy the peace of mind that comes with truly private photo storage and management.
        </p>
      </div>
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