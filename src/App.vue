<template>
  <div id="app">
    <!-- <input
      :value="activeDate ? activeDate : today"
      min="2020-04-01"
      max="2022-04-30"
      step="5"
      class="mx-2 calendar-input border border-slate-300"@click="() => { caldendarModal = true; }"
    /> -->
    <CalendarMonth 
      :toggle="caldendarModal"
      :backdrop="() => { caldendarModal = false; }"
      />
  </div>
</template>

<script>
import CalendarMonth from "./components/CalendarMonth";

export default {
  name: "App",

  components: {
    CalendarMonth,
  },

  data () {
    return {
      caldendarModal: false
    }
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  font-family: sans-serif;
  font-weight: 100;
  --grey-100: #e4e9f0;
  --grey-200: #cfd7e3;
  --grey-300: #b5c0cd;
  --grey-800: #3e4e63;
  --red: #dc2626;
  --grid-gap: 1px;
  --day-label-size: 20px;
}

ol,
li {
  padding: 0;
  margin: 0;
  list-style: none;
}

.calendar-month-header {
  display: flex;
  justify-content: space-between;
  background-color: #fff;
  padding: 10px;
}

.calendar-input {
  padding-left: 25px;
  background: url('~@/assets/image.svg') no-repeat left;
  background-size: 20px;
  /* padding-left:30px; */
}
</style>
