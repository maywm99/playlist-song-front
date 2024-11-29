<script>
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';

  let albumdata = [];
  let newMusic = {
    title: '',
    albumId: ''
  };

  async function fetchData() {
    try {
      const response = await fetch('http://localhost:8888/api/album', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        }
      });

      const result = await response.json();
      console.log('Parsed result:', result);

      albumdata = result._embedded.albumDtoList;

      console.log('Final data:', albumdata);
    } catch (error) {
      console.error('Error:', error);
    }
  }

  async function handleSubmit(event) {
    event.preventDefault(); 

    if (!newMusic.title || !newMusic.albumId) {
      alert('Please fill out all fields');
      return;
    }

    const payload = {
      title: newMusic.title,
      album: {id: newMusic.albumId}
    };

    console.log('Sending payload:', payload);

    try {
      const response = await fetch('http://localhost:8888/api/music', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(payload)
      });

      const result = await response.json();
      console.log('Music added:', result);

      newMusic.title = '';
      newMusic.albumId = '';

      goto("/")

    } catch (error) {
      console.error('Error:', error);
    }
  }

  onMount(() => {
    fetchData();
  });
</script>

<div class="flex items-center justify-center h-screen">
  <div class="container p-10 bg-gray-800 rounded-lg">
    <a
      href="/"
      class="inline-block px-6 py-3 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
    >
      Voltar
    </a>
    <div class="flex justify-center mt-10">
      <form on:submit={handleSubmit} class="flex flex-col gap-4 2xl:w-1/3">
        <h2 class="text-2xl font-semibold">NEW MUSIC</h2>
        <input name="id" type="hidden" />
        <label>
          Title
          <br /><input
            name="title"
            type="text"
            placeholder="Enter music title"
            bind:value={newMusic.title}
            class="w-full p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400"
          />
        </label>
        <label>
          Select an album:<br>
          <select name="albums" id="albums" bind:value={newMusic.albumId} class="p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400 [color-scheme:dark] w-full">
            <option value="" disabled selected>Selecting...</option>
            {#each albumdata as album}
              <option value="{album.id}">{album.title}</option>
            {/each}
          </select>
        </label>
        <button
          type="submit"
          class="inline-block px-6 py-2 mt-6 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
        >ADD</button>
      </form>
    </div>
  </div>
</div>
