<script setup>
import { computed, defineComponent, h, ref } from 'vue'

function icon(name, path) {
  return defineComponent({
    name,
    props: { size: { type: [Number, String], default: 24 } },
    setup(props, { attrs }) {
      return () => h('svg', {
        ...attrs,
        xmlns: 'http://www.w3.org/2000/svg',
        width: props.size,
        height: props.size,
        viewBox: '0 0 24 24',
        fill: 'none',
        stroke: 'currentColor',
        strokeWidth: 2,
        strokeLinecap: 'round',
        strokeLinejoin: 'round',
        'aria-hidden': 'true',
        focusable: 'false'
      }, [h('path', { d: path })])
    }
  })
}

const Accessibility = icon('Accessibility', 'M12 3a2 2 0 1 0 0 4 2 2 0 0 0 0-4ZM4 8l8 2 8-2M12 10v4m0 0-4 7m4-7 4 7m-4-7-6-2m6 2 6-2')
const ArrowRight = icon('ArrowRight', 'M5 12h14m-7-7 7 7-7 7')
const Bell = icon('Bell', 'M18 8a6 6 0 0 0-12 0c0 7-3 7-3 9h18c0-2-3-2-3-9m-8 12h4')
const Check = icon('Check', 'm5 12 4 4L19 6')
const ChevronDown = icon('ChevronDown', 'm6 9 6 6 6-6')
const ChevronRight = icon('ChevronRight', 'm9 18 6-6-6-6')
const CircleHelp = icon('CircleHelp', 'M12 22a10 10 0 1 0 0-20 10 10 0 0 0 0 20Zm-3-13a3 3 0 1 1 5.2 2c-1.1 1.1-2.2 1.2-2.2 3m0 4h.01')
const ClipboardList = icon('ClipboardList', 'M9 5H5v16h14V5h-4M9 3h6v4H9zM9 12h6m-6 4h6')
const Hand = icon('Hand', 'M8 12V6a2 2 0 0 1 4 0v5-7a2 2 0 0 1 4 0v8-5a2 2 0 0 1 4 0v8a7 7 0 0 1-7 7h-1a7 7 0 0 1-6-3l-3-4a2 2 0 0 1 3-3l2 2')
const HeartHandshake = icon('HeartHandshake', 'M20.8 4.6a5.5 5.5 0 0 0-7.8 0L12 5.7l-1.1-1.1a5.5 5.5 0 0 0-7.8 7.8l1.1 1.1L12 21l4.3-4.3m-7-4.2 2-2a2 2 0 0 1 2.8 0l.4.4a2 2 0 0 0 2.8 0l2.1-2.1m-9.6 5 1.4-1.4m1.4 2.8 1.4-1.4m1.4 2.8 1.4-1.4')
const MapPin = icon('MapPin', 'M20 10c0 5-8 12-8 12S4 15 4 10a8 8 0 1 1 16 0Zm-5 0a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z')
const Menu = icon('Menu', 'M4 6h16M4 12h16M4 18h16')
const Mic = icon('Mic', 'M12 2a3 3 0 0 0-3 3v7a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3Zm-7 10a7 7 0 0 0 14 0m-7 7v3m-4 0h8')
const Navigation = icon('Navigation', 'm3 11 18-8-8 18-2-8-8-2Z')
const Search = icon('Search', 'm21 21-4.3-4.3m2.3-5.7a8 8 0 1 1-16 0 8 8 0 0 1 16 0Z')
const Settings = icon('Settings', 'M12 8a4 4 0 1 0 0 8 4 4 0 0 0 0-8Zm0-6v3m0 14v3m10-10h-3M5 12H2m17.1-7.1-2.1 2.1M7 17l-2.1 2.1m14.2 0L17 17M7 7 4.9 4.9')
const ShieldCheck = icon('ShieldCheck', 'M12 22s8-4 8-11V5l-8-3-8 3v6c0 7 8 11 8 11Zm-4-11 3 3 5-5')
const Sparkles = icon('Sparkles', 'm12 3 1.9 5.8L20 11l-6.1 2.2L12 19l-1.9-5.8L4 11l6.1-2.2L12 3Zm7 11 1.2 2.8L23 18l-2.8 1.2L19 22l-1.2-2.8L15 18l2.8-1.2L19 14ZM5 2l1 2 2 1-2 1-1 2-1-2-2-1 2-1 1-2Z')
const Star = icon('Star', 'm12 3 2.7 5.5 6.1.9-4.4 4.3 1 6.1-5.4-2.9-5.4 2.9 1-6.1-4.4-4.3 6.1-.9L12 3Z')
const Text = icon('Text', 'M4 6V4h16v2M12 4v16m-4 0h8')
const Volume2 = icon('Volume2', 'M11 5 6 9H3v6h3l5 4V5Zm5 4a5 5 0 0 1 0 6m3-9a9 9 0 0 1 0 12')
const Waves = icon('Waves', 'M2 8c2.5 0 2.5-2 5-2s2.5 2 5 2 2.5-2 5-2 2.5 2 5 2M2 13c2.5 0 2.5-2 5-2s2.5 2 5 2 2.5-2 5-2 2.5 2 5 2m-20 5c2.5 0 2.5-2 5-2s2.5 2 5 2 2.5-2 5-2 2.5 2 5 2')
const X = icon('X', 'm18 6-12 12M6 6l12 12')

const active = ref('translator')
const mobileMenu = ref(false)
const mode = ref('sign')
const phrase = ref('Good morning, how can I help you?')
const signResults = ref([])
const searchingSigns = ref(false)
const signSearchMessage = ref('')
const signSearchError = ref('')
const query = ref('')
const filters = ref(['Ramps', 'OKU Parking'])
const guideId = ref('card')
const checked = ref(['MyKad'])
const nav = [{ id: 'translator', label: 'Sign translator', short: 'Translate', icon: Hand }, { id: 'map', label: 'Accessible places', short: 'Explore', icon: MapPin }, { id: 'jkm', label: 'JKM benefits & guides', short: 'Benefits', icon: HeartHandshake }]
const filterOptions = ['Ramps', 'OKU Parking', 'Accessible Restrooms', 'Elevators']
const places = [
  { name: 'Central Market Kuala Lumpur', type: 'Shopping · 2 access features', distance: '0.4 km', rating: '4.9', reviews: 28, tags: ['Ramps', 'OKU Parking', 'Accessible Restrooms'], color: 'bg-emerald-100 text-emerald-800', initials: 'CM' },
  { name: 'Kuala Lumpur City Gallery', type: 'Attraction · 3 access features', distance: '0.8 km', rating: '4.8', reviews: 16, tags: ['Ramps', 'Elevators'], color: 'bg-amber-100 text-amber-800', initials: 'KG' },
  { name: 'Merdeka Square', type: 'Outdoor · 2 access features', distance: '1.2 km', rating: '4.6', reviews: 34, tags: ['Ramps', 'Accessible Restrooms'], color: 'bg-sky-100 text-sky-800', initials: 'MS' }
]
const results = computed(() => places.filter(p => `${p.name} ${p.type}`.toLowerCase().includes(query.value.toLowerCase()) && (!filters.value.length || filters.value.some(f => p.tags.includes(f)))))
const guides = [
  { id: 'card', icon: Accessibility, title: 'Apply for your OKU Card', category: 'APPLICATION GUIDE', description: 'A step-by-step guide to registering as a person with disabilities in Malaysia.', color: 'bg-violet-100 text-violet-700', steps: ['Get the OKU registration form (BPPOKU) from JKM or download it online.', 'Have the relevant medical professional complete the verification section.', 'Submit the completed form and supporting documents to your nearest JKM office.'], requirements: ['MyKad', 'Recent photo', 'Medical verification'] },
  { id: 'allowance', icon: ClipboardList, title: 'Disabled Worker Allowance', category: 'ELAUN PEKERJA OKU', description: 'Monthly financial support for registered OKU individuals who are working.', color: 'bg-teal-100 text-teal-700', steps: ['Confirm you have a valid OKU card and meet current income criteria.', 'Prepare proof of employment and a recent payslip.', 'Submit an application through your district JKM office.'], requirements: ['OKU Card', 'Proof of employment', 'Bank account details'] },
  { id: 'job', icon: ShieldCheck, title: 'Job Coach support', category: 'EMPLOYMENT SUPPORT', description: 'Workplace guidance and support to help you thrive in a suitable job.', color: 'bg-orange-100 text-orange-700', steps: ['Contact your state JKM office to ask about Job Coach services.', 'Share your work interests and the support you need.', 'Work with a Job Coach to plan your workplace support.'], requirements: ['OKU Card', 'MyKad'] },
  { id: 'care', icon: HeartHandshake, title: 'Care & support services', category: 'COMMUNITY CARE', description: 'Find community and residential care options for you and your family.', color: 'bg-rose-100 text-rose-700', steps: ['Talk with your district JKM officer about suitable care options.', 'Bring relevant medical or care information to your appointment.', 'Review available services and next steps together.'], requirements: ['MyKad', 'Medical information'] }
]
const selectedGuide = computed(() => guides.find(g => g.id === guideId.value) || guides[0])
function toggleFilter(item) { filters.value = filters.value.includes(item) ? filters.value.filter(f => f !== item) : [...filters.value, item] }
function toggleCheck(item) { checked.value = checked.value.includes(item) ? checked.value.filter(i => i !== item) : [...checked.value, item] }
function youtubeVideoId(url) {
  try {
    const parsed = new URL(url)
    let id = ''
    if (parsed.hostname === 'youtu.be') id = parsed.pathname.slice(1)
    else if (parsed.hostname === 'youtube.com' || parsed.hostname === 'www.youtube.com') {
      id = parsed.pathname === '/watch' ? parsed.searchParams.get('v') || '' : parsed.pathname.startsWith('/embed/') ? parsed.pathname.split('/')[2] : ''
    }
    return /^[\w-]{11}$/.test(id) ? id : ''
  } catch {
    return ''
  }
}
function clearSignResults() {
  signResults.value = []
  signSearchMessage.value = ''
  signSearchError.value = ''
}
async function searchSigns() {
  const words = [...new Set(phrase.value.match(/[\p{L}\p{N}]+/gu) || [])].slice(0, 8)
  signResults.value = []
  signSearchMessage.value = ''
  signSearchError.value = ''
  if (!words.length) {
    signSearchMessage.value = 'Enter an English or Malay word to look up its BIM sign.'
    return
  }

  searchingSigns.value = true
  try {
    const params = new URLSearchParams()
    let filterIndex = 0
    for (const word of words) {
      for (const field of ['Word', 'Perkataan']) {
        params.set(`filters[$or][${filterIndex}][${field}][$containsi]`, word)
        filterIndex += 1
      }
    }
    params.set('pagination[pageSize]', '50')
    params.set('populate', 'category_group')

    const response = await fetch(`https://api.bimsignbank.org/api/bims?${params}`)
    if (!response.ok) throw new Error(`BIM Sign Bank returned an error (${response.status}).`)
    const payload = await response.json()
    if (!Array.isArray(payload.data)) throw new Error('BIM Sign Bank returned an unexpected response.')

    const records = new Map()
    for (const sign of payload.data) {
      if (!sign.Word && !sign.Perkataan) continue
      const key = sign.documentId || sign.id
      if (!records.has(key)) records.set(key, sign)
    }
    signResults.value = [...records.values()].slice(0, 12)
    if (!signResults.value.length) signSearchMessage.value = 'No matching signs found. Try a different English or Malay word.'
  } catch (error) {
    signSearchError.value = error instanceof Error ? error.message : 'Unable to reach BIM Sign Bank. Please try again.'
  } finally {
    searchingSigns.value = false
  }
}
</script>

<template>
  <div class="min-h-screen bg-[#f7f8fa] text-slate-900">
    <aside class="fixed inset-y-0 left-0 z-30 hidden w-[252px] flex-col border-r border-slate-200 bg-white lg:flex">
      <a href="#main" class="flex items-center gap-3 px-7 py-7"><span class="grid h-11 w-11 place-items-center rounded-2xl bg-teal-800 text-white"><Accessibility :size="25" /></span><span><b class="block text-xl">Akses<span class="text-teal-700">Kita</span></b><span class="text-xs text-slate-500">A more accessible Malaysia</span></span></a>
      <div class="px-5 pt-5"><p class="px-3 pb-3 text-[11px] font-bold uppercase tracking-widest text-slate-400">Your toolkit</p><nav aria-label="Main navigation" class="space-y-1"><button v-for="item in nav" :key="item.id" @click="active = item.id" :aria-current="active === item.id ? 'page' : undefined" class="flex min-h-12 w-full items-center gap-3 rounded-xl px-3 text-left text-sm font-semibold" :class="active === item.id ? 'bg-teal-50 text-teal-900' : 'text-slate-600 hover:bg-slate-50'"><component :is="item.icon" :size="19"/>{{ item.label }}</button></nav></div>
      <div class="mt-auto p-5"><div class="rounded-2xl bg-[#f0f7f6] p-4"><CircleHelp class="text-teal-800" :size="22"/><p class="mt-3 text-sm font-bold">Need a hand?</p><p class="mt-1 text-xs leading-5 text-slate-600">We're here to help you find the right support.</p><button class="mt-3 text-sm font-bold text-teal-800 underline">Visit help centre <ArrowRight class="inline" :size="14"/></button></div><button class="mt-4 flex min-h-11 items-center gap-3 px-3 text-sm font-semibold text-slate-600"><Settings :size="18"/> Settings</button></div>
    </aside>
    <header class="sticky top-0 z-20 flex h-[68px] items-center justify-between border-b border-slate-200 bg-white/95 px-4 sm:px-7 lg:ml-[252px] lg:px-10">
      <div class="flex items-center gap-3"><button @click="mobileMenu = !mobileMenu" class="grid h-10 w-10 place-items-center rounded-xl hover:bg-slate-100 lg:hidden" :aria-label="mobileMenu ? 'Close menu' : 'Open menu'"><Menu v-if="!mobileMenu" :size="21"/><X v-else :size="21"/></button><a href="#main" class="font-extrabold lg:hidden">Akses<span class="text-teal-700">Kita</span></a><p class="hidden text-sm text-slate-500 sm:block">A more accessible Malaysia, together.</p></div>
      <div class="flex items-center gap-3"><button class="relative grid h-10 w-10 place-items-center rounded-xl text-slate-600 hover:bg-slate-100" aria-label="Notifications"><Bell :size="19"/><span class="absolute right-2 top-2 h-2 w-2 rounded-full bg-orange-500 ring-2 ring-white"/></button><div class="grid h-9 w-9 place-items-center rounded-full bg-amber-100 text-sm font-bold text-amber-900" aria-label="Aina's profile">AR</div><span class="hidden text-sm font-semibold sm:block">Hi, Aina</span></div>
    </header>
    <div v-if="mobileMenu" class="fixed inset-0 z-40 bg-slate-950/30 lg:hidden" @click.self="mobileMenu = false"><nav class="h-full w-[min(82vw,320px)] bg-white p-5" aria-label="Mobile navigation"><div class="mb-7 flex justify-between font-bold">Explore AksesKita<button @click="mobileMenu = false" aria-label="Close menu"><X/></button></div><button v-for="item in nav" :key="item.id" @click="active = item.id; mobileMenu = false" class="mb-1 flex min-h-12 w-full items-center gap-3 rounded-xl px-3 text-left font-semibold" :class="active === item.id ? 'bg-teal-50 text-teal-900' : 'text-slate-700'"><component :is="item.icon" :size="20"/>{{ item.label }}</button></nav></div>

    <main id="main" class="mx-auto max-w-[1440px] px-4 pb-28 pt-7 sm:px-7 sm:pt-9 lg:ml-[252px] lg:px-10 lg:pb-12">
      <section v-if="active === 'translator'" aria-labelledby="page-title">
        <div class="mb-7 flex flex-col justify-between gap-4 sm:flex-row sm:items-end"><div><div class="mb-2 flex items-center gap-2 text-xs font-bold uppercase tracking-widest text-teal-800"><Waves :size="15"/> Communication, made easier</div><h1 id="page-title" class="text-2xl font-extrabold tracking-tight sm:text-[32px]">Sign language translator</h1><p class="mt-2 max-w-2xl text-sm leading-6 text-slate-600 sm:text-base">A little more understanding goes a long way. Translate between sign and text in either direction.</p></div><button class="inline-flex min-h-11 items-center gap-2 self-start rounded-xl border border-slate-200 bg-white px-4 text-sm font-bold text-slate-700"><CircleHelp :size="17"/> How it works</button></div>
        <div class="mb-5 inline-flex rounded-xl border border-slate-200 bg-white p-1" role="tablist" aria-label="Translation direction"><button @click="mode = 'sign'" role="tab" :aria-selected="mode === 'sign'" class="flex min-h-10 items-center gap-2 rounded-lg px-4 text-sm font-bold" :class="mode === 'sign' ? 'bg-teal-800 text-white' : 'text-slate-600'"><Hand :size="17"/> Sign to text</button><button @click="mode = 'text'" role="tab" :aria-selected="mode === 'text'" class="flex min-h-10 items-center gap-2 rounded-lg px-4 text-sm font-bold" :class="mode === 'text' ? 'bg-teal-800 text-white' : 'text-slate-600'"><Text :size="17"/> Text to sign</button></div>
        <div v-if="mode === 'sign'" class="grid gap-5 xl:grid-cols-[1.35fr_.85fr]"><section class="overflow-hidden rounded-2xl border border-slate-200 bg-white shadow-sm"><div class="flex flex-wrap items-center justify-between gap-3 border-b border-slate-100 px-5 py-4"><div><h2 class="font-bold">Sign to text</h2><p class="mt-1 text-xs text-slate-500">Position your hands inside the guide</p></div><span class="inline-flex items-center gap-2 rounded-full bg-emerald-50 px-3 py-1.5 text-xs font-bold text-emerald-800"><span class="h-2 w-2 rounded-full bg-emerald-500"/> Camera ready</span></div><div class="relative m-4 grid min-h-[270px] place-items-center overflow-hidden rounded-xl bg-[#182a31] sm:min-h-[350px]"><div class="absolute inset-0 opacity-20" style="background-image:linear-gradient(rgba(255,255,255,.16) 1px,transparent 1px),linear-gradient(90deg,rgba(255,255,255,.16) 1px,transparent 1px);background-size:32px 32px"></div><div class="absolute h-52 w-44 rounded-[48%] border border-dashed border-teal-300/60 sm:h-64 sm:w-56"></div><svg class="relative z-10 h-52 w-48 text-teal-200/90 sm:h-64 sm:w-60" viewBox="0 0 220 240" fill="none" aria-label="Hand tracking skeleton guide"><path d="M108 213c-18-2-31-14-36-31L55 135c-4-11 11-18 17-8l16 24-14-78c-2-14 16-17 19-3l13 60-1-103c0-14 19-14 19 0l3 99 10-79c2-14 21-11 19 3l-8 82 18-54c5-13 23-6 18 7l-25 91c-7 24-28 39-52 37z" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/><path d="m55 135 25 23m28-28 1 36m18-38-1 39m21-28-8 34m24-13-13 20" stroke="currentColor" stroke-dasharray="3 5"/><circle cx="108" cy="213" r="3" fill="currentColor"/><circle cx="55" cy="135" r="3" fill="currentColor"/><circle cx="92" cy="78" r="3" fill="currentColor"/><circle cx="105" cy="134" r="3" fill="currentColor"/><circle cx="127" cy="129" r="3" fill="currentColor"/><circle cx="149" cy="137" r="3" fill="currentColor"/><circle cx="174" cy="135" r="3" fill="currentColor"/></svg><div class="absolute bottom-4 text-center text-xs text-white/70">Hand tracking guide · Bahasa Isyarat Malaysia (BIM)</div></div><div class="flex flex-wrap items-center justify-between gap-3 px-5 pb-5"><p class="text-xs text-slate-500">● Good lighting · Hands in frame</p><button class="inline-flex min-h-11 items-center gap-2 rounded-xl bg-teal-800 px-4 text-sm font-bold text-white hover:bg-teal-900"><Mic :size="17"/> Start translating</button></div></section><section class="flex flex-col rounded-2xl border border-slate-200 bg-white p-5 shadow-sm"><div class="flex items-center justify-between"><div><h2 class="font-bold">Live translation</h2><p class="mt-1 text-xs text-slate-500">Translated text appears here</p></div><span class="rounded-lg bg-slate-100 px-2.5 py-1.5 text-xs font-bold text-slate-600">EN</span></div><div class="mt-5 flex flex-1 flex-col justify-center rounded-xl bg-[#f2f8f7] p-5 sm:min-h-[220px]"><span class="mb-3 flex items-center gap-2 text-xs font-bold uppercase tracking-wide text-teal-800"><Sparkles :size="15"/> Detected phrase</span><p class="text-2xl font-bold leading-snug">Good morning, how can I help you?</p><p class="mt-3 text-sm text-slate-600">Bahasa Isyarat Malaysia (BIM)</p></div><div class="mt-4 flex flex-wrap items-center gap-2"><button class="inline-flex min-h-11 items-center gap-2 rounded-xl border border-slate-200 px-4 text-sm font-bold text-slate-700"><Volume2 :size="17"/> Listen</button><button class="min-h-11 rounded-xl px-4 text-sm font-bold text-teal-800">Copy text</button><span class="ml-auto text-xs text-slate-500">Updated just now</span></div></section></div>
        <section v-else class="rounded-2xl border border-slate-200 bg-white p-5 shadow-sm sm:p-7"><h2 class="text-lg font-bold">Look up BIM signs</h2><p class="mt-1 text-sm text-slate-600">Search the BIM Sign Bank vocabulary in English or Malay. Lookups show individual signs; they do not translate sentence grammar.</p><label for="phrase" class="mb-2 mt-5 block text-sm font-bold">Words to look up</label><div class="flex flex-col gap-3 sm:flex-row"><textarea id="phrase" v-model="phrase" @input="clearSignResults" rows="2" class="min-h-14 flex-1 rounded-xl border border-slate-300 px-4 py-3 text-base focus:border-teal-700 focus:outline-none focus:ring-2 focus:ring-teal-700/20" placeholder="Try: gift, family, or hadiah"/><button @click="searchSigns" :disabled="searchingSigns" :aria-busy="searchingSigns" class="inline-flex min-h-12 items-center justify-center gap-2 rounded-xl bg-teal-800 px-5 text-sm font-bold text-white hover:bg-teal-900 disabled:cursor-wait disabled:opacity-70"><ArrowRight :size="17"/>{{ searchingSigns ? 'Searching…' : 'Find BIM signs' }}</button></div><div class="mt-7 flex flex-wrap items-center justify-between gap-2 border-t border-slate-100 pt-5"><h3 class="font-bold">Matching signs <span v-if="signResults.length" class="text-sm font-medium text-slate-500">({{ signResults.length }} shown)</span></h3><a href="https://bimsignbank.org/home" target="_blank" rel="noopener noreferrer" class="text-sm font-bold text-teal-800 underline">Browse BIM Sign Bank</a></div><p v-if="searchingSigns" role="status" class="mt-4 text-sm text-slate-600">Searching the BIM Sign Bank…</p><p v-else-if="signSearchError" role="alert" class="mt-4 rounded-xl bg-rose-50 p-4 text-sm font-medium text-rose-800">{{ signSearchError }}</p><p v-else-if="signSearchMessage" role="status" class="mt-4 text-sm text-slate-600">{{ signSearchMessage }}</p><div v-if="signResults.length" class="mt-4 grid gap-4 sm:grid-cols-2 xl:grid-cols-3"><article v-for="sign in signResults" :key="sign.documentId || sign.id" class="overflow-hidden rounded-xl border border-slate-200 bg-white"><iframe v-if="youtubeVideoId(sign.Video)" :src="`https://www.youtube-nocookie.com/embed/${youtubeVideoId(sign.Video)}`" :title="`${sign.Word || sign.Perkataan} — BIM sign`" class="aspect-video w-full bg-slate-100" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen/><div v-else class="grid aspect-video place-items-center bg-slate-100 px-4 text-sm text-slate-500">No video is available for this entry.</div><div class="p-4"><h4 class="font-bold">{{ sign.Word || sign.Perkataan }}</h4><p v-if="sign.Perkataan && sign.Word" class="mt-1 text-sm text-slate-600">{{ sign.Perkataan }}</p><p v-if="sign.category_group?.GroupCategory" class="mt-2 text-xs text-slate-500">{{ sign.category_group.GroupCategory }}</p><a v-if="youtubeVideoId(sign.Video)" :href="`https://www.youtube.com/watch?v=${youtubeVideoId(sign.Video)}`" target="_blank" rel="noopener noreferrer" class="mt-3 inline-flex min-h-10 items-center text-sm font-bold text-teal-800 underline">Watch original video</a></div></article></div><p class="mt-5 text-xs leading-5 text-slate-500">Vocabulary and videos are provided by <a class="font-semibold text-teal-800 underline" href="https://bimsignbank.org/about-us" target="_blank" rel="noopener noreferrer">BIM Sign Bank by the Malaysia Federation of the Deaf (MFD)</a>. Videos remain hosted by YouTube and are not copied into this app.</p></section>
      </section>

      <section v-else-if="active === 'map'" aria-labelledby="page-title"><div class="mb-7"><div class="mb-2 flex items-center gap-2 text-xs font-bold uppercase tracking-widest text-teal-800"><Navigation :size="15"/> Go with confidence</div><h1 id="page-title" class="text-2xl font-extrabold tracking-tight sm:text-[32px]">Accessible places near you</h1><p class="mt-2 text-sm text-slate-600 sm:text-base">Find places with access features that work for you.</p></div><div class="mb-4 flex flex-col gap-3 md:flex-row"><label class="relative block flex-1"><Search class="absolute left-4 top-1/2 -translate-y-1/2 text-slate-500" :size="18"/><input v-model="query" type="search" aria-label="Search places" placeholder="Search a place or area" class="min-h-12 w-full rounded-xl border border-slate-300 bg-white pl-11 pr-4 text-sm focus:border-teal-700 focus:outline-none focus:ring-2 focus:ring-teal-700/20"/></label><button class="inline-flex min-h-12 items-center justify-center gap-2 rounded-xl border border-slate-300 bg-white px-4 text-sm font-bold text-slate-700"><MapPin :size="17"/> Kuala Lumpur <ChevronDown :size="15"/></button></div><div class="mb-5 flex gap-2 overflow-x-auto pb-1" aria-label="Filter places"><button v-for="filter in filterOptions" :key="filter" @click="toggleFilter(filter)" :aria-pressed="filters.includes(filter)" class="min-h-10 shrink-0 rounded-full border px-4 text-sm font-semibold" :class="filters.includes(filter) ? 'border-teal-800 bg-teal-800 text-white' : 'border-slate-300 bg-white text-slate-700'"><span v-if="filters.includes(filter)">✓ </span>{{ filter }}</button></div><div class="grid items-start gap-5 xl:grid-cols-[1.1fr_.9fr]"><section class="overflow-hidden rounded-2xl border border-slate-200 bg-white shadow-sm"><div class="relative min-h-[310px] overflow-hidden bg-[#e8f0e9] sm:min-h-[430px]" aria-label="Illustrative map of central Kuala Lumpur"><div class="absolute inset-0 opacity-80" style="background-image:linear-gradient(25deg,transparent 45%,#fff 46%,#fff 50%,transparent 51%),linear-gradient(105deg,transparent 42%,#fff 43%,#fff 47%,transparent 48%),linear-gradient(165deg,transparent 56%,#fff 57%,#fff 61%,transparent 62%),linear-gradient(70deg,transparent 23%,#d5e5db 24%,#d5e5db 34%,transparent 35%);background-size:220px 170px,250px 230px,280px 190px,100% 100%"></div><span class="absolute left-[6%] top-[14%] rounded bg-white/80 px-2 py-1 text-[10px] font-semibold text-slate-500">JALAN TUN PERAK</span><span class="absolute right-[9%] top-[32%] rounded bg-white/80 px-2 py-1 text-[10px] font-semibold text-slate-500">JALAN RAJA</span><div class="absolute left-[49%] top-[38%] grid h-12 w-12 place-items-center rounded-full border-4 border-white bg-teal-800 text-white shadow-lg"><MapPin :size="22"/></div><div class="absolute left-[23%] top-[55%] grid h-10 w-10 place-items-center rounded-full border-4 border-white bg-violet-700 text-white shadow-lg"><MapPin :size="17"/></div><div class="absolute right-[20%] top-[26%] grid h-10 w-10 place-items-center rounded-full border-4 border-white bg-orange-600 text-white shadow-lg"><MapPin :size="17"/></div><div class="absolute bottom-4 left-4 rounded-xl bg-white px-3 py-2 text-xs font-semibold text-slate-700 shadow"><span class="mr-1 text-teal-700">●</span> Central Kuala Lumpur</div><button class="absolute bottom-4 right-4 grid h-11 w-11 place-items-center rounded-xl bg-white text-slate-700 shadow" aria-label="Center map on my location"><Navigation :size="19"/></button></div><div class="flex items-center justify-between gap-3 border-t border-slate-100 px-4 py-3 text-xs text-slate-500"><span>Map illustration · Community reported</span><button class="font-bold text-teal-800">Report a place</button></div></section><section><div class="mb-3 flex items-center justify-between"><h2 class="font-bold">Nearby places <span class="text-sm font-medium text-slate-500">({{ results.length }})</span></h2><button class="text-sm font-bold text-teal-800">Sort by <ChevronDown class="inline" :size="14"/></button></div><div v-if="results.length" class="space-y-3"><article v-for="place in results" :key="place.name" class="rounded-2xl border border-slate-200 bg-white p-4 shadow-sm"><div class="flex gap-3"><div class="grid h-12 w-12 shrink-0 place-items-center rounded-xl text-sm font-extrabold" :class="place.color">{{ place.initials }}</div><div class="min-w-0 flex-1"><div class="flex items-start justify-between gap-2"><h3 class="font-bold leading-5">{{ place.name }}</h3><span class="shrink-0 text-xs text-slate-500">{{ place.distance }}</span></div><p class="mt-1 text-xs text-slate-500">{{ place.type }}</p><div class="mt-2 flex items-center gap-1 text-sm font-bold"><Star class="fill-amber-400 text-amber-500" :size="15"/>{{ place.rating }} <span class="font-normal text-slate-500">({{ place.reviews }} reviews)</span></div></div></div><div class="mt-3 flex flex-wrap gap-1.5"><span v-for="tag in place.tags" :key="tag" class="rounded-full bg-slate-100 px-2.5 py-1 text-[11px] font-semibold text-slate-700">{{ tag }}</span></div><button class="mt-3 inline-flex min-h-9 items-center gap-1 text-sm font-bold text-teal-800">View details <ArrowRight :size="15"/></button></article></div><div v-else class="rounded-2xl border border-dashed border-slate-300 bg-white p-7 text-center"><p class="font-bold">No places match your search</p><p class="mt-1 text-sm text-slate-600">Try another search or update your filters.</p><button @click="query = ''; filters = []" class="mt-3 text-sm font-bold text-teal-800 underline">Clear filters</button></div></section></div></section>

      <section v-else aria-labelledby="page-title"><div class="mb-7"><div class="mb-2 flex items-center gap-2 text-xs font-bold uppercase tracking-widest text-teal-800"><HeartHandshake :size="15"/> Support that meets you where you are</div><h1 id="page-title" class="text-2xl font-extrabold tracking-tight sm:text-[32px]">JKM benefits & guides</h1><p class="mt-2 max-w-2xl text-sm leading-6 text-slate-600 sm:text-base">Explore support from Malaysia's Department of Social Welfare (JKM), with simple steps to help you get started.</p></div><div class="mb-6 flex items-start gap-3 rounded-2xl border border-sky-200 bg-sky-50 p-4"><span class="grid h-9 w-9 shrink-0 place-items-center rounded-xl bg-white text-sky-800"><CircleHelp :size="19"/></span><div><p class="text-sm font-bold">A helpful place to start</p><p class="mt-1 text-sm leading-5 text-slate-700">Eligibility and requirements can change. Confirm details with your nearest JKM district office before applying.</p></div></div><div class="grid items-start gap-5 xl:grid-cols-[.8fr_1.2fr]"><div class="grid gap-3 sm:grid-cols-2 xl:grid-cols-1"><button v-for="guide in guides" :key="guide.id" @click="guideId = guide.id" :aria-expanded="guideId === guide.id" class="rounded-2xl border bg-white p-4 text-left shadow-sm" :class="guideId === guide.id ? 'border-teal-700 ring-1 ring-teal-700' : 'border-slate-200'"><div class="flex items-start gap-3"><span class="grid h-11 w-11 shrink-0 place-items-center rounded-xl" :class="guide.color"><component :is="guide.icon" :size="21"/></span><span class="min-w-0 flex-1"><span class="block text-[10px] font-extrabold tracking-widest text-slate-500">{{ guide.category }}</span><span class="mt-1 block font-bold leading-5">{{ guide.title }}</span><span class="mt-1 block text-xs leading-5 text-slate-600">{{ guide.description }}</span></span><ChevronRight class="mt-1 shrink-0 text-slate-400" :size="18"/></div></button></div><article class="rounded-2xl border border-slate-200 bg-white p-5 shadow-sm sm:p-6"><div class="flex items-start gap-3 border-b border-slate-100 pb-5"><span class="grid h-12 w-12 shrink-0 place-items-center rounded-xl" :class="selectedGuide.color"><component :is="selectedGuide.icon" :size="23"/></span><div><p class="text-[10px] font-extrabold tracking-widest text-teal-800">{{ selectedGuide.category }}</p><h2 class="mt-1 text-xl font-extrabold">{{ selectedGuide.title }}</h2><p class="mt-1 text-sm leading-5 text-slate-600">{{ selectedGuide.description }}</p></div></div><div class="grid gap-6 pt-5 sm:grid-cols-2"><div><h3 class="mb-4 text-sm font-bold">Your next steps</h3><ol class="space-y-4"><li v-for="(step, i) in selectedGuide.steps" :key="step" class="flex gap-3"><span class="grid h-7 w-7 shrink-0 place-items-center rounded-full bg-teal-50 text-xs font-extrabold text-teal-800">{{ i + 1 }}</span><p class="pt-1 text-sm leading-5 text-slate-700">{{ step }}</p></li></ol></div><div><h3 class="mb-3 text-sm font-bold">Document checklist</h3><p class="mb-3 text-xs text-slate-500">Tap to mark what you have ready.</p><label v-for="item in selectedGuide.requirements" :key="item" class="mb-2 flex min-h-11 cursor-pointer items-center gap-3 rounded-xl border px-3 text-sm font-medium" :class="checked.includes(item) ? 'border-teal-200 bg-teal-50 text-teal-900' : 'border-slate-200 text-slate-700'"><input type="checkbox" :checked="checked.includes(item)" @change="toggleCheck(item)" class="h-4 w-4 rounded accent-teal-800"/><span class="flex-1">{{ item }}</span><Check v-if="checked.includes(item)" :size="16"/></label></div></div><div class="mt-5 flex flex-col justify-between gap-3 rounded-xl bg-[#f3f7f6] p-4 sm:flex-row sm:items-center"><div><p class="text-sm font-bold">Need help with your application?</p><p class="mt-1 text-xs text-slate-600">Your nearest JKM office can guide you through the process.</p></div><button class="inline-flex min-h-11 shrink-0 items-center justify-center gap-2 rounded-xl bg-teal-800 px-4 text-sm font-bold text-white">Find a JKM office <ArrowRight :size="16"/></button></div></article></div><p class="mt-5 text-xs leading-5 text-slate-500">General information only; this is not an official JKM application. Contact JKM for current eligibility, forms and processing information.</p></section>
    </main>
    <nav class="fixed inset-x-0 bottom-0 z-30 grid grid-cols-3 border-t border-slate-200 bg-white px-2 pb-[env(safe-area-inset-bottom)] pt-2 shadow-[0_-4px_16px_rgba(15,23,42,.05)] lg:hidden" aria-label="Primary navigation"><button v-for="item in nav" :key="item.id" @click="active = item.id" :aria-current="active === item.id ? 'page' : undefined" class="flex min-h-[58px] flex-col items-center justify-center gap-1 rounded-xl text-[11px] font-bold" :class="active === item.id ? 'text-teal-800' : 'text-slate-500'"><component :is="item.icon" :size="20"/><span>{{ item.short }}</span></button></nav>
  </div>
</template>
