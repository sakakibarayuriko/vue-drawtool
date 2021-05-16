<template>
  <div id="app">
    <DrawTool />
  </div>
</template>

<script>
import DrawTool from "./components/DrawTool.vue";

export default {
  name: "App",
  components: {
    DrawTool,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
label {
  margin: 5px;
  display: inline-block;
  width: 40px;
  height: 40px;
  padding: 0;
  border: none;
  background: transparent;
}
button {
  margin: 5px;
  display: inline-block;
  width: 44px;
  height: 44px;
  padding: 0;
  border: none;
  background: transparent;
}
button:focus {
  outline: 0;
}
button:hover {
  border: 2px solid;
}
input {
  display: none;
}
input:checked + label {
  border: 2px solid;
}
svg {
  margin-top: 5px;
}
</style>
