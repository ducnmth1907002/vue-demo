<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h3>Create Employee</h3>
      </div>
      <div class="card-body">
        <form v-on:submit.prevent="addItem">
          <div class="form-group">
            <label>Name:</label>
            <input type="text" class="form-control" v-model="item.name"/>
          </div>
          <div class="form-group">
            <label>Wage:</label>
            <input type="number" class="form-control" v-model="item.wage"/>
          </div>
          <div class="form-group">
            <input type="submit" class="btn btn-primary" value="Create Employee"/>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {
    name: 'AddItem'
  },
  data() {
    return {
      item: {}
    }
  },
  methods: {
    addItem() {
      let uri = 'https://demo-vue-js.herokuapp.com/employees'
      this.axios.post(uri, this.item)
          .then(() => {
            this.$router.push({ name: 'Index' })
          });
    }
  }
}
</script>