<template>
    <main class="site">
        <header class="header">
            <a class="logo" href="#home"><span class="logo-icon">f</span> foundly<span class="period">.</span></a>
            <nav aria-label="Main navigation">
                <a class="nav-active" href="#home">Home</a>
                <a href="#items">Browse items</a>
                <a href="#how-it-works">How it works</a>
            </nav>
            <div class="header-buttons">
                <button class="sign-in" type="button">Sign in</button>
                <a class="post-button" href="#report">＋ <span>Post an item</span></a>
            </div>
        </header>

        <section id="home" class="hero">
            <div class="hero-copy">
                <div class="eyebrow"><span>✳</span> A LITTLE HELP GOES A LONG WAY</div>
                <h1>Lost something?<br />Let’s <em>bring it home.</em></h1>
                <p class="intro">A little kindness can turn a lost day around. Find what’s missing or help someone reconnect with what they love.</p>
                <form class="search" @submit.prevent="scrollToItems">
                    <span class="search-icon" aria-hidden="true">⌕</span>
                    <input v-model="searchQuery" type="search" aria-label="Search items" placeholder="Try “keys”, “backpack”..." />
                    <button type="submit">Search</button>
                </form>
                <div class="popular"><span>Popular:</span><button v-for="tag in popularTags" :key="tag" type="button" @click="searchQuery = tag">{{ tag }}</button></div>
            </div>
            <div class="hero-visual" aria-label="A cheerful lost-and-found box illustration">
                <div class="sun"></div><span class="star star-a">✦</span><span class="star star-b">✳</span>
                <div class="float-card float-top"><span class="float-icon">⌕</span><span><b>Found near you</b><small>New items every day</small></span></div>
                <div class="drawing">
                    <div class="plant plant-a"><i></i><i></i><i></i><b></b></div>
                    <div class="box-back"></div><div class="book"></div><div class="bottle"></div><div class="cap"></div>
                    <div class="box"><div class="slot"></div><div class="box-text">LOST<br /><b>&amp; FOUND</b></div></div>
                    <div class="plant plant-b"><i></i><i></i><i></i><b></b></div>
                </div>
                <div class="float-card float-bottom"><span class="heart">♥</span><span><b>Good things find their way</b><small>One community, looking out</small></span></div>
            </div>
        </section>

        <section class="stats" aria-label="Community impact">
            <div class="stats-intro"><i></i> Small finds. Big relief.</div>
            <div class="stat"><b>2,480<span>+</span></b><small>items reunited</small></div>
            <div class="stat"><b>850<span>+</span></b><small>kind neighbors</small></div>
            <div class="stat"><b>24<span>h</span></b><small>average return</small></div>
            <div class="neighbors"><span class="avatars"><i>J</i><i>M</i><i>A</i></span><span>Join your local<br /><b>good-neighbor network</b></span></div>
        </section>

        <section id="items" class="items-section">
            <div class="section-heading"><div><div class="kicker">THE COMMUNITY BOARD</div><h2>Recently found <span>near you</span></h2></div><a href="#report" class="view-all">View all items <b>↗</b></a></div>
            <div class="filters" aria-label="Filter items by category">
                <button v-for="category in categories" :key="category" :class="{ chosen: selectedCategory === category }" type="button" @click="selectedCategory = category">{{ category }}</button>
            </div>
            <div class="item-grid">
                <article v-for="item in filteredItems" :key="item.id" class="item-card">
                    <div class="item-image" :class="item.color">
                        <span class="item-emoji" aria-hidden="true">{{ item.emoji }}</span>
                        <span class="found"><i></i> Found</span>
                        <button class="favorite" type="button" :aria-label="savedItems.includes(item.id) ? 'Remove from saved items' : 'Save item'" @click="toggleSaved(item.id)">{{ savedItems.includes(item.id) ? '♥' : '♡' }}</button>
                    </div>
                    <div class="item-details"><div class="item-name"><h3>{{ item.name }}</h3><span>{{ item.category }}</span></div><p>⌖ {{ item.location }} <i>·</i> {{ item.time }}</p><button class="claim" type="button">Is this yours? <b>→</b></button></div>
                </article>
                <p v-if="filteredItems.length === 0" class="empty">No items match your search. Try another keyword or category.</p>
            </div>
        </section>

        <section id="how-it-works" class="callout">
            <div class="callout-copy"><span class="callout-icon">✦</span><span><b>Found something that isn’t yours?</b><small>Be someone’s favorite person today.</small></span></div>
            <a id="report" href="mailto:hello@foundly.example?subject=Found%20item">Report a found item <b>→</b></a>
        </section>
        <footer><span>© 2024 foundly. Made for the moments that matter.</span><span>Kindness looks good on you <b>♥</b></span></footer>
    </main>
</template>

<script setup>
import { computed, ref } from 'vue'

const searchQuery = ref('')
const selectedCategory = ref('All items')
const savedItems = ref([])
const categories = ['All items', 'Electronics', 'Accessories', 'Bags', 'Other']
const popularTags = ['Keys', 'Water bottle', 'Wallet']
const items = [
    { id: 1, name: 'Wireless headphones', category: 'Electronics', location: 'Maple Street Café', time: '2 hours ago', emoji: '🎧', color: 'lilac' },
    { id: 2, name: 'Canvas tote bag', category: 'Bags', location: 'Riverside Park', time: '5 hours ago', emoji: '👜', color: 'peach' },
    { id: 3, name: 'Silver keyring', category: 'Accessories', location: 'Central Library', time: 'Yesterday', emoji: '🔑', color: 'mint' },
    { id: 4, name: 'Green water bottle', category: 'Other', location: 'Oakwood Gym', time: 'Yesterday', emoji: '🧴', color: 'butter' }
]

const filteredItems = computed(() => {
    const query = searchQuery.value.trim().toLowerCase()
    return items.filter((item) => {
        const categoryMatch = selectedCategory.value === 'All items' || item.category === selectedCategory.value
        const queryMatch = !query || `${item.name} ${item.category} ${item.location}`.toLowerCase().includes(query)
        return categoryMatch && queryMatch
    })
})

function toggleSaved(id) {
    savedItems.value = savedItems.value.includes(id)
        ? savedItems.value.filter((savedId) => savedId !== id)
        : [...savedItems.value, id]
}

function scrollToItems() {
    document.querySelector('#items')?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Manrope:wght@400;500;600;700;800&display=swap');

:global(*) { box-sizing: border-box; }
:global(body) { margin: 0; background: #fbfaf7; }
.site { max-width: 1440px; min-height: 100vh; margin: 0 auto; padding: 0 7.2%; color: #263d32; font-family: 'DM Sans', sans-serif; }
.header { height: 84px; display: flex; align-items: center; justify-content: space-between; border-bottom: 1px solid #eeeee8; }
.logo { display: inline-flex; align-items: center; gap: 9px; color: #263d32; font: 800 23px 'Manrope', sans-serif; letter-spacing: -1px; text-decoration: none; }
.logo-icon { display: grid; width: 32px; height: 32px; place-items: center; border-radius: 10px; background: #285f49; color: #fff; font-size: 22px; }.period { margin-left: -9px; color: #e4a36c; }
nav { display: flex; align-items: center; align-self: stretch; gap: 36px; }nav a { position: relative; display: flex; align-items: center; color: #80877f; font-size: 12px; font-weight: 600; text-decoration: none; }nav a:hover, nav a.nav-active { color: #285f49; }nav a.nav-active::after { position: absolute; right: 0; bottom: 0; left: 0; height: 2px; background: #285f49; content: ''; }
.header-buttons { display: flex; align-items: center; gap: 19px; }.sign-in { border: 0; background: none; color: #526258; font: 600 12px 'DM Sans', sans-serif; cursor: pointer; }.post-button { padding: 11px 15px; border-radius: 6px; background: #285f49; color: white; font-size: 12px; font-weight: 600; text-decoration: none; }.post-button:hover, .search button:hover { background: #1e4d39; }
.hero { display: grid; grid-template-columns: 1fr 1fr; align-items: center; gap: 38px; padding: 37px 0 30px; }.hero-copy { padding: 10px 0; }.eyebrow, .kicker { color: #899385; font-size: 9px; font-weight: 700; letter-spacing: 1.4px; }.eyebrow { display: flex; align-items: center; gap: 8px; }.eyebrow span { display: grid; width: 23px; height: 23px; place-items: center; border-radius: 50%; background: #e8efe7; color: #4e805a; font-size: 14px; }
h1 { margin: 18px 0 13px; color: #263d32; font: 800 clamp(38px, 4.3vw, 57px)/1.12 'Manrope', sans-serif; letter-spacing: -2.5px; }h1 em { color: #528765; font-style: normal; }.intro { max-width: 410px; margin: 0 0 23px; color: #7c857c; font-size: 12px; line-height: 1.8; }
.search { display: flex; align-items: center; max-width: 465px; height: 52px; padding: 5px 6px 5px 14px; border: 1px solid #e9e9e2; border-radius: 8px; background: #fff; box-shadow: 0 7px 23px #243b3108; }.search-icon { color: #789080; font-size: 25px; }.search input { flex: 1; min-width: 0; padding: 0 9px; border: 0; outline: 0; color: #34463d; font: 12px 'DM Sans', sans-serif; }.search input::placeholder { color: #a3aaa4; }.search button { height: 40px; padding: 0 20px; border: 0; border-radius: 6px; background: #285f49; color: white; font: 600 11px 'DM Sans', sans-serif; cursor: pointer; }
.popular { display: flex; align-items: center; gap: 7px; margin-top: 13px; color: #a0a69f; font-size: 9px; }.popular button { padding: 5px 9px; border: 1px solid #e9ebe4; border-radius: 20px; background: transparent; color: #78827a; font: 9px 'DM Sans', sans-serif; cursor: pointer; }.popular button:hover { border-color: #7d9b83; color: #285f49; }
.hero-visual { position: relative; display: grid; min-height: 345px; place-items: center; overflow: hidden; border-radius: 46% 44% 9px 9px; background: #f1f0e8; }.sun { position: absolute; top: 31px; right: 61px; width: 81px; height: 81px; border-radius: 50%; background: #e7d5a8; }.star { position: absolute; z-index: 2; color: #c6975b; }.star-a { top: 52px; left: 67px; font-size: 23px; }.star-b { top: 118px; right: 41px; color: #83a184; font-size: 16px; }
.drawing { position: relative; width: 260px; height: 235px; margin-top: 55px; }.box-back { position: absolute; bottom: 17px; left: 33px; width: 194px; height: 158px; background: #b9764c; clip-path: polygon(0 0,100% 0,87% 100%,13% 100%); }.box { position: absolute; bottom: 17px; left: 46px; width: 169px; height: 137px; border-radius: 2px 2px 8px 8px; background: #cc8a5d; box-shadow: inset 0 -8px #bd7950; }.box::before { position: absolute; top: -16px; left: -8px; width: 185px; height: 26px; background: #dfa477; clip-path: polygon(8% 0,92% 0,100% 100%,0 100%); content: ''; }.slot { position: absolute; top: 16px; left: 63px; width: 43px; height: 4px; border-radius: 5px; background: #a96843; }.box-text { position: absolute; top: 45px; left: 50px; color: #fff1d9; font: 500 11px/1.3 'Manrope', sans-serif; letter-spacing: 2px; text-align: center; }.box-text b { font-size: 8px; letter-spacing: 1px; }
.book { position: absolute; z-index: 1; top: 49px; left: 73px; width: 54px; height: 81px; border: 4px solid #f2d9a6; border-radius: 4px; background: #86a38a; box-shadow: 4px 2px #daab72; transform: rotate(-11deg); }.book::after { position: absolute; top: 23px; left: 11px; width: 23px; height: 2px; background: #dce3c8; content: ''; }.bottle { position: absolute; z-index: 1; top: 33px; right: 48px; width: 31px; height: 79px; border: 4px solid #f3eee0; border-radius: 8px 8px 12px 12px; background: #91aa8c; transform: rotate(10deg); }.bottle::before { position: absolute; top: -12px; left: 6px; width: 11px; height: 11px; border-radius: 3px 3px 0 0; background: #dca477; content: ''; }.cap { position: absolute; z-index: 2; top: 8px; left: 122px; width: 56px; height: 30px; border-radius: 30px 30px 7px 7px; background: #e5b971; transform: rotate(9deg); }.cap::after { position: absolute; right: -11px; bottom: 0; width: 27px; height: 8px; border-radius: 0 10px 10px 0; background: #d9a961; content: ''; }
.plant { position: absolute; z-index: 2; bottom: 9px; width: 44px; height: 80px; }.plant b { position: absolute; bottom: 0; left: 3px; width: 37px; height: 28px; border-radius: 4px 4px 10px 10px; background: #d6a478; }.plant i { position: absolute; bottom: 24px; left: 17px; width: 14px; height: 33px; border-radius: 100% 0 100% 0; background: #779176; transform: rotate(-23deg); }.plant i:nth-child(2) { left: 3px; bottom: 34px; transform: rotate(-55deg) scale(.8); }.plant i:nth-child(3) { left: 23px; bottom: 47px; transform: rotate(15deg) scale(.75); }.plant-a { left: 0; transform: scale(.8); }.plant-b { right: 0; transform: scale(.86); }.plant-b i { background: #8ba080; }
.float-card { position: absolute; z-index: 3; display: flex; align-items: center; gap: 9px; padding: 10px 12px; border: 1px solid #efeee9; border-radius: 8px; background: #fffefa; box-shadow: 0 8px 22px #33351e12; }.float-card b, .float-card small { display: block; white-space: nowrap; }.float-card b { color: #425348; font-size: 9px; }.float-card small { margin-top: 3px; color: #9a9f97; font-size: 8px; }.float-top { top: 48px; left: 16px; }.float-bottom { right: 13px; bottom: 20px; }.float-icon, .heart { display: grid; width: 28px; height: 28px; place-items: center; border-radius: 8px; background: #eaf1e8; color: #588264; font-size: 17px; }.heart { background: #f8e9dc; color: #d5875f; font-size: 12px; }
.stats { display: flex; min-height: 82px; align-items: center; justify-content: space-between; padding: 0 20px; border: 1px solid #edeee8; border-radius: 9px; background: white; }.stats-intro { display: flex; align-items: center; gap: 8px; color: #58685e; font-size: 10px; font-weight: 600; }.stats-intro i, .found i { width: 7px; height: 7px; border-radius: 50%; background: #70a578; }.stat { display: flex; flex-direction: column; gap: 3px; padding-left: 22px; border-left: 1px solid #eeefe9; }.stat b { color: #315b45; font: 800 16px 'Manrope', sans-serif; }.stat b span { color: #d09a67; font-size: 11px; }.stat small { color: #929991; font-size: 8px; }.neighbors { display: flex; align-items: center; gap: 9px; color: #939b93; font-size: 8px; line-height: 1.6; }.neighbors b { color: #53675b; font-weight: 600; }.avatars { display: flex; padding-left: 5px; }.avatars i { display: grid; width: 25px; height: 25px; margin-left: -5px; place-items: center; border: 2px solid white; border-radius: 50%; background: #d4a187; color: white; font-size: 8px; font-style: normal; }.avatars i:nth-child(2) { background: #83a18a; }.avatars i:nth-child(3) { background: #d1ae70; }
.items-section { padding: 43px 0 28px; }.section-heading { display: flex; align-items: end; justify-content: space-between; }.kicker { margin-bottom: 8px; color: #9a9e91; font-size: 8px; letter-spacing: 1.5px; }h2 { margin: 0; color: #243b31; font: 800 24px 'Manrope', sans-serif; letter-spacing: -.8px; }h2 span { color: #7a8c7c; font-weight: 500; }.view-all { color: #53745e; font-size: 10px; font-weight: 600; text-decoration: none; }.view-all b { margin-left: 5px; }.filters { display: flex; gap: 8px; margin: 19px 0 16px; }.filters button { padding: 7px 12px; border: 1px solid #e9ebe4; border-radius: 20px; background: transparent; color: #7e887f; font: 9px 'DM Sans', sans-serif; cursor: pointer; }.filters button.chosen, .filters button:hover { border-color: #285f49; background: #285f49; color: white; }
.item-grid { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 15px; }.item-card { overflow: hidden; border: 1px solid #eeeee8; border-radius: 9px; background: white; transition: transform .2s, box-shadow .2s; }.item-card:hover { transform: translateY(-3px); box-shadow: 0 10px 24px #243b310e; }.item-image { position: relative; display: grid; height: 129px; place-items: center; overflow: hidden; }.item-image::before, .item-image::after { position: absolute; width: 100px; height: 100px; border: 1px solid #ffffff58; border-radius: 50%; content: ''; }.item-image::before { top: -57px; left: -23px; }.item-image::after { right: -37px; bottom: -72px; width: 135px; height: 135px; }.lilac { background: #e9e5ed; }.peach { background: #f2e5da; }.mint { background: #e5ece2; }.butter { background: #f0eddb; }.item-emoji { z-index: 1; display: grid; width: 72px; height: 72px; place-items: center; border: 1px solid #ffffffa3; border-radius: 22px; background: #ffffff8a; box-shadow: 0 8px 17px #44432712; font-size: 36px; transform: rotate(-5deg); }.found { position: absolute; z-index: 2; top: 9px; left: 9px; display: flex; align-items: center; gap: 5px; padding: 5px 7px; border-radius: 20px; background: white; color: #66766a; font-size: 8px; font-weight: 600; }.found i { width: 5px; height: 5px; }.favorite { position: absolute; z-index: 2; top: 8px; right: 9px; display: grid; width: 26px; height: 26px; place-items: center; border: 0; border-radius: 50%; background: #ffffffd9; color: #68766c; font-size: 16px; cursor: pointer; }.favorite:hover { color: #cf7768; }.item-details { padding: 11px 12px 12px; }.item-name { display: flex; align-items: center; justify-content: space-between; gap: 5px; }.item-name h3 { overflow: hidden; margin: 0; color: #34483c; font: 700 10px 'Manrope', sans-serif; text-overflow: ellipsis; white-space: nowrap; }.item-name span { flex-shrink: 0; color: #a0a69e; font-size: 8px; }.item-details p { margin: 7px 0 9px; color: #949c94; font-size: 8px; }.item-details p:first-letter { color: #7b9a7f; }.item-details p i { padding: 0 3px; font-style: normal; }.claim { padding: 0; border: 0; background: transparent; color: #4f795b; font: 600 9px 'DM Sans', sans-serif; cursor: pointer; }.claim b { padding-left: 3px; }.empty { grid-column: 1 / -1; padding: 28px; border: 1px dashed #dfe5dc; border-radius: 9px; color: #7e887f; font-size: 12px; text-align: center; }
.callout { display: flex; align-items: center; justify-content: space-between; margin: 4px 0 21px; padding: 14px 19px; border-radius: 9px; background: #edf2eb; }.callout-copy { display: flex; align-items: center; gap: 11px; }.callout-icon { display: grid; width: 34px; height: 34px; place-items: center; border-radius: 9px; background: #dce8dc; color: #4e805a; font-size: 18px; }.callout-copy b, .callout-copy small { display: block; }.callout-copy b { color: #405a49; font-size: 10px; }.callout-copy small { margin-top: 4px; color: #89958a; font-size: 8px; }.callout > a { padding: 10px 13px; border-radius: 6px; background: white; color: #4f7158; font-size: 9px; font-weight: 600; text-decoration: none; }.callout > a b { padding-left: 5px; }footer { display: flex; justify-content: space-between; padding-bottom: 20px; color: #a0a49d; font-size: 8px; }footer b { color: #ce8c71; }
@media (max-width: 850px) { .site { padding: 0 5%; }nav { gap: 20px; }.hero { gap: 20px; }.stats { padding: 0 12px; }.stat { padding-left: 12px; }.item-grid { gap: 10px; }.item-details { padding: 10px 8px; } }
@media (max-width: 650px) { .site { padding: 0 19px; }.header { height: 69px; }nav { display: none; }.header-buttons { gap: 12px; }.post-button { padding: 10px 12px; }.hero { grid-template-columns: 1fr; gap: 24px; padding: 34px 0 25px; }.hero-visual { min-height: 310px; }.stats { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; padding: 17px; }.stats-intro, .neighbors { grid-column: 1 / -1; }.item-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }.item-image { height: 140px; }.items-section { padding-top: 37px; } }
@media (max-width: 400px) { .site { padding: 0 14px; }.logo { font-size: 21px; }.logo-icon { width: 29px; height: 29px; }.sign-in { font-size: 11px; }.post-button { padding: 9px; font-size: 10px; }.hero-visual { min-height: 280px; }.drawing { transform: scale(.85); }.float-card { padding: 8px; }.float-card b { font-size: 8px; }.float-card small { font-size: 7px; }.section-heading { align-items: start; gap: 8px; }h2 { font-size: 20px; }.view-all { margin-top: 20px; white-space: nowrap; font-size: 9px; }.filters { overflow-x: auto; padding-bottom: 3px; }.filters button { flex-shrink: 0; }.item-image { height: 120px; }.item-name { align-items: flex-start; flex-direction: column; gap: 3px; }.callout { gap: 8px; padding: 12px; }.callout > a { flex-shrink: 0; padding: 9px; font-size: 8px; }footer { gap: 10px; font-size: 7px; } }
</style>