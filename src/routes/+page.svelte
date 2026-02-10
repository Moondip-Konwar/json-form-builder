<script>
  import { resolve } from "$app/paths";
  import { Plus } from "lucide-svelte";
</script>

<!-- Hero -->
<main
  class="flex flex-col items-center justify-center h-screen px-8 py-4 gap-12"
>
  <!-- Title -->
  <div class="flex flex-col items-center">
    <h1 class="text-center text-gray-800 font-medium text-6xl">
      Create JSON Forms with Ease
    </h1>
    <p class="text-gray-600 text-center mt-4 text-xl max-w-5xl">
      <!-- A short description of >50 words -->
      Json Forms is a powerful tool that allows you to create dynamic and interactive
      forms using JSON.
    </p>
  </div>

  <!-- Create Button  -->
  <div class="flex flex-col items-center justify-center">
    <a
      href={resolve("/new")}
      class="rounded-lg p-3 bg-black/95 text-white font-medium cursor-pointer flex flex-row items-center gap-2"
    >
      <Plus size="20" strokeWidth="1.3"></Plus>
      Create New Form</a
    >
  </div>
</main>
