<template>
  <section id="projects" class="projects">
    <div class="container">
      <div class="head">
        <span class="eyebrow r">// Проекты</span>
        <h2 class="heading r d1">Работы, в которых есть результат</h2>
        <div class="rule r d1"></div>
      </div>
    </div>

    <div class="list">
      <article class="card r" :class="[`d${i + 1}`, { featured: p.featured }]" v-for="(p, i) in projects" :key="p.title">
        <div class="card-in">
          <div class="card-num eyebrow">{{ String(i + 1).padStart(2, '0') }}</div>
          <div class="card-body">
            <div class="card-top">
              <div>
                <h3 class="card-title">{{ p.title }}</h3>
                <p class="card-sub">{{ p.period }}</p>
              </div>
              <div class="award eyebrow" v-if="p.award">
                <svg width="9" height="9" viewBox="0 0 10 10" fill="currentColor">
                  <path d="M5 0L6.3 3.5H10L7.1 5.7L8.1 9.3L5 7.3L1.9 9.3L2.9 5.7L0 3.5H3.7Z" />
                </svg>
                {{ p.award }}
              </div>
            </div>

            <div class="preview-block">
              <div class="image-shell">
                <div class="image-track" :style="{ transform: `translateX(-${p.activeIndex * 100}%)` }">
                  <img v-for="(img, idx) in p.images" :key="`${p.title}-${idx}`" :src="img" :alt="`${p.title} ${idx + 1}`" class="preview-image" />
                </div>
                <div v-if="p.images.length > 1" class="slider-controls">
                  <button class="slider-btn" type="button" @click.stop="prevSlide(p)" aria-label="Предыдущий кадр">←</button>
                  <div class="slider-dots">
                    <button
                      v-for="(_, idx) in p.images"
                      :key="`${p.title}-dot-${idx}`"
                      class="slider-dot"
                      :class="{ active: idx === p.activeIndex }"
                      type="button"
                      :aria-label="`Показать кадр ${idx + 1}`"
                      @click.stop="goToSlide(p, idx)"
                    />
                  </div>
                  <button class="slider-btn" type="button" @click.stop="nextSlide(p)" aria-label="Следующий кадр">→</button>
                </div>
              </div>
              <div class="preview-copy">
                <div class="preview-item">
                  <span class="preview-label">Проблема</span>
                  <p>{{ p.problem }}</p>
                </div>
                <div class="preview-item">
                  <span class="preview-label">Решение</span>
                  <p>{{ p.solution }}</p>
                </div>
              </div>
            </div>

            <p class="card-desc">{{ p.desc }}</p>

            <div class="card-foot">
              <div class="card-tags">
                <span class="tag" v-for="t in p.tags" :key="t">{{ t }}</span>
              </div>
              <div class="card-links">
                <a v-if="p.demo" :href="p.demo" target="_blank" rel="noopener" class="lnk lnk-l">Live →</a>
                <a v-if="p.github" :href="p.github" target="_blank" rel="noopener" class="lnk">GitHub</a>
              </div>
            </div>
          </div>
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
import { onMounted, reactive } from 'vue'
import projectTfh1 from '@/assets/img/tfh1.png'
import projectTfh2 from '@/assets/img/tfh2.png'
import projectTfh3 from '@/assets/img/tfh3.png'
import projectAnitim1 from '@/assets/img/anitim1.png'
import projectAnitim2 from '@/assets/img/anitim2.png'
import projectAnitim3 from '@/assets/img/anitim3.png'
import projectAnitim4 from '@/assets/img/anitim4.png'
import projectAnitim5 from '@/assets/img/anitim5.png'
import projectStena1 from '@/assets/img/stena1.png'
import projectStena2 from '@/assets/img/stena2.png'
import projectStena3 from '@/assets/img/stena3.png'

function nextSlide(project) {
  project.activeIndex = (project.activeIndex + 1) % project.images.length
}

function prevSlide(project) {
  project.activeIndex = (project.activeIndex - 1 + project.images.length) % project.images.length
}

function goToSlide(project, index) {
  project.activeIndex = index
}

const projects = reactive([
  {
    title: 'Обработчик Яндекс Форм',
    period: 'Командная разработка · 2 месяца',
    desc: 'Веб-сервис для работы с формами Яндекс Форм: редактирование данных, поиск, скрытие столбцов, экспорт в Excel/CSV и удобное управление регистрациями.',
    problem: 'Обычная работа с Яндекс Формами была неудобной: сложно контролировать дубли, редактировать записи и управлять участниками без отдельной системы.',
    solution: 'Мы собрали внутренний сервис с авторизацией, CRUD по данным, фильтрацией, поиском, экспортом и логикой обработки форм на собственном сервере.',
    tags: ['Vue 3', 'Vuex', 'Vue Router', 'PostgreSQL', 'FastAPI', 'OpenAPI', 'JWT', 'Docker', 'Excel / CSV'],
    demo: 'http://80.87.195.228/forms',
    github: '',
    featured: true,
    award: 'Командный продукт',
    images: [projectTfh1, projectTfh2, projectTfh3],
    activeIndex: 0,
  },
  {
    title: 'АО АНИТИМ',
    period: 'Корпоративный сайт · реальное ТЗ',
    desc: 'Корпоративный сайт для компании с адаптивной архитектурой, динамическими блоками и интеграцией с внешними сервисами.',
    problem: 'Нужен был современный сайт с понятной структурой, который выглядел строго, но при этом отражал реальную бизнес-логику.',
    solution: 'Сделали удобный интерфейс на Vue 3 с навигацией, блоками под контент и интеграциями, которые помогли представить компанию профессионально.',
    tags: ['Vue 3', 'Vuex', 'Vue Router', 'Firebase', 'HH.ru API', 'Rutube API', 'CRM'],
    demo: 'https://anitim-9c1d1.web.app/',
    github: 'https://github.com/ShadowRaze-ru/anitim-website',
    award: 'Икар Код — Алтайский край',
    images: [projectAnitim1, projectAnitim2, projectAnitim3, projectAnitim4, projectAnitim5],
    activeIndex: 0,
  },
  {
    title: 'СтеныПро',
    period: 'Лендинг · заявки и квиз',
    desc: 'Сайт для услуги по монтажу перегородок и отделке с квизом, калькулятором выгоды и быстрыми заявками.',
    problem: 'Нужно было превратить обычный сайт в инструмент, который помогает пользователю быстро понять цену и оставить заявку.',
    solution: 'Реализовали логику квиза, валидацию формы, отправку заявок и быстрый пользовательский путь от просмотра до контакта.',
    tags: ['Vue 3', 'Vite', 'EmailJS', 'Firebase Hosting', 'Puppeteer', 'SPA'],
    demo: 'https://возведениеперегородок.рф/',
    github: 'https://github.com/ShadowRaze-ru/stenapro',
    images: [projectStena1, projectStena2, projectStena3],
    activeIndex: 0,
  },
])

onMounted(() => {
  const o = new IntersectionObserver(es => es.forEach(e => e.isIntersecting && e.target.classList.add('in')), { threshold: .07 })
  document.querySelectorAll('#projects .r').forEach(el => o.observe(el))
})
</script>

<style scoped>
.projects {
  padding: 110px 0;
  border-top: 1px solid var(--line);
}

.head {
  margin-bottom: 52px;
}

.heading {
  font-family: var(--font-display);
  font-weight: 700;
  font-size: clamp(3rem, 5.5vw, 5rem);
  line-height: .95;
  color: var(--white);
  margin: 14px 0 0;
}

.rule {
  width: 32px;
  height: 1px;
  background: var(--green-d);
  margin-top: 22px;
}

.list {
  display: flex;
  flex-direction: column;
  gap: 18px;
}

.card {
  transition: transform .25s ease;
}

.card:hover {
  transform: translateY(-2px);
}

.card-in {
  max-width: 1100px;
  margin: 0 auto;
  padding: 28px 28px;
  display: grid;
  grid-template-columns: 68px 1fr;
  gap: 16px;
  border: 1px solid var(--line);
  border-radius: 24px;
  background: linear-gradient(135deg, rgba(255,255,255,.03), rgba(255,255,255,.015));
  box-shadow: 0 18px 50px rgba(0,0,0,.16);
}

.card.featured .card-in {
  border-color: rgba(78,140,98,.26);
  background: linear-gradient(135deg, rgba(78,140,98,.08), rgba(255,255,255,.025));
}

.card-num {
  padding-top: 5px;
  color: var(--dim);
  font-size: .58rem;
}

.card-body {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.card-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 16px;
  flex-wrap: wrap;
}

.card-title {
  font-family: var(--font-display);
  font-weight: 700;
  font-size: clamp(1.6rem, 2.5vw, 2.1rem);
  color: var(--white);
  line-height: 1.1;
  transition: color .28s;
}

.card:hover .card-title {
  color: var(--green-l);
}

.card-sub {
  font-size: .8rem;
  color: var(--mid);
  letter-spacing: .08em;
  text-transform: uppercase;
  margin-top: 6px;
}

.award {
  display: flex;
  align-items: center;
  gap: 7px;
  color: var(--gold);
  border: 1px solid rgba(160, 124, 42, .26);
  border-radius: 999px;
  padding: 5px 12px;
  font-size: .58rem;
  white-space: nowrap;
  background: rgba(160, 124, 42, .08);
}

.preview-block {
  display: grid;
  grid-template-columns: 1.08fr .92fr;
  gap: 14px;
  align-items: stretch;
}

.image-shell {
  position: relative;
  overflow: hidden;
  border-radius: 18px;
  border: 1px solid var(--line);
  background: rgba(255,255,255,.02);
  aspect-ratio: 16 / 10;
  min-height: 220px;
}

.image-track {
  display: flex;
  transition: transform .35s ease;
}

.preview-image {
  width: 100%;
  height: 100%;
  min-width: 100%;
  object-fit: cover;
  object-position: center;
  display: block;
}

.slider-controls {
  position: absolute;
  inset: auto 12px 12px 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  pointer-events: none;
}

.slider-btn {
  width: 34px;
  height: 34px;
  border: 0;
  border-radius: 999px;
  background: rgba(6, 13, 8, .72);
  color: var(--white);
  cursor: pointer;
  pointer-events: auto;
  display: grid;
  place-items: center;
  transition: transform .2s ease, background .2s ease;
}

.slider-btn:hover {
  transform: translateY(-1px);
  background: rgba(78, 140, 98, .9);
}

.slider-dots {
  display: flex;
  gap: 7px;
  flex: 1;
  justify-content: center;
}

.slider-dot {
  width: 8px;
  height: 8px;
  border-radius: 999px;
  border: 0;
  background: rgba(255,255,255,.45);
  cursor: pointer;
  pointer-events: auto;
  transition: transform .2s ease, background .2s ease;
}

.slider-dot.active {
  background: var(--green-l);
  transform: scale(1.2);
}

.preview-copy {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.preview-item {
  padding: 14px 16px;
  border: 1px solid var(--line);
  border-radius: 16px;
  background: rgba(255,255,255,.03);
}

.preview-label {
  display: block;
  font-size: .6rem;
  letter-spacing: .16em;
  text-transform: uppercase;
  color: var(--green-l);
  margin-bottom: 8px;
}

.preview-item p {
  font-size: .84rem;
  line-height: 1.64;
  color: var(--mid);
}

.card-desc {
  font-size: .93rem;
  color: var(--mid);
  font-weight: 300;
  line-height: 1.8;
  max-width: 680px;
}

.card-foot {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 14px;
}

.card-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 7px;
}

.tag {
  padding: 5px 11px;
  border: 1px solid rgba(255,255,255,.08);
  border-radius: 999px;
  font-size: .66rem;
  letter-spacing: .04em;
  color: var(--mid);
  background: rgba(255,255,255,.025);
}

.card-links {
  display: flex;
  gap: 22px;
}

.lnk {
  font-size: .7rem;
  font-weight: 600;
  letter-spacing: .14em;
  text-transform: uppercase;
  color: var(--mid);
  transition: color .28s;
}

.lnk-l {
  color: var(--green-l);
}

.lnk:hover {
  color: var(--white);
}

@media(max-width:760px) {
  .preview-block {
    grid-template-columns: 1fr;
  }
}

@media(max-width:600px) {
  .projects {
    padding: 64px 0;
  }

  .head {
    margin-bottom: 36px;
  }

  .card-in {
    display: block;
    padding: 24px 20px;
  }

  .card-num {
    display: none;
  }

  .card-title {
    font-size: clamp(1.5rem, 6vw, 1.9rem);
  }

  .card-desc {
    font-size: .95rem;
    line-height: 1.75;
    color: var(--mid);
    max-width: 100%;
  }

  .award {
    white-space: normal;
  }

  .card-foot {
    flex-direction: column;
    align-items: flex-start;
    gap: 12px;
  }

  .lnk {
    font-size: .76rem;
  }

  .card-links {
    gap: 24px;
  }

  .tag {
    font-size: .7rem;
    padding: 5px 11px;
  }
}

@media(max-width:380px) {
  .card-in {
    padding: 24px 16px;
  }
}
</style>