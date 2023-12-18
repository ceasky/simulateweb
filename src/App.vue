<template>
  <div id="app">
    <NavBar class="navbarcss" />
    <main role="main" class="maincss">
      <router-view />
    </main>
    <Footer class="footercss" />
  </div>
</template>

<script>
import "bootstrap";
import "bootstrap/dist/css/bootstrap.min.css";
import NavBar from "./components/NavBar";
import Footer from "./components/Footer";
export default {
  components: {
    NavBar,
    Footer,
  },
  data() {
    return {};
  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: white;
  background-color: #141414;
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
.navbarcss {
  position: sticky;
  top: 0;
  left: 2.5%;
  background-color: #141414;
  /* background-color:yellow ; */
  z-index: 1;
}
.maincss {
  flex-grow: 1;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
