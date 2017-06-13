<template>
<div class="task-panel">
  <div class="panel panel-default">
    <div class="panel-heading"><strong>{{title}}</strong></div>
    <div class="panel-body">
      <p>Point: {{point}}</p>
      <p>Asign to: {{asignTo}}</p>
      <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#detailModal" @click="getTaskDetail(data)">Show Detail</button>
    </div>
  </div>
</div>
</template>

<script>

export default {
  props: ['title', 'desc', 'asignTo', 'point', 'data'],
  name: 'task-panel',
  data() {
    return {
    }
  },
  methods: {
    getTaskDetail(data){
      this.$emit('detailData', data)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .panel:hover {
    box-shadow: 0 1px 6px rgba(0,0,0,.2);
    border-color: #eee;
  }
</style>
