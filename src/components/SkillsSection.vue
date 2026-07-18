<template>
  <section id="skills" class="skills">
    <div class="container">
      <div class="head">
        <span class="eyebrow r">// Стек</span>
        <h2 class="heading r d1">Технологии и инструменты</h2>
        <div class="rule r d1"></div>
      </div>
      <div class="bands">
        <div class="band r" :class="`d${i % 4 + 1}`" v-for="(g, i) in groups" :key="g.t">
          <div class="band-l">
            <span class="band-n eyebrow">{{ String(i + 1).padStart(2, '0') }}</span>
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
  { t: 'Frontend', s: ['HTML5', 'CSS3', 'JavaScript (ES6+)', 'Bootstrap', 'Vue 3', 'Composition API', 'Vuex', 'Vue Router', 'Vite'] },
  { t: 'Backend', s: ['Node.js', 'Express.js', 'REST API', 'Firebase', 'JWT', 'Auth'] },
  { t: 'Data & Integrations', s: ['PostgreSQL', 'Excel / CSV', 'OpenAPI', 'JSON', 'Axios', 'Fetch'] },
  { t: 'Tools', s: ['Git', 'GitHub', 'GitHub Pages', 'Docker', 'Docker Compose', 'SEO', 'Env'] },
]
onMounted(() => {
  const o = new IntersectionObserver(es => es.forEach(e => e.isIntersecting && e.target.classList.add('in')), { threshold: .08 })
  document.querySelectorAll('#skills .r').forEach(el => o.observe(el))
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

.bands { display:flex; flex-direction:column; gap:12px; }
.band {
  display:flex; align-items:center; gap:52px;
  padding:22px 24px;
  border:1px solid var(--line);
  border-radius:20px;
  background: linear-gradient(135deg, rgba(255,255,255,.035), rgba(255,255,255,.02));
  transition:transform .25s, border-color .25s, background .25s;
}
.band:hover {
  transform: translateY(-2px);
  border-color:rgba(78,140,98,.28);
  background: linear-gradient(135deg, rgba(78,140,98,.08), rgba(255,255,255,.025));
}

.band-l { display:flex; align-items:baseline; gap:18px; min-width:200px; flex-shrink:0; }
.band-n { color:var(--dim); }
.band-t {
  font-family:var(--font-display); font-style:italic; font-weight:400;
  font-size:1.3rem; color:var(--white);
}

.band-pills { display:flex; flex-wrap:wrap; gap:8px; }
.pill {
  padding:6px 12px;
  border:1px solid rgba(255,255,255,.08);
  border-radius:999px;
  font-size:.7rem; letter-spacing:.04em; color:var(--mid);
  background: rgba(255,255,255,.03);
  transition:border-color .25s, color .25s, background .25s;
}
.band:hover .pill { border-color:rgba(78,140,98,.24); color:var(--white); background:rgba(46,82,56,.15); }

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
    padding:20px 18px;
  }

  .band-l { min-width:auto; gap:12px; }
  .band-n { font-size:.6rem; }
  .band-t { font-size:1.15rem; }

  .pill { font-size:.72rem; padding:6px 12px; }
}
</style>