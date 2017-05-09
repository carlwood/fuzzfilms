<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>

export default {
  name: 'app'
}
</script>

<style>

* {
  box-sizing: border-box;
}

body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 80px;
}

h1, h2, h3, h4, p {
  margin-top: 0;
}

.container {
  margin: 0 auto;
  max-width: 1200px;
  padding: 0 20px;
}

.logo {
  color: #e0822c;
  font-size: 28px;
  letter-spacing: -2px;
  position: absolute;
  left: 20px;
  top: 15px;
}

img {
  max-width: 100%;
}

.btn {
  border: 0;
  cursor: pointer;
  font-size: 16px;
  padding: 10px;
  text-decoration: none;
}

.btn--primary {
  background: #e0822c;
  color: #fff;
}

.btn--check {
  background: #333;
  color: #fff;
  font-size: 11px;
  letter-spacing: 3px;
  text-transform: uppercase;
}

.btn--lg {
  font-size: 20px;
  padding: 10px 20px;
}

.btn--block {
  display: block;
  width: 100%;
}

input[type=text] {
  display: block;
  font-size: 16px;
  padding: 10px;
  width: 100%;
}

.page-title {
  font-size: 28px;
  letter-spacing: -1px;
  text-align: left;
}

</style>
