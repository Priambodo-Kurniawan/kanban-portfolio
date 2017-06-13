<template>
<div class="detail-task" v-if="data != null">
  <div id="detailModal" class="modal fade" role="dialog">
    <div class="modal-dialog">

      <!-- Modal content-->
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal">&times;</button>
          <h4 class="modal-title">{{data.title}}</h4>
        </div>
        <div class="modal-body">
          <h5><strong>Task Description</strong></h5>
          <p>{{data.description}}</p>
          <br>
          <h5><strong>Point</strong></h5>
          <p>{{data.point}}</p>
          <br>
          <h5><strong>Status</strong></h5>
          <p>{{dataStatus(data.status)}}</p><br>
        </div>
        <div class="modal-footer">
          <button v-if= "data.status > 0" type="button" class="btn btn-default btn-warning" @click="backTask(data.status)">Back</button>
          <button type="button" class="btn btn-default btn-danger pull-center" @click="deleteTask(data.id)">Delete</button>
          <button v-if= "data.status < 3" type="button" class="btn btn-default pull-right btn-success" @click="nextTask(data.status)" >Next</button>
        </div>
      </div>

    </div>
  </div>
</div>
</template>

<script>

export default {
  props: ['data'],
  name: 'detail-task',
  data() {
    return {
      newTask: {
        title: '',
        description: '',
        point: 0,
        asignTo: '',
        status: 0
      }
    }
  },
  methods: {
    submitData(name){
      this.newTask.title = this.$refs.title.value
      this.newTask.description = this.$refs.description.value
      this.newTask.point = this.$refs.point.value
      this.newTask.asignTo = this.$refs.asignTo.value

      this.$emit('submitData', this.newTask)
    },
    dataStatus(data) {
      if(data !== null){
        switch (data) {
          case 0:
            return data = "Back Log"
          break;
          case 1:
            return data = "To-Do"
          break;
          case 2:
            return data = "Doing"
          break;
          default:
            return data = "Done"
        }
      }
    },
    nextTask(status) {
      this.$emit('toNext', status += 1)
    },
    backTask(status) {
      this.$emit('toBack', status -= 1)
    },
    deleteTask(id) {
      this.$emit('delete', id)
    }
  },
  created () {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .modal-footer{
    text-align: left;
  }
  .pull-center {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
  }
</style>
