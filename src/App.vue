<template>
  <div class="app-shell">
    <router-view />
  </div>
</template>

<script>
export default {}
</script>

<style>
@font-face {
  font-family: 'Disney';
  src: url('/fonts/waltographUI.ttf') format('truetype');
}

body {
  margin: 0;
  min-height: 100vh;
  background: linear-gradient(to bottom, #01147c, #02021a);
  color: white;
  font-family: 'Quicksand', sans-serif;
}

body::before {
  content: "";
  position: fixed;
  inset: 0;
  background: url('https://www.transparenttextures.com/patterns/stardust.png');
  opacity: 0.12;
  z-index: -1;
}

.app-shell {
  min-height: 100vh;
}

button {
  font-family: inherit;
}
</style>
