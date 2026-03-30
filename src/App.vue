<template>
	<div class="min-h-screen bg-slate-50 font-sans text-slate-900 flex flex-col">
		<header class="bg-white py-10 px-6 flex flex-col items-center border-b-4 border-yellow-500 shadow-md w-full relative">
			<div class="h-32 mb-6 w-full flex items-center justify-center">
				<img src="/logo-md.png" alt="M&D Locações" class="h-full object-contain max-w-[80%]" @error="logoError = true" v-if="!logoError" />
				<h2 v-else class="text-4xl font-black text-blue-800 tracking-tighter border-4 border-blue-800 p-2 rounded">M&D LOCAÇÕES</h2>
			</div>

			<h1 class="text-blue-800 font-black text-center text-2xl md:text-4xl uppercase tracking-tighter leading-tight max-w-4xl">
				Tudo em <span class="bg-blue-800 text-white px-2">equipamentos</span> para sua <br />
				obra ou <span class="text-blue-600">reforma.</span>
			</h1>
		</header>

		<main class="w-full flex-grow py-12 px-6 md:px-12">
			<div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6 md:gap-8 max-w-[1920px] mx-auto">
				<div
					v-for="item in equipamentos"
					:key="item.id"
					class="bg-white p-4 pb-6 rounded-2xl shadow-sm border border-gray-100 flex flex-col hover:shadow-xl transition-all hover:-translate-y-1"
				>
					<div class="h-48 w-full flex items-center justify-center mb-4 p-4 bg-gray-50 rounded-xl">
						<img
							:src="item.src"
							:alt="item.nome"
							class="max-h-full max-w-full object-contain mix-blend-multiply hover:scale-110 transition-transform duration-300"
						/>
					</div>

					<h3
						class="font-extrabold text-blue-900 uppercase text-xs md:text-sm text-center mb-6 min-h-[40px] flex items-center justify-center leading-tight px-2"
					>
						{{ item.nome }}
					</h3>

					<div class="flex flex-row gap-3 mt-auto w-full">
						<button
							@click="falarCom('Cesar', item.nome)"
							class="w-full bg-blue-700 hover:bg-blue-800 text-white py-3 rounded-lg text-xs font-bold flex items-center justify-center gap-2 transition-colors shadow-sm"
						>
							<i class="fab fa-whatsapp text-lg"></i> FALAR COM CÉSAR
						</button>
						<button
							@click="falarCom('Darlan', item.nome)"
							class="w-full bg-slate-700 hover:bg-slate-800 text-white py-3 rounded-lg text-xs font-bold flex items-center justify-center gap-2 transition-colors shadow-sm"
						>
							<i class="fab fa-whatsapp text-lg"></i> FALAR COM DARLAN
						</button>
					</div>
				</div>
			</div>
		</main>

		<footer class="bg-blue-800 text-white mt-auto w-full border-t border-blue-900">
			<div class="w-full px-6 py-14 max-w-[1920px] mx-auto">
				<div class="grid grid-cols-1 md:grid-cols-2 gap-12 relative">
					<div class="flex flex-col items-center md:items-end text-center md:text-right">
						<div class="flex items-center gap-3 mb-2 group cursor-pointer" @click="falarCom('Cesar', 'Geral')">
							<i class="fab fa-whatsapp text-3xl text-green-400 group-hover:scale-110 transition-transform"></i>
							<span class="text-2xl font-bold tracking-tight">41 9.9735-2785</span>
						</div>
						<p class="text-sm uppercase tracking-[0.3em] opacity-80">
							Mário <span class="font-black italic text-yellow-400 opacity-100 text-lg">César</span>
						</p>
					</div>

					<div
						class="hidden md:block absolute left-1/2 top-2 bottom-2 w-px bg-gradient-to-b from-transparent via-blue-400 to-transparent opacity-30"
					></div>

					<div class="flex flex-col items-center md:items-start text-center md:text-left border-t border-blue-700 pt-8 md:border-0 md:pt-0">
						<div class="flex items-center gap-3 mb-2 group cursor-pointer" @click="falarCom('Darlan', 'Geral')">
							<i class="fab fa-whatsapp text-3xl text-green-400 group-hover:scale-110 transition-transform"></i>
							<span class="text-2xl font-bold tracking-tight">41 9.9251-5319</span>
						</div>
						<p class="text-lg font-black uppercase tracking-[0.2em] italic text-slate-200">Darlan</p>
					</div>
				</div>
			</div>
			<div class="bg-yellow-500 py-3 text-center text-blue-900 text-xs font-black uppercase w-full tracking-widest">São José Dos Pinhais</div>
		</footer>
	</div>
</template>

<script setup>
import { ref } from 'vue';

const logoError = ref(false);

const equipamentos = ref([
	{ id: 1, nome: 'Betoneira 400L', src: '/img/1774877029627.png'},
	{ id: 2, nome: 'Andaime Tubular 1m/1,5m', src: '/img/andaime.png' },
	{ id: 3, nome: 'Compactador de Solo', src: '/img/comapctador.png' },
	{ id: 4, nome: 'Martelo Demolidor 16kg', src: '/img/1774874938485.png' },
	{ id: 5, nome: 'Furadeira de Impacto', src: '/img/1774873925363.png' },
	{ id: 6, nome: 'Furadeira Profissional', src: '/img/furadeira_2.png' },
	{ id: 7, nome: 'Esmerilhadeira', src: '/img/esmerilhadeira.png' },
	{ id: 8, nome: 'Martelete Rompedor', src: '/img/martelete.png' },
	{ id: 9, nome: 'Soprador Térmico', src: '/img/soprador.png' },
	{ id: 10, nome: 'Plaina Elétrica', src: '/img/plaina.png' },
	{ id: 11, nome: 'Lixadeira de Cinta', src: '/img/lixadeira_cinta.png' },
	{ id: 12, nome: 'Serra Tico-Tico', src: '/img/tico_tico.png' },
	{ id: 13, nome: 'Parafusadeira a Bateria', src: '/img/parafusadeira.png' },
	{ id: 14, nome: 'Serra Mármore', src: '/img/serra_marmore.png' },
	{ id: 15, nome: 'Serra Circular', src: '/img/serra_circular.png' },
	{ id: 16, nome: 'Policorte / Serra de Bancada', src: '/img/policorte.png' },
]);

const falarCom = (quem, produto) => {
	const fones = {
		Cesar: '5541997352785',
		Darlan: '5541992515319',
	};

	const msg = encodeURIComponent(`Olá ${quem}! Gostaria de informações sobre a locação de: ${produto}`);
	window.open(`https://wa.me/${fones[quem]}?text=${msg}`, '_blank');
};
</script>
