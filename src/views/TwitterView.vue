<template>
     <!-- <div>
        <span>Twubric Score	:</span>
        <input type="number" v-model.number="minTotal" />
      </div> -->
      <div class="Date">
    <div class="start-date">
      <span>Start Date</span> 
      <VueDatePicker v-model="startDate"  />
      <span class="gap"></span>
      <span>Endt Date</span>
      <VueDatePicker v-model="endDate" />
    </div>

     
      </div>
    <div class="container">
    <div v-for="(item,index) in filteredData " :key="index"  class="box">
      <div  class="row">
        <div class="cell top-left">{{ item.fullname }}</div>
        <div class="cell top-right">{{ item.twubric.total }}</div>
      </div>
      <div class="divider"></div>
      <div class="row">
        <div class="cell">{{ item.twubric.friends }}</div>
        <div class="cell">{{ item.twubric.influence }}</div>
        <div class="cell">{{ item.twubric.chirpiness }}</div>
      </div>
      <div class="row">
        <div class="cell">friends</div>
        <div class="cell">influence</div>
        <div class="cell">chirpriness</div>
      </div>
      <div class="divider"></div>
      <div class="row">
        <div class="cell bottom-left">{{ formatDate(item.join_date) }}</div>
        <button class="cell bottom-right">Remove</button>
      </div>
      <div class="divider"></div>
    </div>
</div>
  </template>
  
  <script setup>
  import {ref,computed} from 'vue'
  import moment from 'moment'
  import VueDatePicker from 'vue3-datepicker'

  const data = ref([
  {
    "uid": 1,
    "username": "sampleuser1",
    "image": "https://randomuser.me/api/portraits/men/1.jpg",
    "fullname": "Sample User One",
    "twubric": {
      "total": 3.5,
      "friends": 1,
      "influence": 1,
      "chirpiness": 1.5
    },
    "join_date": 1358899200
  },
  {
    "uid": 2,
    "username": "sampleuser2",
    "image": "https://randomuser.me/api/portraits/women/2.jpg",
    "fullname": "Sample User Two",
    "twubric": {
      "total": 5,
      "friends": 1,
      "influence": 1,
      "chirpiness": 1.5
    },
    "join_date": 1355270400
  },
  {
    "uid": 3,
    "username": "sampleuser3",
    "image": "https://randomuser.me/api/portraits/women/3.jpg",
    "fullname": "Sample User Three",
    "twubric": {
      "total": 7,
      "friends": 1,
      "influence": 1,
      "chirpiness": 1.5
    },
    "join_date": 1289433600
  },
  {
    "uid": 4,
    "username": "sampleuser4",
    "image": "https://randomuser.me/api/portraits/men/4.jpg",
    "fullname": "Sample User Four",
    "twubric": {
      "total": 9,
      "friends": 2,
      "influence": 3,
      "chirpiness": 4
    },
    "join_date": 1300838400
  },
  {
    "uid": 5,
    "username": "sampleuser5",
    "image": "https://randomuser.me/api/portraits/men/5.jpg",
    "fullname": "Sample User Five",
    "twubric": {
      "total": 9,
      "friends": 1,
      "influence": 4,
      "chirpiness": 4
    },
    "join_date": 1230768000
  },
  {
    "uid": 6,
    "username": "sampleuser6",
    "image": "https://randomuser.me/api/portraits/men/6.jpg",
    "fullname": "Sample User Six",
    "twubric": {
      "total": 6,
      "friends": 2,
      "influence": 3,
      "chirpiness": 1
    },
    "join_date": 1252454400
  },
  {
    "uid": 7,
    "username": "sampleuser7",
    "image": "https://randomuser.me/api/portraits/women/7.jpg",
    "fullname": "Sample User Seven",
    "twubric": {
      "total": 8,
      "friends": 2,
      "influence": 4,
      "chirpiness": 2
    },
    "join_date": 1278201600
  },
  {
    "uid": 8,
    "username": "sampleuser8",
    "image": "https://randomuser.me/api/portraits/women/8.jpg",
    "fullname": "Sample User Eight",
    "twubric": {
      "total": 7,
      "friends": 2,
      "influence": 3,
      "chirpiness": 2
    },
    "join_date": 1331510400
  },
  {
    "uid": 9,
    "username": "sampleuser9",
    "image": "https://randomuser.me/api/portraits/men/9.jpg",
    "fullname": "Sample User Nine",
    "twubric": {
      "total": 8,
      "friends": 1,
      "influence": 4,
      "chirpiness": 3
    },
    "join_date": 1367971200
  },
  {
    "uid": 10,
    "username": "sampleuser10",
    "image": "https://randomuser.me/api/portraits/men/10.jpg",
    "fullname": "Sample User Ten",
    "twubric": {
      "total": 5,
      "friends": 1,
      "influence": 1,
      "chirpiness": 3
    },
    "join_date": 1228953600
  }
])

const startDate = ref('')
const endDate = ref('')

const formatDate = (date) => {
  return moment(date * 1000).format('MMM D, YYYY')
}

// Define a computed property to filter data based on start and end date
const filteredData = computed(() => {
  const startTimestamp = startDate.value ? moment(startDate.value).startOf('day').unix() : 0
  const endTimestamp = endDate.value ? moment(endDate.value).endOf('day').unix() : moment().endOf('day').unix()
  return data.value.filter(item => {
    const itemTimestamp = moment(item.join_date * 1000).unix()
    return itemTimestamp >= startTimestamp && itemTimestamp <= endTimestamp
  })
})





  </script>
  
  <style scoped>
 .Date {
  border: 1px solid #000;
  border-radius: 5px;
  padding: 20px;
}

.start-date {
  display: flex;
  align-items: center;
}



.gap {
  margin-right: 450px; 
}

  .container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 10px;
}
  .box {
    border: 1px solid #000;
    max-width: 400px;
  }
  
  .row {
    display: flex;
  }
  
  .cell {
    flex: 1;
    padding: 5px;
    text-align: center;
  }
  
  .top-left,
  .top-right,
  .bottom-left,
  /* .bottom-right {
    border: none;
  } */
  
  .top-center,
  .bottom-center {
    border-left: 1px solid #000;
    border-right: 1px solid #000;
  }
  
  .divider {
    border-bottom: 1px solid #000;
  }
  </style>
  