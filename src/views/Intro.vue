<template>
  <div class="intro-page">
    <div class="stars"></div>
    <div class="intro-card text-center">
      <div class="logo">Disney<span>World</span></div>
      <p class="subtitle">Your Disney character journey starts here.</p>
      <button @click="$router.push('/characters')" class="btn btn-disney btn-lg">
        Explore Characters
      </button>
      <p class="hint">Click to enter the Disney character gallery.</p>
    </div>
  </div>
</template>

<style scoped>
.intro-page {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  background: radial-gradient(circle at top, #7ecfff 0%, #0d1c5e 40%, #050b20 100%);
  overflow: hidden;
}

.stars {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.95) 1px, transparent 1px) 0 0/24px 24px;
  opacity: 0.22;
  pointer-events: none;
}

.intro-card {
  position: relative;
  z-index: 1;
  max-width: 560px;
  width: 100%;
  padding: 3rem 2rem;
  border-radius: 2rem;
  background: rgba(2, 9, 43, 0.88);
  border: 1px solid rgba(255, 255, 255, 0.18);
  box-shadow: 0 0 80px rgba(0, 0, 0, 0.35);
  text-align: center;
}

.logo {
  display: inline-block;
  width: 100%;
  max-width: 100%;
  font-family: 'Disney', cursive;
  font-size: clamp(3rem, 6vw, 4rem);
  letter-spacing: 0.18em;
  text-transform: uppercase;
  text-shadow: 0 0 24px rgba(255, 255, 255, 0.55);
  margin-bottom: 1rem;
  white-space: normal;
}

.logo span {
  display: block;
  color: #ffd700;
  font-size: 0.65em;
  margin-top: -0.25em;
  letter-spacing: 0.14em;
}

.subtitle {
  color: #d7e7ff;
  font-size: 1.25rem;
  margin: 0 0 2rem;
}

.btn-disney {
  background: linear-gradient(135deg, #ffce00 0%, #e8437d 100%);
  border: none;
  color: #111;
  box-shadow: 0 14px 30px rgba(232, 67, 125, 0.35);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  border-radius: 999px;
  padding: 0.95rem 2.2rem;
  font-weight: 700;
}

.btn-disney:hover {
  transform: translateY(-3px);
  box-shadow: 0 18px 36px rgba(232, 67, 125, 0.55);
}

.hint {
  margin-top: 1.5rem;
  color: #b8cdff;
}
</style>
