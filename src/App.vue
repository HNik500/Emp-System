<template>
  <div>
    <!-- Header -->
    <nav class="navbar bg-dark shadow-sm">
      <div class="container">
        <span class="navbar-brand text-white fw-bold">
          <i class="bi bi-people-fill me-2"></i>Employee Management System
        </span>
      </div>
    </nav>

    <!-- Main Content -->
    <div class="container py-5">
      <PostComp @employee-added="refreshData" />
      <EmployeeList :key="refreshKey" />
      <UpdateList :key="refreshKey" />
      <DeleteList :key="refreshKey" />
    </div>
  </div>
</template>

<script>
import PostComp from './components/PostComp.vue';
import EmployeeList from './components/EmployeeList.vue';
import UpdateList from './components/UpdateList.vue';
import DeleteList from './components/DeleteList.vue';

export default {
  components: {
    PostComp,
    EmployeeList,
    UpdateList,
    DeleteList
  },
  data() {
    return {
      refreshKey: 0
    }
  },
  methods: {
    refreshData() {
      this.refreshKey++;
    }
  }
}
</script>