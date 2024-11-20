<div class="flex items-center justify-center h-screen">
  <div class="container p-10 bg-gray-800 rounded-lg">
    <a
      href="/"
      class="inline-block px-6 py-3 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
    >
      Voltar
    </a>
    <div class="flex justify-center mt-10">
      <form method="POST" class="flex flex-col gap-4 2xl:w-1/3">
        <h2 class="text-2xl font-semibold">NEW ALBUM</h2>
        <input name="id" type="hidden" />
        <label>
          Title
          <br /><input
            name="title"
            type="text"
            placeholder="Enter album title"
            class="w-full p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400"
          />
        </label>
        <label>
          Artist
          <br /><input
            name="artist"
            type="text"
            placeholder="Enter artists names"
            class="w-full p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400"
          />
        </label>
        <div class="bg-slate-400 h-px"></div>
        <div class="flex flex-row justify-between">
          <label for="songs">Songs</label>
          <a
            href="/newsong"
            class="inline-block px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
          >ADD
          </a>
        </div>
        <div class="flex flex-col">
          <div class="w-full p-2 mt-1 border rounded-lg border-slate-400 flex justify-between items-center">
            <p>song</p>
            <button class="px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-red-500">REMOVE</button>
          </div>
          <div class="w-full p-2 mt-1 border rounded-lg border-slate-400 flex justify-between items-center">
            <p>song</p>
            <button class="px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-red-500">REMOVE</button>
          </div>
        </div>
        <button
          class="inline-block px-6 py-2 mt-6 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
          >CREATE</button
        >
      </form>
    </div>
  </div>
</div>
