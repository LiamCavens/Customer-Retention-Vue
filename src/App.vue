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
  font-family: "Montserrat", sans-serif;
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

.bnd-btn {
  font-family: "Montserrat", sans-serif;
  font-weight: 600;
  -webkit-border-radius: 20px;
  -moz-border-radius: 20px;
  border-radius: 500px;
  cursor: pointer;
  text-align: center;
  margin: 10px;
  height: 50px;
  padding: 2px;
  box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.2);
}

.green-btn {
  background: #789904;
  color: #ffffff;
  border: solid #637e05 1px;
}

.orange-btn {
  background: #ee7623;
  color: #ffffff;
  border: solid #f17216 1px;
}

.white-btn {
  background-color: #fff;
  color: #789904;
  border: 1px solid #789904;
}

.bnd-btn:focus {
  outline: none;
}

.bnd-btn:active {
  box-shadow: inset 0px 4px 15px rgba(0, 0, 0, 0.2);
}

.accordion-btn {
  width: 200px;
}
</style>
