<template>
  <div class="card border-0 shadow-sm rounded-3 mb-4">
    <div class="card-body p-4">
      <h5 class="card-title fw-semibold mb-3">
        <i class="bi bi-pencil-square me-2 text-warning"></i>Update Employee
      </h5>
      <hr>

      <div class="table-responsive">
        <table class="table table-hover align-middle mb-0">
          <thead class="table-light">
            <tr>
              <th>Name</th>
              <th>Designation</th>
              <th>Department</th>
              <th>Salary</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in list" :key="item.id">
              <td>{{ item.name }}</td>
              <td>{{ item.designation }}</td>
              <td>{{ item.department }}</td>
              <td>₹{{ item.salary }}</td>
              <td>
                <button class="btn btn-outline-warning btn-sm" @click="editItem(item)">
                  <i class="bi bi-pencil me-1"></i>Edit
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- Edit Form -->
      <div v-if="editData.id" class="mt-4 p-3 bg-light rounded-3">
        <h6 class="fw-semibold mb-3"><i class="bi bi-pencil me-1"></i> Editing Employee</h6>

        <div class="row">
          <div class="col-md-6 mb-3">
            <label class="form-label fw-medium">Name</label>
            <input v-model="editData.name" class="form-control">
          </div>
          <div class="col-md-6 mb-3">
            <label class="form-label fw-medium">Designation</label>
            <input v-model="editData.designation" class="form-control">
          </div>
          <div class="col-md-6 mb-3">
            <label class="form-label fw-medium">Department</label>
            <input v-model="editData.department" class="form-control">
          </div>
          <div class="col-md-6 mb-3">
            <label class="form-label fw-medium">Salary</label>
            <input type="number" v-model="editData.salary" class="form-control">
          </div>
        </div>

        <button class="btn btn-success px-4 me-2" @click="updateData">
          <i class="bi bi-check-circle me-1"></i> Update
        </button>
        <button class="btn btn-outline-secondary px-4" @click="editData = { id: null, name: '', designation: '', department: '', salary: 0 }">
          Cancel
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      API: "https://69f4bb64fb098eb7f0b4ceb0.mockapi.io/WPAssignment",
      list: [],
      editData: {
        id: null,
        name: "",
        designation: "",
        department: "",
        salary: 0
      }
    }
  },

  methods: {
    async fetchData() {
      try {
        const res = await axios.get(this.API);
        this.list = res.data;
      } catch (err) {
        console.error(err);
      }
    },

    editItem(item) {
      this.editData = { ...item };
    },

    async updateData() {
      try {
        await axios.put(`${this.API}/${this.editData.id}`, this.editData);

        this.fetchData();

        this.editData = {
          id: null,
          name: "",
          designation: "",
          department: "",
          salary: 0
        };

      } catch (err) {
        console.error(err);
      }
    }
  },

  mounted() {
    this.fetchData();
  }
}
</script>