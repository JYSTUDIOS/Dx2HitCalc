<template>
  <div id="app">
    <img src="./assets/logo.jpg">
    <h1>Dx2命中率计算器Beta</h1>
    <p>@一等星的光辉 大佬提供数据支持</p>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flow;
  /*color: #2c3e50;*/
  /*margin-top: 60px;*/
}
</style>
