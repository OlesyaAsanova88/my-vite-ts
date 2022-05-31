<script setup lang="ts">
import  TimerNew from "../components/TimerNew.vue";
import { ref, onMounted, onUnmounted } from "vue";


const newYears = '1 Jan 2022';
const RemainingDays = ref('');
const RemainingHours = ref('');
const RemainingMinutes = ref('');
const RemainingSeconds = ref('');


function countDown() {

   const newYearsDate: Date = new Date(newYears);
   const currentDate: Date = new Date();

   const totalSeconds = (newYearsDate.getTime() - currentDate.getTime()) / 1000;

   const days = Math.floor(totalSeconds / 3600 /24);
   const hours = Math.floor(totalSeconds / 3600) % 24;
   const mins = Math.floor(totalSeconds / 60) % 60;
   const seconds = Math.floor(totalSeconds) % 60;

   RemainingDays.value = setTime(days);
   RemainingHours.value = setTime(hours);
   RemainingMinutes.value = setTime(mins);
   RemainingSeconds.value = setTime(seconds);

}

   function setTime(value: number) {
      return value >= 10 ? value.toString() : `0${value}`
   }


let timeInterval : ReturnType<typeof setInterval>
onMounted(()=> {
   timeInterval = setInterval(countDown, 1000)
})

onUnmounted(()=> {
   clearInterval(timeInterval)
})

 
</script>

<template>
  <div class="container">
     <div class="title">
        New Year Count Down
     </div>
     <div class="timer">
        <TimerNew :count="RemainingDays" label="Days" />
        <TimerNew :count="RemainingHours" label="Hours" />
        <TimerNew :count="RemainingMinutes" label="Minutes" />
        <TimerNew :count="RemainingSeconds" label="Seconds" />
     </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,700;1,400&display=swap');

   body {
      margin: 0;
      font-family: 'Roboto', sans-serif;
   }

   .container {
      height: 100vh;
      background-image: url('public/bg-timer.jpg');
      background-repeat: no-repeat;
      background-size: cover;
      background-position: center center;
      text-align: center;
      color: #2c4a64;
   }
   .title {
      font-size: 5rem;
      font-weight: bold; 
   }

   .timer {
      display: flex;
      align-items: center;
      justify-content: space-around;
   }

</style>
