<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
document.addEventListener('DOMContentLoaded', () => {
  const html = document.querySelector('html')
  let fontSize = window.innerWidth / 15
  fontSize = fontSize <= 50 ? fontSize : 50
  html.style.fontSize = fontSize + 'px'
})
</script>

<style>
#app {

}
</style>
