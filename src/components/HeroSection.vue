<template>
  <section id="hero" class="hero">
    <div class="bg-glow"></div>

    <div class="container hero-wrap">

      <div class="hero-top r">
        <span class="eyebrow">Frontend Developer · 14 лет</span>
        <div class="ht-right">
          <span class="eyebrow year">Россия · Vue 3</span>
          <span class="status-dot"></span>
        </div>
      </div>

      <div class="name-block">
        <h1 class="n-last r d1">Юсупов</h1>
        <div class="n-second-row">
          <h1 class="n-first r d2"><em>Артур</em></h1>
          <span class="n-year r d2">2026</span>
        </div>
      </div>

      <div class="hero-bottom r d3">
        <div class="hb-left">
          <p class="hero-sub">Строю интерфейсы на Vue 3. От идеи до деплоя.</p>
          <div class="badges">
            <span class="badge">Vue 3</span>
            <span class="badge">Firebase</span>
            <span class="badge">Vite</span>
          </div>
        </div>
        <div class="hero-cta">
          <a href="#projects" class="cta-a" @click.prevent="go('#projects')">Проекты</a>
          <a href="#contact"  class="cta-b" @click.prevent="go('#contact')">Написать</a>
        </div>
      </div>

    </div>

    <div class="sc r d4"><div class="sc-fill"></div></div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'
function go(h) { document.querySelector(h)?.scrollIntoView({ behavior:'smooth' }) }
onMounted(() => setTimeout(() => document.querySelectorAll('#hero .r').forEach(e=>e.classList.add('in')), 50))
</script>

<style scoped>
.hero {
  min-height: 100svh;
  position: relative;
  display: flex;
  align-items: stretch;
  overflow: hidden;
}
.bg-glow {
  position: absolute; inset: 0; pointer-events: none;
  background:
    radial-gradient(ellipse 70% 55% at 15% 55%, rgba(30,72,46,.2) 0%, transparent 65%),
    radial-gradient(ellipse 45% 35% at 80% 30%, rgba(18,52,32,.1) 0%, transparent 65%);
}
.hero-wrap {
  display: flex; flex-direction: column;
  justify-content: space-between;
  padding-top: 130px; padding-bottom: 56px;
  width: 100%; position: relative; z-index: 1;
  min-height: 100svh;
}

.hero-top {
  display: flex; justify-content: space-between; align-items: center;
  border-bottom: 1px solid var(--line); padding-bottom: 20px;
  gap: 16px;
}
.ht-right { display: flex; align-items: center; gap: 12px; flex-shrink: 0; }
.year { color: var(--dim); white-space: nowrap; }
.hero-top > .eyebrow { white-space: nowrap; }
.status-dot {
  width: 6px; height: 6px; border-radius: 50%;
  background: var(--green-l); box-shadow: 0 0 8px var(--green-l);
  animation: pulse 2.8s ease infinite; flex-shrink: 0;
}
@keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.25} }

.name-block {
  flex: 1; display: flex; flex-direction: column;
  justify-content: center; padding: 24px 0 16px;
}
.n-last {
  font-family: var(--font-display); font-weight: 900;
  font-size: clamp(56px, 14vw, 200px);
  line-height: .88; letter-spacing: -.03em; color: var(--white);
}
.n-second-row {
  display: flex; align-items: flex-end; justify-content: space-between;
}
.n-first {
  font-family: var(--font-display); font-weight: 400;
  font-size: clamp(50px, 12.5vw, 178px);
  line-height: .92; letter-spacing: -.02em;
}
.n-first em {
  font-style: italic; color: var(--green-l); font-weight: 400;
}
.n-year {
  font-family: var(--font-body); font-weight: 300;
  font-size: clamp(.9rem, 1.8vw, 1.4rem);
  color: var(--dim); letter-spacing: .1em;
  padding-bottom: .22em; flex-shrink: 0;
}

.hero-bottom {
  display: flex; align-items: flex-end;
  justify-content: space-between;
  border-top: 1px solid var(--line);
  padding-top: 24px; gap: 24px; flex-wrap: wrap;
}
.hb-left { display: flex; flex-direction: column; gap: 14px; }
.hero-sub {
  font-size: .94rem; color: var(--mid); font-weight: 300;
  line-height: 1.72; max-width: 360px;
  font-family: var(--font-body);
}
.badges { display: flex; gap: 8px; flex-wrap: wrap; }
.badge {
  padding: 4px 12px; border: 1px solid var(--green-d);
  font-size: .62rem; font-weight: 500;
  letter-spacing: .16em; text-transform: uppercase; color: var(--green);
  font-family: var(--font-body);
}

.hero-cta { display: flex; gap: 10px; flex-shrink: 0; }
.cta-a {
  padding: 13px 32px; background: var(--green); color: #fff;
  font-size: .7rem; font-weight: 500; letter-spacing: .18em; text-transform: uppercase;
  transition: background .28s, transform .18s; font-family: var(--font-body);
}
.cta-a:hover { background: #5fa072; transform: translateY(-1px); }
.cta-b {
  padding: 13px 32px; border: 1px solid var(--dim); color: var(--mid);
  font-size: .7rem; font-weight: 500; letter-spacing: .18em; text-transform: uppercase;
  transition: border-color .28s, color .28s, transform .18s; font-family: var(--font-body);
}
.cta-b:hover { border-color: var(--green-d); color: var(--white); transform: translateY(-1px); }

.sc {
  position: absolute; left: 52px; bottom: 56px;
  width: 1px; height: 52px; background: var(--dim); overflow: hidden;
}
.sc-fill {
  width: 100%; height: 45%; background: var(--green-l);
  animation: scA 2.2s ease-in-out infinite;
}
@keyframes scA { 0%{transform:translateY(-100%)} 100%{transform:translateY(230%)} }

@media(max-width:680px) {
  .sc, .n-year, .ht-right { display: none; }
  .hero-wrap { padding-top: 76px; padding-bottom: 32px; }
  .name-block { padding: 18px 0 14px; }
  .n-last  { font-size: clamp(72px, 22vw, 112px); line-height: .86; }
  .n-first { font-size: clamp(64px, 20vw, 100px); line-height: .90; }
  .n-second-row { justify-content: flex-start; }
  .hero-bottom { flex-direction: column; align-items: flex-start; gap: 18px; padding-top: 20px; }
  .hero-sub { max-width: 100%; font-size: .9rem; }
  .hero-cta { width: 100%; flex-direction: column; gap: 8px; }
  .cta-a, .cta-b { width: 100%; text-align: center; padding: 15px; font-size: .72rem; }
}
</style>