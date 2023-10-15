<script setup lang="ts">
import RemoteJobsFilter from "./RemoteJobsFilter.vue";
import RemoteJobsCard from "./RemoteJobsCard.vue";
import { type Job } from "./RemoteJobsCard.vue";
import { ref, onBeforeMount } from "vue";

const jobsArr = ref<Job[]>([]);

onBeforeMount(async () => {
  const res = await fetch(
    "https://api.github.com/gists/913347818225313b00dfbef7cd65fc4a"
  );

  const jsonRes = await res.json();
  const jsonContent = JSON.parse(jsonRes.files["jobs-list.json"].content);

  jobsArr.value = jsonContent;
});
</script>

<template>
  <div class="headerWrapper">
    <span class="categoryTitle">Remote jobs</span>
    <span class="title">Remote jobs</span>
    <span class="subtitle">
      Find your next remote job at companies like
      <span class="subtitleMarked"> Intercom</span>,
      <span class="subtitleMarked"> Spotify</span>,
      <span class="subtitleMarked"> Square</span>, and
      <span class="subtitleMarked"> Twitter</span>.
    </span>
    <RemoteJobsFilter class="remoteJobsFilter" />
  </div>
  <div class="jobsListingWrapper">
    <div class="jobsColumns">
      <div class="jobsListing">
        <div class="jobsListingHeader">
          <span class="jobsCounter">{{ jobsArr.length }} jobs</span>
        </div>
        <div class="jobsListWrapper">
          <RemoteJobsCard v-for="job in jobsArr" :job="job" />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.headerWrapper {
  display: flex;
  flex-direction: column;
  gap: 16px;
  background: var(--background-color);
  padding-top: 50px;
}

.headerWrapper,
.jobsListingWrapper {
  padding: 0 10vw;
}

.title {
  font-size: 48px;
  font-weight: 500;
}

.categoryTitle {
  color: var(--subtitle-purple);
  font-weight: 600;
  font-size: 13px;
}

.subtitle {
  color: var(--subtitle-purple);
  font-size: 18px;
  font-weight: 500;
}

.subtitle .subtitleMarked {
  color: var(--bright-purple);
  font-weight: 600;
}

.remoteJobsFilter {
  margin-top: 26px;
  margin-bottom: 60px;
}

.jobsListingWrapper {
  margin: 55px 0;
  display: grid;
  grid-template-columns: 2fr 1fr;
}

.jobsListingHeader {
  display: flex;
  justify-content: space-between;
}

.jobsCounter {
  color: var(--subtitle-gray);
  font-weight: 500;
}

.jobsListing {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.jobsListWrapper {
  display: flex;
  flex-direction: column;
  gap: 14px;
}
</style>
