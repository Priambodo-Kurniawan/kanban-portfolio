<template>
  <div class="main-page container-fluid">
    <div class="row" style="margin-bottom: 20px">
      <div class="col-md-6">
        <h3><strong>Kanban Portfolio - Iam</strong></h3>
      </div>
      <div class="col-md-6">
        <button type="button" class="btn btn-info pull-right" data-toggle="modal" data-target="#myModal">New Task</button>
      </div>
    </div>
    <div class="row">
      <div class="col-md-3">
        <div class="panel panel-default">
          <div class="panel-heading brand-danger">Back-Log</div>
          <div class="panel-body">
            <TaskPanel
              v-for="task in backLogs"
              :key="task.title"
              :data="task"
              :title="task.title"
              :desc="task.description"
              :asignTo="task.asignTo"
              :point="task.point"
              @detailData="detailTaskData" />
          </div>
        </div>
      </div>
      <div class="col-md-3">
        <div class="panel panel-default">
          <div class="panel-heading brand-warning">To-Do</div>
          <div class="panel-body">
            <TaskPanel
              v-for="task in todos"
              :key="task.title"
              :data="task"
              :title="task.title"
              :desc="task.description"
              :asignTo="task.asignTo"
              :point="task.point"
              @detailData="detailTaskData" />
          </div>
        </div>
      </div>
      <div class="col-md-3">
        <div class="panel panel-default">
          <div class="panel-heading brand-primary">Doing</div>
          <div class="panel-body">
            <TaskPanel
              v-for="task in doings"
              :key="task.title"
              :data="task"
              :title="task.title"
              :desc="task.description"
              :asignTo="task.asignTo"
              :point="task.point"
              @detailData="detailTaskData" />
          </div>
        </div>
      </div>
      <div class="col-md-3">
        <div class="panel panel-default">
          <div class="panel-heading brand-success">Done</div>
          <div class="panel-body">
            <TaskPanel
              v-for="task in dones"
              :key="task.title"
              :data="task"
              :title="task.title"
              :desc="task.description"
              :asignTo="task.asignTo"
              :point="task.point"
              @detailData="detailTaskData" />
          </div>
        </div>
      </div>
    </div>
    <NewTask @submitData="createTask" />
    <DetailTask :data="detailData" @toNext="nextStatus" @toBack="backStatus" @delete="deleteTask" />
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
const dbRefObject = firebase.database().ref('kanban/tasks')

// Sync object changes


import NewTask from './NewTask'
import TaskPanel from './TaskPanel'
import DetailTask from './DetailTask'
export default {
  components: {
    NewTask,
    TaskPanel,
    DetailTask
  },
  name: 'main-page',
  data () {
    return {
      id: null,
      detail: null,
      description: null,
      asignTo: null,
      point: null,
      status: 0,
      backLogs: null,
      todos: null,
      doings: null,
      dones: null,
      detailData: null
    }
  },
  firebase: {
    tasks: null,
  },
  mounted () {
    this.$nextTick(() => {
      $('.hello').hide();
      $('.hello').fadeIn('slow');
    })
  },
  methods: {
    createTask: function(data){
      var dbRef = dbRefObject.push(data);
      var key = dbRef.key;
      data.id = key
      dbRefObject.child(key).set(data)

      console.log('task-added');
      $('.close').trigger('click')
    },
    detailTaskData: function(data){
      this.detailData = data
    },
    getData: function() {
      dbRefObject.orderByChild("status").equalTo(0).on('value', response => {
        this.backLogs = response.val()
      })
      dbRefObject.orderByChild("status").equalTo(1).on('value', response => {
        this.todos = response.val()
      })
      dbRefObject.orderByChild("status").equalTo(2).on('value', response => {
        this.doings = response.val()
      })
      dbRefObject.orderByChild("status").equalTo(3).on('value', response => {
        this.dones = response.val()
      })
    },
    nextStatus: function(status) {
      this.detailData.status = status
      dbRefObject.child(this.detailData.id).set(this.detailData)
      $('.close').trigger('click')
    },
    backStatus: function(status) {
      this.detailData.status = status
      dbRefObject.child(this.detailData.id).set(this.detailData)
      $('.close').trigger('click')
    },
    deleteTask: function(id){
      // console.log(id);
      dbRefObject.child(id).remove()
      $('.close').trigger('click')
    }
  },
  created () {
    this.getData()
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
.panel:hover {
  box-shadow: 0 1px 6px rgba(0,0,0,.2);
  border-color: #eee;
}
.panel-heading {
  font-weight: bold;
}
</style>
