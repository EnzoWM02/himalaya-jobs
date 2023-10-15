<script setup lang="ts">
import "./styles/Vars.css";
import "./styles/Reset.css";
import Navbar from "./components/navbar/Navbar.vue";
import RemoteJobs from "./components/pages/jobs/remote/RemoteJobsPage.vue";
</script>

<template>
  <div class="AppWrapper">
    <Navbar />
    <RemoteJobs />
  </div>
</template>

<style>
body {
  font-family: "Poppins", sans-serif;
}
</style>
