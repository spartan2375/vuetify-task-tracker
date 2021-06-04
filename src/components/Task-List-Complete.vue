<template>
  <div class="task-list-complete">
    <v-subheader>Completed Tasks</v-subheader>
    <v-list subheader flat>
      <v-list-item v-for="task in tasks" v-show="task.finished" :key="task.id">
        <template v-slot:default>
          <v-list-item-action>
            <v-checkbox
              v-model="task.finished"
              color="primary"
            ></v-checkbox>
          </v-list-item-action>

          <v-list-item-content class="text-decoration-line-through">
            <v-list-item-title>{{ task.title }}</v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>
            <v-btn @click.stop="$emit('delete-task', task.id)" icon>
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
        </template>
      </v-list-item>
    </v-list>
  </div>
</template>

<script>
export default {
    name: 'task-list-complete',
    props: ['tasks']
}
</script>