<div class="flex items-center justify-center h-screen">
  <div class="container p-10 bg-gray-800 rounded-lg">
    <a
      href="/"
      class="inline-block px-6 py-3 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
    >
      Voltar
    </a>
    <form method="POST" class="flex flex-col justify-center">
      <input name="id" type="hidden" />
      <label>
        Title
        <br /><input name="title" type="text" class="text-slate-900" />
      </label>
      <label
        >Date
        <br /><input name="date" type="date" class="text-slate-900" />
      </label>
      <button
        class="inline-block px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
        >ADD</button
      >
    </form>
  </div>
</div>
