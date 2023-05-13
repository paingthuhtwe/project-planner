<template>
  <div class="xs:p-0 mx-auto md:w-full md:max-w-md">
    <div class="bg-white shadow w-full rounded-lg divide-y divide-gray-200">
      <form class="px-5 py-7" @submit.prevent="add">
        <label class="font-semibold text-sm text-gray-600 pb-1 block"
          >Title</label
        >
        <input
          type="text"
          class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
          ref="title"
          v-model="title"
        />
        <label class="font-semibold text-sm text-gray-600 pb-1 block"
          >Description</label
        >
        <textarea
          class="border rounded-lg px-3 py-2 mt-1 mb-5 text-sm w-full"
          ref="description"
          v-model="description"
        >
        </textarea>
        <button
          type="submit"
          class="transition duration-200 bg-blue-500 hover:bg-blue-600 focus:bg-blue-700 focus:shadow-sm focus:ring-4 focus:ring-blue-500 focus:ring-opacity-50 text-white w-full py-2.5 rounded-lg text-sm shadow-sm hover:shadow-md font-semibold text-center inline-block"
        >
          <span class="inline-block mr-2">Add</span>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            class="w-4 h-4 inline-block"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M17 8l4 4m0 0l-4 4m4-4H3"
            />
          </svg>
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      url: "http://localhost:8000/api/projects",
      title: "",
      description: "",
    };
  },
  methods: {
    add() {
      if (this.title && this.description) {
        fetch(this.url, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            title: this.title,
            description: this.description,
          }),
        }).then(() => this.$router.push({ name: "home" }));
      } else if (!this.title) {
        this.$refs.title.focus();
      } else if (!this.description) {
        this.$refs.description.focus();
      }
    },
  },
};
</script>

<style>
</style>