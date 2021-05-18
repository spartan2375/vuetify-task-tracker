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

    <v-list subheader flat>
      <v-subheader>Active Tasks</v-subheader>

      <v-list-item v-for="task in tasks" v-show="!task.finished" :key="task.id">
        <template v-slot:default>
          <v-list-item-action>
            <v-checkbox
              :input-value="task.finished"
              color="primary"
              @click="task.finished = !task.finished"
            ></v-checkbox>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title>{{ task.title }}</v-list-item-title>
          </v-list-item-content>
        </template>
      </v-list-item>

      <v-subheader>Completed Tasks</v-subheader>

      <v-list-item v-for="task in tasks" v-show="task.finished" :key="task.id">
        <template v-slot:default>
          <v-list-item-action>
            <v-checkbox
              :input-value="task.finished"
              color="primary"
              @click="task.finished = !task.finished"
            ></v-checkbox>
          </v-list-item-action>

          <v-list-item-content class="text-decoration-line-through">
            <v-list-item-title>{{ task.title }}</v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>
            <v-btn @click.stop="deleteTask(task.id)" icon>
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
        </template>
      </v-list-item>
    </v-list>

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
export default {
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
