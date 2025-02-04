<template>
  <div id="app">
    <!-- Sidebar -->
    <Sidebar />
    
    <!-- Main content -->
    <div id="main-content">
      <Sample /> <!-- Import your Sales Forecasting Tool here -->
    </div>
  </div>
</template>

<script>
import Sidebar from '@/components/Sidebar.vue';  // Import Sidebar component
import Sample from '@/views/sample.vue';  // Import SalesForecastingTool component

export default {
  components: {
    Sidebar,
    Sample,
  }
};
</script>

<style>
#app {
  display: flex;
  height: 100vh;
}

#main-content {
  margin-left: 200px;  /* Adjust this value based on the sidebar width */
  padding: 20px;
  flex-grow: 1;
}
</style>
