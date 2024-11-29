<script>
  import { onMount } from 'svelte';

  let albumdata = [];
  let loading = true;
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
      console.log('Parsed result:', result); // Let's see the full structure

      // Access the data through _embedded
      albumdata = result._embedded.albumDtoList; // or result._embedded.musics depending on your API
      loading = false;

      console.log('Final data:', albumdata);
    } catch (error) {
      console.error('Error:', error);
      loading = false;
    }
  }

  async function handleSubmit(event) {
    event.preventDefault(); // Prevent the default form submission

    // Prepare the payload
    const payload = {
      title: newMusic.title,
      album: {id: newMusic.albumId}
    };

    console.log('Sending payload:', payload); // Log the payload being sent

    try {
      const response = await fetch('http://localhost:8888/api/music', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(payload)
      });

      if (!response.ok) {
        throw new Error('Failed to add new music');
      }

      // Optionally, you can handle the response
      const result = await response.json();
      console.log('Music added:', result);

      // Reset the form
      newMusic.title = '';
      newMusic.albumId = '';

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
      <form on:submit={handleSubmit} action="/" class="flex flex-col gap-4 2xl:w-1/3">
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
          Choose an album:<br>
          <select name="albums" id="albums" class="p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400 [color-scheme:dark] w-full">
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
