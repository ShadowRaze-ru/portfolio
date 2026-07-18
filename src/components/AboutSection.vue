<template>
  <section id="about" class="about">
    <div class="container">
      <div class="label-row r"><span class="eyebrow">// О себе</span></div>

      <div class="grid">
        <div class="col-img r d1">
          <div class="frame">
            <img src="@/assets/img/kodama.jpg" class="photo" alt="Кодама" />
            <div class="frame-cap">
              <span class="cap-title">Кодама</span>
              <span class="eyebrow cap-sub">Принцесса Мононоке, 1997</span>
            </div>
          </div>
          <div class="stats">
            <div class="st" v-for="s in stats" :key="s.n">
              <span class="st-n">{{ s.n }}</span>
              <span class="eyebrow st-l">{{ s.l }}</span>
            </div>
          </div>
        </div>

        <div class="col-txt">
          <h2 class="heading r d1">Привет,<br/>я <em>Артур</em></h2>
          <div class="rule r d2"></div>
          <p class="body r d2">
            Мне 14 лет. Чуть больше года назад начал с HTML —
            и уже дошёл до полноценных SPA на Vue&nbsp;3
            с Firebase-бэкендом. Делаю живые рабочие проекты, не учебные.
          </p>
          <p class="body r d3">
            Третий проект — корпоративный сайт для
            <strong>АНИТИМ Барнаул</strong> по реальному ТЗ.
            С ним выиграл региональный конкурс
            <strong>«Икар Код»</strong> в Алтайском крае.
          </p>
          <div class="tl r d4">
            <div class="tl-row" v-for="t in tl" :key="t.y">
              <span class="tl-y eyebrow">{{ t.y }}</span>
              <span class="tl-t">{{ t.t }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue'
const stats = [
  {n:'3',l:'Проекта'},{n:'1',l:'Победа'},{n:'14',l:'Лет'},
]
const tl = [
  {y:'Нач. 2025',t:'Первые шаги — HTML / CSS'},
  {y:'Сер. 2025',t:'Vue 3, Firebase, REST API'},
  {y:'Кон. 2025',t:'АНИТИМ Барнаул + Икар Код'},
  {y:'2026',t:'Продолжаю расти'},
]
onMounted(() => {
  const o = new IntersectionObserver(es=>es.forEach(e=>e.isIntersecting&&e.target.classList.add('in')),{threshold:.1})
  document.querySelectorAll('#about .r').forEach(el=>o.observe(el))
})
</script>

<style scoped>
.about { padding:110px 0; border-top:1px solid var(--line); }
.label-row { margin-bottom:52px; }

.grid {
  display:grid; grid-template-columns:420px 1fr;
  gap:80px; align-items:start;
}

.frame { position:relative; overflow:hidden; }
.photo {
  width:100%; display:block; aspect-ratio:3/4; object-fit:cover;
  filter:brightness(.78) contrast(1.06) saturate(.65);
  transition:filter .5s,transform .5s;
}
.frame:hover .photo { filter:brightness(.88) saturate(.9); transform:scale(1.02); }
.frame-cap {
  position:absolute; bottom:0; left:0; right:0; padding:18px 20px;
  background:linear-gradient(to top,rgba(6,13,8,.92),transparent);
  display:flex; justify-content:space-between; align-items:flex-end;
}
.cap-title { font-family:var(--font-display); font-style:italic; font-size:1.2rem; color:var(--white); }
.cap-sub { color:var(--mid); }

.stats { display:flex; border:1px solid var(--line); border-top:none; }
.st {
  flex:1; padding:18px 20px; border-right:1px solid var(--line);
  display:flex; flex-direction:column; gap:4px;
}
.st:last-child { border-right:none; }
.st-n { font-family:var(--font-display); font-weight:700; font-size:2.2rem; line-height:1; color:var(--green-l); }
.st-l { color:var(--mid); margin-top:2px; }

.col-txt { padding-top:6px; }
.heading {
  font-family:var(--font-display); font-weight:700;
  font-size:clamp(2.6rem,4vw,3.8rem);
  line-height:1.08; color:var(--white);
}
.heading em { font-style:italic; font-weight:300; color:var(--green-l); }
.rule { width:32px; height:1px; background:var(--green-d); margin:22px 0 28px; }
.body { font-size:.94rem; line-height:1.88; color:var(--mid); font-weight:300; margin-bottom:18px; }
.body strong { color:var(--white); font-weight:500; }

.tl { margin-top:36px; border-top:1px solid var(--line); }
.tl-row {
  display:flex; gap:28px; padding:13px 0;
  border-bottom:1px solid var(--line2); align-items:baseline;
}
.tl-y { min-width:72px; color:var(--green); font-size:.6rem; letter-spacing:.08em; }
.tl-t { font-size:.86rem; color:var(--mid); font-weight:300; }

@media(max-width:900px) {
  .grid { grid-template-columns:300px 1fr; gap:48px; }
}

@media(max-width:680px) {
  .about { padding:64px 0; }
  .label-row { margin-bottom:28px; }

  .grid {
    grid-template-columns: 1fr;
    gap: 32px;
  }

  .col-txt { order: 1; }
  .col-img { order: 2; }

  .heading { font-size: clamp(2.4rem, 10vw, 3.2rem); }

  .body { font-size: 1rem; line-height: 1.75; color: var(--mid); }
  .body strong { color: var(--white); }

  .photo { aspect-ratio: 4/3; }

  .tl-y { font-size:.66rem; letter-spacing:.06em; min-width:72px; }
  .tl-t { font-size:.92rem; }

  .st { padding:16px 14px; }
  .st-n { font-size:2rem; }
}
</style>