<script>
    import { goto } from '$app/navigation';
    import { onMount } from 'svelte';
  
  let album = {
    id: '',
    title: '',
    artist: '',
    date: ''
  };

  const albumId = localStorage.getItem('albumId');

  async function fetchData() {
    try {
      const response = await fetch(`http://localhost:8888/api/album/${albumId}`, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        }
      });

      const result = await response.json();
      console.log('Parsed result:', result); // Let's see the full structure

      album = {
        id: result.id,
        title: result.title,
        artist: result.artist,
        date: formatDate(result.releaseDate)
      };

      console.log('Final data:', album);
    } catch (error) {
      console.error('Error:', error);
    }
  }

  function formatDate(dateString) {
    if (!dateString) return ''; // Handle case where dateString is undefined or null
    const date = new Date(dateString);
    return date.toISOString().split('T')[0];
  }

  onMount(() => {
    fetchData();
  });
  
  async function handleSubmit(event) {
    event.preventDefault(); // Prevent the default form submission
  
    // Prepare the payload
    const payload = {
        id: album.id,
      title: album.title,
      artist: album.artist,
      releaseDate: album.date
    };
  
    console.log('Sending payload:', payload); // Log the payload being sent
  
    try {
      const response = await fetch('http://localhost:8888/api/album', {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(payload)
      });
  
      if (!response.ok) {
        throw new Error('Failed to change album');
      }
  
      // Optionally, you can handle the response
      const result = await response.json();
      console.log('Album changed:', result);
  
      console.log('redirecionando')
      goto("/album");
  
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
        Voltar
      </a>
      <div class="flex justify-center mt-10">
        <form on:submit={handleSubmit} class="flex flex-col gap-4 2xl:w-1/3">
          <h2 class="text-2xl font-semibold">EDIT ALBUM</h2>
          <input name="id" type="hidden" />
          <label>
            Title
            <br /><input
              name="title"
              type="text"
              placeholder="Enter album title"
              bind:value={album.title}
              class="w-full p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400"
            />
          </label>
          <label>
            Artist
            <br /><input
              name="artist"
              type="text"
              placeholder="Enter artists names"
              bind:value={album.artist}
              class="w-full p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400"
            />
          </label>
          <label
            >Date
            <br /><input
              name="date"
              type="date"
              bind:value={album.date}
              class="p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400 [color-scheme:dark] w-full"
            />
          </label>
          <button
            type="submit"
            class="inline-block px-6 py-2 mt-6 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
          >CHANGE</button>
        </form>
      </div>
    </div>
  </div>
  