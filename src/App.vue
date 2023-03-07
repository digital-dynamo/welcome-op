<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col text-center" style="font-size:50px;font-weight:bold;">
          <MultiWordClock />
        </div>
      </div>
    </div>
  
    <div class="container">
      <ul>   
        <li>
          <span class=""><WelcomeToOpportunity msg="Welcome to Opportunity"/></span>
        </li>
      </ul>
      <event-component></event-component>
    </div>
  </div>
</template>

<script>
import WelcomeToOpportunity from './components//WelcomeToOpportunity.vue'
import MultiWordClock from './components/MultiWordClock.vue'
import EventComponent from './components/EventComponent.vue';

export default {
  name: 'App',
  components: {
    WelcomeToOpportunity,
    MultiWordClock,
    EventComponent,
  },
  data() {
    return {
      currentDate: '',
    };
  },
  methods: {
    updateCurrentDate() {
      let current = new Date();
      this.currentDate = `${current.getDate()}.${current.getMonth()+1}.${current.getFullYear()}`;
    },
    refreshData() {
      this.updateCurrentDate();
    },
  },
  mounted() {
    this.refreshData();
    setInterval(this.refreshData, 1800000);
  },
};
</script>

<style>
/* Add your styles here */
</style>


<style>
#app {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  /* font-family: 'Inter', sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
body {
 
  margin-bottom:25vh;
}
/* .infoBoxBs {
  background-color: #0F05A0;
  padding-left:25px;
} */
footer {
  background-color:white;
  padding: 20px;
  position:fixed;
  bottom: 0;
  z-index: 1;
}
.footer-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 100%;
  margin: 0 auto;
}
.footer-item {
  flex-basis: calc(33.33% - 10px);
  text-align: center;
}
.footer-item img {
  max-width: 100%;
 
}
ul {
  list-style: none;
}
</style>