<template>
  <div class="grid gap-6 ">
    <Assignments></Assignments>

  </div>
</template>

<script>
import Assignments from "./components/Assignments.vue";
import Panel from "./components/Panel.vue";
export default {
  components: {
    Assignments,
    Panel,
  },
};
</script>
