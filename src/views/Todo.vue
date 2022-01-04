<template>
    <div class="pa-3"> 
    <v-text-field
    class="pa-3"
            outlined
             append-icon="mdi-plus-circle"
            hide-details
            clearable
            @keypress.enter="addTask"
            @click:append="addTask"
            v-model="newTask"
          >
          </v-text-field>
   <v-list class="pt-0" flat>
    
    <v-list-item-group >
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
          <v-btn icon  @click.stop="deleteTask(task.id)">
            <v-icon color="red accent-3" >mdi-delete-alert</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>
        </v-list-item>
    <v-divider></v-divider>
      </div>
    </v-list-item-group>
  </v-list>
    </div>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      newTask:'',
      tasks: [  ],
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
            // localStorage.setItem('taskList',JSON.stringify(this.tasks))

              
          } 
      },
      addTask(){
          this.tasks.push({id:Date.now(), title:this.newTask, done:false})
        //   localStorage.setItem('taskList',JSON.stringify(this.tasks))
        this.newTask=''
      }
  },
  mounted(){
      let getItem = localStorage.getItem("taskList")
      this.tasks = getItem?JSON.parse(getItem):[]

  },
  updated(){
    localStorage.setItem('taskList',JSON.stringify(this.tasks))
  }

};
</script>