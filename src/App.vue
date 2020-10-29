<template>
  <div id="app">
    <img class="headerLogo" alt="BnD Logo" src="./assets/BnDinline.png" />
    <Retention />
  </div>
</template>

<script>
import Retention from "./components/Retention.vue";

export default {
  name: "App",
  components: {
    Retention,
  },
};
</script>

<style>
#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #00263a;
  height: 100vh;
  display: flex;
  flex-flow: column;
  align-items: center;
}

.headerLogo {
  height: 70px;
  max-width: 100%;
}

.link {
  position: relative;
  color: #789904;
  text-decoration: none;
}

.link:hover {
  color: #789904;
}

.link::before {
  content: "";
  position: absolute;
  width: 100%;
  height: 2px;
  bottom: 0;
  left: 0;
  background-color: #789904;
  visibility: hidden;
  transform: scaleX(0);
  transition: all 0.3s ease-in-out 0s;
}

.link:hover::before {
  visibility: visible;
  transform: scaleX(1);
}

.green-btn {
  font-family: 'Montserrat', sans-serif;
  background: #789904;
  -webkit-border-radius: 20px;
  -moz-border-radius: 20px;
  border-radius: 500px;
  color: #ffffff;
  height: 50px;
  padding: 2px;
  box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.2);
  border: solid #637e05 1px;
  cursor: pointer;
  text-align: center;
  margin: 10px;
}

.orange-btn {
  font-family: 'Montserrat', sans-serif;
  background:#ee7623;
  -webkit-border-radius: 20px;
  -moz-border-radius: 20px;
  border-radius: 500px;
  color: #ffffff;
  height: 50px;
  padding: 2px;
  box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.2);
  border: solid #f17216 1px;
  cursor: pointer;
  text-align: center;
  margin: 10px;
}

.green-btn:focus,
.orange-btn:focus {
  outline: none;
}

.green-btn:active,
.orange-btn:active {
  box-shadow: inset 0px 4px 15px rgba(0, 0, 0, 0.2);
}

.accordion-btn {
    width: 200px;
}
</style>
