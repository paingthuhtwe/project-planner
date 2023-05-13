<template>
  <div class="">
    <nav class="mb-[2em]">
      <button
        @click="filterBy('all')"
        :class="{ 'text-purple-700 bg-slate-300': current === 'all' }"
        class="text-lg px-1 mr-2 text-slate-950 font-medium px-3 py-1 rounded-md transition duration-700"
      >
        View All
      </button>
      <button
        @click="filterBy('complete')"
        :class="{ 'text-purple-700 bg-slate-300': current === 'complete' }"
        class="text-lg px-1 mx-2 text-slate-950 font-medium px-3 py-1 rounded-md transition duration-700"
      >
        Completed
      </button>
      <button
        @click="filterBy('onGoing')"
        :class="{ 'text-purple-700 bg-slate-300': current === 'onGoing' }"
        class="text-lg px-1 mx-2 text-slate-950 font-medium px-3 py-1 rounded-md transition duration-700"
      >
        OnGoing
      </button>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    filterBy(value) {
      this.$emit("filterValue", value);
    },
  },
};
</script>

<style scoped>
nav a.router-link-exact-active {
  color: #624fdc;
}
</style>