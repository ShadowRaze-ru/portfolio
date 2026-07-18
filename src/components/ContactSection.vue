<template>
  <section id="contact" class="contact">
    <div class="container">
      <div class="intro-shell">
        <div class="left">
          <span class="eyebrow r">// Контакт</span>
          <h2 class="heading r d1">Готов к новым задачам</h2>
          <div class="rule r d2"></div>
          <p class="desc r d2">
            Если нужен человек, который может взять проект от идеи до рабочего результата — пишите.
            Мне интересны реальные задачи, продуктовая логика и развитие вместе с командой.
          </p>
        </div>

        <div class="right r d2">
          <div class="panel-card links-card">
            <div class="links-head">
              <span class="eyebrow">Контакты</span>
              <p>Доступен в Telegram, GitHub и по почте.</p>
            </div>

            <div class="links-stack">
              <a v-for="l in links" :key="l.label" :href="hrefIs(l)" target="_blank" rel="noopener" class="clink">
                <span class="cl-label eyebrow">{{ l.label }}</span>
                <span class="cl-val">{{ l.val }}</span>
                <svg width="13" height="13" viewBox="0 0 14 14" fill="none">
                  <path d="M2 12L12 2M12 2H6M12 2V8" stroke="currentColor" stroke-width="1.2" stroke-linecap="round"
                    stroke-linejoin="round" />
                </svg>
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="panel-card form-card">
        <div class="form-head">
          <div class="form-badge">
            <span class="badge-dot"></span>
            <span>Отклик в течение дня</span>
          </div>
          <h3>Написать сообщение</h3>
          <p>Опишите задачу, сроки или идею — и я быстро отвечу.</p>
        </div>

        <form class="form" @submit.prevent="submitForm">
          <div class="field-row">
            <label class="field">
              <span class="field-label">Имя</span>
              <input v-model="form.name" type="text" placeholder="Как к вам обращаться" required />
            </label>
            <label class="field">
              <span class="field-label">Email</span>
              <input v-model="form.email" type="email" placeholder="you@example.com" required />
            </label>
          </div>

          <div class="field-row">
            <label class="field">
              <span class="field-label">Telegram</span>
              <input v-model="form.telegram" type="text" placeholder="необязательно" />
            </label>
            <label class="field">
              <span class="field-label">Телефон</span>
              <input v-model="form.phone" type="text" placeholder="необязательно" />
            </label>
          </div>

          <label class="field full">
            <span class="field-label">Что вы хотите сделать?</span>
            <textarea v-model="form.message" rows="5" placeholder="Опишите задачу, сроки или идею" required></textarea>
          </label>

          <div class="form-actions">
            <button class="submit-btn" :disabled="isSubmitting">
              {{ isSubmitting ? 'Отправляю…' : 'Отправить сообщение' }}
            </button>
          </div>

          <p v-if="statusMessage" class="status-msg" :class="statusType">{{ statusMessage }}</p>
        </form>
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
import { onMounted, reactive, ref } from 'vue'
import emailjs from '@emailjs/browser'

const links = [
  { label: 'GitHub', val: 'ShadowRaze-ru', href: 'https://github.com/ShadowRaze-ru' },
  { label: 'Telegram', val: '@xletx', href: 'https://t.me/xletx' },
  { label: 'Mail', val: 'usupovarthu7@gmail.com' },
  { label: 'Phone', val: '+79530375593' },
]

const form = reactive({
  name: '',
  email: '',
  telegram: '',
  phone: '',
  message: '',
})

const isSubmitting = ref(false)
const statusMessage = ref('')
const statusType = ref('')

function hrefIs(l) {
  if (l.label === 'Mail') {
    return `mailto:${l.val}`
  } else if (l.label === 'Phone') {
    return `tel:${l.val}`
  } else {
    return l.href
  }
}

function resetForm() {
  form.name = ''
  form.email = ''
  form.telegram = ''
  form.phone = ''
  form.message = ''
}

function emailConfigured() {
  const serviceId = import.meta.env.VITE_EMAILJS_SERVICE_ID?.trim() || ''
  const templateId = import.meta.env.VITE_EMAILJS_TEMPLATE_ID?.trim() || ''
  const publicKey = import.meta.env.VITE_EMAILJS_PUBLIC_KEY?.trim() || ''

  return Boolean(serviceId && templateId && publicKey && !/your_|replace|example/i.test(serviceId + templateId + publicKey))
}

async function submitForm() {
  if (!form.name.trim() || !form.email.trim() || !form.message.trim()) {
    statusMessage.value = 'Пожалуйста, заполните имя, почту и текст сообщения.'
    statusType.value = 'error'
    return
  }

  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!emailPattern.test(form.email)) {
    statusMessage.value = 'Пожалуйста, введите корректный email.'
    statusType.value = 'error'
    return
  }

  isSubmitting.value = true
  statusMessage.value = ''
  statusType.value = ''

  try {
    if (emailConfigured()) {
      await emailjs.send(
        import.meta.env.VITE_EMAILJS_SERVICE_ID,
        import.meta.env.VITE_EMAILJS_TEMPLATE_ID,
        {
          from_name: form.name.trim(),
          from_email: form.email.trim(),
          from_phone: form.phone.trim() || '—',
          from_telegram: form.telegram.trim() || '—',
          message: form.message.trim(),
          reply_to: form.email.trim(),
          to_name: 'Артур Юсупов',
        },
        import.meta.env.VITE_EMAILJS_PUBLIC_KEY,
      )

      statusMessage.value = 'Сообщение отправлено. Спасибо!'
      statusType.value = 'success'
      resetForm()
    } else {
      const subject = encodeURIComponent(`Новое сообщение с сайта от ${form.name.trim()}`)
      const body = encodeURIComponent(
        `Имя: ${form.name.trim()}\nEmail: ${form.email.trim()}\nTelegram: ${form.telegram.trim() || '—'}\nТелефон: ${form.phone.trim() || '—'}\n\n${form.message.trim()}`,
      )
      window.location.href = `mailto:usupovarthu7@gmail.com?subject=${subject}&body=${body}`
      statusMessage.value = 'Открылся почтовый клиент для отправки сообщения.'
      statusType.value = 'success'
      resetForm()
    }
  } catch (error) {
    console.error(error)
    statusMessage.value = 'Не удалось отправить сообщение. Пожалуйста, напишите напрямую на почту.'
    statusType.value = 'error'
  } finally {
    isSubmitting.value = false
  }
}

onMounted(() => {
  const o = new IntersectionObserver(es => es.forEach(e => e.isIntersecting && e.target.classList.add('in')), { threshold: .1 })
  document.querySelectorAll('#contact .r').forEach(el => o.observe(el))
})
</script>

<style scoped>
.contact {
  padding: 110px 0 0;
  border-top: 1px solid var(--line);
}

.grid {
  display: grid;
  gap: 24px;
  padding: 34px 32px 36px;
  border: 1px solid var(--line);
  border-radius: 28px;
  background: linear-gradient(135deg, rgba(255, 255, 255, .035), rgba(255, 255, 255, .02));
  box-shadow: 0 24px 60px rgba(0, 0, 0, .16);
}

.intro-shell {
  display: grid;
  grid-template-columns: 1.1fr .9fr;
  gap: 40px;
  align-items: start;
}

.heading {
  font-family: var(--font-display);
  font-weight: 700;
  font-size: clamp(3.2rem, 6vw, 5.5rem);
  line-height: .92;
  color: var(--white);
  margin: 16px 0 0;
}

.rule {
  width: 32px;
  height: 1px;
  background: var(--green-d);
  margin: 24px 0 22px;
}

.desc {
  font-size: .95rem;
  color: var(--mid);
  font-weight: 300;
  line-height: 1.78;
  margin-bottom: 26px;
}

.status {
  display: flex;
  align-items: center;
  gap: 10px;
}

.dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--green-l);
  box-shadow: 0 0 9px var(--green-l);
  animation: bl 2.8s ease infinite;
}

@keyframes bl {

  0%,
  100% {
    opacity: 1
  }

  50% {
    opacity: .2
  }
}

.right {
  display: flex;
  flex-direction: column;
  gap: 18px;
  justify-content: center;
}

.form-card {
  margin-top: 100px;
  padding: 22px 22px 20px;
  border-color: rgba(106, 171, 126, .18);
  position: relative;
  overflow: hidden;
  background: linear-gradient(145deg, rgba(10, 20, 14, .84), rgba(16, 24, 18, .72));
  box-shadow: 0 10px 28px rgba(0, 0, 0, .12);
}

.panel-card {
  padding: 22px;
  border: 1px solid var(--line);
  border-radius: 24px;
  background: linear-gradient(135deg, rgba(255, 255, 255, .045), rgba(255, 255, 255, .02));
  backdrop-filter: blur(14px);
  box-shadow: 0 12px 32px rgba(0, 0, 0, .1);
}

.form-card::before {
  content: '';
  position: absolute;
  inset: 0 0 auto 0;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(106, 171, 126, .35), transparent);
}

.form-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 5px 9px;
  border-radius: 999px;
  border: 1px solid rgba(106, 171, 126, .16);
  background: rgba(106, 171, 126, .08);
  color: var(--green-l);
  font-size: .6rem;
  letter-spacing: .16em;
  text-transform: uppercase;
}

.badge-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--green-l);
  box-shadow: 0 0 10px var(--green-l);
}

.form-head {
  margin-bottom: 20px;
  position: relative;
  z-index: 1;
}

.form-head h3 {
  margin: 10px 0 6px;
  font-family: var(--font-display);
  font-size: 1.2rem;
  color: var(--white);
}

.form-head p {
  margin-top: 6px;
  color: var(--mid);
  font-size: .9rem;
  line-height: 1.55;
}

.links-card {
  padding: 22px 22px 20px;
}

.links-head {
  margin-bottom: 14px;
}

.links-head p {
  margin-top: 8px;
  color: var(--mid);
  font-size: .9rem;
  line-height: 1.6;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.field-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 14px;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.field.full {
  width: 100%;
}

.field-label {
  margin-top: 10px;
  font-size: .72rem;
  letter-spacing: .18em;
  text-transform: uppercase;
  color: var(--dim);
}

.field input,
.field textarea {
  width: 100%;
  border: 1px solid rgba(255, 255, 255, .1);
  border-radius: 14px;
  padding: 12px 14px;
  background: rgba(255, 255, 255, .05);
  color: var(--white);
  font: inherit;
  outline: none;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, .04);
  transition: border-color .25s, box-shadow .25s, background .25s, transform .2s;
}

.field input::placeholder,
.field textarea::placeholder {
  color: var(--dim);
}

.field input:focus,
.field textarea:focus {
  border-color: rgba(106, 171, 126, .5);
  box-shadow: 0 0 0 3px rgba(106, 171, 126, .14);
  background: rgba(255, 255, 255, .08);
  transform: translateY(-1px);
}

.field textarea {
  resize: vertical;
  min-height: 108px;
}

.form-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  align-items: center;
  justify-content: space-between;
}

.submit-btn {
  border: none;
  border-radius: 999px;
  padding: 10px 16px;
  font-weight: 600;
  color: var(--bg);
  background: linear-gradient(135deg, var(--green-l), var(--green));
  cursor: pointer;
  transition: transform .2s, box-shadow .2s;
  box-shadow: 0 8px 18px rgba(78, 140, 98, .2);
}

.submit-btn:hover {
  transform: translateY(-1px);
}

.submit-btn:disabled {
  opacity: .75;
  cursor: wait;
}

.form-hint {
  color: var(--mid);
  font-size: .83rem;
  line-height: 1.5;
  max-width: 260px;
}

.status-msg {
  border-radius: 14px;
  padding: 12px 14px;
  font-size: .92rem;
}

.status-msg.success {
  background: rgba(78, 140, 98, .16);
  color: #d7f7de;
}

.status-msg.error {
  background: rgba(192, 64, 64, .16);
  color: #ffd4d4;
}

.links-stack {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.clink {
  display: grid;
  grid-template-columns: 84px 1fr auto;
  align-items: center;
  gap: 18px;
  min-height: 66px;
  padding: 18px 20px;
  border: 1px solid var(--line);
  border-radius: 16px;
  background: rgba(255, 255, 255, .03);
  transition: transform .25s, border-color .25s, background .25s;
}

.clink:hover {
  transform: translateY(-2px);
  border-color: rgba(78, 140, 98, .3);
  background: rgba(78, 140, 98, .08);
}

.cl-label {
  min-width: 76px;
  flex-shrink: 0;
}

.cl-val {
  flex: 1;
  font-size: .94rem;
  color: var(--mid);
  font-weight: 300;
  transition: color .28s;
}

.clink svg {
  color: var(--dim);
  transition: color .28s, transform .28s;
  margin-left: auto;
  flex-shrink: 0;
}

.clink:hover .cl-val {
  color: var(--white);
}

.clink:hover svg {
  color: var(--green-l);
  transform: translate(3px, -3px);
}

.footer {
  border-top: none;
  margin-top: 26px;
  padding-top: 14px;
}

.foot-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 22px 20px;
  flex-wrap: wrap;
  gap: 8px;
}

.f-name {
  font-family: var(--font-display);
  font-style: italic;
  font-size: .9rem;
  color: var(--mid);
}

.f-stack {
  color: var(--dim);
  letter-spacing: .14em;
}

@media(max-width:700px) {
  .contact {
    padding: 64px 0 0;
  }

  .grid {
    gap: 24px;
    padding: 24px 20px 28px;
  }

  .intro-shell {
    grid-template-columns: 1fr;
    gap: 24px;
  }

  .form-card {
    margin-top: 16px;
    padding: 18px;
  }

  .heading {
    font-size: clamp(2.8rem, 11vw, 4rem);
  }

  .desc {
    font-size: 1rem;
    color: var(--mid);
  }

  .field-row {
    grid-template-columns: 1fr;
  }

  .form-actions {
    align-items: flex-start;
    flex-direction: column;
  }

  .form-hint {
    max-width: none;
  }

  .panel-card {
    padding: 20px;
  }

  .form-card {
    padding: 22px;
  }

  .clink {
    padding: 16px 16px;
    gap: 14px;
  }

  .cl-label {
    min-width: 80px;
    font-size: .6rem;
  }

  .cl-val {
    font-size: .95rem;
  }

  .foot-row {
    flex-direction: column;
    gap: 4px;
  }

  .f-stack {
    font-size: .56rem;
    letter-spacing: .12em;
  }
}
</style>