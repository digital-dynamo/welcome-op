<div class="container">
    <div class="row">
      <div class="col-sm-12 bg-info m-3"></div>
      <div class="col-sm-12 bg-info m-3"></div>
      <div class="col-sm-12 bg-info m-3"></div>
    </div>
  </div>
  

'WelcomeToOpportunity'



<script>
/* WelcomeOpportunity.vue ln 28 -32 das
  data() {
    return {
      events: [],
    }
  } */


  export default {
    name: "app",
    data(){
      return {
};
    },
    methods: {

getDate(){
    
  },
  updateCurrentDate() {

  let current = new Date();
  this.currentDate = `${current.getDate()}.${current.getMonth()+1}.${current.getFullYear()}`;

  },

  refreshData() {
    this.updateCurrentDate();
    this.getDate();
  },
},
mounted() {
  this.refreshData();
  setInterval(this.refreshData,1800000)
},

};

</script>


<script>
/*   CEventcomponent without  Intrerval */
import axios from 'axios';
import { Script } from 'vm';

export default {
  data() {
    return {
      events: [],
    };
  },
  mounted() {
    axios
      .get(
        'https://docs.google.com/spreadsheets/d/e/2PACX-1vQAtedpdobvMaK5tGM2fUqJON-l2Btu5bL6vLxkXCgGWYjZzLaUsAEDZfvEH9PNEWJ2WI-2BKb-M4jC/pub?output=csv'
      )
      .then((response) => {
        const data = response.data.trim().split('\n').slice(1).map((line) => {
          const [eventDate, eventTitle, eventInfo] = line.split(',');
          return { eventDate, eventTitle, eventInfo };
        });
        this.events = data;
      })
      .catch((error) => {
        console.error(error);
      });
  },
};
</script>