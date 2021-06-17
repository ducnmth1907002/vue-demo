<template>
  <div class="container p-4">
    <div class="card">
      <div class="card-header">
        <h3>Update Employee</h3>
      </div>
      <div class="card-body">
        <form v-on:submit.prevent="updateItem">
          <div class="form-group">
            <label>Name:</label>
            <input type="text" class="form-control" v-model="item.name"/>
          </div>
          <div class="form-group">
            <label>Wage:</label>
            <input type="number" class="form-control" v-model="item.wage"/>
          </div>
          <div class="form-group">
            <input type="submit" class="btn btn-primary" value="Update Employee"/>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    id: Number
  },
  data() {
    return {
      item: {}
    }
  },

  created: function () {
    this.getItem();
  },

  methods: {
    getItem() {
      let uri = 'https://demo-vue-js.herokuapp.com/employees/' + this.id;
      this.axios.get(uri).then((response) => {
        this.item = response.data;
      });
    },

    updateItem() {
      let uri = 'https://demo-vue-js.herokuapp.com/employees/' + this.id;
      this.axios.put(uri, this.item).then(() => {
        this.$emit('close')
      });
    }
  }
}
</script>
