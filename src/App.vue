<template>
  <div id="app">
    <Clock
      :radius="50"
      :minute="minute"
      :hour="hour"
      :showHourMarks="showHourMarks"
      :showMinuteMarks="showMinuteMarks"
    />
    <p>{{ hour + ":" + minute}}</p>
    <input type="number" v-model.number="hour" min="1" max="12">
    <input type="number" v-model.number="minute">
    <label for="showHourMarks">
      <input id="showHourMarks" type="checkbox" v-model="showHourMarks">
      Show hour marks
    </label>
    <label for="showMinuteMarks">
      <input id="showMinuteMarks" type="checkbox" v-model="showMinuteMarks">
      Show minute marks
    </label>
  </div>
</template>

<script>
import Clock from "./components/Clock";

export default {
  name: "App",
  components: {
    Clock
  },
  data() {
    return { hour: 12, minute: 0, showHourMarks: true, showMinuteMarks: true };
  }
};
</script>

<style>
</style>
