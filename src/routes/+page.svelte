<script lang="ts">
  import { resolve } from "$app/paths";
  import { Copy, Delete, Plus } from "lucide-svelte";
  import { onMount } from "svelte";

  function copyToClipboard(data) {
    const jsonString = JSON.stringify(data, null, 2);
    navigator.clipboard.writeText(jsonString);
  }

  type FormEntry = {
    name: string;
    url: string;
  };

  let forms: FormEntry[] = [];

  onMount(() => {
    // Load forms from local storage on component mount
    forms = localStorage.getItem("forms")
      ? JSON.parse(localStorage.getItem("forms")!)
      : [];
  });
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

<!-- Created Forms -->
<section class="flex flex-col items-center justify-center p-16 gap-12">
  <h2 class="text-3xl text-gray-800 font-medium">Your Created Forms</h2>

  {#if forms.length > 0}
    <ul class="flex flex-col gap-4 w-full max-w-3xl list-disc">
      {#each forms as form}
        <li>
          <div class="flex flex-row items-center gap-16 justify-between">
            <!-- Form -->
            <a
              href={form.url}
              class="flex flex-row items-center gap-4 bg-gray-100 rounded-md p-4 hover:bg-gray-200 transition-all"
            >
              {form.name}
            </a>

            <!-- Actions -->
            <div class="flex flex-row items-center gap-2">
              <!-- Copy Button -->
              <button
                onclick={() => copyToClipboard(form)}
                class="flex items-center gap-2 px-3 py-1.5 bg-black text-white rounded-md hover:bg-gray-800 transition-all active:scale-95 ml-4"
                type="submit"
              >
                <Copy></Copy>
              </button>

              <!-- Delete Button  -->
              <button
                onclick={() => {
                  // Remove form from local storage
                  forms = forms.filter((f) => f.url !== form.url);
                  localStorage.setItem("forms", JSON.stringify(forms));
                }}
                class="flex items-center gap-2 px-3 py-1.5 bg-black text-white rounded-md hover:bg-red-800 transition-all active:scale-95 ml-4"
                type="submit"
              >
                <Delete></Delete>
              </button>
            </div>
          </div>
        </li>
      {/each}
    </ul>
  {:else}
    <p class="text-gray-600">
      You haven't created any forms yet. Start by clicking the "Create New Form"
      button above!
    </p>
  {/if}
</section>
