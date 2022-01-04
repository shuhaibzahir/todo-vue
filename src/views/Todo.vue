<template>
  <v-list class="pt-0" flat>
    <v-list-item-group v-model="settings" multiple>
      <div v-for="task of tasks" :key="task.id">
        <v-list-item @click="doneTask(task.id)" :class="{'blue lighten-5':task.done}">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title :class="{'text-decoration-line-through':task.done}">{{ task.title }}</v-list-item-title>
            </v-list-item-content>
              <v-list-item-action>
          <v-btn icon  @click="deleteTask(task.id)">
            <v-icon color="red accent-3" >mdi-delete-alert</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>
        </v-list-item>
    <v-divider></v-divider>
      </div>
    </v-list-item-group>
  </v-list>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      tasks: [
        { id: 1, title: "wake up", done:false },
        { id: 2, title: "meditation", done:false },
        { id: 3, title: "read book", done:false },
        { id: 4, title: "Task creation", done:false },
        { id: 5, title: "Calender checking", done:false },
        { id: 6, title: "Start working", done:false },
      ],
    };
  },
  methods:{
      doneTask(id){
          let current = this.tasks.find(i=>i.id==id)
          current.done=!current.done
      },
      deleteTask(id){
          if(confirm('are you sure?')){
              this.tasks = this.tasks.filter(i=>i.id!==id)
          } 
      }
  }

};
</script>