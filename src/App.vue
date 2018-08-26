<!-- PARENT COMPONENT -->
<template>
  <div id="app">
    <nav class="navbar navbar-dark bg-dark">
      <div>
        <h1 class="title">Navstone</h1>
      </div>
      <div class="btn-toolbar" role="toolbar" aria-label="Toolbar with button groups">
        <div class="btn-group mr-2" role="group" aria-label="First group">
          <button type="button" class="btn-nav">About</button>
          <button type="button" class="btn-nav">Account</button>
          <button type="button" class="btn-nav">Signup</button>
          <button type="button" class="btn-nav">Login</button>
        </div>
      </div>
    </nav>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}
.photo {
  border-radius: 50%;
}
#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
