<template>
  <section id="contact" class="contact">
    <div class="container">
      <div class="grid">

        <div class="left">
          <span class="eyebrow r">// Контакт</span>
          <h2 class="heading r d1">Напишите<br/>мне</h2>
          <div class="rule r d2"></div>
          <p class="desc r d2">Открыт к проектам,<br/>сотрудничеству и интересным разговорам.</p>
          <div class="status r d3">
            <span class="dot"></span>
            <span class="eyebrow">Открыт к работе</span>
          </div>
        </div>

        <div class="right r d2">
          <a v-for="l in links" :key="l.label"
             :href="l.href" target="_blank" rel="noopener" class="clink">
            <span class="cl-label eyebrow">{{ l.label }}</span>
            <span class="cl-val">{{ l.val }}</span>
            <svg width="13" height="13" viewBox="0 0 14 14" fill="none">
              <path d="M2 12L12 2M12 2H6M12 2V8" stroke="currentColor" stroke-width="1.2"
                    stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </a>
        </div>

      </div>
    </div>

    <footer class="footer">
      <div class="container foot-row">
        <span class="f-name">Артур Юсупов</span>
        <span class="eyebrow f-stack">Vue 3 · Vite · Firebase · {{ new Date().getFullYear() }}</span>
      </div>
    </footer>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'
const links = [
  { label:'GitHub',   val:'ShadowRaze-ru', href:'https://github.com/ShadowRaze-ru' },
  { label:'Telegram', val:'@xletx',        href:'https://t.me/xletx' },
]
onMounted(() => {
  const o = new IntersectionObserver(es=>es.forEach(e=>e.isIntersecting&&e.target.classList.add('in')),{threshold:.1})
  document.querySelectorAll('#contact .r').forEach(el=>o.observe(el))
})
</script>

<style scoped>
.contact { padding:110px 0 0; border-top:1px solid var(--line); }

.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 80px;
  align-items: start;
  padding-bottom: 72px;
}

.heading {
  font-family:var(--font-display); font-weight:700;
  font-size: clamp(3.2rem,6vw,5.5rem);
  line-height:.92; color:var(--white); margin:16px 0 0;
}
.rule { width:32px; height:1px; background:var(--green-d); margin:24px 0 22px; }
.desc { font-size:.94rem; color:var(--mid); font-weight:300; line-height:1.78; margin-bottom:26px; }

.status { display:flex; align-items:center; gap:10px; }
.dot {
  width:7px; height:7px; border-radius:50%;
  background:var(--green-l); box-shadow:0 0 9px var(--green-l);
  animation: bl 2.8s ease infinite;
}
@keyframes bl { 0%,100%{opacity:1} 50%{opacity:.2} }

.right { display:flex; flex-direction:column; }
.clink {
  display:flex; align-items:center; gap:18px;
  padding:24px 0; border-bottom:1px solid var(--line);
  transition: background .25s, padding-left .3s;
}
.clink:first-child { border-top:1px solid var(--line); }
.clink:hover { padding-left:8px; }
.cl-label { min-width:76px; flex-shrink:0; }
.cl-val { flex:1; font-size:.94rem; color:var(--mid); font-weight:300; transition:color .28s; }
.clink svg { color:var(--dim); transition:color .28s, transform .28s; margin-left:auto; flex-shrink:0; }
.clink:hover .cl-val { color:var(--white); }
.clink:hover svg { color:var(--green-l); transform:translate(3px,-3px); }

.footer { border-top:1px solid var(--line); }
.foot-row {
  display:flex; justify-content:space-between; align-items:center;
  padding:22px 20px; flex-wrap:wrap; gap:8px;
}
.f-name { font-family:var(--font-display); font-style:italic; font-size:.9rem; color:var(--mid); }
.f-stack { color:var(--dim); letter-spacing:.14em; }

@media(max-width:700px) {
  .contact { padding:64px 0 0; }
  .grid { grid-template-columns:1fr; gap:36px; padding-bottom:52px; }
  .heading { font-size: clamp(2.8rem, 11vw, 4rem); }
  .desc { font-size:1rem; color:var(--mid); }
  .right { border-left: none; }
  .clink { padding:20px 0; gap:14px; }
  .clink:first-child { border-top: 1px solid var(--line); }
  .clink:hover { padding-left:0; }
  .cl-label { min-width:80px; font-size:.6rem; }
  .cl-val { font-size:.95rem; }
  .foot-row { flex-direction:column;  gap:4px; }
  .f-stack { font-size: .56rem; letter-spacing: .12em; }
}
</style>