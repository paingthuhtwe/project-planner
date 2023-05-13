<template>
  <div
    class="bg-slate-200 shadow-md mb-6 p-5 py-10 rounded-md"
    :class="{
      'border-s-4 border-red-700': !project.completed,
      'border-s-4 border-teal-600': project.completed,
    }"
    :id="'project' + project.id"
  >
    <h1 class="text-xl font-semibold flex justify-between items-center">
      <div class="cursor-pointer" @click.self="showDetail = !showDetail">
        {{ project.title }}
      </div>
      <div class="float-right flex">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }">
          <fa
            class="px-2 text-yellow-500 cursor-pointer hover:text-yellow-600"
            :icon="['fas', 'edit']"
          />
        </router-link>
        <fa
          v-if="project.completed"
          @click="deleteProject"
          class="px-2 text-red-700 cursor-pointer hover:text-red-800"
          :icon="['fas', 'trash']"
        />
        <fa
          v-if="!project.completed"
          @click="finishProject"
          class="px-2 text-teal-600 cursor-pointer hover:text-teal-700"
          :icon="['fas', 'check']"
        />
      </div>
    </h1>
    <div v-if="showDetail" class="mt-3">
      {{ project.description }}
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      url: "http://localhost:8000/api/projects/",
      showDetail: false,
    };
  },
  methods: {
    deleteProject() {
      fetch(this.url + this.project.id, {
        method: "DELETE",
      }).then(() => this.$emit("delete", this.project.id));
    },
    finishProject() {
      fetch(this.url + this.project.id, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          completed: 1,
        }),
      }).then(() => this.$emit("finish", this.project.id));
    },
  },
  components: {},
};
</script>

<style>
</style>