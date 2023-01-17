
<template>
<h1>MedBrief</h1>
 <div class="container">
  <div class="row">
    <div class="col-8">
      <ReportInput />
    </div>
    <div class="col-4">
      <ChatBox />
    </div>
  </div>
</div>

</template>
<script setup>
import ReportInput from "./components/ReportInput.vue"
import ChatBox from "./components/ChatBox.vue"
</script>
<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
