<template>
  <div class="container-fluid" id="app">

    <img alt="Taylor & Pond logo" src="./assets/logo.png">

    <HelloWorld msg="Super dank ticket app"/>

    <div class="input-group input-group-lg">
      <input class="form-control" v-model="title" type="text" placeholder="Enter a task title"/>
      <textarea class="form-control" v-model="desc" placeholder="Enter a task description"></textarea>
      <button class="btn btn-lg btn-success" v-on:click="addTask">Add Task</button>
    </div>

    <!-- <div class="row input-group input-group-lg">
      <select @change="filterTasks" class="col-4 offset-4 form-control">
        <option value="1">All</option>
        <option value="2">Pending</option>
        <option value="3">Active</option>
        <option value="4">Complete</option>
      </select>
    </div> -->

    <draggable class="row" v-model="tasks" @start="drag=true" @end="drag=false">
      <div class="col-3" v-for="task in tasks" :key="task.id">
        <TaskCard class="m-3"
          v-bind:taskName="task.title"
          v-bind:taskDetails="task.desc"
          v-bind:status="task.status"
          v-bind:id="task.id"
          v-bind:rmTask="rmTask"
        />
      </div>
    </draggable>

  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TaskCard from './components/TaskCard.vue'
import draggable from 'vuedraggable'

export default {
  name: 'app',
  components: {
    HelloWorld,
    TaskCard,
    draggable
  },
  data: function() {
    return {
      title: '',
      desc: '',
      tasks: []
    }
  },
  methods: {
    addTask: function() {
      var timeStamp = new Date().getTime()
      this.tasks.push({ title: this.title, desc: this.desc, id: timeStamp});
      this.title = '';
      this.desc = '';
    },
    rmTask: function(id) {
      this.tasks.splice(findWithAttr(this.tasks, "id", id),1);
    }
  }
}

function findWithAttr(array, attr, value) {
    for(var i = 0; i < array.length; i += 1) {
        if(array[i][attr] === value) {
            return i;
        }
    }
    return -1;
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
