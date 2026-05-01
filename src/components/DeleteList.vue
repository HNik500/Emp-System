<template>
  <div class="card border-0 shadow-sm rounded-3 mb-4">
    <div class="card-body p-4">
      <h5 class="card-title fw-semibold mb-3">
        <i class="bi bi-trash3 me-2 text-danger"></i>Delete Employee
      </h5>
      <hr>

      <div class="table-responsive">
        <table class="table table-hover align-middle mb-0">
          <thead class="table-light">
            <tr>
              <th>Name</th>
              <th>Department</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in list" :key="item.id">
              <td>{{ item.name }}</td>
              <td>{{ item.department }}</td>
              <td>
                <button class="btn btn-outline-danger btn-sm" @click="deleteItem(item.id)">
                  <i class="bi bi-trash me-1"></i>Delete
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      list: [],
      api: "https://69f4bb64fb098eb7f0b4ceb0.mockapi.io/WPAssignment"
    }
  },

  methods: {
    async fetchData() {
      const res = await axios.get(this.api);
      this.list = res.data;
    },

    async deleteItem(id) {
      await axios.delete(`${this.api}/${id}`);
      this.list = this.list.filter(item => item.id !== id);
    }
  },

  mounted() {
    this.fetchData();
  }
}
</script>