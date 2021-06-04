<template>
  <div class="home pa-6">
    <v-text-field
      class="hidden-md-and-down"
      label="New Task"
      append-outer-icon="mdi-plus"
      clearable
      v-model="newTaskTitle"
      @click:append-outer="addTask"
      @keyup.enter="addTask"
    ></v-text-field>
    
    <task-list :tasks='tasks' v-on:delete-task="deleteTask"> </task-list>

    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          class="included hidden-lg-and-up"
          absolute
          fab
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
          right
        >
          <v-icon class="included">mdi-plus</v-icon>
        </v-btn>
      </template>
      <v-card
        v-click-outside="{
          handler: clickMe,
          include: include,
        }"
      >
        <v-card-title>
          <span class="headline">Add Task</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field
                  label="Task Title*"
                  v-model="newTaskTitle"
                  required
                  @keyup.enter="addTask"
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialog = false">
            Close
          </v-btn>
          <v-btn color="blue darken-1" text @click="addTask"> Add Task </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import TaskList from '@/components/Task-List.vue'

export default {
  components: { TaskList, },
  name: "Home",
  data() {
    return {
      dialog: false,
      newTaskTitle: "",
      tasks: [
        {
          id: 1,
          title: "Eat soup",
          finished: false,
        },

        {
          id: 2,
          title: "Hit the vape",
          finished: false,
        },

        {
          id: 3,
          title: "Get back to work",
          finished: false,
        },
      ],
    };
  },
  methods: {
    addTask() {
      this.dialog = false;
      console.log("add a task here");
      if (this.newTaskTitle != "") {
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          finished: false,
        };
        this.tasks.push(newTask);
        this.newTaskTitle = "";
      }
    },

    deleteTask(id) {
      console.log("id: ", id);
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },

    clickMe() {
      console.log("Click Me");
      this.dialog = false;
      this.newTaskTitle = "";
    },

    include() {
      return [document.querySelector(".included")];
    },
  },
};
</script>
