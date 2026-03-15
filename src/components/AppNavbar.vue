<template>
  <header class="nav" :class="{solid:scrolled}">
    <div class="container nav-in">
      <a class="brand" href="#hero" @click.prevent="go('#hero')">
        <img src="@/assets/img/kodama.jpg" class="bimg" alt="" />
        <span class="bname">Arthur Yusupov</span>
      </a>
      <nav class="links">
        <a v-for="l in nav" :key="l.id" :href="'#'+l.id" @click.prevent="go('#'+l.id)">{{ l.ru }}</a>
      </nav>
      <button class="burger" :class="{x:open}" @click="open=!open" aria-label="Меню">
        <span/><span/>
      </button>
    </div>
    <div class="mob" :class="{open}">
      <a v-for="l in nav" :key="l.id" :href="'#'+l.id"
         @click.prevent="go('#'+l.id);open=false">{{ l.ru }}</a>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
const scrolled=ref(false), open=ref(false)
const nav=[{id:'about',ru:'О себе'},{id:'skills',ru:'Стек'},{id:'projects',ru:'Проекты'},{id:'contact',ru:'Контакт'}]
function go(h){document.querySelector(h)?.scrollIntoView({behavior:'smooth'});open.value=false}
const fn=()=>scrolled.value=scrollY>40
onMounted(()=>addEventListener('scroll',fn))
onUnmounted(()=>removeEventListener('scroll',fn))
</script>

<style scoped>
.nav{position:fixed;inset:0 0 auto;z-index:500;padding:20px 0;transition:background .4s,border-color .4s,padding .4s}
.nav.solid{background:rgba(6,13,8,.93);backdrop-filter:blur(18px);border-bottom:1px solid var(--line);padding:13px 0}
.nav-in{display:flex;align-items:center;justify-content:space-between}
.brand{display:flex;align-items:center;gap:10px}
.bimg{width:28px;height:28px;border-radius:50%;object-fit:cover;filter:grayscale(1) brightness(.55);border:1px solid var(--dim)}
.bname{font-size:.8rem;letter-spacing:.06em;color:var(--mid);transition:color .3s}
.brand:hover .bname{color:var(--white)}
.links{display:flex;gap:32px}
.links a{font-size:.68rem;font-weight:500;letter-spacing:.18em;text-transform:uppercase;color:var(--mid);transition:color .3s;position:relative}
.links a::after{content:'';position:absolute;left:0;bottom:-3px;width:0;height:1px;background:var(--green-l);transition:width .3s}
.links a:hover{color:var(--white)}.links a:hover::after{width:100%}

.burger{display:none;flex-direction:column;gap:6px;background:none;border:none;cursor:pointer;padding:4px}
.burger span{display:block;width:20px;height:1px;background:var(--mid);transition:all .32s;transform-origin:center}
.burger.x span:first-child{transform:translateY(3.5px) rotate(45deg)}
.burger.x span:last-child{transform:translateY(-3.5px) rotate(-45deg)}

.mob{
  display:none;flex-direction:column;gap:0;
  background:rgba(6,13,8,.97);
  border-top:1px solid var(--line);
  max-height:0;overflow:hidden;
  transition:max-height .4s ease;
}
.mob.open{max-height:320px;}
.mob a{
  display:block;
  font-size:.9rem;font-weight:500;letter-spacing:.14em;text-transform:uppercase;
  color:var(--mid);transition:color .3s, background .3s;
  padding:16px 20px;
  border-bottom:1px solid var(--line2);
}
.mob a:last-child{border-bottom:none;}
.mob a:hover{color:var(--green-l);background:rgba(78,140,98,.05);}

@media(max-width:700px){
  .links{display:none}
  .burger{display:flex}
  .mob{display:flex}
}
</style>