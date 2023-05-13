<template>
  <FilterNav @filterValue="current = $event" :current="current"></FilterNav>
  <div v-for="project in filterProjects" :key="project.id">
    <SingleProject
      :project="project"
      @delete="deleteProject"
      @finish="finishProject"
    ></SingleProject>
  </div>
</template>

<script>
import FilterNav from "../components/FilterNav";
import SingleProject from "./SingleProject";
export default {
  components: {
    FilterNav,
    SingleProject,
  },
  data() {
    return {
      url: "http://localhost:8000/api/projects/",
      projects: [],
      current: "all",
    };
  },
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter((project) => project.id != id);
    },
    finishProject(id) {
      let project = this.projects.find((json) => json.id === id);
      project.completed = 1;
    },
  },
  mounted() {
    fetch(this.url)
      .then((res) => res.json())
      .then((json) => (this.projects = json));
  },
  computed: {
    filterProjects() {
      if (this.current === "complete") {
        return this.projects.filter((json) => json.completed);
      }
      if (this.current === "onGoing") {
        return this.projects.filter((json) => !json.completed);
      }
      return this.projects;
    },
  },
};
</script>

<style>
</style>