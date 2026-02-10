<div class="px-8 py-4 flex justify-center items-center">
  <!-- Card -->
  <section class="prose p-8 w-full">
    <!-- Title -->
    <h2 class="text-center">Create New Form</h2>

    <!-- Form -->
    <form action="" on:submit|preventDefault class="flex flex-col gap-6 mt-8">
      <!-- Form Fields -->
      <div class="flex flex-col gap-8">
        <!-- Form Name -->
        <div class="flex flex-col gap-1">
          <label for="form-name" class="font-medium">Form Name *</label>
          <input
            type="text"
            required
            id="form-name"
            name="form-name"
            placeholder="Enter form name"
            class="border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
          />
        </div>

        <!-- Form Description -->
        <div class="flex flex-col gap-1">
          <label for="form-description" class="font-medium"
            >Form Description</label
          >
          <textarea
            id="form-description"
            name="form-description"
            placeholder="Enter form description"
            class="border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
          />
        </div>
      </div>

      <!-- Author Name -->
      <div class="flex flex-col gap-1">
        <label for="author-name" class="font-medium">Author Name</label>
        <input
          type="text"
          id="author-name"
          name="author-name"
          placeholder="Enter author name"
          class="border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
        />
      </div>

      <!-- Submit Button  -->
      <button
        type="submit"
        class="mt-6 bg-black/95 text-white font-medium rounded-lg px-4 py-2 hover:bg-black/80 transition-colors duration-200"
      >
        Create Form
      </button>
    </form>
  </section>
</div>
