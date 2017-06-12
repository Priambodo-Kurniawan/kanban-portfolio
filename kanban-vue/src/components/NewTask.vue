<template>
<div class="new-task">
  <div id="myModal" class="modal fade" role="dialog">
    <div class="modal-dialog">

      <!-- Modal content-->
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal">&times;</button>
          <h4 class="modal-title">Modal Header</h4>
        </div>
        <div class="modal-body">
          <form>
            <div class="form-group">
              <label for="title">Title</label>
              <input type="text" class="form-control" id="title" ref="title">
            </div>
            <div class="form-group">
              <label for="description">Description</label>
              <input type="text" class="form-control" id="description" ref="description">
            </div>
            <div class="form-group">
              <label for="point">Point</label>
              <input type="number" class="form-control" id="point" ref="point">
            </div>
            <div class="form-group">
              <label for="asign-to">Asign To</label>
              <input type="text" class="form-control" id="asign-to" ref="asignTo">
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-default" @click="submitData(newTask)">Create</button>
          <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        </div>
      </div>

    </div>
  </div>
</div>
</template>

<script>

export default {
  name: 'new-task',
  data() {
    return {
      newTask: {
        title: '',
        description: '',
        point: 0,
        asignTo: ''
      }
    }
  },
  methods: {
    submitData(name){
      this.newTask.title = this.$refs.title.value
      this.newTask.description = this.$refs.description.value
      this.newTask.point = this.$refs.point.value
      this.newTask.asignTo = this.$refs.asignTo.value

      console.log(this.newTask);

      this.$emit('submitData', this.newTask)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
