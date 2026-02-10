<script lang="ts">
  import { base, resolve } from "$app/paths";
  import { Delete, Plus } from "lucide-svelte";
  import { onMount } from "svelte";

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
      Build dynamic forms in seconds and share them instantly with a URL. No accounts,
      no sign-ups—just a link for anyone to fill out.
    </p>
  </div>

  <!-- Create Button  -->
  <div class="flex flex-col items-center justify-center">
    <a
      href={`${base}/new`}
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
              href={`${base}${form.url}`}
              class="flex flex-row items-center gap-4 bg-gray-100 rounded-md p-4 hover:bg-gray-200 transition-all"
            >
              {form.name}
            </a>

            <!-- Actions -->
            <div class="flex flex-row items-center gap-2">
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

<!-- About -->
<section
  class="flex flex-col items-center justify-center p-16 pb-32 gap-12 bg-gray-50 border-t border-gray-200"
  id="about"
>
  <div class="flex flex-col items-center max-w-4xl text-center gap-6">
    <h2 class="text-3xl text-gray-800 font-medium">About Json Forms</h2>
    <p class="text-gray-600 text-lg leading-relaxed">
      Json Forms is a zero-backend tool that turns data structures into
      shareable interfaces. Using a visual UI builder, you can craft complex
      forms that live entirely within a URL. When you share a link, you aren't
      sending a database ID—you're sending the form itself. No servers, no
      tracking, just pure JSON data.
    </p>
  </div>

  <div class="flex flex-col gap-4 w-full max-w-3xl">
    <details
      class="group border border-gray-300 rounded-xl bg-white transition-all"
    >
      <summary
        class="flex justify-between items-center p-5 cursor-pointer list-none font-medium text-gray-800"
      >
        How do I use this?
        <span class="transition group-open:rotate-180">↓</span>
      </summary>
      <div class="px-5 pb-5 text-gray-600 leading-relaxed">
        Start by clicking <strong>"Create New Form"</strong>. Use the UI builder
        to add fields like text, numbers, or dropdowns. Once you're done, copy
        the generated link and send it to whoever needs to fill it out.
      </div>
    </details>

    <details
      class="group border border-gray-300 rounded-xl bg-white transition-all"
    >
      <summary
        class="flex justify-between items-center p-5 cursor-pointer list-none font-medium text-gray-800"
      >
        Where is my form saved?
        <span class="transition group-open:rotate-180">↓</span>
      </summary>
      <div class="px-5 pb-5 text-gray-600 leading-relaxed">
        It isn't! The entire form configuration is encoded into the URL. This
        means the link <em>is</em> the form. If you lose the link, the form is gone
        unless you saved it to your dashboard (which uses your browser's local storage).
      </div>
    </details>

    <details
      class="group border border-gray-300 rounded-xl bg-white transition-all"
    >
      <summary
        class="flex justify-between items-center p-5 cursor-pointer list-none font-medium text-gray-800"
      >
        What happens when someone fills out the form?
        <span class="transition group-open:rotate-180">↓</span>
      </summary>
      <div class="px-5 pb-5 text-gray-600 leading-relaxed">
        Once a user completes the fields, the app generates a raw JSON object
        based on their input. They can then copy that JSON to use in their own
        projects, APIs, or documentation.
      </div>
    </details>

    <details
      class="group border border-gray-300 rounded-xl bg-white transition-all"
    >
      <summary
        class="flex justify-between items-center p-5 cursor-pointer list-none font-medium text-gray-800"
      >
        Is my data private?
        <span class="transition group-open:rotate-180">↓</span>
      </summary>
      <div class="px-5 pb-5 text-gray-600 leading-relaxed">
        Completely. Since there is no database, your form data never touches a
        server. All the processing happens locally in the browser of the person
        filling it out.
      </div>
    </details>
  </div>
</section>
