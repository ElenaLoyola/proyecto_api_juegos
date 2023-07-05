<template>
  <nav>
    <h4>Games Opinion <i class="fa-solid fa-gamepad" style="color: #ffffff;"></i></h4>
    <div>
      <i class="fa-solid fa-house" style="color: #ffffff;"></i>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
  </nav>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
  background-color: black;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
h4 {
  color: white;
  margin-bottom: 0px;
}
i {
  margin-right: 5px;
  margin-left: 5px;
}
nav a {
  font-weight: bold;
  color: white;
  text-decoration: none;
}

nav a.router-link-exact-active {
  color: cornflowerblue;
}
</style>
