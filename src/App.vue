<template>
  <div class="App">
    <!--
    <div class="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    -->
    <router-view />
  </div>
</template>

<style lang="scss">
@import '@/main.scss';

.App {
  padding-top: 64px;
  height: 100%;
  background-color: $appBlack;
  color: $appWhite;
  font-family: roboto;
  text-align: center;
}
</style>
