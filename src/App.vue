<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col text-center" style="font-size:50px;font-weight:bold;">
          <MultiWordClock />
        </div>
      </div>
      <div class="row">
        <div class="col text-align" style="font-size:10px;font-weight:bold;">
          <WelcomeToOpportunity msg="Welcome to Opportunity"/>
        </div>
      </div>
      <div class="row">
        <div class="col text-center" style="font-size:20px;">
          <span>{{ currentDate }}</span>
        </div>
      </div>
    </div>
  
    <div class="container">
      <ul>   
        <li>
          <event-component></event-component>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import WelcomeToOpportunity from './components/WelcomeToOpportunity.vue'
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
      events: [], // initialize events array
    };
  },
  methods: {
    updateCurrentDate() {
      let current = new Date();
      this.currentDate = `${current.getDate()}.${current.getMonth()+1}.${current.getFullYear()}`;
    },
    refreshEvents() {
      // fetch events from server and update events array
      fetch('/api/events')
        .then(response => response.json())
        .then(data => {
          this.events = data;
        })
        .catch(error => console.error(error));
    },
  },
  mounted() {
    this.updateCurrentDate();
    setInterval(this.updateCurrentDate, 60000);
    this.refreshEvents(); // initial fetch of events
    setInterval(this.refreshEvents, 300000); // refresh events every 5 minutes
  },
};
</script>

<!--some styliiin baab-->
<style>
#app {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-sizing: border-box;
  padding-top: 20px;
  padding-bottom: 50px;
  min-height: 100vh;
}
.container {
  max-width: 95%;
  margin: 0 auto;
}
.row {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.col {
  flex-basis: 100%;
  text-align: center;
  margin-bottom: 20px;
}
@media (min-width: 768px) {
  .col {
    flex-basis: 50%;
    margin-bottom: 0;
  }
}
@media (min-width: 992px) {
  .col {
    flex-basis: 33.33%;
  }
}
.text-center {
  text-align: center;
}
h1 {
  font-size: 3rem;
  margin-bottom: 30px;
}
h2 {
  font-size: 2rem;
  margin-bottom: 20px;
}
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
li {
  margin-bottom: 20px;
  font-size: 1.5rem;
}
</style>
