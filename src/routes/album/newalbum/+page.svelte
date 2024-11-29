<script>
  // Get today's date in YYYY-MM-DD format
  const today = new Date().toISOString().split("T")[0];

let newAlbum = {
  title: '',
  artist: '',
  date: today
};


async function handleSubmit(event) {
  event.preventDefault(); // Prevent the default form submission

  // Prepare the payload
  const payload = {
    title: newAlbum.title,
    artist: newAlbum.artist,
    releaseDate: newAlbum.date
  };

  console.log('Sending payload:', payload); // Log the payload being sent

  try {
    const response = await fetch('http://localhost:8888/api/album', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(payload)
    });

    if (!response.ok) {
      throw new Error('Failed to add new album');
    }

    // Optionally, you can handle the response
    const result = await response.json();
    console.log('Album added:', result);

    // Reset the form
    newAlbum.title = '';
    newAlbum.artist = '';
    newAlbum.date = today;

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
        <h2 class="text-2xl font-semibold">NEW ALBUM</h2>
        <input name="id" type="hidden" />
        <label>
          Title
          <br /><input
            name="title"
            type="text"
            placeholder="Enter album title"
            bind:value={newAlbum.title}
            class="w-full p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400"
          />
        </label>
        <label>
          Artist
          <br /><input
            name="artist"
            type="text"
            placeholder="Enter artists names"
            bind:value={newAlbum.artist}
            class="w-full p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400"
          />
        </label>
        <label
          >Date
          <br /><input
            name="date"
            type="date"
            bind:value={newAlbum.date}
            class="p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400 [color-scheme:dark] w-full"
          />
        </label>
        <button
          type="submit"
          class="inline-block px-6 py-2 mt-6 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
        >CREATE</button>
      </form>
    </div>
  </div>
</div>
