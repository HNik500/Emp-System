<template>
  <div class="card border-0 shadow-sm rounded-3 mb-4">
    <div class="card-body p-4">
      <h5 class="card-title fw-semibold mb-3">
        <i class="bi bi-list-ul me-2 text-success"></i>Employee List
      </h5>
      <hr>

      <div class="table-responsive">
        <table class="table table-hover align-middle mb-0">
          <thead class="table-light">
            <tr>
              <th>ID</th>
              <th>Name</th>
              <th>Designation</th>
              <th>Department</th>
              <th>Salary</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in list" :key="item.id">
              <td><span class="badge bg-secondary">{{ item.id }}</span></td>
              <td>{{ item.name }}</td>
              <td>{{ item.designation }}</td>
              <td>{{ item.department }}</td>
              <td>₹{{ item.salary }}</td>
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
  name: "EmployeeList",
  data() {
    return { list: [] }
  },
  mounted() {
    axios.get("https://69f4bb64fb098eb7f0b4ceb0.mockapi.io/WPAssignment")
      .then(res => this.list = res.data)
      .catch(err => console.log(err));
  }
}
</script>