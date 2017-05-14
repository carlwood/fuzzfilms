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

html {
  height: auto;
}

body {
  height: 100%;
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 20px 0;
}

h1, h2, h3, h4, p {
  margin-top: 0;
}

.container {
  margin: 0 auto;
  max-width: 1200px;
  padding: 0 25px;
}

.logo {
  color: #e0822c;
  display: flex;
  font-size: 6vw;
  text-transform: uppercase;
  left: 30px;
  top: 20px;
  opacity: 0.6;
  text-align: center;
  justify-content: space-between;
  border-bottom: solid 10px #e0822c;
}

img {
  max-width: 100%;
}

.btn {
  border: 0;
  cursor: pointer;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
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
  font-size: 10px;
  letter-spacing: 2px;
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
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  display: block;
  font-size: 15px;
  padding: 10px;
  width: 100%;
  border: solid 1px #ccc;
}

.page-title {
  font-size: 28px;
  letter-spacing: -1px;
  text-align: left;
  margin-bottom: 35px;
}

</style>
