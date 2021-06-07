<template>
  <v-list subheader flat>
    <v-subheader>{{ subtitle }}</v-subheader>

    <v-list-item
      v-for="task in tasks"
      v-show="task.finished == isActive"
      :key="task.id"
    >
      <template v-slot:default>
        <v-list-item-action>
          <v-checkbox v-model="task.finished" color="primary"></v-checkbox>
        </v-list-item-action>

        <v-list-item-content
          :class="{ 'text-decoration-line-through': isActive }"
        >
          <v-list-item-title
            :class="{
              'font-weight-bold red--text': (dueDate(task)).includes('day'),
              'orange--text': (dueDate(task)).includes('week'),
              'grey--text text--darken-2': (dueDate(task)).includes('Past'),
              'blue--text': (dueDate(task)).includes('in ')
            }"
            >{{ task.title }}</v-list-item-title
          >
          <v-list-item-subtitle>
            Due: {{ dueDate(task) }}
          </v-list-item-subtitle>
        </v-list-item-content>

        <v-list-item-action v-show="isActive">
          <v-btn @click.stop="$emit('delete-task', task.id)" icon>
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
        <v-list-item-action v-show="!isActive">
          <v-btn @click.stop="$emit('edit-task', task.id)" icon>
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </v-list-item-action>
      </template>
    </v-list-item>
  </v-list>
</template>

<script>
export default {
  name: "task-list",
  props: {
    tasks: Array,
    isActive: Boolean,
    subtitle: String,
  },

  data() {
    return {
      taskPriority: String,
    };
  },

  methods: {
    dueDate(task) {
      let todayString = new Date().toISOString().substr(0, 10);
      if (task.due === todayString) {
        // this.taskPriority = 'day'
        return 'Today!';
      }

      let dateOfDue = task.due.split("-");
      let dueYear = parseInt(dateOfDue[0]);
      let dueMonth = parseInt(dateOfDue[1]);
      let dueDay = parseInt(dateOfDue[2]);
      let today = [
        parseInt(todayString.split("-")[0]),
        parseInt(todayString.split("-")[1]),
        parseInt(todayString.split("-")[2]),
      ];

      if (
        (today[2] > dueDay && today[1] >= dueMonth && today[0] >= dueYear) ||
        (today[1] > dueMonth && today[0] >= dueYear) ||
        today[0] > dueYear
      ) {
        this.taskPriority = 'past'
        return 'Past due!!!';
      } 
      else {
        var months = ["January","February","March","April","May","June","July","August","September","October","November","December",];
        if (dueYear > today[0]) {
          // this.taskPriority = 'year'
          return 'in ' + dueYear.toString();
        } 
        else if (dueMonth > today[1]) {
          // this.taskPriority = 'month'
          return 'in ' + months[dueMonth - 1] + ", " + dueDay;
        } 
        else {
          if (dueDay - today[2] > 6) {
            // this.taskPriority = 'week'
            return (
              months[dueMonth - 1].toString() +
              ", " +
              dueDay.toString() +
              ": " +
              Math.floor((dueDay - today[2]) / 7).toString() +
              " weeks"
            );
          } 
          else {
            // this.taskPriority = 'day'
            return (
              months[dueMonth - 1].toString() +
              ", " +
              dueDay.toString() +
              ": " +
              (dueDay - today[2]).toString() +
              " days"
            );
          }
        }
      }
    },

    deleteTask(id) {
      console.log("id: ", id);
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
  },
};
</script>