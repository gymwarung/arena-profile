<template>
<main class="pt-20">
    <section class="py-16 md:py-24 bg-[#131313] relative metal-grid min-h-screen">
        <div class="max-w-screen-2xl mx-auto px-6 md:px-16 flex flex-col pt-12">

            <!-- Header Section -->
            <div class="text-center mb-12">
                <span class="font-label-caps text-brand-red text-xs uppercase tracking-[0.3em] block mb-4">[ INVENTORY ]</span>
                <h1 class="font-headline-lg text-4xl sm:text-5xl md:text-6xl uppercase italic tracking-wider text-white drop-shadow-lg">
                    KITA <span class="text-brand-red">PUNYA</span>
                </h1>
                <p class="font-body-md text-on-surface-variant text-lg mt-4 max-w-2xl mx-auto">
                    Beragam fasilitas kelas dunia yang siap memaksimalkan pengalaman latihan harian Anda.
                </p>
            </div>

            <!-- Filter Section -->
            <div class="flex flex-col sm:flex-row items-center justify-between gap-4 mb-16 max-w-screen-xl mx-auto w-full">
                <div class="flex flex-nowrap sm:flex-wrap justify-center sm:justify-start gap-1 sm:gap-3 overflow-x-auto w-full sm:w-auto pb-2 sm:pb-0">
                    <button @click="currentCategory = 'all'" :class="{ active: currentCategory === 'all' }" class="filter-btn shrink-0">Semua</button>
                    <button @click="currentCategory = 'cardio'" :class="{ active: currentCategory === 'cardio' }" class="filter-btn shrink-0">Cardio</button>
                    <button @click="currentCategory = 'strength'" :class="{ active: currentCategory === 'strength' }" class="filter-btn shrink-0">Strength</button>
                    <button @click="currentCategory = 'lainnya'" :class="{ active: currentCategory === 'lainnya' }" class="filter-btn shrink-0">Lainnya</button>
                </div>
                <div class="relative w-full sm:w-48 shrink-0">
                    <span class="material-symbols-outlined absolute left-4 top-1/2 -translate-y-1/2 text-on-surface-variant/50 text-[18px]">search</span>
                    <input type="text" v-model="searchQuery" placeholder="CARI..." class="w-full bg-[#1f1f1f] border border-white/10 text-white font-label-caps text-[10px] sm:text-xs py-2 sm:py-3 pl-10 pr-4 rounded-full focus:outline-none focus:border-brand-red transition-colors placeholder:text-on-surface-variant/30">
                </div>
            </div>

            <!-- Cards Section -->
            <div class="grid grid-cols-4 sm:grid-cols-4 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-2 sm:gap-6">
                <template v-for="facility in filteredFacilities" :key="facility.name">
                    <div class="glass-panel rounded-sm flex flex-col group cursor-default relative overflow-hidden h-36 sm:h-[360px] border border-white/10 hover:border-brand-red/60 transition-all duration-300 p-0">
                        <div class="h-20 sm:h-[240px] w-full relative overflow-hidden bg-black shrink-0">
                            <img :src="facility.img" :alt="facility.name" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500">
                            <div class="absolute inset-0 bg-gradient-to-t from-[#131313] via-transparent to-transparent opacity-80"></div>
                        </div>
                        <div class="flex flex-col p-2 sm:p-5 flex-grow justify-between relative z-10 bg-[#131313]/50">
                            <h3 class="font-headline-md text-[9px] sm:text-lg text-white tracking-wide uppercase line-clamp-2 leading-tight">
                                {{ facility.name }}
                            </h3>
                            <div class="flex items-center justify-between mt-auto pt-1 sm:pt-3 border-t border-white/10">
                                <span class="font-label-caps text-[7px] sm:text-xs text-brand-red font-bold tracking-widest">
                                    {{ facility.qty }}
                                </span>
                            </div>
                        </div>
                    </div>
                </template>
            </div>

        </div>
    </section>
</main>
</template>

<script setup>
import { ref, computed } from 'vue'

const currentCategory = ref('all')
const searchQuery = ref('')

const facilities = [
    { name: 'Treadmill', qty: '3 Unit', category: 'cardio', img: '/images/treadmill.jpeg' },
    { name: 'Spinning Bike', qty: '2 Unit', category: 'cardio', img: '/images/spinning-bike.jpeg' },
    { name: 'Samsak / Sandsack', qty: '1 Unit', category: 'cardio', img: '/images/samsak.png' },
    { name: 'Smith Machine', qty: '1 Unit', category: 'strength', img: '/images/smith-machine.jpeg' },
    { name: 'Chest Press', qty: '1 Unit', category: 'strength', img: '/images/chest-press.jpeg' },
    { name: 'Leg Curl + Leg Extension + Triceps', qty: '1 Unit', category: 'strength', img: '/images/leg-curl-extension-triceps.jpeg' },
    { name: 'Lat Pulldown', qty: '2 Unit', category: 'strength', img: '/images/lat-pulldown.jpeg' },
    { name: 'Flat Bench Press', qty: '1 Unit', category: 'strength', img: '/images/flat-bench-press.jpeg' },
    { name: 'Leg Press + Dips', qty: '1 Unit', category: 'strength', img: '/images/leg-press-dips.jpeg' },
    { name: 'Peck Deck Butterfly', qty: '1 Unit', category: 'strength', img: '/images/peck-deck-butterfly.jpeg' },
    { name: 'Abductor', qty: '1 Unit', category: 'strength', img: '/images/Abductor.jpeg' },
    { name: 'Dumbel', qty: '1-4kg & 2.5-20kg', category: 'strength', img: '/images/dumbel.jpeg' },
    { name: 'Bumper Plate Untuk Deadlift', qty: '5-20kg', category: 'strength', img: '/images/bumper-plate-deadlift.jpeg' },
    { name: 'Adjustable Bench', qty: '3 Unit', category: 'strength', img: 'https://images.unsplash.com/photo-1584863231364-2edc166de576?w=500&h=400&fit=crop' },
    { name: 'Alat Sit Up', qty: '1 Unit', category: 'strength', img: 'https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?w=500&h=400&fit=crop' },
    { name: 'Tempat Pull Up', qty: '2 Unit', category: 'strength', img: 'https://images.unsplash.com/photo-1598971639058-fab3c3109a00?w=500&h=400&fit=crop' },
    { name: 'Toilet & Loker', qty: 'Tersedia', category: 'lainnya', img: '/images/toilet-loker.jpeg' },
    { name: 'Tempat Ibadah / Sholat', qty: 'Tersedia', category: 'lainnya', img: '/images/musholla.png' },
    { name: 'Free WiFi', qty: 'Tersedia', category: 'lainnya', img: 'https://images.unsplash.com/photo-1563986768609-322da13575f3?w=500&h=400&fit=crop' },
    { name: 'Sirkulasi Udara Lancar + Kipas Angin', qty: 'Tersedia', category: 'lainnya', img: '/images/kipas.png' },
    { name: 'Warung', qty: '1 Unit', category: 'lainnya', img: '/images/warung.jpg' },
]

const filteredFacilities = computed(() => {
  return facilities.filter(f => {
    const matchCategory = currentCategory.value === 'all' || f.category === currentCategory.value
    const matchSearch = f.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    return matchCategory && matchSearch
  })
})
</script>
