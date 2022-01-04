<template>
       <v-list
      subheader
      two-line
      flat
    >
     

      <v-list-item-group
        v-model="settings"
        multiple
      >
        <v-list-item
        v-for="task of tasks"
        :key='task.id'
        >
          <template v-slot:default="{ active, }">
            <v-list-item-action>
              <v-checkbox
                :input-value="active"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>
              <v-list-item-content>
              <v-list-item-title>{{task.title}}</v-list-item-title>
             </v-list-item-content>
          </template>
        </v-list-item>
  
      </v-list-item-group>
    </v-list>

</template>

<script>

export default{
    name:'Todo',
    data(){
        return{
            tasks:[
                {id:1, title:'wake up'},
                {id:2, title:'meditation'},
                {id:3, title:'read book'},
                {id:4, title:'Task creation'},
                {id:5, title:'Calender checking'},
                {id:6, title:'Start working'},
            ]
        }
    }
}
</script>