<script lang="ts">
    import { fade } from 'svelte/transition';
    import { cubicOut } from 'svelte/easing';
  
    let dragActive = false;
    let files: FileList | null = null;
    let names = '';
    let tags = '';
    let uploading = false;
    let uploadStatus: 'idle' | 'success' | 'error' = 'idle';
  
    function handleDragEnter(e: DragEvent) {
      e.preventDefault();
      e.stopPropagation();
      dragActive = true;
    }
  
    function handleDragLeave(e: DragEvent) {
      e.preventDefault();
      e.stopPropagation();
      dragActive = false;
    }
  
    function handleDragOver(e: DragEvent) {
      e.preventDefault();
      e.stopPropagation();
    }
  
    function handleDrop(e: DragEvent) {
      e.preventDefault();
      e.stopPropagation();
      dragActive = false;
      if (e.dataTransfer) {
        files = e.dataTransfer.files;
      }
    }
  
    function handleFileInput(e: Event) {
      const target = e.target as HTMLInputElement;
      if (target.files) {
        files = target.files;
      }
    }
  
    async function handleSubmit() {
      if (!files || files.length === 0) {
        alert('Please select a file to upload.');
        return;
      }
  
      uploading = true;
      uploadStatus = 'idle';
  
      // Mock API call
      try {
        await new Promise(resolve => setTimeout(resolve, 2000)); // Simulate network delay
        
        // Simulate successful upload
        console.log('Uploaded file:', files[0].name);
        console.log('Names:', names);
        console.log('Tags:', tags);
        
        uploadStatus = 'success';
      } catch (error) {
        console.error('Upload failed:', error);
        uploadStatus = 'error';
      } finally {
        uploading = false;
      }
    }
  </script>
  
  <main class="min-h-screen bg-gradient-to-br from-purple-100 to-pink-100 p-4 md:p-8">
    <div class="max-w-2xl mx-auto">
      <h1 class="text-3xl font-bold mb-6 text-center text-transparent bg-clip-text bg-gradient-to-r from-purple-400 via-pink-500 to-red-500">
        Upload Your Photo
      </h1>
  
      <form on:submit|preventDefault={handleSubmit} class="bg-white bg-opacity-90 rounded-2xl shadow-lg p-6">
        <div
          class="border-2 border-dashed border-gray-300 rounded-lg p-8 mb-4 text-center cursor-pointer transition-colors duration-300"
          class:border-purple-500={dragActive}
          on:dragenter={handleDragEnter}
          on:dragleave={handleDragLeave}
          on:dragover={handleDragOver}
          on:drop={handleDrop}
        >
          <input
            type="file"
            id="fileInput"
            class="hidden"
            on:change={handleFileInput}
            accept="image/*"
          />
          <label for="fileInput" class="cursor-pointer">
            {#if files && files.length > 0}
              <p class="text-lg font-medium text-gray-700">Selected file: {files[0].name}</p>
            {:else}
              <p class="text-lg font-medium text-gray-700">Drag and drop your photo here, or click to select</p>
            {/if}
          </label>
        </div>
  
        <div class="mb-4">
          <label for="names" class="block text-sm font-medium text-gray-700 mb-1">Names of people in the photo (optional)</label>
          <input
            type="text"
            id="names"
            bind:value={names}
            class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent"
            placeholder="e.g. John Doe, Jane Smith"
          />
        </div>
  
        <div class="mb-6">
          <label for="tags" class="block text-sm font-medium text-gray-700 mb-1">Tags (optional)</label>
          <input
            type="text"
            id="tags"
            bind:value={tags}
            class="w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent"
            placeholder="e.g. vacation, beach, sunset"
          />
        </div>
  
        <button
          type="submit"
          class="w-full bg-gradient-to-r from-purple-400 via-pink-500 to-red-500 text-white font-bold py-2 px-4 rounded-md hover:opacity-90 transition-opacity duration-300 focus:outline-none focus:ring-2 focus:ring-purple-500 focus:ring-opacity-50"
          disabled={uploading}
        >
          {uploading ? 'Uploading...' : 'Upload Photo'}
        </button>
  
        {#if uploadStatus === 'success'}
          <p class="mt-4 text-green-600 text-center" transition:fade={{ duration: 300, easing: cubicOut }}>Upload successful!</p>
        {:else if uploadStatus === 'error'}
          <p class="mt-4 text-red-600 text-center" transition:fade={{ duration: 300, easing: cubicOut }}>Upload failed. Please try again.</p>
        {/if}
      </form>
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