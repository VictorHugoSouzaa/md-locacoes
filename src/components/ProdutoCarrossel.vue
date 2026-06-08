<template>
	<section class="mb-12">

		<!-- Cabeçalho da categoria -->
		<div class="flex items-center gap-3 mb-4">
			<div class="w-1 h-6 bg-yellow-400 rounded-full shrink-0"></div>
			<h3 class="font-black text-blue-900 text-sm md:text-base uppercase tracking-tighter">{{ titulo }}</h3>
			<div v-if="items.length > 1" class="flex items-center gap-1.5 ml-1">
				<button @click="prev" :disabled="isBeginning"
					class="w-7 h-7 rounded-full border-2 border-blue-800 text-blue-800 flex items-center justify-center hover:bg-blue-800 hover:text-white transition-all disabled:opacity-20 disabled:cursor-not-allowed text-base font-bold leading-none select-none">
					‹
				</button>
				<button @click="next" :disabled="isEnd"
					class="w-7 h-7 rounded-full border-2 border-blue-800 text-blue-800 flex items-center justify-center hover:bg-blue-800 hover:text-white transition-all disabled:opacity-20 disabled:cursor-not-allowed text-base font-bold leading-none select-none">
					›
				</button>
			</div>
		</div>

		<!-- Carrossel -->
		<Swiper
			:slides-per-view="2"
			:space-between="12"
			:breakpoints="{
				500:  { slidesPerView: 2.4, spaceBetween: 14 },
				640:  { slidesPerView: 3,   spaceBetween: 16 },
				900:  { slidesPerView: 4,   spaceBetween: 18 },
				1200: { slidesPerView: 5,   spaceBetween: 20 },
				1500: { slidesPerView: 6,   spaceBetween: 20 },
			}"
			@swiper="onSwiper"
			@slideChange="onSlideChange"
			style="overflow: visible;"
		>
			<SwiperSlide v-for="item in items" :key="item.id" style="height: auto;">
				<div class="bg-white rounded-xl border border-gray-100 shadow-sm hover:shadow-lg hover:-translate-y-0.5 transition-all duration-200 flex flex-col h-full group cursor-default overflow-hidden">

					<!-- Imagem -->
					<div class="bg-gray-50 flex items-center justify-center p-3" style="height: 140px;">
						<img
							:src="item.src"
							:alt="item.nome"
							class="max-h-full max-w-full object-contain mix-blend-multiply group-hover:scale-105 transition-transform duration-300"
						/>
					</div>

					<!-- Conteúdo -->
					<div class="p-3 flex flex-col flex-1 gap-2">
						<h3 class="font-extrabold text-blue-900 uppercase text-[11px] leading-tight line-clamp-2">
							{{ item.nome }}
						</h3>
						<p class="text-slate-500 text-[11px] leading-relaxed line-clamp-2 flex-1">
							{{ item.descricao }}
						</p>
						<button
							@click="$emit('consultar', item)"
							class="w-full bg-blue-800 hover:bg-blue-700 active:scale-95 text-white font-bold uppercase text-[10px] py-2 rounded-lg transition-all tracking-wide mt-auto">
							Consultar
						</button>
					</div>
				</div>
			</SwiperSlide>
		</Swiper>

	</section>
</template>

<script setup>
import { ref } from 'vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';

defineProps({
	titulo: { type: String, required: true },
	items: { type: Array, required: true },
});

defineEmits(['consultar']);

const swiperRef = ref(null);
const isBeginning = ref(true);
const isEnd = ref(false);

const onSwiper = (swiper) => {
	swiperRef.value = swiper;
	isBeginning.value = swiper.isBeginning;
	isEnd.value = swiper.isEnd;
};

const onSlideChange = (swiper) => {
	isBeginning.value = swiper.isBeginning;
	isEnd.value = swiper.isEnd;
};

const prev = () => swiperRef.value?.slidePrev();
const next = () => swiperRef.value?.slideNext();
</script>
