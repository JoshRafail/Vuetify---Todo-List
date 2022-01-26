<template>
  <div class="home">
    <v-text-field
      v-model="newTaskTitle"
      @click:append='addTask'
      @keyup.enter='addTask'
      outlined
      label="Append"
      append-icon="mdi-flower-poppy"
      class = "pa-3"
      color="green"
      hide-details
      clearable
    ></v-text-field>
    <v-list
      two-line
      flat
      class = "pt-0"
    >
      <div
        v-for="task in taskArray"
        :key="task.id"
      >
        <v-list-item
        @click="doneTask(task.id)"
        :class="{'green lighten-4':task.done}"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="green"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              :class="{'text-decoration-line-through' : task.done }"
              >{{task.title}}</v-list-item-title>
              <v-list-item-subtitle></v-list-item-subtitle>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn 
                @click.stop="deleteTask(task.id)"
                icon
              >
                <v-icon
                color='green'
                >mdi-bomb</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider> </v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
  export default {
    name: 'Home',
    data(){
      return{
        newTaskTitle:'',
        taskArray:[
          {
            id:1,
            title: "Get up",
            done: false
          },
          {
            id:2,
            title: "roll out of bed",
            done: false
          },
          {
            id:3,
            title: "get down with yah bad self",
            done: false
          },
        ]
      }
    },
    methods: {
      addTask(){
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false,
        }
        this.taskArray.push(newTask)
        this.newTaskTitle = ''
      },
      doneTask(id){
          let task = this.taskArray.filter(task => task.id === id)[0]
        task.done = !task.done
      },
      deleteTask(id){
        this.taskArray = this.taskArray.filter(task => task.id !== id)
      }
    }
  }
</script>
