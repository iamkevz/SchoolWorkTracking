<template>
  <form @submit.prevent="add">
    <div class="border border-gray-680 text-black">
      <input
        v-model="newAssignment"
        placeholder="New assignment..."
        class="p-2"
      />
      <button type="submit" class="bg-white p-2 border-l">Add</button>
    </div>
  </form>
</template>

<script>
export default {
    props: {
        assignments: Array
    },
  data() {
    return {
      newAssignment: "",
    };
  },
  methods: {
    add() {
      this.assignments.push({
        name: this.newAssignment,
        completed: false,
        id: this.assignments.length + 1,
      });

      this.newAssignment = "";
    },
  },
};
</script>
