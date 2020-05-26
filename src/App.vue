<template>
  <div id="app">
    <Clock :radius="50" :minute="30" :hour="12" :showHourMarks="true" :showMinuteMarks="true"/>
  </div>
</template>

<script>
import Clock from "./components/Clock";

export default {
  name: "App",
  components: {
    Clock
  }
};
</script>

<style>
</style>
