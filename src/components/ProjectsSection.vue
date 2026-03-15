<template>
  <section id="projects" class="projects">
    <div class="container">
      <div class="head">
        <span class="eyebrow r">// Проекты</span>
        <h2 class="heading r d1">Живые работы</h2>
        <div class="rule r d1"></div>
      </div>
    </div>

    <div class="list">
      <article class="card r" :class="[`d${i+1}`,{featured:p.featured}]"
               v-for="(p,i) in projects" :key="i">
        <div class="card-in">
          <div class="card-num eyebrow">{{ String(i+1).padStart(2,'0') }}</div>
          <div class="card-body">
            <div class="card-top">
              <h3 class="card-title">{{ p.title }}</h3>
              <div class="award eyebrow" v-if="p.award">
                <svg width="9" height="9" viewBox="0 0 10 10" fill="currentColor">
                  <path d="M5 0L6.3 3.5H10L7.1 5.7L8.1 9.3L5 7.3L1.9 9.3L2.9 5.7L0 3.5H3.7Z"/>
                </svg>
                {{ p.award }}
              </div>
            </div>
            <p class="card-desc">{{ p.desc }}</p>
            <div class="card-foot">
              <div class="card-tags">
                <span class="tag" v-for="t in p.tags" :key="t">{{ t }}</span>
              </div>
              <div class="card-links">
                <a :href="p.demo" target="_blank" rel="noopener" class="lnk lnk-l">Live →</a>
                <a :href="p.github" target="_blank" rel="noopener" class="lnk">GitHub</a>
              </div>
            </div>
          </div>
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'
const projects = [
  {
    title:'SmartFood',
    desc:'Приложение для планирования питания — рецепты, калорийность, меню. Первый боевой проект с Firebase.',
    tags:['HTML','CSS','JavaScript','Firebase'],
    demo:'https://smartfood-46550.web.app/',
    github:'https://github.com/ShadowRaze-ru/SmartFood',
  },
  {
    title:'Freelance Platform',
    desc:'SPA-платформа для фриланса: авторизация, профили, посты. Vue 3 Composition API + Vuex + Firebase.',
    tags:['Vue 3','Composition API','Vuex','Vue Router','Firebase'],
    demo:'https://freelance-ae474.web.app/',
    github:'https://github.com/ShadowRaze-ru/freelance',
  },
  {
    title:'АНИТИМ Барнаул',
    desc:'Корпоративный сайт по реальному ТЗ для компании АНИТИМ. Настоящее сотрудничество — настоящий результат.',
    tags:['Vue 3','Vuex','Vue Router','HH.ru API','Cloudinary','Firebase'],
    demo:'https://anitim-9c1d1.web.app/',
    github:'https://github.com/ShadowRaze-ru/anitim-website',
    featured:true,
    award:'Икар Код — Алтайский край',
  },
]
onMounted(() => {
  const o = new IntersectionObserver(es=>es.forEach(e=>e.isIntersecting&&e.target.classList.add('in')),{threshold:.07})
  document.querySelectorAll('#projects .r').forEach(el=>o.observe(el))
})
</script>

<style scoped>
.projects { padding:110px 0; border-top:1px solid var(--line); }
.head { margin-bottom:52px; }
.heading {
  font-family:var(--font-display); font-weight:700;
  font-size:clamp(3rem,5.5vw,5rem);
  line-height:.95; color:var(--white); margin:14px 0 0;
}
.rule { width:32px; height:1px; background:var(--green-d); margin-top:22px; }

.list { display:flex; flex-direction:column; }
.card { border-top:1px solid var(--line); transition:background .28s; }
.card:last-child { border-bottom:1px solid var(--line); }
.card:hover { background:rgba(255,255,255,.014); }
.card.featured { background:rgba(78,140,98,.04); }
.card.featured:hover { background:rgba(78,140,98,.07); }

.card-in {
  max-width: 1100px;
  margin: 0 auto;
  padding: 36px 52px;
  display: grid;
  grid-template-columns: 68px 1fr;
  gap: 0;
}

.card-num { padding-top:5px; color:var(--dim); font-size:.58rem; }
.card-body { display:flex; flex-direction:column; gap:14px; }

.card-top {
  display:flex; justify-content:space-between;
  align-items:flex-start; gap:16px; flex-wrap:wrap;
}
.card-title {
  font-family:var(--font-display); font-weight:700;
  font-size:clamp(1.6rem,2.5vw,2.1rem);
  color:var(--white); line-height:1.1; transition:color .28s;
}
.card:hover .card-title { color:var(--green-l); }
.award {
  display:flex; align-items:center; gap:7px;
  color:var(--gold); border:1px solid rgba(160,124,42,.28);
  padding:5px 13px; font-size:.58rem; white-space:nowrap;
}
.card-desc { font-size:.9rem; color:var(--mid); font-weight:300; line-height:1.8; max-width:580px; }
.card-foot { display:flex; align-items:center; justify-content:space-between; flex-wrap:wrap; gap:14px; }
.card-tags { display:flex; flex-wrap:wrap; gap:7px; }
.tag { padding:4px 11px; border:1px solid var(--dim); font-size:.66rem; letter-spacing:.04em; color:var(--mid); }
.card-links { display:flex; gap:22px; }
.lnk { font-size:.7rem; font-weight:500; letter-spacing:.14em; text-transform:uppercase; color:var(--mid); transition:color .28s; }
.lnk-l { color:var(--green-l); }
.lnk:hover { color:var(--white); }

@media(max-width:600px) {
  .projects { padding:64px 0; }
  .head { margin-bottom:36px; }

  .card-in {
    display: block;
    padding: 24px 20px; 
  }

  .card-num { display:none; }
  .card-title { font-size: clamp(1.5rem, 6vw, 1.9rem); }
  .card-desc { font-size:.95rem; line-height:1.75; color:var(--mid); max-width:100%; }
  .award { white-space:normal; }
  .card-foot { flex-direction:column; align-items:flex-start; gap:12px; }
  .lnk { font-size:.76rem; }
  .card-links { gap:24px; }
  .tag { font-size:.7rem; padding:5px 11px; }
}

@media(max-width:380px) {
  .card-in { padding: 24px 16px; }
}
</style>