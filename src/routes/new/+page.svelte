<script>
  import { Plus } from "lucide-svelte";
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
    <!-- Add Field -->
    <div class="flex flex-row gap-4">
      <!-- Label -->
      <input type="text" placeholder="Field Label" class="flex-1" />

      <!-- Field Types -->
      <select class="bg-white border border-gray-300 rounded-md p-2">
        <option value="text">Text</option>
        <option value="number">Number</option>
      </select>

      <!-- Button -->
      <button
        type="button"
        class="cursor-pointer bg-black text-white rounded-md p-2 flex items-center gap-2"
        on:click={() => alert("Add Field")}
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
