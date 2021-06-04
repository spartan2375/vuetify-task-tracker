<template>
  <v-list subheader flat>
    <v-subheader>Active Tasks</v-subheader>

    <v-list-item v-for="task in tasks" v-show="!task.finished" :key="task.id">
      <template v-slot:default>
        <v-list-item-action>
          <v-checkbox
            v-model="task.finished"
            color="primary"
            
          ></v-checkbox>
        </v-list-item-action>

        <v-list-item-content>
          <v-list-item-title>{{ task.title }}</v-list-item-title>
        </v-list-item-content>
      </template>
    </v-list-item>
  </v-list>
</template>
<script>
export default {
    name: 'task-list-incomplete',
    props: ['tasks']

}
</script>