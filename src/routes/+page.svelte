<script>
  import { onMount } from 'svelte';

  let data = [];
  let loading = true;

  async function fetchData() {
    try {
      const response = await fetch('http://localhost:8888/api/music', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        }
      });

      const result = await response.json();
      console.log('Parsed result:', result); // Let's see the full structure

      // Access the data through _embedded
      data = result._embedded.musicDtoList; // or result._embedded.musics depending on your API
      loading = false;

      console.log('Final data:', data);
    } catch (error) {
      console.error('Error:', error);
      loading = false;
    }
  }

  onMount(() => {
    fetchData();
  });

  async function remove(id) {
    try {
      const response = await fetch(`http://localhost:8888/api/music/${id}` , {
        method: 'DELETE',
        headers: {
          'Content-Type': 'application/json',
        }
      });
      if (!response.ok) {
        const errorMessage = await response.text();
        throw new Error(`Failed to delete music: ${errorMessage}`);
      }

      console.log('Music removed');
      // Update the data by filtering out the removed item
      data = data.filter(music => music.id !== id);
    } catch (error) {
      console.error('Error:', error);
    }
  }
</script>

<div class="flex items-center justify-center h-screen">
  <div class="container p-10 bg-gray-800 rounded-lg">
    <a
      href="/album"
      class="inline-block px-6 py-3 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
    >
      ALBUM
    </a>

    <div class="flex flex-row items-center justify-between my-2">
      <p class="text-2xl font-semibold">MUSIC</p>
      <a
        href="/newmusic"
        class="inline-block px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
      >
        + MUSIC
      </a>
    </div>

    <table class="w-full table-auto">
      <thead class="text-left border-b-2 border-slate-400">
        <tr>
          <th>Title</th>
          <th>Artists</th>
          <th>Album</th>
        </tr>
      </thead>
      <tbody>
        {#each data as music}
          <tr class="border-b border-slate-400">
            <td>{music.title}</td>
            <td>{music.album.artist}</td>
            <td>{music.album.title}</td>
            <td class="flex flex-row justify-end gap-4 py-2">
              <a
                href="/"
                class="px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
              >
                EDIT
              </a>
              <button
                on:click={() => remove(music.id)}
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
