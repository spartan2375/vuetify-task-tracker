<template>
  <div>
    <div class="about pa-6">
      <h1>This is an about page</h1>
      <p>
        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Consequuntur
        voluptate in quia eius unde! Numquam deleniti cupiditate vel possimus
        perferendis, natus facere eum beatae quisquam, ea, accusantium animi.
        Voluptas, aperiam.
      </p>
    </div>

    <v-row justify="center">
      <v-dialog v-model="dialog" persistent max-width="600px">
        <template v-slot:activator="{ on, attrs }">
          <v-btn color="primary" dark v-bind="attrs" v-on="on" class="included">
            <v-icon>mdi-plus</v-icon>
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
                  <v-text-field label="Email*" required></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="dialog = false">
              Close
            </v-btn>
            <v-btn color="blue darken-1" text @click="dialog = false">
              Add Task
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>

    <v-row>
      <v-spacer></v-spacer>
      <v-date-picker
      :elevation="3"
        v-model="date"
        v-show="showDatePicker"
        @input="showDatePicker = false">
        <v-spacer></v-spacer>
        <v-btn text color="primary" @click="showDatePicker = false">
          Cancel
        </v-btn>
        </v-date-picker>
      <v-btn
        class="mx-10"
        fab
        dark
        right
        color="primary"
        @click="showDatePicker = !showDatePicker"
      >
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </v-row>
  </div>
</template>

<script>
import TaskList from "../components/Task-List.vue";
export default {
  components: { TaskList },
  data() {
    return {
      TaskList,
      dialog: false,
      showDatePicker: false,
      date: "",
    };
  },

  methods: {
    clickMe() {
      console.log("Click Me");
      this.dialog = false;
    },

    include() {
      return [document.querySelector(".included")];
    },
  },
};
</script>
