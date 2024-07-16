<script>
    import { getFile, uploadFile } from '../lib/storage';
    import { writable } from 'svelte/store';
  
    let selectedFile = null;
    let uploaded = writable(null);
    let inputRef;
  
    const handleUpload = async () => {
      const folder = "user/";
      const imagePath = await uploadFile(selectedFile, folder);
      const imageUrl = await getFile(imagePath);
      uploaded.set(imageUrl);
    };
  </script>
  
  <style>
    .container {
      max-width: 560px;
      margin: 2rem auto;
    }
    .button {
      margin-top: 1.25rem;
      background-color: #16a34a;
      color: white;
      border-radius: 0.5rem;
      padding: 0.5rem 1rem;
      width: 100%;
      transition: background-color 0.2s;
    }
    .button:hover {
      background-color: #166534;
    }
  </style>
  
  <div class="container">
    <div class="flex justify-between items-center pb-4 border-b border-dashed border-gray-900 mb-4">
      <h1 class="text-3xl font-semibold">Upload File</h1>
    </div>
    <input
      type="file"
      bind:this={inputRef}
      on:change={(e) => {
        selectedFile = e.target.files[0];
      }}
    />
    <button class="button" type="button" on:click={handleUpload}>
      Upload File
    </button>
    {#if $uploaded}
      <img src={$uploaded} class="my-5 max-w-[400px]" alt="upload file" />
    {/if}
  </div>
  
  <svelte:head>
    <title>Upload File</title>
  </svelte:head>
  