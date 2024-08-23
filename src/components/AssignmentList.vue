<template>
  <section v-show="assignments.length">
    <h2 class="font-bold mb-2">
      {{ title }}
      <span>({{ assignments.length }})</span>
    </h2>

    <assignment-tags
      v-model="currentTag"
      :initial-tags="assignments.map((a) => a.tag)"
    ></assignment-tags>

    <ul class="border border-gray-680 divide-y divide-gray-680 mt-6">
      <assignment
        v-for="assignment in filteredAssignments"
        :key="assignment.id"
        :assignment="assignment"
      ></assignment>
    </ul>
  </section>
</template>

<script>
import AssignmentTags from "./AssignmentTags.vue";
import Assignment from "./Assignment.vue";

export default {
  components: {
    Assignment,
    AssignmentTags,
  },
  props: {
    assignments: Array,
    title: String,
  },
  data() {
    return {
      currentTag: "all",
    };
  },
  computed: {
    filteredAssignments() {
      if (this.currentTag === "all") {
        return this.assignments;
      }
      return this.assignments.filter((a) => a.tag === this.currentTag);
    },
  },
};
</script>
