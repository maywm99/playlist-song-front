<div class="flex items-center justify-center h-screen">
  <div class="container p-10 bg-gray-800 rounded-lg">
    <a
      href="/album"
      class="inline-block px-6 py-3 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
    >
      ALBUM
    </a>

    <div class="flex flex-row items-center justify-between my-2">
      <p class="text-2xl font-semibold">SONGS</p>
      <a
        href="/newsong"
        class="inline-block px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
      >
        + SONG
      </a>
    </div>

    <table class="w-full table-auto">
      <thead class="text-left border-b-2 border-slate-400">
        <tr>
          <th>Song</th>
          <th>Artist</th>
          <th>Year</th>
        </tr>
      </thead>
      <tbody>
        <tr class="border-b border-slate-400">
          <td>The Sliding Mr. Bones (Next Stop, Pottersville)</td>
          <td>Malcolm Lockyer</td>
          <td>1961</td>
          <td class="flex flex-row justify-end gap-4 py-2">
            <a
              href="/"
              class="px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-emerald-400"
            >
              EDIT
            </a>
            <a
              href="/"
              class="px-6 py-2 font-semibold bg-purple-500 rounded-full hover:bg-red-500"
            >
              REMOVE
            </a>
          </td>
        </tr>
        <tr class="border-b border-slate-400">
          <td>Witchy Woman</td>
          <td>The Eagles</td>
          <td>1972</td>
        </tr>
        <tr class="border-b border-slate-400">
          <td>Shining Star</td>
          <td>Earth, Wind, and Fire</td>
          <td>1975</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
