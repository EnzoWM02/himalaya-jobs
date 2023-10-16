<script setup lang="ts">
import RemoteJobsFilter from "@/components/pages/jobs/remote/RemoteJobsFilter.vue";
import RemoteJobsCard from "@/components/pages/jobs/remote/RemoteJobsCard.vue";
import { ref, onBeforeMount } from "vue";
import Icon from "@/components/ui/Icon.vue";
import Tag from "@/components/ui/Tag.vue";

export interface Job {
  jobTitleText: string;
  companyName: string;
  companyLogoUrl: string;
  locationName: string;
  annualWage: number;
  rating: number;
  payPeriod: string;
  payCurrency: string;
}

const jobsArr = ref<Job[]>([]);
const alertFunc = (msg: string) => {
  alert(msg);
};

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
    <div class="jobsSidebar">
      <form class="weeklyNewsletter">
        <div class="feedIconContainer">
          <Icon icon="feed" />
        </div>
        <span class="newsletterTitle">Weekly newsletter</span>
        <span class="newsletterDesc"
          >We'll keep you updated when the best new remote jobs pop up on
          Himalayas.</span
        >
        <input
          class="newsletterInput"
          type="email"
          placeholder="Enter your email"
        />
        <span class="newsletterPrivacyPolicy"
          >We care about your data in our
          <span class="underscore" @click="alertFunc('your data is safe')"
            >privacy policy</span
          ></span
        >
        <button class="newsletterSubmitButton">Subscribe</button>
      </form>
      <div class="popularSearchesWrapper">
        <span class="popularSearchesTitle">Popular Searches</span>
        <div class="popularSearchesListing">
          <div class="popularSearch">
            <span>Software Developer</span>
            <Tag color="#8442f5" background-color="#e0dff1" text="23 jobs" />
          </div>
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
  column-gap: 24px;
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

.jobsSidebar {
  padding-top: 39px;
  display: flex;
  flex-direction: column;
  gap: 22px;
}

.weeklyNewsletter,
.popularSearchesWrapper {
  display: flex;
  flex-direction: column;
  gap: 16px;
  width: 100%;
  background-color: #edebfd;
  border-radius: 8px;
  padding: 22px;
}

.feedIconContainer {
  width: 50px;
  height: 50px;
  border-radius: 100%;
  background-color: #e4e1fe;
  display: flex;
  justify-content: center;
  align-items: center;
}

.weeklyNewsletter .icon {
  padding: 16px;
  color: var(--title-purple);
}

.newsletterTitle {
  color: var(--title-dark-purple);
  font-weight: 600;
  font-size: 16px;
}

.newsletterDesc {
  color: var(--title-purple);
  font-size: 14px;
}

.newsletterInput {
  background-color: white;
  padding: 12px 8px;
  border-radius: 8px;
  border: 1px solid rgba(0, 0, 0, 0.3);
  font-size: 14px;
}

.newsletterInput::placeholder {
  color: rgba(0, 0, 0, 0.5);
}

.newsletterPrivacyPolicy {
  font-size: 12px;
  color: var(--title-purple);
}

.newsletterPrivacyPolicy .underscore {
  text-decoration-line: underline;
  cursor: pointer;
}

.newsletterSubmitButton {
  width: 100%;
  background-color: var(--title-purple);
  color: white;
  padding: 16px 20px;
  border-radius: 12px;
  font-size: 14px;
  cursor: pointer;
}

.popularSearchesTitle {
  font-weight: 500;
}

.popularSearchesListing {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.popularSearch {
  display: flex;
  justify-content: space-between;
}

.popularSearch span {
  font-size: 14px;
}
</style>
