<template>
  <section class="flex gap-8">
    <assignment-list :assignments="filters.inProgress" title="In Progress">
      <assignment-create @add="add" />
    </assignment-list>

    <div v-show="showCompleted">
      <assignment-list
        :assignments="filters.completed"
        title="Completed"
        can-toggle
        @toggle="showCompleted = !showCompleted"
      ></assignment-list>
    </div>
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
        /*  { name: "Finish project", complete: false, id: 1, tag: "english" },
        { name: "Read Chapter 4", complete: false, id: 2, tag: "math" },
        { name: "Turn in Homework", complete: false, id: 3, tag: "math" }, */
      ],
      showCompleted: true,
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
  created() {
    fetch("http://localhost:8000/assignments")
      .then((response) => response.json())
      .then((assignments) => {
        this.assignments = assignments;
      });
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
