<template>
    <div class="home-view">
      <Form></Form>
      <!-- <Chart /> -->
      <!-- <Chart></Chart> -->
    </div>
  </template>
  
  <script>
  import Form from '../components/Form/Form.vue';
//   import Chart from './Chart.vue';
  
  export default {
    name: 'HomeView',
    components: {
      Form,
    //   Chart,
    },
  };
  </script>
  
  <style scoped>
  .home-view {
    background-color: #1a202c;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: #fff;
    height: 100vh;
  }
  </style>
  