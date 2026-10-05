<template>
<main class="pt-20">
    <!-- Hero Banner -->
    <div class="relative w-full h-[400px] md:h-[500px] border-b border-white/10 metal-grid bg-[#131313]">
        <div class="absolute inset-0 bg-gradient-to-t from-[#131313] via-transparent to-transparent z-10 opacity-70"></div>
        <img src="/images/team1.jpg" alt="Personal Trainer" class="w-full h-full object-cover object-center">
        <div class="absolute inset-0 flex flex-col justify-end items-center z-20 pb-16 px-6">
            <span class="font-label-caps text-brand-red text-xs uppercase tracking-[0.3em] block mb-2">[ ELITE COACHING ]</span>
            <h1 class="font-headline-lg text-4xl sm:text-6xl md:text-7xl uppercase italic tracking-tight text-white mb-2 drop-shadow-lg">
                PERSONAL <span class="text-brand-red">TRAINER</span>
            </h1>
        </div>
    </div>

    <!-- Personal Trainers Section -->
    <section class="py-16 md:py-24 bg-[#131313] relative">
        <div class="max-w-screen-2xl mx-auto px-6 md:px-16">
            <div class="mb-12 text-center md:text-left">
                <span class="font-label-caps text-brand-red text-xs uppercase tracking-[0.3em] block mb-3">[ PROFIL COACH ]</span>
                <h2 class="font-headline-md text-3xl md:text-5xl mb-4 text-white uppercase italic tracking-wider">
                    Temukan PT <span class="text-brand-red">sesuai kebutuhanmu!</span>
                </h2>
                <p class="font-body-md text-on-surface-variant text-lg md:text-xl max-w-3xl">
                    Capai tujuan fitness lebih aman, terukur, dan berkelanjutan dengan bimbingan personal trainer berpengalaman. Klik card untuk melihat profil lengkap.
                </p>
            </div>

            <!-- Cards Grid -->
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-8 max-w-4xl mx-auto">
                
                <!-- CARD GHION (TEXT ONLY) -->
                <div 
                    @click="openModal('ghion')" 
                    class="glass-panel p-6 sm:p-8 flex flex-col justify-between border border-white/10 hover:border-brand-red/70 transition-all duration-300 group cursor-pointer rounded-xl relative hover:shadow-[0_10px_35px_rgba(255,85,64,0.15)]"
                >
                    <div>
                        <!-- Header Name -->
                        <div class="mb-5 pb-5 border-b border-white/10">
                            <h3 class="font-headline-md text-3xl sm:text-4xl text-white uppercase tracking-wider m-0 leading-tight group-hover:text-brand-red transition-colors">
                                {{ ghionData.name }}
                            </h3>
                        </div>

                        <!-- Spesialisasi Tags Preview -->
                        <div class="flex flex-wrap gap-1.5 mb-5">
                            <span v-for="tag in ghionData.specialties" :key="tag" class="px-2.5 py-1 bg-white/5 border border-white/10 text-brand-red font-label-caps text-[10px] uppercase tracking-wider rounded">
                                {{ tag }}
                            </span>
                        </div>

                        <!-- Deskripsi Preview -->
                        <div class="p-4 bg-white/5 rounded-lg border border-white/5 mb-4">
                            <p class="font-body-md text-xs sm:text-sm leading-relaxed text-on-surface-variant line-clamp-3">
                                {{ ghionData.previewDesc }}
                            </p>
                        </div>
                    </div>

                    <!-- CTA Action Button -->
                    <div class="mt-6 pt-4 border-t border-white/10 flex items-center justify-between text-brand-red group-hover:text-white transition-colors">
                        <span class="font-headline-md text-xs sm:text-sm tracking-wider uppercase flex items-center gap-1.5">
                            <span class="material-symbols-outlined text-[18px]">visibility</span>
                            Buka Profil Lengkap
                        </span>
                        <span class="material-symbols-outlined text-[18px] transform group-hover:translate-x-1 transition-transform">
                            arrow_forward
                        </span>
                    </div>
                </div>

                <!-- CARD FANNY (TEXT ONLY) -->
                <div 
                    @click="openModal('fanny')" 
                    class="glass-panel p-6 sm:p-8 flex flex-col justify-between border border-white/10 hover:border-brand-red/70 transition-all duration-300 group cursor-pointer rounded-xl relative hover:shadow-[0_10px_35px_rgba(255,85,64,0.15)]"
                >
                    <div>
                        <!-- Header Name -->
                        <div class="mb-5 pb-5 border-b border-white/10">
                            <h3 class="font-headline-md text-3xl sm:text-4xl text-white uppercase tracking-wider m-0 leading-tight group-hover:text-brand-red transition-colors">
                                {{ fannyData.name }}
                            </h3>
                        </div>

                        <!-- Spesialisasi Tags Preview -->
                        <div class="flex flex-wrap gap-1.5 mb-5">
                            <span v-for="tag in fannyData.specialties" :key="tag" class="px-2.5 py-1 bg-white/5 border border-white/10 text-white/80 font-label-caps text-[10px] uppercase tracking-wider rounded">
                                {{ tag }}
                            </span>
                        </div>

                        <!-- Deskripsi Preview -->
                        <div class="p-4 bg-white/5 rounded-lg border border-white/5 mb-4">
                            <p class="font-body-md text-xs sm:text-sm leading-relaxed text-on-surface-variant italic">
                                "{{ fannyData.desc }}"
                            </p>
                        </div>
                    </div>

                    <!-- CTA Action Button -->
                    <div class="mt-6 pt-4 border-t border-white/10 flex items-center justify-between text-brand-red group-hover:text-white transition-colors">
                        <span class="font-headline-md text-xs sm:text-sm tracking-wider uppercase flex items-center gap-1.5">
                            <span class="material-symbols-outlined text-[18px]">visibility</span>
                            Buka Profil Lengkap
                        </span>
                        <span class="material-symbols-outlined text-[18px] transform group-hover:translate-x-1 transition-transform">
                            arrow_forward
                        </span>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- ========================================== -->
    <!-- POPUP MODAL: PROFIL LENGKAP COACH GHION   -->
    <!-- ========================================== -->
    <Teleport to="body">
        <Transition name="modal-fade">
            <div 
                v-if="activeModal === 'ghion'" 
                class="fixed inset-0 z-[999] flex items-center justify-center p-3 sm:p-6 bg-black/85 backdrop-blur-md"
                @click.self="closeModal"
            >
                <div class="relative w-full max-w-4xl max-h-[92vh] bg-[#141414] border border-white/15 rounded-2xl shadow-[0_0_60px_rgba(255,85,64,0.18)] flex flex-col overflow-hidden text-left animate-in fade-in zoom-in-95 duration-200">
                    
                    <!-- Modal Header (Tanpa Foto) -->
                    <div class="sticky top-0 z-20 bg-[#161616]/95 backdrop-blur-md px-6 py-4 border-b border-white/10 flex items-center justify-between">
                        <div class="flex items-center gap-3">
                            <div class="w-10 h-10 sm:w-12 sm:h-12 rounded-xl bg-brand-red/10 border border-brand-red/40 flex items-center justify-center text-brand-red shrink-0">
                                <span class="material-symbols-outlined text-[24px]">fitness_center</span>
                            </div>
                            <div>
                                <div class="flex items-center gap-2">
                                    <h3 class="font-headline-md text-lg sm:text-2xl text-white uppercase tracking-wider m-0">
                                        {{ ghionData.name }}
                                    </h3>
                                    <span class="px-2 py-0.5 bg-brand-red text-black text-[10px] font-bold rounded uppercase">
                                        {{ ghionData.age }} TAHUN
                                    </span>
                                </div>
                                <p class="text-xs text-brand-red font-medium">
                                    Personal Trainer / Fitness Coach
                                </p>
                            </div>
                        </div>

                        <!-- Close Button -->
                        <button 
                            @click="closeModal" 
                            class="p-2 rounded-full bg-white/5 hover:bg-brand-red hover:text-black text-white/70 transition-colors flex items-center justify-center"
                            title="Tutup (Esc)"
                        >
                            <span class="material-symbols-outlined text-[20px]">close</span>
                        </button>
                    </div>

                    <!-- Modal Body (Scrollable) -->
                    <div class="overflow-y-auto custom-scrollbar p-6 sm:p-8 space-y-8 text-on-surface">
                        
                        <!-- Top Summary Badge -->
                        <div class="bg-white/5 border border-white/10 p-4 rounded-xl flex flex-col sm:flex-row sm:items-center justify-between gap-3">
                            <div>
                                <span class="font-label-caps text-brand-red text-[10px] uppercase tracking-widest block mb-1">PROFIL PELATIH GYM</span>
                                <h4 class="font-headline-md text-white text-base sm:text-lg uppercase">
                                    WARGYM PERSONAL TRAINER
                                </h4>
                            </div>
                            <div class="flex flex-wrap gap-1.5">
                                <span v-for="tag in ghionData.specialties" :key="tag" class="px-2.5 py-1 bg-brand-red/10 border border-brand-red/30 text-brand-red text-xs font-semibold rounded-full">
                                    {{ tag }}
                                </span>
                            </div>
                        </div>

                        <!-- 1. TENTANG SAYA -->
                        <div class="space-y-3">
                            <div class="flex items-center gap-2 border-b border-white/10 pb-2">
                                <span class="material-symbols-outlined text-brand-red text-[20px]">person</span>
                                <h4 class="font-headline-md text-xl text-white uppercase tracking-wider">
                                    TENTANG SAYA
                                </h4>
                            </div>
                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant">
                                Saya adalah seorang Personal Trainer yang memiliki fokus pada kebugaran, kesehatan, pengelolaan berat badan, peningkatan massa otot, serta longevity—membangun tubuh yang kuat dan sehat agar dapat mendukung kualitas hidup dalam jangka panjang.
                            </p>
                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant">
                                Bagi saya, fitness bukan sekadar tentang memiliki bentuk tubuh yang ideal. Fitness adalah tentang memiliki tubuh yang kuat, aktif, sehat, dan mampu menjalani kehidupan dengan lebih baik, termasuk ketika usia terus bertambah.
                            </p>
                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant">
                                Pendekatan latihan saya menekankan program yang terukur, bertahap, konsisten, dan disesuaikan dengan kondisi serta kemampuan setiap individu.
                            </p>
                        </div>

                        <!-- 2. PERJALANAN PRIBADI: DARI KONDISI KRITIS MENUJU KEBUGARAN -->
                        <div class="bg-gradient-to-br from-[#1d1414] to-[#121212] border border-brand-red/30 p-5 sm:p-7 rounded-xl space-y-4">
                            <div class="flex items-center gap-2 text-brand-red">
                                <span class="material-symbols-outlined text-[22px]">healing</span>
                                <h4 class="font-headline-md text-lg sm:text-xl text-white uppercase tracking-wider">
                                    PERJALANAN PRIBADI: DARI KONDISI KRITIS MENUJU KEBUGARAN
                                </h4>
                            </div>

                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-white/90">
                                Perjalanan saya di dunia fitness juga lahir dari pengalaman pribadi.
                            </p>
                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant">
                                Saya pernah mengalami masa kritis akibat kondisi autoimun yang berkaitan dengan hipertiroid. Pada masa tersebut, kondisi tubuh menjadi pengingat bahwa kesehatan tidak boleh dianggap sebagai sesuatu yang otomatis kita miliki selamanya.
                            </p>
                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant">
                                Dari pengalaman itu, saya semakin memahami bahwa latihan fisik tidak bisa dilakukan secara sembarangan. Intensitas yang terlalu tinggi, program yang tidak sesuai kondisi tubuh, atau mengejar hasil secara instan bukanlah pendekatan yang saya percaya.
                            </p>
                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant">
                                Saya kemudian menjalani proses membangun kembali kebugaran secara bertahap, terukur, dan disesuaikan dengan kemampuan tubuh, dengan tetap memperhatikan penanganan medis yang diperlukan.
                            </p>
                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant">
                                Seiring waktu, kondisi kebugaran dan kemampuan fisik saya semakin membaik. Pengalaman tersebut mengubah cara pandang saya terhadap fitness. Saya belajar bahwa latihan bukan tentang seberapa berat kita mampu berlatih hari ini, tetapi tentang bagaimana kita membangun tubuh yang dapat bertahan dan berfungsi dengan baik dalam jangka panjang.
                            </p>
                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant">
                                Pengalaman pribadi inilah yang kemudian menjadi salah satu alasan saya ingin membantu orang lain menemukan cara berlatih yang lebih aman, realistis, terukur, dan berkelanjutan.
                            </p>

                            <!-- Highlight Quote -->
                            <div class="p-4 bg-brand-red/10 border-l-4 border-brand-red rounded-r-lg">
                                <p class="font-headline-md text-sm sm:text-base text-brand-red italic tracking-wide">
                                    "Saya tidak hanya mengajarkan fitness dari teori, tetapi juga dari perjalanan saya sendiri dalam membangun kembali kebugaran tubuh."
                                </p>
                            </div>
                        </div>

                        <!-- 3. SPESIALISASI -->
                        <div class="space-y-4">
                            <div class="flex items-center gap-2 border-b border-white/10 pb-2">
                                <span class="material-symbols-outlined text-brand-red text-[20px]">military_tech</span>
                                <h4 class="font-headline-md text-xl text-white uppercase tracking-wider">
                                    SPESIALISASI
                                </h4>
                            </div>

                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                                <!-- Longevity & Healthy Aging -->
                                <div class="bg-white/5 border border-white/10 p-4 rounded-xl space-y-1.5 hover:border-brand-red/50 transition-colors">
                                    <h5 class="font-headline-md text-base text-white uppercase flex items-center gap-2">
                                        <span>🧬</span> Longevity & Healthy Aging
                                    </h5>
                                    <p class="font-body-md text-xs sm:text-sm text-on-surface-variant leading-relaxed">
                                        Membangun fondasi kebugaran yang dapat membantu seseorang mempertahankan kekuatan, massa otot, mobilitas, keseimbangan, stamina, dan kemandirian fisik seiring bertambahnya usia.
                                    </p>
                                </div>

                                <!-- Fat Loss -->
                                <div class="bg-white/5 border border-white/10 p-4 rounded-xl space-y-1.5 hover:border-brand-red/50 transition-colors">
                                    <h5 class="font-headline-md text-base text-white uppercase flex items-center gap-2">
                                        <span>🔥</span> Fat Loss
                                    </h5>
                                    <p class="font-body-md text-xs sm:text-sm text-on-surface-variant leading-relaxed">
                                        Membantu klien mengurangi lemak tubuh dengan pendekatan yang menggabungkan latihan kekuatan, aktivitas fisik, pola makan yang sesuai, dan kebiasaan hidup yang dapat dipertahankan dalam jangka panjang.
                                    </p>
                                </div>

                                <!-- Muscle Building / Bulking -->
                                <div class="bg-white/5 border border-white/10 p-4 rounded-xl space-y-1.5 hover:border-brand-red/50 transition-colors">
                                    <h5 class="font-headline-md text-base text-white uppercase flex items-center gap-2">
                                        <span>💪</span> Muscle Building / Bulking
                                    </h5>
                                    <p class="font-body-md text-xs sm:text-sm text-on-surface-variant leading-relaxed">
                                        Membantu meningkatkan massa otot dan berat badan secara terarah melalui resistance training, progres latihan, pemulihan, dan strategi nutrisi yang sesuai dengan kebutuhan individu.
                                    </p>
                                </div>

                                <!-- Health & Fitness -->
                                <div class="bg-white/5 border border-white/10 p-4 rounded-xl space-y-1.5 hover:border-brand-red/50 transition-colors">
                                    <h5 class="font-headline-md text-base text-white uppercase flex items-center gap-2">
                                        <span>❤️</span> Health & Fitness
                                    </h5>
                                    <p class="font-body-md text-xs sm:text-sm text-on-surface-variant leading-relaxed">
                                        Membangun kebugaran secara menyeluruh melalui peningkatan kekuatan, daya tahan, mobilitas, koordinasi, dan kapasitas fisik untuk menunjang aktivitas sehari-hari.
                                    </p>
                                </div>

                                <!-- Strength Training (Span full on sm) -->
                                <div class="sm:col-span-2 bg-white/5 border border-white/10 p-4 rounded-xl space-y-1.5 hover:border-brand-red/50 transition-colors">
                                    <h5 class="font-headline-md text-base text-white uppercase flex items-center gap-2">
                                        <span>🏋️</span> Strength Training
                                    </h5>
                                    <p class="font-body-md text-xs sm:text-sm text-on-surface-variant leading-relaxed">
                                        Mengembangkan kekuatan dan massa otot sebagai salah satu fondasi penting untuk menjaga kemampuan fisik, terutama dalam menghadapi proses penuaan.
                                    </p>
                                </div>
                            </div>
                        </div>

                        <!-- 4. PENDEKATAN LATIHAN -->
                        <div class="space-y-4">
                            <div class="flex items-center gap-2 border-b border-white/10 pb-2">
                                <span class="material-symbols-outlined text-brand-red text-[20px]">tune</span>
                                <h4 class="font-headline-md text-xl text-white uppercase tracking-wider">
                                    PENDEKATAN LATIHAN
                                </h4>
                            </div>

                            <p class="font-body-md text-sm sm:text-base text-on-surface-variant leading-relaxed">
                                Saya percaya bahwa setiap tubuh memiliki cerita dan kebutuhan yang berbeda. Karena itu, program latihan disesuaikan dengan kondisi dan tujuan masing-masing klien, termasuk:
                            </p>

                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-2.5">
                                <div v-for="point in ghionData.approachPoints" :key="point" class="flex items-center gap-2.5 p-2.5 bg-white/5 rounded-lg border border-white/5">
                                    <span class="text-brand-red font-bold">&check;</span>
                                    <span class="text-xs sm:text-sm text-white/90">{{ point }}</span>
                                </div>
                            </div>

                            <!-- Principle Workflow -->
                            <div class="bg-black/50 border border-brand-red/30 p-4 rounded-xl text-center space-y-2">
                                <span class="font-label-caps text-brand-red text-[10px] uppercase tracking-widest block">PRINSIP KERJA</span>
                                <div class="font-headline-md text-xs sm:text-base text-white tracking-wider flex flex-wrap items-center justify-center gap-2 sm:gap-3">
                                    <span class="px-2.5 py-1 bg-white/10 rounded">Measure</span>
                                    <span class="text-brand-red">&gt;</span>
                                    <span class="px-2.5 py-1 bg-white/10 rounded">Plan</span>
                                    <span class="text-brand-red">&gt;</span>
                                    <span class="px-2.5 py-1 bg-white/10 rounded">Train</span>
                                    <span class="text-brand-red">&gt;</span>
                                    <span class="px-2.5 py-1 bg-white/10 rounded">Adapt</span>
                                    <span class="text-brand-red">&gt;</span>
                                    <span class="px-2.5 py-1 bg-brand-red text-black font-bold rounded">Progress</span>
                                </div>
                                <p class="text-xs sm:text-sm text-on-surface-variant pt-2">
                                    Latihan dimulai dari kemampuan yang dimiliki, kemudian dikembangkan secara bertahap berdasarkan respons tubuh dan perkembangan klien.
                                </p>
                            </div>
                        </div>

                        <!-- 5. FILOSOFI LATIHAN -->
                        <div class="space-y-4">
                            <div class="flex items-center gap-2 border-b border-white/10 pb-2">
                                <span class="material-symbols-outlined text-brand-red text-[20px]">psychology</span>
                                <h4 class="font-headline-md text-xl text-white uppercase tracking-wider">
                                    FILOSOFI LATIHAN
                                </h4>
                            </div>

                            <blockquote class="p-4 sm:p-5 bg-white/5 border-l-4 border-brand-red rounded-r-xl">
                                <p class="font-headline-md text-base sm:text-lg text-white italic tracking-wide">
                                    "Bukan sekadar membentuk tubuh untuk hari ini, tetapi membangun tubuh yang mampu menemani kita menjalani kehidupan lebih panjang dengan kualitas yang lebih baik."
                                </p>
                            </blockquote>

                            <p class="font-body-md text-sm sm:text-base text-on-surface-variant leading-relaxed">
                                Fitness bukan hanya mengenai six-pack, angka timbangan, atau seberapa berat beban yang dapat diangkat. Fitness adalah tentang kemampuan untuk:
                            </p>

                            <div class="grid grid-cols-2 sm:grid-cols-3 gap-3">
                                <div class="p-3 bg-white/5 rounded-lg border border-white/5 text-center">
                                    <p class="text-xs sm:text-sm font-medium text-white">Bergerak dengan baik</p>
                                </div>
                                <div class="p-3 bg-white/5 rounded-lg border border-white/5 text-center">
                                    <p class="text-xs sm:text-sm font-medium text-white">Menjadi lebih kuat</p>
                                </div>
                                <div class="p-3 bg-white/5 rounded-lg border border-white/5 text-center">
                                    <p class="text-xs sm:text-sm font-medium text-white">Memiliki stamina</p>
                                </div>
                                <div class="p-3 bg-white/5 rounded-lg border border-white/5 text-center">
                                    <p class="text-xs sm:text-sm font-medium text-white">Mempertahankan massa otot</p>
                                </div>
                                <div class="p-3 bg-white/5 rounded-lg border border-white/5 text-center">
                                    <p class="text-xs sm:text-sm font-medium text-white">Menjaga fungsi tubuh</p>
                                </div>
                                <div class="p-3 bg-white/5 rounded-lg border border-white/5 text-center">
                                    <p class="text-xs sm:text-sm font-medium text-white">Tetap mandiri & aktif seiring usia</p>
                                </div>
                            </div>

                            <p class="font-body-md text-sm sm:text-base text-on-surface-variant leading-relaxed">
                                Pengalaman saya sendiri mengajarkan bahwa kondisi tubuh dapat berubah, tetapi dengan pendekatan yang tepat, konsistensi, dan perhatian terhadap kondisi kesehatan, kita dapat terus berusaha membangun kemampuan fisik yang lebih baik.
                            </p>
                        </div>

                        <!-- 6. VISI -->
                        <div class="bg-white/5 border border-white/10 p-5 sm:p-6 rounded-xl space-y-2">
                            <span class="font-label-caps text-brand-red text-xs uppercase tracking-widest block">VISI COACH</span>
                            <h4 class="font-headline-md text-base sm:text-xl text-white uppercase tracking-wide">
                                "Membantu setiap orang membangun tubuh yang bukan hanya terlihat sehat, tetapi juga benar-benar kuat, bugar, berfungsi dengan baik, dan mampu mendukung kualitas hidup hingga usia lanjut."
                            </h4>
                        </div>

                        <!-- 7. SLOGAN & CTA BANNER -->
                        <div class="bg-gradient-to-r from-brand-red/20 via-black to-brand-red/20 border border-brand-red/40 p-6 rounded-2xl text-center space-y-3">
                            <p class="font-headline-md text-base sm:text-lg text-white/90 italic tracking-wider">
                                Train for today. Build for tomorrow. Live stronger for longer.
                            </p>
                            <h3 class="font-headline-lg text-2xl sm:text-3xl text-brand-red uppercase tracking-widest drop-shadow">
                                START A BETTER LIFE.
                            </h3>
                            <div class="pt-2">
                                <a 
                                    href="https://wa.me/6289508366293?text=Halo%20Coach%20Ghion%20WARGYM%2C%20saya%20tertarik%20untuk%20konsultasi%20program%20latihan%20Personal%20Trainer."
                                    target="_blank"
                                    class="btn-primary inline-flex items-center gap-2 py-3 px-8 text-sm tracking-widest rounded-lg shadow-lg"
                                >
                                    <span class="material-symbols-outlined text-[20px]">chat</span>
                                    KONSULTASI DENGAN COACH GHION
                                </a>
                            </div>
                        </div>

                    </div>

                    <!-- Modal Footer (Sticky) -->
                    <div class="sticky bottom-0 z-20 bg-[#161616]/95 backdrop-blur-md px-6 py-4 border-t border-white/10 flex flex-wrap items-center justify-between gap-3">
                        <span class="text-xs text-on-surface-variant font-label-caps">
                            WARGYM MOJOSONGO • PERSONAL TRAINER
                        </span>
                        <div class="flex items-center gap-3">
                            <button 
                                @click="closeModal" 
                                class="px-4 py-2 rounded border border-white/20 text-white/80 hover:text-white hover:bg-white/10 text-xs uppercase font-headline-md tracking-wider transition-colors"
                            >
                                Tutup
                            </button>
                            <a 
                                href="https://wa.me/6289508366293?text=Halo%20Coach%20Ghion%20WARGYM%2C%20saya%20tertarik%20untuk%20konsultasi%20program%20latihan%20Personal%20Trainer."
                                target="_blank"
                                class="px-5 py-2 rounded bg-brand-red text-black hover:bg-white text-xs uppercase font-headline-md tracking-wider font-bold transition-colors inline-flex items-center gap-1.5"
                            >
                                <span class="material-symbols-outlined text-[16px]">chat</span>
                                WhatsApp
                            </a>
                        </div>
                    </div>

                </div>
            </div>
        </Transition>
    </Teleport>

    <!-- ========================================== -->
    <!-- POPUP MODAL: PROFIL COACH FANNY            -->
    <!-- ========================================== -->
    <Teleport to="body">
        <Transition name="modal-fade">
            <div 
                v-if="activeModal === 'fanny'" 
                class="fixed inset-0 z-[999] flex items-center justify-center p-3 sm:p-6 bg-black/85 backdrop-blur-md"
                @click.self="closeModal"
            >
                <div class="relative w-full max-w-2xl max-h-[92vh] bg-[#141414] border border-white/15 rounded-2xl shadow-[0_0_60px_rgba(255,85,64,0.18)] flex flex-col overflow-hidden text-left animate-in fade-in zoom-in-95 duration-200">
                    
                    <!-- Modal Header (Tanpa Foto) -->
                    <div class="bg-[#161616]/95 backdrop-blur-md px-6 py-4 border-b border-white/10 flex items-center justify-between">
                        <div class="flex items-center gap-3">
                            <div class="w-10 h-10 sm:w-12 sm:h-12 rounded-xl bg-brand-red/10 border border-brand-red/40 flex items-center justify-center text-brand-red shrink-0">
                                <span class="material-symbols-outlined text-[24px]">fitness_center</span>
                            </div>
                            <div>
                                <div class="flex items-center gap-2">
                                    <h3 class="font-headline-md text-xl sm:text-2xl text-white uppercase tracking-wider m-0">
                                        {{ fannyData.name }}
                                    </h3>
                                    <span class="px-2 py-0.5 bg-brand-red text-black text-[10px] font-bold rounded uppercase">
                                        {{ fannyData.age }} TAHUN
                                    </span>
                                </div>
                                <p class="text-xs text-brand-red font-medium">Personal Trainer / Fitness Coach</p>
                            </div>
                        </div>

                        <button 
                            @click="closeModal" 
                            class="p-2 rounded-full bg-white/5 hover:bg-brand-red hover:text-black text-white/70 transition-colors flex items-center justify-center"
                            title="Tutup (Esc)"
                        >
                            <span class="material-symbols-outlined text-[20px]">close</span>
                        </button>
                    </div>

                    <!-- Modal Body -->
                    <div class="overflow-y-auto custom-scrollbar p-6 sm:p-8 space-y-6 text-on-surface">
                        <div class="space-y-3">
                            <span class="font-label-caps text-brand-red text-xs uppercase tracking-widest block">SPESIALISASI PROGRAM</span>
                            <div class="flex flex-wrap gap-1.5">
                                <span v-for="tag in fannyData.specialties" :key="tag" class="px-2.5 py-1 bg-brand-red/10 border border-brand-red/30 text-brand-red text-xs font-semibold rounded-full">
                                    {{ tag }}
                                </span>
                            </div>
                        </div>

                        <div class="space-y-3">
                            <h4 class="font-headline-md text-lg text-white uppercase tracking-wider">
                                TENTANG PROFIL COACH FANNY
                            </h4>
                            <div class="p-4 bg-white/5 border border-dashed border-white/20 rounded-xl">
                                <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant italic">
                                    "Deskripsi profil lengkap sedang dalam proses penyusunan dan akan segera diperbarui."
                                </p>
                            </div>
                            <p class="font-body-md text-sm sm:text-base leading-relaxed text-on-surface-variant">
                                Siap membantu dan mendampingi Anda dalam program latihan beban, pembentukan tubuh, peningkatan kebugaran fisik, serta panduan latihan terarah di WARGYM Mojosongo.
                            </p>
                        </div>

                        <div class="p-5 bg-white/5 border border-white/10 rounded-xl text-center space-y-3">
                            <p class="font-headline-md text-sm sm:text-base text-white">
                                Ingin konsultasi latihan privat bersama Coach Fanny?
                            </p>
                            <a 
                                href="https://wa.me/6289508366293?text=Halo%20Admin%20WARGYM%2C%20saya%20tertarik%20konsultasi%20program%20latihan%20dengan%20Coach%20Fanny."
                                target="_blank"
                                class="btn-primary inline-flex items-center gap-2 py-3 px-8 text-xs sm:text-sm tracking-widest rounded-lg"
                            >
                                <span class="material-symbols-outlined text-[18px]">chat</span>
                                KONSULTASI VIA WHATSAPP
                            </a>
                        </div>
                    </div>

                    <!-- Modal Footer -->
                    <div class="bg-[#161616]/95 backdrop-blur-md px-6 py-4 border-t border-white/10 flex justify-end">
                        <button 
                            @click="closeModal" 
                            class="px-5 py-2 rounded bg-white/10 hover:bg-white/20 text-white text-xs uppercase font-headline-md tracking-wider transition-colors"
                        >
                            Tutup
                        </button>
                    </div>

                </div>
            </div>
        </Transition>
    </Teleport>

</main>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const activeModal = ref(null)

const openModal = (id) => {
    activeModal.value = id
    if (typeof document !== 'undefined') {
        document.body.style.overflow = 'hidden'
    }
}

const closeModal = () => {
    activeModal.value = null
    if (typeof document !== 'undefined') {
        document.body.style.overflow = ''
    }
}

const handleKeydown = (e) => {
    if (e.key === 'Escape' && activeModal.value) {
        closeModal()
    }
}

onMounted(() => {
    window.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
    window.removeEventListener('keydown', handleKeydown)
    if (typeof document !== 'undefined') {
        document.body.style.overflow = ''
    }
})

// Data Coach Ghion
const ghionData = {
    name: 'GHION',
    age: 32,
    profession: 'Personal Trainer / Fitness Coach',
    specialties: ['Longevity', 'Healthy Aging', 'Fitness', 'Fat Loss', 'Muscle Building'],
    previewDesc: 'Personal Trainer yang berfokus pada kebugaran, kesehatan, pengelolaan berat badan, massa otot, serta longevity—membangun tubuh yang kuat dan sehat untuk kualitas hidup jangka panjang.',
    approachPoints: [
        'Usia dan tingkat kebugaran',
        'Pengalaman latihan',
        'Komposisi tubuh',
        'Tujuan fat loss atau muscle gain',
        'Kekuatan dan kemampuan gerak',
        'Aktivitas sehari-hari',
        'Kemampuan recovery',
        'Riwayat kondisi kesehatan yang relevan',
        'Target jangka pendek dan jangka panjang'
    ]
}

// Data Coach Fanny
const fannyData = {
    name: 'FANNY',
    age: 26,
    profession: 'Personal Trainer / Fitness Coach',
    specialties: ['Personal Trainer', 'Fitness Coach', 'Muscle Building', 'Weight Management'],
    desc: 'Deskripsi profil menyusul. Siap mendampingi dan memandu program latihan kebugaran, kekuatan, dan pembentukan tubuh Anda di WARGYM Mojosongo.'
}
</script>

<style scoped>
.modal-fade-enter-active,
.modal-fade-leave-active {
    transition: opacity 0.25s ease, transform 0.25s ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
    opacity: 0;
    transform: scale(0.96);
}

/* Custom smooth scrollbar for popup */
.custom-scrollbar::-webkit-scrollbar {
    width: 6px;
}
.custom-scrollbar::-webkit-scrollbar-track {
    background: #181818;
}
.custom-scrollbar::-webkit-scrollbar-thumb {
    background: #333;
    border-radius: 3px;
}
.custom-scrollbar::-webkit-scrollbar-thumb:hover {
    background: #ff5540;
}
</style>
