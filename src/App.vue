<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Vue Todo Management.</h1>
    <hr>
    <!-- 自己終了形式のコンポーネントにより閉じタグ不要 -->
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
