<template>
  <div id="app">
    <div class="logo has-background-white">
      <router-link to="/"><img class="img has-background-white" src="./assets/logo.png" alt=""></router-link>
    </div>
  
    <router-view/>
  </div>
</template>

<style>

.img{
  width: 200px;
  height: 70px;
}
.logo{
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 70px;
  background-color: white;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
