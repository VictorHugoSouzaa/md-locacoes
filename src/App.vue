<template>
	<div class="min-h-screen bg-slate-50 font-sans text-slate-900 flex flex-col">

		<header class="bg-white border-b-4 border-yellow-400 shadow-sm">
			<nav class="max mx-auto px-6 py-4 flex items-center justify-between gap-6 bg-zinc-300">

				<div class="flex items-center gap-8">
					<a href="#" class="flex items-center gap-3">
						<img src="/logo-md.png" alt="M&D Locações" class="h-14 w-auto object-contain" />
					</a>

					<div class="hidden md:flex items-center gap-4">

						<a href="#sobre"
							class="bg-blue-800 hover:bg-blue-700 text-white font-bold uppercase text-sm px-4 py-2 rounded-lg transition-colors shadow-sm">
							Sobre nós
						</a>

						<a href="#contato"
							class="bg-blue-800 hover:bg-blue-700 text-white font-bold uppercase text-sm px-4 py-2 rounded-lg transition-colors shadow-sm">
							Entre em contato
						</a>

						<a href="#faq"
							class="bg-blue-800 hover:bg-blue-700 text-white font-bold uppercase text-sm px-4 py-2 rounded-lg transition-colors shadow-sm">
							FAQ
						</a>
					</div>
				</div>

				<div class="w-full max-w-xs">
					<input type="text" v-model="filtroProduto" placeholder="Buscar produto..."
						class="w-full px-4 py-2 rounded-lg border border-gray-300 bg-white text-sm text-slate-800 placeholder:text-slate-400 focus:outline-none focus:ring-2 focus:ring-blue-700 focus:border-blue-700" />
				</div>

			</nav>
		</header>

		<section class="bg-white py-10 px-6 flex flex-col items-center border-b-4 border-yellow-500 shadow-md w-full relative">
			<div class="h-32 mb-6 w-full flex items-center justify-center">
				<img src="/logo-md.png" alt="M&D Locações" class="h-full object-contain max-w-[80%]" @error="logoError = true"
					v-if="!logoError" />

				<h2 v-else class="text-4xl font-black text-blue-800 tracking-tighter border-4 border-blue-800 p-2 rounded">
					M&D LOCAÇÕES
				</h2>
			</div>

			<h1
				class="text-blue-800 font-black text-center text-2xl md:text-4xl uppercase tracking-tighter leading-tight max-w-4xl">
				Tudo em <span class="bg-blue-800 text-white px-2">equipamentos</span> para sua <br />
				obra ou <span class="text-blue-600">reforma.</span>
			</h1>
		</section>

		<main class="w-full flex-grow py-12 px-6 md:px-12">
			<div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6 md:gap-8 max-w-[1920px] mx-auto">
				<div v-for="item in equipamentosFiltrados" :key="item.id"
					class="bg-white p-4 pb-6 rounded-2xl shadow-sm border border-gray-100 flex flex-col hover:shadow-xl transition-all hover:-translate-y-1">
					<div class="h-48 w-full flex items-center justify-center mb-4 p-4 bg-gray-50 rounded-xl">
						<img :src="item.src" :alt="item.nome"
							class="max-h-full max-w-full object-contain mix-blend-multiply hover:scale-110 transition-transform duration-300" />
					</div>

					<h3
						class="font-extrabold text-blue-900 uppercase text-xs md:text-sm text-center mb-2 min-h-[40px] flex items-center justify-center leading-tight px-2">
						{{ item.nome }}
					</h3>

					<span class="text-[10px] font-bold uppercase text-blue-700 bg-blue-50 px-3 py-1 rounded-full mx-auto mb-3">
						{{ item.categoria }}
					</span>

					<p class="text-slate-600 text-xs md:text-sm text-center leading-relaxed mt-auto px-2">
						{{ item.descricao }}
					</p>
				</div>
			</div>

			<p v-if="equipamentosFiltrados.length === 0" class="text-center text-slate-500 font-semibold mt-10">
				Nenhum produto encontrado.
			</p>
		</main>

	</div>
	<div class="fixed bottom-6 right-6 z-50">
		<div v-if="mostrarOpcoesContato"
			class="mb-3 bg-white rounded-2xl shadow-xl border border-gray-200 p-3 flex flex-col gap-2 w-48">
			<button @click="falarCom('Cesar')"
				class="bg-blue-700 hover:bg-blue-800 text-white py-3 rounded-lg text-xs font-bold transition-colors">
				FALAR COM CÉSAR
			</button>

			<button @click="falarCom('Darlan')"
				class="bg-slate-700 hover:bg-slate-800 text-white py-3 rounded-lg text-xs font-bold transition-colors">
				FALAR COM DARLAN
			</button>
		</div>

		<button @click="mostrarOpcoesContato = !mostrarOpcoesContato"
			class="w-16 h-16 bg-green-500 hover:bg-green-600 text-white rounded-full shadow-xl flex items-center justify-center transition-all hover:scale-110"
			aria-label="Entrar em contato pelo WhatsApp">
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-9 h-9 text-white">
				<path
					d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.472-.148-.67.15-.198.297-.767.966-.94 1.164-.173.198-.347.223-.644.074-.297-.149-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.372-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.67-.51-.173-.008-.372-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.71.306 1.263.489 1.694.626.712.226 1.36.194 1.872.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.29.173-1.413-.074-.124-.272-.198-.57-.347z" />
				<path
					d="M12.04 2C6.58 2 2.13 6.45 2.13 11.91c0 1.75.46 3.45 1.33 4.95L2.05 22l5.27-1.38c1.45.79 3.08 1.21 4.72 1.21h.01c5.46 0 9.91-4.45 9.91-9.91C21.96 6.45 17.51 2 12.04 2zm0 18.15h-.01c-1.47 0-2.91-.39-4.18-1.13l-.3-.18-3.13.82.84-3.05-.2-.31c-.82-1.31-1.25-2.83-1.25-4.39 0-4.54 3.69-8.23 8.23-8.23 2.2 0 4.27.86 5.82 2.41 1.56 1.56 2.41 3.62 2.41 5.82 0 4.54-3.69 8.24-8.23 8.24z" />
			</svg>
		</button>
	</div>


	<footer>
		<div>
			<h3>pé</h3>
		</div>
		<div>
			<Span>São josé dos Pinhais</Span>
		</div>
	</footer>

</template>

<script setup>
import { ref, computed } from 'vue';

const mostrarOpcoesContato = ref(false);
const logoError = ref(false);
const filtroProduto = ref('');

const equipamentos = ref([
	// Mistura de concreto
	{
		id: 1,
		nome: 'Betoneira 400L',
		categoria: 'Mistura de Concreto',
		src: '/img/betoneira.png',
		descricao: 'Equipamento ideal para mistura de concreto, argamassa e outros materiais em obras de pequeno e médio porte.'
	},

	// Acesso e sustentação
	{
		id: 2,
		nome: 'Andaime Tubular 1m/1,5m',
		categoria: 'Acesso e Sustentação',
		src: '/img/andaime.png',
		descricao: 'Estrutura metálica utilizada para trabalhos em altura, oferecendo apoio e segurança durante reformas e construções.'
	},
	{
		id: 5,
		nome: 'Escoras Metálicas',
		categoria: 'Acesso e Sustentação',
		src: '/img/escoras.png',
		descricao: 'Suportes ajustáveis utilizados para sustentação temporária de lajes, vigas e estruturas durante a construção.'
	},

	// Compactação
	{
		id: 3,
		nome: 'Placa Vibratória',
		categoria: 'Compactação',
		src: '/img/comapctador.png',
		descricao: 'Máquina indicada para compactação de solos, areia, brita e pavimentos, garantindo melhor acabamento e estabilidade.'
	},
	{
		id: 4,
		nome: 'Compactador de Solo',
		categoria: 'Compactação',
		src: '/img/Compactador_Solo.png',
		descricao: 'Equipamento usado para compactar terrenos e valas, ideal para preparação de bases em obras e pavimentações.'
	},

	// Perfuração
	{
		id: 6,
		nome: 'Perfurador de Solo',
		categoria: 'Perfuração',
		src: '/img/perfurador.png',
		descricao: 'Ferramenta prática para abertura de buracos no solo, muito usada em instalação de postes, cercas e fundações leves.'
	},
	{
		id: 8,
		nome: 'Furadeira de Impacto',
		categoria: 'Perfuração',
		src: '/img/furadeira_1.png',
		descricao: 'Ferramenta versátil para perfurações em concreto, alvenaria, madeira e metal, ideal para obras e reformas.'
	},
	{
		id: 9,
		nome: 'Furadeira Profissional',
		categoria: 'Perfuração',
		src: '/img/furadeira_2.png',
		descricao: 'Equipamento de alto desempenho para perfurações precisas e uso contínuo em trabalhos profissionais.'
	},

	// Demolição
	{
		id: 7,
		nome: 'Martelo Demolidor 16kg',
		categoria: 'Demolição',
		src: '/img/marteloDemolidor.png',
		descricao: 'Equipamento robusto para demolição de concreto, pisos, paredes e estruturas rígidas com alta eficiência.'
	},

	// Corte
	{
		id: 14,
		nome: 'Serra Tico-Tico',
		categoria: 'Corte',
		src: '/img/tico_tico.png',
		descricao: 'Equipamento ideal para cortes curvos, retos e detalhados em madeira, plástico e materiais similares.'
	},
	{
		id: 16,
		nome: 'Serra Mármore',
		categoria: 'Corte',
		src: '/img/serra_marmore.png',
		descricao: 'Equipamento utilizado para cortes em pisos, azulejos, pedras, mármore e outros materiais de construção.'
	},
	{
		id: 17,
		nome: 'Serra Circular',
		categoria: 'Corte',
		src: '/img/serra_circular.png',
		descricao: 'Ferramenta indicada para cortes retos e precisos em madeira, MDF, compensados e materiais semelhantes.'
	},
	{
		id: 18,
		nome: 'Policorte / Serra de Bancada',
		categoria: 'Corte',
		src: '/img/policorte.png',
		descricao: 'Equipamento robusto para cortes rápidos e precisos em metais, tubos, barras e perfis.'
	},

	// Acabamento
	{
		id: 10,
		nome: 'Esmerilhadeira',
		categoria: 'Acabamento',
		src: '/img/esmerilhadeira.png',
		descricao: 'Ferramenta utilizada para corte, desbaste e acabamento em metais, pedras, concreto e outros materiais.'
	},
	{
		id: 11,
		nome: 'Soprador Térmico',
		categoria: 'Acabamento',
		src: '/img/soprador.png',
		descricao: 'Equipamento indicado para aquecer, remover tintas, moldar plásticos e realizar aplicações com ar quente.'
	},
	{
		id: 12,
		nome: 'Plaina Elétrica',
		categoria: 'Acabamento',
		src: '/img/plaina.png',
		descricao: 'Ferramenta usada para nivelar, desbastar e dar acabamento em superfícies de madeira com rapidez e precisão.'
	},
	{
		id: 13,
		nome: 'Lixadeira de Cinta',
		categoria: 'Acabamento',
		src: '/img/lixadeira_cinta.png',
		descricao: 'Ferramenta indicada para desbaste, nivelamento e acabamento em madeira e outras superfícies.'
	},

	// Fixação e montagem
	{
		id: 15,
		nome: 'Parafusadeira a Bateria',
		categoria: 'Fixação e Montagem',
		src: '/img/parafusadeira.png',
		descricao: 'Ferramenta prática para apertar e remover parafusos com agilidade, ideal para montagens e instalações.'
	}
]);

const equipamentosFiltrados = computed(() => {
	const termo = filtroProduto.value.trim().toLowerCase();

	if (!termo) {
		return equipamentos.value;
	}

	return equipamentos.value.filter((item) =>
		item.nome.toLowerCase().includes(termo)
	);
});

const falarCom = (quem) => {
	const fones = {
		Cesar: '5541997352785',
		Darlan: '5541992515319',
	};

	const msg = encodeURIComponent(`Olá ${quem}! Gostaria de informações sobre a locação de equipamentos.`);
	window.open(`https://wa.me/${fones[quem]}?text=${msg}`, '_blank');

	mostrarOpcoesContato.value = false;
};
</script>