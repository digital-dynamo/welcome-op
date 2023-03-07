<template>
    <div>
      <h1>{{ greeting }}</h1>
      <h2>{{ time }}</h2>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        greeting: "No time to waste!",
        time: new Date().toLocaleTimeString(),
      };
    },
    mounted() {
      setInterval(() => {
        this.time = new Date().toLocaleTimeString();
      }, 1000);
    },
  };
  </script>
  