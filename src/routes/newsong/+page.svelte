<script>
  // Get today's date in YYYY-MM-DD format
  const today = new Date().toISOString().split("T")[0];
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
      <form method="POST" class="flex flex-col gap-4 2xl:w-1/3">
        <input name="id" type="hidden" />
        <label>
          Title
          <br /><input
            name="title"
            type="text"
            placeholder="Enter song title"
            class="w-full p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400"
          />
        </label>
        <label
          >Date
          <br /><input
            name="date"
            type="date"
            value={today}
            class="p-2 mt-1 bg-gray-800 border rounded-lg border-slate-400 [color-scheme:dark] w-full"
          />
        </label>
        <button
          class="inline-block px-6 py-2 mt-6 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
          >ADD</button
        >
      </form>
    </div>
  </div>
</div>
