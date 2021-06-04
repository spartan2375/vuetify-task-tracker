<template>
  <div class="Task-List-Component">
    <task-list-incomplete :tasks="tasks"></task-list-incomplete>
    <task-list-complete
      :tasks="tasks"
      v-on="$listeners"
    ></task-list-complete>
  </div>
</template>

<script>
import TaskListIncomplete from "./Task-List-Incomplete.vue";
import TaskListComplete from "./Task-List-Complete.vue";

export default {
  components: { TaskListIncomplete, TaskListComplete },
  name: "task-list",
  props: ['tasks'],
  // data: function () {
  //   return {
  //     tasks: [
  //       {
  //         id: 1,
  //         title: "Eat soup",
  //         finished: false,
  //       },

  //       {
  //         id: 2,
  //         title: "Hit the vape",
  //         finished: false,
  //       },

  //       {
  //         id: 3,
  //         title: "Get back to work",
  //         finished: false,
  //       },
  //     ],
  //   };
  // },

  methods: {
    deleteTask(id) {
      console.log("id: ", id);
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>