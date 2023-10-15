<script setup lang="ts">
import { ref } from "vue";
import Icon from "../../../ui/Icon.vue";
import Tag from "../../../ui/Tag.vue";
import { type Job } from "./RemoteJobsPage.vue";

const props = defineProps<{
  job: Job;
}>();

const randomHoursAgo = ref(0);
randomHoursAgo.value = Math.floor(Math.random() * 15) + 1;

const wageAproxValue = ref<number[]>([]);
const roundedValue: number =
  Math.round(parseFloat(props.job.annualWage.toString().slice(0, -3)) / 10) *
  10;
wageAproxValue.value = [roundedValue - 10, roundedValue + 10];
</script>

<template>
  <div class="cardWrapper">
    <div class="imageContainer">
      <img class="cardImage" :src="job.companyLogoUrl" />
    </div>
    <div class="cardTextContainer">
      <div class="textFirstRow">
        <span class="jobTitle">
          {{ job.jobTitleText }}
        </span>
        <span class="jobTimeAgo"> {{ randomHoursAgo }} days ago </span>
      </div>
      <div class="textSecondRow">
        <span class="jobCompany">{{ job.companyName }}</span>
        <div class="employeeCountContainer">
          <Icon icon="star" />
          <span> {{ job.rating }} </span>
        </div>
        <div class="jobWageContainer">
          <Icon icon="attach_money" />
          <span> {{ wageAproxValue[0] }}k-{{ wageAproxValue[1] }}k </span>
        </div>
        <Tag
          :text="job.locationName"
          color="#7b7e98"
          background-color="#ebedf2"
          dot
        />
      </div>
      <div class="textThirdRow">
        <Tag text="Full time" color="#8442f5" background-color="#edebfd" />
        <Tag
          v-if="job.jobTitleText.includes('Software')"
          text="Software Developer"
          color="#4383ed"
          background-color="#e1efff"
          dot
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.cardWrapper {
  border: 1px solid rgba(0, 0, 0, 0.1);
  padding: 24px;
  border-radius: 8px;
  display: grid;
  grid-template-columns: 50px 1fr;
  column-gap: 20px;
}

.imageContainer {
  display: flex;
  justify-content: center;
}

.cardImage {
  width: 50px;
  height: 50px;
}

.cardTextContainer {
  display: grid;
  grid-template-rows: 1fr 1fr 1fr;
  gap: 12px;
}

.textFirstRow {
  display: flex;
  justify-content: space-between;
}

.jobTitle {
  font-weight: 600;
}

.jobTimeAgo {
  color: var(--subtitle-gray);
  font-size: 12px;
  font-weight: 600;
}

.textSecondRow {
  display: flex;
  align-items: center;
  gap: 12px;
}

.textSecondRow .jobCompany {
  font-weight: 500;
  color: black;
}

.textSecondRow span {
  font-size: 14px;
  color: var(--subtitle-gray);
  font-weight: 500;
}

.employeeCountContainer {
  display: flex;
  gap: 4px;
}

.jobWageContainer {
  display: flex;
}

.employeeCountContainer .icon,
.jobWageContainer .icon {
  font-size: 18px;
  color: var(--subtitle-gray);
}

.textThirdRow {
  display: flex;
  gap: 8px;
}
</style>
