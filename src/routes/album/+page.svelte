<script>
  import { goto } from '$app/navigation';
  import { onMount } from 'svelte';

  let data = [];

  async function fetchData() {
    try {
      const response = await fetch('http://localhost:8888/api/album', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        }
      });

      const result = await response.json();
      console.log('Parsed result:', result); // Let's see the full structure

      // Access the data through _embedded
      data = result._embedded.albumDtoList; // or result._embedded.musics depending on your API

      console.log('Final data:', data);
    } catch (error) {
      console.error('Error:', error);
    }
  }

  onMount(() => {
    fetchData();
  });

  function edit(id) {
    // Store the selected album in localStorage
    localStorage.setItem('albumId', id);
    // Navigate to the edit page
    goto('/album/editalbum');
  }

  async function remove(id) {
    try {
      const response = await fetch(`http://localhost:8888/api/album/${id}` , {
        method: 'DELETE',
        headers: {
          'Content-Type': 'application/json',
        }
      });
      if (!response.ok) {
        const errorMessage = await response.text();
        throw new Error(`Failed to delete album: ${errorMessage}`);
      }

      console.log('album removed');
      // Update the data by filtering out the removed item
      data = data.filter(album => album.id !== id);
    } catch (error) {
      console.error('Error:', error);
    }
  }
</script>

<div class="flex items-center justify-center h-screen">
  <div class="container p-10 bg-gray-800 rounded-lg">
    <a
      href="/"
      class="inline-block px-6 py-3 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
    >
      MUSICS
    </a>
    <div class="flex flex-row items-center justify-between my-2">
      <p class="text-2xl font-semibold">ALBUMS</p>
      <a
        href="/album/newalbum"
        class="inline-block px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
      >
        + ALBUM
      </a>
    </div>

    <table class="w-full table-auto">
      <thead class="text-left border-b-2 border-slate-400">
        <tr>
          <th>Title</th>
          <th>Artists</th>
          <th>Date</th>
        </tr>
      </thead>
      <tbody>
        {#each data as album}
          <tr class="border-b border-slate-400">
            <td>{album.title}</td>
            <td>{album.artist}</td>
            <td>{album.releaseDate.split('T')[0]}</td>
            <td class="flex flex-row justify-end gap-4 py-2">
              <button
                on:click={() => edit(album.id)}
                class="px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
              >
                EDIT
            </button>
              <button
                on:click={() => remove(album.id)}
                class="px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-red-500"
              >
                REMOVE
            </button>
            </td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>
</div>
