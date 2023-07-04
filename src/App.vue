<template>
  <router-view/>
</template>

<style>
@import url("../public/fonts/stylesheet.css");
#app {
  font-family: RF Dewi, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 24px 24px;
}
body{
  margin: 0;
}
@media (max-width: 400px) {
  #app {
    margin: 15px 17px;
  }
}
@media (min-width: 401px) and  (max-width: 768px) {
  #app {
    margin: 15px 36px;
  }
}
</style>
