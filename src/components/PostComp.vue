<template>
  <div class="card border-0 shadow-sm rounded-3 mb-4">
    <div class="card-body p-4">
      <h5 class="card-title fw-semibold mb-3">
        <i class="bi bi-person-plus-fill me-2 text-primary"></i>Add Employee
      </h5>
      <hr>

      <form @submit="postData">
        <div class="row">
          <div class="col-md-6 mb-3">
            <label class="form-label fw-medium">Name</label>
            <input v-model="emp.name" class="form-control" placeholder="Enter name" required>
          </div>
          <div class="col-md-6 mb-3">
            <label class="form-label fw-medium">Designation</label>
            <input v-model="emp.designation" class="form-control" placeholder="Enter designation" required>
          </div>
          <div class="col-md-6 mb-3">
            <label class="form-label fw-medium">Department</label>
            <input v-model="emp.department" class="form-control" placeholder="Enter department" required>
          </div>
          <div class="col-md-6 mb-3">
            <label class="form-label fw-medium">Salary</label>
            <input type="number" v-model="emp.salary" class="form-control" placeholder="Enter salary" required>
          </div>
        </div>

        <button type="submit" class="btn btn-primary px-4">
          <i class="bi bi-plus-circle me-1"></i> Add Employee
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "PostComp",
  data() {
    return {
      emp: {
        name: "",
        designation: "",
        department: "",
        salary: 0
      }
    }
  },
  methods: {
    postData(e) {
      e.preventDefault();

      axios.post("https://69f4bb64fb098eb7f0b4ceb0.mockapi.io/WPAssignment", this.emp)
        .then(() => {
          alert("Employee added successfully!");
          this.emp = { name: "", designation: "", department: "", salary: 0 };
          this.$emit('employee-added');
        })
        .catch(err => {
          alert("Error adding employee!");
          console.log(err);
        });
    }
  }
}
</script>