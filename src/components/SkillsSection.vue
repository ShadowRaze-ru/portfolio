<template>
  <section id="skills" class="skills">
    <div class="container">
      <div class="head">
        <span class="eyebrow r">// Стек</span>
        <h2 class="heading r d1">Технологии</h2>
        <div class="rule r d1"></div>
      </div>
      <div class="bands">
        <div class="band r" :class="`d${i%4+1}`" v-for="(g,i) in groups" :key="g.t">
          <div class="band-l">
            <span class="band-n eyebrow">{{ String(i+1).padStart(2,'0') }}</span>
            <h3 class="band-t">{{ g.t }}</h3>
          </div>
          <div class="band-pills">
            <span class="pill" v-for="s in g.s" :key="s">{{ s }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'
const groups = [
  {t:'Frontend',     s:['HTML5','CSS3','JavaScript ES6+','Bootstrap','Адаптив']},
  {t:'Vue 3',        s:['Options API','Composition API','Vuex','Vue Router','Axios']},
  {t:'Бэкенд & API', s:['REST API','Node.js','Express.js','XHR / Fetch / Axios']},
  {t:'Firebase',     s:['Firestore CRUD','Authentication','Hosting','Deploy']},
  {t:'Инструменты',  s:['Git','GitHub','GitHub Pages','Vite','VS Code']},
]
onMounted(() => {
  const o = new IntersectionObserver(es=>es.forEach(e=>e.isIntersecting&&e.target.classList.add('in')),{threshold:.08})
  document.querySelectorAll('#skills .r').forEach(el=>o.observe(el))
})
</script>

<style scoped>
.skills { padding:110px 0; border-top:1px solid var(--line); }
.head { margin-bottom:52px; }
.heading {
  font-family:var(--font-display); font-weight:700;
  font-size:clamp(3rem,5.5vw,5rem);
  line-height:.95; color:var(--white); margin:14px 0 0;
}
.rule { width:32px; height:1px; background:var(--green-d); margin-top:22px; }

.bands { display:flex; flex-direction:column; }
.band {
  display:flex; align-items:center; gap:52px;
  padding:26px 0;
  border-bottom:1px solid var(--line);
  transition:background .25s, padding-left .3s;
}
.band:first-child { border-top:1px solid var(--line); }
.band:hover { background:rgba(255,255,255,.015); padding-left:14px; }

.band-l { display:flex; align-items:baseline; gap:18px; min-width:200px; flex-shrink:0; }
.band-n { color:var(--dim); }
.band-t {
  font-family:var(--font-display); font-style:italic; font-weight:400;
  font-size:1.3rem; color:var(--white);
}

.band-pills { display:flex; flex-wrap:wrap; gap:8px; }
.pill {
  padding:5px 13px;
  border:1px solid var(--dim);
  font-size:.7rem; letter-spacing:.04em; color:var(--mid);
  transition:border-color .25s, color .25s, background .25s;
}
.band:hover .pill { border-color:var(--green-d); color:var(--white); background:rgba(46,82,56,.15); }

@media(max-width:860px){
  .band { gap:28px; }
  .band-l { min-width:150px; }
}

@media(max-width:680px){
  .skills { padding:56px 0; }
  .head { margin-bottom:36px; }

  .band {
    flex-direction:column;
    align-items:flex-start;
    gap:12px;
    padding:20px 0;
  }
  .band:hover { padding-left:0; }

  .band-l { min-width:auto; gap:12px; }
  .band-n { font-size:.6rem; }
  .band-t { font-size:1.15rem; }

  .pill { font-size:.72rem; padding:6px 12px; }
}
</style>