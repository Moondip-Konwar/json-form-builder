<script lang="ts">
  import { Delete, Plus } from "lucide-svelte";

  let fieldLabelText = $state("");
  let selectedFieldType = $state("text");

  let fields = $state<{ label: string; type: string }[]>([
    { label: "First Name", type: "text" },
    { label: "Age", type: "number" },
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
</script>

<form class="px-8 py-4 flex flex-row gap-8">
  <!-- Form Details -->
  <section class="prose">
    <h3>Form Details</h3>
    <!-- Form Name -->
    <div class="form-control">
      <label for="form-name" class="label">Form Name *</label>
      <input
        id="form-name"
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
      ></textarea>
    </div>

    <!-- Author Name -->
    <div class="form-control">
      <label for="author-name" class="label">Author Name</label>
      <input id="author-name" type="text" placeholder="Enter author name" />
    </div>
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
        <option value="text">Text</option>
        <option value="number">Number</option>
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
  input,
  textarea {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
</style>
