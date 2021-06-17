<template>
  <div>
    <h1>Items</h1>

    <table class="table table-hover">
      <thead>
      <tr>
        <td>ID</td>
        <td>Name</td>
        <td>Wage</td>
        <td>Actions</td>
      </tr>
      </thead>

      <tbody>
      <tr v-for="item in items" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.wage }}</td>
        <td>
          <button class="btn btn-primary" v-on:click="openModal(item.id)">Edit</button>
          <button class="btn btn-danger ml-1" v-on:click="deleteItem(item.id)">Delete</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

import Edit from "./Edit";
export default {
  data() {
    return {
      items: []
    }
  },

  created: function () {
    this.fetchItems();
  },

  methods: {
    fetchItems() {
      let uri = 'https://demo-vue-js.herokuapp.com/employees';
      this.axios.get(uri).then((response) => {
        this.items = response.data;
      });
    },
    deleteItem(id) {
      let uri = 'https://demo-vue-js.herokuapp.com/employees/' + id;

      this.axios.delete(uri).then(() => {
        this.fetchItems()
      });
    },
    openModal(id) {
      const modalWidth = window && window.innerWidth > 800 ? '750px' : '95%'
      this.$modal.show(Edit, {
        id: id
      }, {
        width: modalWidth,
        height: 'auto'
      }, {
        closed: this.fetchItems,
      })
    }
  }
}
</script>
