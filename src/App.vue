<template>
	<!--
		App.vue — Componente raiz (página única / SPA sem router)

		Estrutura de seções (top → bottom):
		  1. Navbar      — navegação sticky com menu mobile
		  2. Hero        — chamada principal com CTAs
		  3. Benefícios  — faixa amarela com 3 diferenciais rápidos
		  4. Equipamentos — grid filtrável por categoria e busca
		  5. Sobre Nós   — apresentação da empresa
		  6. FAQ         — perguntas frequentes (accordion)
		  7. CTA Banner  — chamada final para orçamento
		  8. Footer      — links, contato e copyright

		Fora do wrapper principal (z-index alto):
		  - Botão flutuante do WhatsApp (fixed, canto inferior direito)
	-->
	<div class="min-h-screen bg-slate-50 font-sans text-slate-900 flex flex-col">

		<!-- ══════════════════════════════════════════════════════════
		     NAVBAR
		     sticky top-0 garante que fica visível durante o scroll
		     ══════════════════════════════════════════════════════════ -->
		<header class="bg-white border-b-4 border-yellow-400 shadow-sm sticky top-0 z-40">
			<nav class="max-w-7xl mx-auto px-6 py-3 flex items-center gap-6">

				<!-- Logo — clique volta ao topo -->
				<a href="#" class="shrink-0">
					<img src="/logo-md.png" alt="M&D Locações" class="h-20 w-auto object-contain" />
				</a>

				<!-- Links de navegação — visíveis apenas em desktop (md+) -->
				<div class="hidden md:flex items-center gap-6">
					<a href="#equipamentos" class="text-slate-700 hover:text-blue-800 font-semibold text-sm transition-colors">Equipamentos</a>
					<a href="#sobre"        class="text-slate-700 hover:text-blue-800 font-semibold text-sm transition-colors">Sobre nós</a>
					<a href="#faq"          class="text-slate-700 hover:text-blue-800 font-semibold text-sm transition-colors">FAQ</a>
				</div>

				<div class="flex-1"></div>

				<!-- Campo de busca — visível apenas em desktop; versão mobile está no menu abaixo -->
				<input
					type="text"
					v-model="filtroProduto"
					placeholder="Buscar produto..."
					class="hidden md:block w-full max-w-xs px-4 py-2 rounded-lg border border-gray-200 bg-gray-50 text-sm text-slate-800 placeholder:text-slate-400 focus:outline-none focus:ring-2 focus:ring-blue-700 focus:border-blue-700 focus:bg-white transition-colors"
				/>

				<!-- Botão hambúrguer — visível apenas em mobile -->
				<button
					@click="menuMobileAberto = !menuMobileAberto"
					class="md:hidden p-2 rounded-lg text-slate-700 hover:bg-gray-100 transition-colors"
					aria-label="Abrir menu"
				>
					<svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
						<!-- Ícone muda de hambúrguer para X conforme o estado -->
						<path v-if="!menuMobileAberto" stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16" />
						<path v-else                   stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
					</svg>
				</button>
			</nav>

			<!-- Menu mobile — dropdown abaixo da navbar, oculto por padrão -->
			<div v-show="menuMobileAberto" class="md:hidden bg-white border-t border-gray-100 px-6 py-4 flex flex-col gap-1">
				<input
					type="text"
					v-model="filtroProduto"
					placeholder="Buscar produto..."
					class="w-full px-4 py-2 mb-2 rounded-lg border border-gray-200 bg-gray-50 text-sm text-slate-800 placeholder:text-slate-400 focus:outline-none focus:ring-2 focus:ring-blue-700"
				/>
				<!-- @click fecha o menu ao navegar -->
				<a href="#equipamentos" @click="menuMobileAberto = false" class="text-slate-700 font-semibold text-sm py-3 border-b border-gray-100">Equipamentos</a>
				<a href="#sobre"        @click="menuMobileAberto = false" class="text-slate-700 font-semibold text-sm py-3 border-b border-gray-100">Sobre nós</a>
				<a href="#faq"          @click="menuMobileAberto = false" class="text-slate-700 font-semibold text-sm py-3">FAQ</a>
			</div>
		</header>

		<!-- ══════════════════════════════════════════════════════════
		     HERO
		     Fundo azul-escuro com padrão geométrico decorativo (opacity 4%)
		     ══════════════════════════════════════════════════════════ -->
		<section class="bg-blue-900 py-16 md:py-24 px-6 relative overflow-hidden">
			<!-- Padrão de listras diagonais decorativo -->
			<div
				class="absolute inset-0 opacity-[0.04]"
				style="background-image: repeating-linear-gradient(45deg, white 0, white 1px, transparent 0, transparent 50%); background-size: 22px 22px;"
			></div>

			<div class="max-w-3xl mx-auto text-center relative z-10">
				<!-- Badge de localização -->
				<div class="inline-flex items-center gap-2 bg-yellow-400/20 border border-yellow-400/40 text-yellow-400 text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full mb-6">
					<svg class="w-3.5 h-3.5 shrink-0" fill="currentColor" viewBox="0 0 20 20">
						<path fill-rule="evenodd" d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd" />
					</svg>
					São José dos Pinhais e região
				</div>

				<!-- Headline principal -->
				<h1 class="text-white font-black text-3xl md:text-5xl uppercase tracking-tight leading-tight mb-5">
					Alugue os melhores<br />
					<span class="text-yellow-400">equipamentos</span><br />
					para sua obra
				</h1>

				<p class="text-blue-200 text-base md:text-lg leading-relaxed mb-10 max-w-xl mx-auto">
					Betoneiras, andaimes, compactadores, serras e muito mais — entrega rápida e preço justo.
				</p>

				<!-- CTAs principais -->
				<div class="flex flex-col sm:flex-row gap-3 justify-center">
					<a
						href="#equipamentos"
						class="bg-yellow-400 hover:bg-yellow-300 text-blue-900 font-extrabold uppercase text-sm px-8 py-4 rounded-xl transition-colors shadow-lg tracking-wide"
					>
						Ver Equipamentos
					</a>
					<button
						@click="mostrarOpcoesContato = true"
						class="bg-white/10 hover:bg-white/20 border border-white/20 text-white font-bold text-sm px-8 py-4 rounded-xl transition-all tracking-wide"
					>
						Falar no WhatsApp
					</button>
				</div>
			</div>
		</section>

		<!-- ══════════════════════════════════════════════════════════
		     FAIXA DE BENEFÍCIOS
		     3 pontos rápidos que constroem confiança logo abaixo do hero
		     ══════════════════════════════════════════════════════════ -->
		<section class="bg-yellow-400 py-5 px-6">
			<div class="max-w-5xl mx-auto grid grid-cols-1 sm:grid-cols-3 gap-4 text-blue-900 text-center sm:text-left">
				<div class="flex items-center justify-center sm:justify-start gap-3">
					<!-- Ícone: calendário -->
					<svg class="w-5 h-5 shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
						<path stroke-linecap="round" stroke-linejoin="round" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
					</svg>
					<span class="font-bold text-sm">Locação diária, semanal ou mensal</span>
				</div>
				<div class="flex items-center justify-center sm:justify-start gap-3">
					<!-- Ícone: localização -->
					<svg class="w-5 h-5 shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
						<path stroke-linecap="round" stroke-linejoin="round" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
						<path stroke-linecap="round" stroke-linejoin="round" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
					</svg>
					<span class="font-bold text-sm">Entrega em SJP e região</span>
				</div>
				<div class="flex items-center justify-center sm:justify-start gap-3">
					<!-- Ícone: mensagem / WhatsApp -->
					<svg class="w-5 h-5 shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
						<path stroke-linecap="round" stroke-linejoin="round" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
					</svg>
					<span class="font-bold text-sm">Atendimento direto pelo WhatsApp</span>
				</div>
			</div>
		</section>

		<!-- ══════════════════════════════════════════════════════════
		     CATÁLOGO DE EQUIPAMENTOS
		     - Filtros por categoria (gerados a partir do array `equipamentos`)
		     - Busca por texto (campo na navbar)
		     - Os dois filtros funcionam em conjunto
		     ══════════════════════════════════════════════════════════ -->
		<main id="equipamentos" class="w-full flex-grow py-12 px-6 md:px-12">
			<div class="max-w-[1600px] mx-auto">

				<!-- Título da seção -->
				<div class="flex items-center gap-4 mb-6">
					<div>
						<h2 class="text-blue-900 font-black text-xl md:text-2xl uppercase tracking-tight">Nossos Equipamentos</h2>
						<div class="w-12 h-1 bg-yellow-400 mt-1 rounded-full"></div>
					</div>
					<div class="flex-1 h-px bg-gray-200 ml-2 hidden sm:block"></div>
				</div>

				<!-- Filtros de categoria — gerados do computed `categorias` -->
				<div class="flex gap-2 mb-8 overflow-x-auto pb-1 -mx-1 px-1">
					<button
						v-for="cat in categorias"
						:key="cat"
						@click="categoriaAtiva = cat"
						:class="[
							'shrink-0 px-4 py-2 rounded-full text-xs font-bold uppercase tracking-wide border transition-all',
							categoriaAtiva === cat
								? 'bg-blue-800 text-white border-blue-800 shadow-sm'
								: 'bg-white text-slate-600 border-gray-200 hover:border-blue-800 hover:text-blue-800'
						]"
					>
						{{ cat }}
					</button>
				</div>

				<!-- Indicador de busca ativa -->
				<p v-if="filtroProduto.trim()" class="text-slate-500 text-sm mb-5">
					<strong class="text-slate-700">{{ equipamentosVisiveis.length }}</strong> resultado(s) para
					"<strong class="text-blue-800">{{ filtroProduto }}</strong>"
				</p>

				<!-- Grid de produtos -->
				<!-- Clicar em qualquer lugar do card (inclusive no botão) abre o popup do WhatsApp -->
				<div
					v-if="equipamentosVisiveis.length > 0"
					class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-3 md:gap-4"
				>
					<div
						v-for="item in equipamentosVisiveis"
						:key="item.id"
						class="bg-white rounded-xl overflow-hidden border border-gray-100 shadow-sm hover:shadow-md hover:-translate-y-0.5 transition-all duration-200 flex flex-col group cursor-pointer"
						@click="mostrarOpcoesContato = true"
					>
						<!-- Imagem do produto: fundo cinza claro, mix-blend-multiply remove o fundo branco das fotos PNG -->
						<div class="aspect-square bg-gray-50 flex items-center justify-center p-5">
							<img
								:src="item.src"
								:alt="item.nome"
								loading="lazy"
								class="w-full h-full object-contain mix-blend-multiply group-hover:scale-105 transition-transform duration-300"
							/>
						</div>

						<!-- Nome e botão -->
						<div class="p-3 flex flex-col gap-2 border-t border-gray-100 flex-1">
							<h3 class="text-blue-900 font-bold text-xs md:text-sm text-center leading-snug flex-1">
								{{ item.nome }}
							</h3>
							<button class="w-full bg-blue-800 hover:bg-blue-700 text-white text-[11px] font-bold uppercase py-2 rounded-lg tracking-wide transition-colors">
								Consultar
							</button>
						</div>
					</div>
				</div>

				<!-- Estado vazio — busca sem resultado -->
				<p v-else class="text-center text-slate-500 font-semibold mt-10">
					Nenhum produto encontrado.
				</p>

			</div>
		</main>

		<!-- ══════════════════════════════════════════════════════════
		     SOBRE NÓS
		     Texto institucional + 4 cartões de diferenciais (dados em `diferenciais`)
		     ══════════════════════════════════════════════════════════ -->
		<section id="sobre" class="bg-white py-16 px-6 md:px-12 border-t-4 border-yellow-400">
			<div class="max-w-5xl mx-auto">
				<h2 class="text-blue-800 font-black text-3xl md:text-4xl uppercase tracking-tighter mb-2">Sobre Nós</h2>
				<div class="w-16 h-1 bg-yellow-400 mb-10"></div>

				<div class="grid md:grid-cols-2 gap-12 items-center">
					<!-- Texto institucional — edite diretamente aqui -->
					<div>
						<p class="text-slate-600 text-base leading-relaxed mb-4">
							A <strong class="text-blue-800">M&D Locações</strong> é uma empresa especializada em locação de
							equipamentos para construção civil, reformas e obras em geral, atendendo São José dos Pinhais e região.
						</p>
						<p class="text-slate-600 text-base leading-relaxed mb-4">
							Com uma equipe comprometida e um amplo portfólio de equipamentos, nossa missão é oferecer as
							melhores ferramentas e máquinas para tornar o seu projeto mais eficiente, seguro e econômico.
						</p>
						<p class="text-slate-600 text-base leading-relaxed">
							Acreditamos que ter acesso a equipamentos de qualidade não precisa ser caro. Por isso, oferecemos
							condições flexíveis e atendimento personalizado para cada cliente.
						</p>
					</div>

					<!-- Cartões de diferenciais — gerados pelo array `diferenciais` no script -->
					<div class="grid grid-cols-2 gap-4">
						<div
							v-for="item in diferenciais"
							:key="item.titulo"
							class="bg-blue-50 border-l-4 border-yellow-400 p-5 rounded-xl"
						>
							<div class="w-8 h-8 bg-blue-800 rounded-full flex items-center justify-center mb-3">
								<svg class="w-4 h-4 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
									<path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
								</svg>
							</div>
							<h3 class="font-extrabold text-blue-900 uppercase text-xs mb-1">{{ item.titulo }}</h3>
							<p class="text-slate-600 text-xs leading-relaxed">{{ item.texto }}</p>
						</div>
					</div>
				</div>

				<!-- Banner de localização com CTA -->
				<div class="mt-10 bg-blue-800 text-white rounded-2xl p-6 flex flex-col md:flex-row items-center justify-between gap-4">
					<div class="flex items-center gap-4">
						<svg class="w-8 h-8 text-yellow-400 shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
							<path stroke-linecap="round" stroke-linejoin="round" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
							<path stroke-linecap="round" stroke-linejoin="round" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
						</svg>
						<div>
							<p class="font-bold uppercase text-yellow-400 text-xs mb-0.5">Nossa Localização</p>
							<p class="text-white text-lg font-semibold">São José dos Pinhais — PR</p>
						</div>
					</div>
					<button
						@click="mostrarOpcoesContato = true"
						class="bg-yellow-400 hover:bg-yellow-300 text-blue-900 font-extrabold uppercase text-sm px-6 py-3 rounded-lg transition-colors shadow-sm"
					>
						Entre em Contato
					</button>
				</div>
			</div>
		</section>

		<!-- ══════════════════════════════════════════════════════════
		     FAQ — PERGUNTAS FREQUENTES
		     Accordion: apenas uma resposta aberta por vez
		     Perguntas gerenciadas pelo array `faqItens` no script
		     ══════════════════════════════════════════════════════════ -->
		<section id="faq" class="bg-slate-50 py-16 px-6 md:px-12 border-t border-gray-200">
			<div class="max-w-3xl mx-auto">
				<h2 class="text-blue-800 font-black text-3xl md:text-4xl uppercase tracking-tighter mb-2">Perguntas Frequentes</h2>
				<div class="w-16 h-1 bg-yellow-400 mb-10"></div>

				<div class="flex flex-col gap-3">
					<div
						v-for="(item, index) in faqItens"
						:key="index"
						class="bg-white rounded-xl border border-gray-200 shadow-sm overflow-hidden"
					>
						<!-- Cabeçalho clicável — toggleFaq fecha a pergunta anterior automaticamente -->
						<button
							@click="toggleFaq(index)"
							class="w-full flex items-center justify-between px-6 py-4 text-left hover:bg-blue-50 transition-colors"
						>
							<span class="font-bold text-blue-900 text-sm md:text-base pr-4">{{ item.pergunta }}</span>
							<!-- O "+" gira 45° para virar "×" quando aberto -->
							<span
								class="text-blue-800 font-black text-2xl flex-shrink-0 transition-transform duration-300 leading-none"
								:class="{ 'rotate-45': faqAberto === index }"
							>+</span>
						</button>
						<div v-show="faqAberto === index" class="px-6 pb-5 border-t border-gray-100">
							<p class="text-slate-600 text-sm md:text-base leading-relaxed pt-4">{{ item.resposta }}</p>
						</div>
					</div>
				</div>
			</div>
		</section>

		<!-- ══════════════════════════════════════════════════════════
		     CTA FINAL — banner de conversão antes do rodapé
		     ══════════════════════════════════════════════════════════ -->
		<section class="bg-blue-800 py-14 px-6">
			<div class="max-w-3xl mx-auto text-center">
				<h2 class="text-white font-black text-2xl md:text-3xl uppercase tracking-tight mb-3">
					Pronto para começar sua obra?
				</h2>
				<p class="text-blue-200 text-base leading-relaxed mb-8">
					Entre em contato agora e garanta os equipamentos que você precisa, com agilidade e preço justo.
				</p>
				<button
					@click="mostrarOpcoesContato = true"
					class="bg-yellow-400 hover:bg-yellow-300 text-blue-900 font-extrabold uppercase text-sm px-10 py-4 rounded-xl transition-colors shadow-lg tracking-wide"
				>
					Solicitar Orçamento
				</button>
			</div>
		</section>

		<!-- ══════════════════════════════════════════════════════════
		     FOOTER
		     Dentro do wrapper flex para que flex-grow em <main>
		     empurre o footer para o fundo mesmo em páginas curtas
		     ══════════════════════════════════════════════════════════ -->
		<footer class="bg-blue-900 text-white py-10 px-6 md:px-12">
			<div class="max-w-5xl mx-auto grid md:grid-cols-3 gap-8">
				<!-- Coluna 1: marca -->
				<div>
					<img src="/logo-md.png" alt="M&D Locações" class="h-20 w-auto object-contain mb-3 brightness-0 invert" />
					<p class="text-slate-300 text-sm leading-relaxed">Locação de equipamentos para construção civil, reformas e obras em São José dos Pinhais e região.</p>
				</div>

				<!-- Coluna 2: navegação -->
				<div>
					<h4 class="font-extrabold uppercase text-yellow-400 text-xs mb-4">Navegação</h4>
					<ul class="flex flex-col gap-2">
						<li><a href="#"             class="text-slate-300 hover:text-white text-sm transition-colors">Início</a></li>
						<li><a href="#equipamentos" class="text-slate-300 hover:text-white text-sm transition-colors">Equipamentos</a></li>
						<li><a href="#sobre"        class="text-slate-300 hover:text-white text-sm transition-colors">Sobre Nós</a></li>
						<li><a href="#faq"          class="text-slate-300 hover:text-white text-sm transition-colors">FAQ</a></li>
					</ul>
				</div>

				<!-- Coluna 3: contato — clique abre WhatsApp via falarCom() -->
				<div>
					<h4 class="font-extrabold uppercase text-yellow-400 text-xs mb-4">Contato</h4>
					<p class="text-slate-300 text-sm mb-3">São José dos Pinhais — PR</p>
					<div class="flex flex-col gap-2">
						<button @click="falarCom('Cesar')"  class="text-left text-slate-300 hover:text-white text-sm transition-colors">César: (41) 99735-2785</button>
						<button @click="falarCom('Darlan')" class="text-left text-slate-300 hover:text-white text-sm transition-colors">Darlan: (41) 99251-5319</button>
					</div>
				</div>
			</div>

			<!-- Copyright com ano dinâmico -->
			<div class="max-w-5xl mx-auto mt-8 pt-6 border-t border-blue-800 text-center text-slate-400 text-xs">
				© {{ anoAtual }} M&D Locações. Todos os direitos reservados.
			</div>
		</footer>

	</div><!-- fim do wrapper principal -->

	<!-- ══════════════════════════════════════════════════════════
	     BOTÃO FLUTUANTE DO WHATSAPP
	     fixed: fica visível em todas as seções durante o scroll
	     Abre popup com escolha entre César e Darlan
	     ══════════════════════════════════════════════════════════ -->
	<div class="fixed bottom-6 right-6 z-50">
		<!-- Popup de seleção de contato -->
		<div
			v-if="mostrarOpcoesContato"
			class="mb-3 bg-white rounded-2xl shadow-xl border border-gray-200 p-3 flex flex-col gap-2 w-52"
		>
			<p class="text-slate-500 text-[10px] font-bold uppercase text-center px-2 pb-1 border-b border-gray-100">Falar com:</p>
			<button @click="falarCom('Cesar')"  class="bg-blue-700 hover:bg-blue-800 text-white py-3 rounded-lg text-xs font-bold transition-colors">CÉSAR</button>
			<button @click="falarCom('Darlan')" class="bg-slate-700 hover:bg-slate-800 text-white py-3 rounded-lg text-xs font-bold transition-colors">DARLAN</button>
		</div>

		<!-- Botão principal — alterna exibição do popup -->
		<button
			@click="mostrarOpcoesContato = !mostrarOpcoesContato"
			class="w-16 h-16 bg-green-500 hover:bg-green-600 text-white rounded-full shadow-xl flex items-center justify-center transition-all hover:scale-110"
			aria-label="Entrar em contato pelo WhatsApp"
		>
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-9 h-9">
				<path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.472-.148-.67.15-.198.297-.767.966-.94 1.164-.173.198-.347.223-.644.074-.297-.149-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.372-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.67-.51-.173-.008-.372-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.71.306 1.263.489 1.694.626.712.226 1.36.194 1.872.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.29.173-1.413-.074-.124-.272-.198-.57-.347z" />
				<path d="M12.04 2C6.58 2 2.13 6.45 2.13 11.91c0 1.75.46 3.45 1.33 4.95L2.05 22l5.27-1.38c1.45.79 3.08 1.21 4.72 1.21h.01c5.46 0 9.91-4.45 9.91-9.91C21.96 6.45 17.51 2 12.04 2zm0 18.15h-.01c-1.47 0-2.91-.39-4.18-1.13l-.3-.18-3.13.82.84-3.05-.2-.31c-.82-1.31-1.25-2.83-1.25-4.39 0-4.54 3.69-8.23 8.23-8.23 2.2 0 4.27.86 5.82 2.41 1.56 1.56 2.41 3.62 2.41 5.82 0 4.54-3.69 8.24-8.23 8.24z" />
			</svg>
		</button>
	</div>

</template>

<script setup>
import { ref, computed } from 'vue';

// ─────────────────────────────────────────────────────────────────────────────
// ESTADO DA INTERFACE
// ─────────────────────────────────────────────────────────────────────────────

const mostrarOpcoesContato = ref(false); // exibe/oculta o popup do WhatsApp
const filtroProduto        = ref('');    // texto digitado na busca
const faqAberto            = ref(null);  // índice da pergunta aberta no FAQ (null = todas fechadas)
const menuMobileAberto     = ref(false); // controla o menu hambúrguer no mobile
const anoAtual             = new Date().getFullYear(); // atualiza automaticamente todo ano

// ─────────────────────────────────────────────────────────────────────────────
// DADOS ESTÁTICOS — EDITE AQUI PARA ATUALIZAR O CONTEÚDO DO SITE
// ─────────────────────────────────────────────────────────────────────────────

// Cartões da seção "Sobre Nós"
// Para editar: altere titulo e texto de cada item
const diferenciais = [
	{ titulo: 'Qualidade', texto: 'Equipamentos modernos e bem conservados, revisados antes de cada locação.' },
	{ titulo: 'Variedade', texto: 'Grande seleção de equipamentos para atender todas as etapas da sua obra.' },
	{ titulo: 'Agilidade', texto: 'Entrega e retirada no prazo combinado para não atrasar o seu trabalho.' },
	{ titulo: 'Suporte',   texto: 'Atendimento direto pelo WhatsApp para esclarecer dúvidas e resolver imprevistos.' },
];

// Perguntas frequentes
// Para adicionar: insira um novo objeto { pergunta, resposta } no array
const faqItens = [
	{
		pergunta: 'Como funciona a locação de equipamentos?',
		resposta: 'É simples! Entre em contato pelo WhatsApp, informe o equipamento que precisa e o período de uso. Confirmamos a disponibilidade, alinhamos os detalhes e combinamos a entrega ou retirada do equipamento.'
	},
	{
		pergunta: 'Qual o prazo mínimo de locação?',
		resposta: 'O prazo mínimo é de 1 dia. Trabalhamos com locações diárias, semanais e mensais, sempre adaptando às necessidades do cliente.'
	},
	{
		pergunta: 'Preciso pagar caução ou depósito?',
		resposta: 'Sim, pode ser solicitado um valor de caução dependendo do equipamento. Esse valor é devolvido integralmente na devolução do equipamento em boas condições.'
	},
	{
		pergunta: 'Como é feita a entrega e retirada dos equipamentos?',
		resposta: 'Oferecemos entrega e retirada em São José dos Pinhais e região. O frete pode ser incluído no contrato ou cobrado à parte, conforme a distância. Combine diretamente conosco pelo WhatsApp.'
	},
	{
		pergunta: 'O que acontece se um equipamento apresentar defeito durante a locação?',
		resposta: 'Entre em contato imediatamente pelo WhatsApp. Avaliaremos o problema e, se for defeito do equipamento (e não mau uso), faremos a substituição o mais rápido possível para não prejudicar seu trabalho.'
	},
	{
		pergunta: 'Quais são as formas de pagamento aceitas?',
		resposta: 'Aceitamos Pix, dinheiro e transferência bancária. Consulte-nos para saber as condições disponíveis.'
	},
];

// Catálogo de equipamentos
// Para ADICIONAR um item: copie um objeto existente, dê um id único (número),
//   preencha nome, categoria (deve estar em ORDEM_CATEGORIAS), src (caminho
//   da imagem em /public/img/) e descricao.
// Para REMOVER: apague o objeto do array.
// Para EDITAR: altere os campos diretamente.
const equipamentos = ref([
	{ id: 1,  nome: 'Betoneira 400L',            categoria: 'Mistura de Concreto',  src: '/img/betoneira.png',        descricao: 'Equipamento ideal para mistura de concreto, argamassa e outros materiais em obras de pequeno e médio porte.' },
	{ id: 2,  nome: 'Andaime Tubular 1m/1,5m',   categoria: 'Acesso e Sustentação', src: '/img/andaime.png',           descricao: 'Estrutura metálica utilizada para trabalhos em altura, oferecendo apoio e segurança durante reformas e construções.' },
	{ id: 5,  nome: 'Escoras Metálicas',          categoria: 'Acesso e Sustentação', src: '/img/escoras.png',           descricao: 'Suportes ajustáveis utilizados para sustentação temporária de lajes, vigas e estruturas durante a construção.' },
	{ id: 3,  nome: 'Placa Vibratória',           categoria: 'Compactação',          src: '/img/comapctador.png',       descricao: 'Máquina indicada para compactação de solos, areia, brita e pavimentos, garantindo melhor acabamento e estabilidade.' },
	{ id: 4,  nome: 'Compactador de Solo',        categoria: 'Compactação',          src: '/img/Compactador_Solo.png',  descricao: 'Equipamento usado para compactar terrenos e valas, ideal para preparação de bases em obras e pavimentações.' },
	{ id: 6,  nome: 'Perfurador de Solo',         categoria: 'Perfuração',           src: '/img/perfurador.png',        descricao: 'Ferramenta prática para abertura de buracos no solo, muito usada em instalação de postes, cercas e fundações leves.' },
	{ id: 8,  nome: 'Furadeira de Impacto',       categoria: 'Perfuração',           src: '/img/furadeira_1.png',       descricao: 'Ferramenta versátil para perfurações em concreto, alvenaria, madeira e metal, ideal para obras e reformas.' },
	{ id: 9,  nome: 'Furadeira Profissional',     categoria: 'Perfuração',           src: '/img/furadeira_2.png',       descricao: 'Equipamento de alto desempenho para perfurações precisas e uso contínuo em trabalhos profissionais.' },
	{ id: 7,  nome: 'Martelo Demolidor 16kg',     categoria: 'Demolição',            src: '/img/marteloDemolidor.png',  descricao: 'Equipamento robusto para demolição de concreto, pisos, paredes e estruturas rígidas com alta eficiência.' },
	{ id: 14, nome: 'Serra Tico-Tico',            categoria: 'Corte',                src: '/img/tico_tico.png',         descricao: 'Equipamento ideal para cortes curvos, retos e detalhados em madeira, plástico e materiais similares.' },
	{ id: 16, nome: 'Serra Mármore',              categoria: 'Corte',                src: '/img/serra_marmore.png',     descricao: 'Equipamento utilizado para cortes em pisos, azulejos, pedras, mármore e outros materiais de construção.' },
	{ id: 17, nome: 'Serra Circular',             categoria: 'Corte',                src: '/img/serra_circular.png',    descricao: 'Ferramenta indicada para cortes retos e precisos em madeira, MDF, compensados e materiais semelhantes.' },
	{ id: 18, nome: 'Policorte / Serra de Bancada', categoria: 'Corte',              src: '/img/policorte.png',         descricao: 'Equipamento robusto para cortes rápidos e precisos em metais, tubos, barras e perfis.' },
	{ id: 10, nome: 'Esmerilhadeira',             categoria: 'Acabamento',           src: '/img/esmerilhadeira.png',    descricao: 'Ferramenta utilizada para corte, desbaste e acabamento em metais, pedras, concreto e outros materiais.' },
	{ id: 11, nome: 'Soprador Térmico',           categoria: 'Acabamento',           src: '/img/soprador.png',          descricao: 'Equipamento indicado para aquecer, remover tintas, moldar plásticos e realizar aplicações com ar quente.' },
	{ id: 12, nome: 'Plaina Elétrica',            categoria: 'Acabamento',           src: '/img/plaina.png',            descricao: 'Ferramenta usada para nivelar, desbastar e dar acabamento em superfícies de madeira com rapidez e precisão.' },
	{ id: 13, nome: 'Lixadeira de Cinta',         categoria: 'Acabamento',           src: '/img/lixadeira_cinta.png',   descricao: 'Ferramenta indicada para desbaste, nivelamento e acabamento em madeira e outras superfícies.' },
	{ id: 15, nome: 'Parafusadeira a Bateria',    categoria: 'Fixação e Montagem',   src: '/img/parafusadeira.png',     descricao: 'Ferramenta prática para apertar e remover parafusos com agilidade, ideal para montagens e instalações.' },
]);

// Ordem de exibição das categorias nos botões de filtro
// Para adicionar uma nova categoria: inclua aqui E use o mesmo nome exato em `equipamentos`
const ORDEM_CATEGORIAS = [
	'Mistura de Concreto',
	'Acesso e Sustentação',
	'Compactação',
	'Perfuração',
	'Demolição',
	'Corte',
	'Acabamento',
	'Fixação e Montagem',
];

// ─────────────────────────────────────────────────────────────────────────────
// FILTRAGEM DE PRODUTOS
// ─────────────────────────────────────────────────────────────────────────────

const categoriaAtiva = ref('Todos');

// Lista de botões de filtro: ["Todos", ...categorias presentes no catálogo, em ordem]
const categorias = computed(() =>
	['Todos', ...ORDEM_CATEGORIAS.filter(c => equipamentos.value.some(e => e.categoria === c))]
);

// Produtos exibidos no grid: aplica filtro de categoria E busca por texto simultaneamente
const equipamentosVisiveis = computed(() => {
	let lista = equipamentos.value;

	if (categoriaAtiva.value !== 'Todos')
		lista = lista.filter(e => e.categoria === categoriaAtiva.value);

	const termo = filtroProduto.value.trim().toLowerCase();
	if (termo)
		lista = lista.filter(e => e.nome.toLowerCase().includes(termo));

	return lista;
});

// ─────────────────────────────────────────────────────────────────────────────
// AÇÕES
// ─────────────────────────────────────────────────────────────────────────────

// Abre/fecha item do FAQ; clicar no mesmo índice já aberto fecha tudo
const toggleFaq = (index) => {
	faqAberto.value = faqAberto.value === index ? null : index;
};

// Abre o WhatsApp com mensagem pré-preenchida
// Para alterar números: edite o objeto fones abaixo
const falarCom = (quem) => {
	const fones = {
		Cesar:  '5541997352785',
		Darlan: '5541992515319',
	};
	const msg = encodeURIComponent(`Olá ${quem}! Gostaria de informações sobre a locação de equipamentos.`);
	window.open(`https://wa.me/${fones[quem]}?text=${msg}`, '_blank');
	mostrarOpcoesContato.value = false;
};
</script>
