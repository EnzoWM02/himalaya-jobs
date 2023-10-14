<script setup>
import HimalayaLogo from "./HimalayaLogo.vue";
</script>

<template>
  <div class="navbarContainer">
    <div class="navbarWrapper">
      <HimalayaLogo />
      <ul class="navbarOptions">
        <li>
          Jobs
          <span class="material-symbols-outlined"> expand_more </span>
        </li>
        <li>
          Companies
          <span class="material-symbols-outlined"> expand_more </span>
        </li>
        <li>Pricing</li>
        <li>Advice</li>
        <li>Updates</li>
        <li>Community</li>
        <li>
          <div class="roundedOption">
            <img src="../../assets/profilePic.png" />
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.navbarContainer {
  padding: 0 10vw;
  background: var(--background-color);
}
.navbarWrapper {
  width: 100%;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.navbarOptions {
  display: flex;
  align-items: center;
}

.navbarOptions > li {
  display: inline-flex;
  font-size: 16px;
  margin: 0 15px;
  color: var(--subtitle-purple);
  font-weight: 600;
}

.roundedOption > img {
  width: 50px;
  height: 50px;
  border-radius: 100%;
}
</style>
