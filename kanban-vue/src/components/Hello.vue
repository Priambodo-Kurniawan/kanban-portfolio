<template>
  <div class="hello">
    <div>
      <div class="col-md-12">
        <button type="button" class="btn btn-info pull-right" data-toggle="modal" data-target="#myModal">New Task</button>
      </div>
    </div>
    <div class="">
      <div class="col-md-3">
        <div class="panel panel-default">
          <div class="panel-heading">Back-Log</div>
          <div class="panel-body">
            <TaskPanel />
          </div>
        </div>
      </div>
    </div>
    <NewTask @submitData="createTask"></NewTask>
  </div>
</template>

<script>
var config = {
  apiKey: "AIzaSyDZX_qPJUCxqY3Qp7kygynERDkFgI0ephE",
  authDomain: "fir-project-4bcfc.firebaseapp.com",
  databaseURL: "https://fir-project-4bcfc.firebaseio.com",
  projectId: "fir-project-4bcfc",
  storageBucket: "fir-project-4bcfc.appspot.com",
  messagingSenderId: "670786535968"
};
firebase.initializeApp(config);

// Create references
const dbRefObject = firebase.database().ref('kanban')

// Sync object changes
dbRefObject.on('value', response => {
  console.log(response.val());
})

import NewTask from './NewTask'
import TaskPanel from './TaskPanel'
export default {
  components: {
    NewTask,
    TaskPanel
  },
  firebase: {
    task: dbRefObject
  },
  name: 'hello',
  data () {
    return {
      detail: null,
      description: null,
      asignTo: null,
      point: null,
      status: 0
    }
  },
  mounted() {
    this.$nextTick(() => {
      $('.hello').hide();
      $('.hello').fadeIn('slow');
    })
  },
  methods: {
    createTask: function(data){
      // Listen data
      var listenData = firebase.database().ref('kanban/task').push(data)
      console.log('task-added');
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
