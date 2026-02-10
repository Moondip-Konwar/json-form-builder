<script lang="ts">
  import { page } from "$app/state"; // Svelte 5 style
  import { Clipboard, Check } from "lucide-svelte";

  let copied = $state(false);

  function copyToClipboard() {
    const jsonString = JSON.stringify(data, null, 2);
    navigator.clipboard.writeText(jsonString);

    // Visual feedback
    copied = true;
    setTimeout(() => (copied = false), 2000);
  }

  const name = page.url.searchParams.get("formName");
  const description = page.url.searchParams.get("formDescription");
  const author = page.url.searchParams.get("authorName");

  // Parse the fields back into an array
  const fieldsRaw = page.url.searchParams.get("fields") || "[]";
  const fields = JSON.parse(fieldsRaw);
  let data = $state({});
</script>

<div class="w-full h-full flex flex-col justify-center p-8 gap-4">
  <!-- Form -->
  <section class="h-full flex flex-col gap-8 flex-1 p-8">
    <!-- Details -->
    <div class="flex flex-col gap-2">
      <h1 class="text-center text-4xl">{name}</h1>
      {#if description}
        <p class="text-center">{description}</p>
      {/if}

      {#if author}
        <p class="text-center italic">Created by: {author}</p>
      {/if}
    </div>

    <!-- Fields -->
    <div class="flex flex-col gap-4">
      {#each fields as field}
        <div class="flex flex-col gap-1">
          <label for={field.label}>{field.label}</label>
          <input
            name={field.label}
            type={field.type}
            bind:value={data[field.label]}
            class="rounded-md"
            placeholder="Enter: {field.label} as {field.type.toLowerCase()}"
          />
        </div>
      {/each}
    </div>
  </section>

  <!-- Json Output -->
  <section class="h-full flex flex-col gap-8 p-8 flex-1">
    <div class="flex justify-between items-center mb-4">
      <h2 class="text-2xl">Form JSON Output</h2>

      <button
        onclick={copyToClipboard}
        class="flex items-center gap-2 px-3 py-1.5 bg-black text-white rounded-md hover:bg-gray-800 transition-all active:scale-95"
        type="submit"
      >
        {#if copied}
          <Check size={16} class="text-white" />
          <span>Copied!</span>
        {:else}
          <Clipboard size={16} />
          <span>Copy JSON</span>
        {/if}
      </button>
    </div>

    <pre
      class="bg-gray-100 p-6 rounded-md flex-1 overflow-auto font-mono text-sm leading-relaxed border border-gray-200 shadow-inner">
    {JSON.stringify(data, null, 2).trim()}
  </pre>
  </section>
</div>

<style>
  p {
    color: var(--color-gray-700);
  }
  /* Ensure the pre tag respects the indentations */
  pre {
    white-space: pre-wrap;
    word-break: break-all;
  }
</style>
