<script lang="ts">
  import { Delete, Plus } from "lucide-svelte";
  import { goto } from "$app/navigation";

  // Form Details
  let formName = $state("");
  let formDescription = $state("");
  let authorName = $state("");

  // Form Field
  let fieldLabelText = $state("");
  let selectedFieldType = $state("text");
  let fields = $state<{ label: string; type: string }[]>([
    { label: "Name", type: "text" },
  ]);

  function addField() {
    // Validate field label
    if (!fieldLabelText) {
      alert("Please enter a field label.");
      return;
    }

    fields = [...fields, { label: fieldLabelText, type: selectedFieldType }];
    fieldLabelText = "";
  }

  function handleSubmit(event: SubmitEvent) {
    event.preventDefault();

    const params = new URLSearchParams({
      formName,
      formDescription,
      authorName,
      fields: JSON.stringify(fields),
    });

    goto(`/forms?${params.toString()}`);
  }
</script>

<form class="px-8 py-4 flex flex-row gap-8" onsubmit={handleSubmit}>
  <!-- Form Details -->
  <section class="prose">
    <h3>Form Details</h3>
    <!-- Form Name -->
    <div class="form-control">
      <label for="form-name" class="label"
        >Form Name <span class="text-red-900">*</span></label
      >
      <input
        id="form-name"
        bind:value={formName}
        required
        type="text"
        placeholder="Enter form name"
      />
    </div>

    <!-- Form Description -->
    <div class="form-control">
      <label for="form-description" class="label">Form Description</label>
      <textarea
        id="form-description"
        placeholder="Enter form description"
        rows="4"
        bind:value={formDescription}
      ></textarea>
    </div>

    <!-- Author Name -->
    <div class="form-control">
      <label for="author-name" class="label">Author Name</label>
      <input
        id="author-name"
        bind:value={authorName}
        type="text"
        placeholder="Enter author name"
      />
    </div>

    <!-- Create Form: Submit -->
    <button class="bg-black p-2 rounded-md" id="submit-button" type="submit"
      >Create Form</button
    >
  </section>

  <!-- Form Content -->
  <section class="prose">
    <h3>Form Content</h3>
    <!-- Added Fields -->
    {#each fields as field}
      <div class="flex flex-row gap-4 items-center">
        <input value={field.label} readonly class="flex-1 bg-gray-100" />
        <input value={field.type.toUpperCase()} readonly class="bg-gray-100" />
        <!-- Delete Button -->
        <button
          type="button"
          class="cursor-pointer bg-black text-white rounded-md p-2"
          onclick={() => (fields = fields.filter((f) => f !== field))}
        >
          <Delete></Delete>
        </button>
      </div>
    {/each}

    <!-- Add Field -->
    <div class="flex flex-row gap-4">
      <!-- Label -->
      <input
        type="text"
        bind:value={fieldLabelText}
        placeholder="Field Label"
        class="flex-1"
      />

      <!-- Field Types -->
      <select
        class="bg-white border border-gray-300 rounded-md p-2"
        bind:value={selectedFieldType}
      >
        <option value="text">TEXT</option>
        <option value="number">NUMBER</option>
        <option value="email">EMAIL</option>
        <option value="date">DATE</option>
        <option value="url">URL</option>
        <option value="time">TIME</option>
      </select>

      <!-- Button -->
      <button
        type="button"
        class="cursor-pointer bg-black text-white rounded-md p-2 flex items-center gap-2"
        onclick={addField}
      >
        <Plus size={16} /> Add Field
      </button>
    </div>
  </section>
</form>

<style>
  form > section {
    flex: 1;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    height: fit-content;
  }

  .form-control {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  #submit-button {
    color: white !important;
  }
  button:hover {
    cursor: pointer;
  }
</style>
