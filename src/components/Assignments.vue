<template>
  <section class="space-y-6">
    <assignment-list
      :assignments="filters.inProgress"
      title="In Progress"
    ></assignment-list>

    <assignment-list
      :assignments="filters.completed"
      title="Completed"
    ></assignment-list>

    <assignment-create @add="add"></assignment-create>
  </section>
</template>

<script>
import AssignmentList from "./AssignmentList.vue";
import AssignmentCreate from "./AssignmentCreate.vue";

export default {
  components: { AssignmentList, AssignmentCreate },
  data() {
    return {
      assignments: [
        { name: "Finish project", complete: false, id: 1, tag: 'english' },
        { name: "Read Chapter 4", complete: false, id: 2, tag: 'math' },
        { name: "Turn in Homework", complete: false, id: 3, tag: 'math'},
      ],
    };
  },
  computed: {
    filters() {
      return {
        inProgress: this.assignments.filter(
          (assignment) => !assignment.complete
        ),
        completed: this.assignments.filter((assignment) => assignment.complete),
      };
    },
  },
  methods: {
    add(name) {
      this.assignments.push({
        name: name,
        completed: false,
        id: this.assignments.length + 1,
      });
    },
  },
};
</script>
