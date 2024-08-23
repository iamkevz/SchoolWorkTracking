<template>
  <Panel v-show="assignments.length" class="w-68 ">
    <div class="flex justify-between items-start">
        <h2 class="font-bold mb-2">
      {{ title }}
      <span>({{ assignments.length }})</span>
    </h2>

    <button v-show="canToggle" @click="$emit('toggle')">&times;</button>
    </div>
    

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

    <slot></slot>

    <template #footer>
        my footer goes here
    </template>
  </Panel>
</template>

<script>
import AssignmentTags from "./AssignmentTags.vue";
import Assignment from "./Assignment.vue";
import AssignmentCreate from "./AssignmentCreate.vue";
import Panel from "./Panel.vue";

export default {
  components: {
    Assignment,
    AssignmentTags,
    AssignmentCreate,
    Panel
  },
  props: {
    assignments: Array,
    title: String,
    canToggle: {type: Boolean, default:false}
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
