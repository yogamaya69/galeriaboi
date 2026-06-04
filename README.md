<html lang="pt-BR" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galeria Boi | Arte Contemporânea</title>
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&family=Playfair+Display:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Playfair Display', 'serif'],
                    },
                    colors: {
                        'gallery-white': '#fcfcfc',
                        'gallery-offwhite': '#f5f5f5',
                        'gallery-black': '#111111',
                        'gallery-gray': '#888888',
                    }
                }
            }
        }
    </script>

    <style>
        /* --- HACKS ANTI-JEKYLL PARA O GITHUB PAGES --- */
        body, html {
            margin: 0 !important;
            padding: 0 !important;
            max-width: 100% !important;
            background-color: #fcfcfc;
            color: #111111;
            overflow-x: hidden;
        }
        .wrapper, .container-lg, main.page-content, .markdown-body, .main-content { 
            max-width: 100% !important; 
            margin: 0 !important; 
            padding: 0 !important; 
            background: transparent !important;
            border: none !important;
        }
        .site-header, .site-footer, header.header, .page-header, body > header { 
            display: none !important; 
        }
        .markdown-body h1:first-child, .markdown-body > h1:first-of-type, #project_title {
            display: none !important;
        }

        /* --- Custom Scrollbar --- */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #fcfcfc;
        }
        ::-webkit-scrollbar-thumb {
            background: #d1d5db;
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #9ca3af;
        }

        /* --- Scroll Horizontal das Mini Galerias --- */
        .horizontal-scroll {
            overflow-x: auto;
            scroll-behavior: smooth;
            -webkit-overflow-scrolling: touch;
            scrollbar-width: none;
            cursor: grab;
        }
        .horizontal-scroll:active {
            cursor: grabbing;
        }
        .horizontal-scroll.is-dragging {
            scroll-behavior: auto;
            scroll-snap-type: none;
        }
        .horizontal-scroll::-webkit-scrollbar {
            display: none;
        }

        /* --- Animações de entrada --- */
        .reveal-up {
            opacity: 0;
            transform: translateY(40px);
            transition: all 1s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .reveal-up.active {
            opacity: 1;
            transform: translateY(0);
        }

        /* --- Hero Image Parallax Box --- */
        .hero-img-container {
            clip-path: inset(0);
        }
        .hero-img {
            position: absolute;
            top: -10%;
            left: 0;
            width: 100%;
            height: 120%;
            object-fit: cover;
            transform-origin: center;
            will-change: transform;
        }

        /* --- Efeito de profundidade nas obras --- */
        .artwork-card img {
            transition: transform 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
            will-change: transform;
        }
        .artwork-card:hover img {
            transform: scale(1.05);
        }
        .artwork-card .overlay {
            opacity: 0;
            transition: opacity 0.4s ease;
            background: linear-gradient(to top, rgba(17,17,17,0.7) 0%, rgba(17,17,17,0) 100%);
        }
        .artwork-card:hover .overlay {
            opacity: 1;
        }

        /* --- Lightbox e Menu --- */
        #lightbox, #mobile-menu {
            transition: opacity 0.3s ease, visibility 0.3s ease;
        }
        .hidden-modal, .hidden-menu {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }
    </style>
</head>
<body class="antialiased selection:bg-gallery-black selection:text-white">

    <!-- Navegação -->
    <nav id="navbar" class="fixed top-0 w-full z-[99] transition-all duration-300 pointer-events-none">
        <div id="nav-container" class="flex justify-between items-center px-6 py-5 md:px-12 md:py-8 w-full transition-all duration-300 pointer-events-auto">
            
            <!-- Logo em Imagem (Apenas 'invert' para ficar branca no topo escuro) -->
            <img id="main-logo" src="./logoboi.svg" alt="Galeria Boi" class="h-12 md:h-20 w-auto object-contain cursor-pointer transition-all duration-300 origin-left invert" style="mix-blend-mode: normal !important;" onclick="window.scrollTo(0,0)">
            
            <!-- Desktop Links -->
            <div id="desktop-links" class="hidden md:flex gap-8 text-sm font-sans tracking-widest uppercase mix-blend-difference text-white transition-colors duration-300">
                <a href="#acervo" class="hover:opacity-60 transition-opacity">Acervo</a>
                <a href="#sobre" class="hover:opacity-60 transition-opacity">A Galeria</a>
            </div>
            
            <!-- Mobile Menu Button -->
            <div id="mobile-btn" class="md:hidden mix-blend-difference text-white transition-colors duration-300">
                <button onclick="toggleMobileMenu()" class="uppercase text-xs tracking-widest hover:opacity-70 transition-opacity">Menu</button>
            </div>
        </div>
    </nav>

    <!-- Menu Mobile Overlay -->
    <div id="mobile-menu" class="hidden-menu fixed inset-0 z-[100] bg-gallery-black text-white flex flex-col justify-center items-center">
        <button onclick="toggleMobileMenu()" class="absolute top-6 right-6 p-4 uppercase text-xs tracking-widest opacity-70 hover:opacity-100">Fechar</button>
        <div class="flex flex-col gap-10 text-center font-serif text-3xl">
            <a href="#acervo" onclick="toggleMobileMenu()" class="hover:text-gallery-gray transition-colors">Acervo</a>
            <a href="#sobre" onclick="toggleMobileMenu()" class="hover:text-gallery-gray transition-colors">A Galeria</a>
            <a href="mailto:contato@galeriaboi.com" class="hover:text-gallery-gray transition-colors">Contato</a>
        </div>
    </div>

    <!-- Hero Section -->
    <section id="hero" class="w-full min-h-screen flex flex-col lg:flex-row relative bg-gallery-white">
        <!-- Lado do Texto -->
        <div class="w-full lg:w-1/2 flex flex-col justify-center px-8 md:px-16 lg:px-24 pt-32 pb-16 lg:py-0 z-10 min-h-[60vh] lg:min-h-screen">
            <div class="max-w-xl reveal-up active mx-auto lg:mx-0 w-full">
                <p class="text-gallery-gray text-sm md:text-base tracking-[0.2em] uppercase mb-6 font-medium">Acervo Permanente</p>
                <h1 class="text-6xl md:text-7xl lg:text-[5.5rem] font-serif leading-none mb-10">NOVA FORNOS</h1>
                <p class="font-sans text-gallery-gray font-light leading-relaxed mb-12 text-base md:text-lg">
                    Um catálogo imersivo dos artistas mais proeminentes da nossa curadoria. Deslize para baixo para conhecer os criadores e horizontalmente para explorar suas respectivas mini galerias.
                </p>
                <a href="#acervo" class="inline-flex items-center gap-4 text-sm uppercase tracking-widest font-medium group pb-2 border-b border-gallery-black/20 hover:border-gallery-black transition-colors">
                    Explorar Acervo
                    <span class="transform transition-transform group-hover:translate-y-1">↓</span>
                </a>
            </div>
        </div>

        <!-- Lado da Imagem com o ficheiro galeria.jpg -->
        <div class="w-full lg:w-1/2 h-[50vh] lg:h-screen relative overflow-hidden bg-gray-100 hero-img-container">
            <img src="./galeria.jpg" 
                 alt="Interior da Galeria de Arte" 
                 class="hero-img" 
                 id="heroImage">
        </div>
    </section>

    <!-- Seção Principal: Artistas e Mini Galerias -->
    <section id="acervo" class="pt-24 pb-16 bg-gallery-white w-full">
        <div class="max-w-[1800px] mx-auto w-full">
            
            <div class="text-center mb-16 md:mb-24 px-4 md:px-6 reveal-up w-full">
                <h2 class="text-4xl md:text-5xl font-serif mb-8 md:mb-12">Nossos Artistas</h2>
                <div class="border-t border-gray-200 w-full mb-6 md:mb-8"></div>
                <div class="flex items-center justify-center gap-2 md:gap-4 text-gallery-gray">
                    <span class="text-base md:text-lg -translate-y-[1px]">←</span>
                    <p class="font-sans font-light text-[10px] md:text-sm uppercase tracking-widest md:tracking-[0.25em] max-w-[220px] md:max-w-none leading-relaxed md:leading-none">Deslize ou arraste as obras horizontalmente</p>
                    <span class="text-base md:text-lg -translate-y-[1px]">→</span>
                </div>
            </div>

            <!-- O JavaScript injetará os artistas aqui -->
            <div id="artists-container" class="flex flex-col gap-16 md:gap-24 w-full"></div>

        </div>
    </section>

    <!-- Rodapé PRETO -->
    <footer id="sobre" class="bg-gallery-black text-white py-24 px-8 md:px-16 mt-12 w-full">
        <div class="max-w-screen-2xl mx-auto grid grid-cols-1 md:grid-cols-4 gap-12 font-sans">
            <div class="md:col-span-2">
                <!-- Logo no Rodapé (Apenas 'invert' para ficar branca) -->
                <img src="./logoboi.svg" alt="Logo Galeria Boi" class="h-16 md:h-24 w-auto mb-8 object-contain origin-left invert" style="mix-blend-mode: normal !important;">
                <p class="text-base text-gray-400 font-light max-w-md leading-relaxed">Dedicada a expor as narrativas visuais mais instigantes da arte contemporânea, com exposições imersivas e curatoriais focadas no diálogo entre a materialidade e o espaço.</p>
            </div>
            
            <div class="md:col-span-1 flex flex-col items-start text-left w-full">
                <h4 class="uppercase tracking-widest text-xs font-semibold mb-6 text-white w-full">Localização</h4>
                <p class="text-sm text-gray-400 font-light leading-relaxed w-full">
                    Travessa Mestre Vitalino, 9a<br>
                    Alto do Moura, Caruaru - PE<br>
                    Ter - Sáb, 11h às 19h
                </p>
            </div>
            
            <div class="md:col-span-1 flex flex-col items-start text-left w-full">
                <h4 class="uppercase tracking-widest text-xs font-semibold mb-6 text-white w-full">Contato</h4>
                <ul class="text-sm text-gray-400 font-light space-y-3 w-full p-0 m-0">
                    <li><a href="mailto:contato@galeriaboi.com" class="hover:text-white transition-colors">contato@galeriaboi.com</a></li>
                    <li><a href="#" class="hover:text-white transition-colors">+55 11 9999-0000</a></li>
                    <li><a href="https://www.instagram.com/galeriaboi/" target="_blank" rel="noopener noreferrer" class="hover:text-white transition-colors">Instagram</a></li>
                </ul>
            </div>
        </div>
        <div class="max-w-screen-2xl mx-auto mt-24 pt-8 border-t border-gray-800 text-xs text-gray-500 flex flex-col md:flex-row justify-between items-center gap-4">
            <p>&copy; 2026 Galeria Boi. Todos os direitos reservados.</p>
            <p>Design web otimizado</p>
        </div>
    </footer>

    <!-- Modal Tela Cheia (Lightbox) -->
    <div id="lightbox" class="hidden-modal fixed inset-0 z-[110] bg-gallery-white flex flex-col lg:flex-row h-[100dvh]">
        <!-- Botão Fechar -->
        <button aria-label="Fechar galeria" onclick="closeLightbox()" class="absolute top-4 right-4 lg:top-8 lg:right-8 z-[120] p-4 group cursor-pointer bg-white/50 lg:bg-transparent rounded-full backdrop-blur-md lg:backdrop-blur-none">
            <span class="block w-6 h-px bg-gallery-black transform rotate-45 translate-y-0.5 transition-transform group-hover:bg-red-500"></span>
            <span class="block w-6 h-px bg-gallery-black transform -rotate-45 -translate-y-0.5 transition-transform group-hover:bg-red-500"></span>
        </button>

        <!-- Área da Imagem -->
        <div class="w-full lg:w-3/4 h-[50dvh] lg:h-full bg-[#f2f2f2] flex items-center justify-center p-4 lg:p-24 relative select-none">
            <img id="lb-image" src="" alt="Obra de arte em detalhes" class="max-w-full max-h-full object-contain shadow-xl transition-opacity duration-300">
            
            <button aria-label="Obra anterior" onclick="prevImage(event)" class="absolute left-2 lg:left-8 top-1/2 -translate-y-1/2 p-3 lg:p-4 text-2xl lg:text-3xl font-serif text-gallery-black lg:text-gallery-gray lg:hover:text-gallery-black bg-white/70 rounded-full backdrop-blur-md transition-all cursor-pointer z-10 shadow-sm">←</button>
            <button aria-label="Próxima obra" onclick="nextImage(event)" class="absolute right-2 lg:right-8 top-1/2 -translate-y-1/2 p-3 lg:p-4 text-2xl lg:text-3xl font-serif text-gallery-black lg:text-gallery-gray lg:hover:text-gallery-black bg-white/70 rounded-full backdrop-blur-md transition-all cursor-pointer z-10 shadow-sm">→</button>
        </div>

        <!-- Área de Informações -->
        <div class="w-full lg:w-1/4 h-[50dvh] lg:h-full overflow-y-auto p-6 lg:p-12 flex flex-col bg-white">
            <span id="lb-artist" class="text-xs tracking-widest uppercase mb-3 block font-sans text-gallery-gray">Artista</span>
            <h2 id="lb-title" class="text-2xl lg:text-3xl font-serif mb-2 leading-tight">Título</h2>
            <p id="lb-year" class="font-sans text-gallery-gray mb-6 text-sm">Ano</p>
            
            <div class="space-y-5 text-sm font-sans text-gallery-gray font-light mb-8 border-t border-gray-100 pt-6">
                <div>
                    <strong class="block text-gallery-black uppercase tracking-widest text-[10px] mb-1">Técnica</strong>
                    <span id="lb-technique"></span>
                </div>
                <div>
                    <strong class="block text-gallery-black uppercase tracking-widest text-[10px] mb-1">Dimensões</strong>
                    <span id="lb-dimensions"></span>
                </div>
            </div>

            <div class="mt-auto pt-6">
                <button class="w-full py-4 border border-gallery-black text-xs uppercase tracking-widest font-sans hover:bg-gallery-black hover:text-white transition-colors duration-300 cursor-pointer">
                    Solicitar Valor
                </button>
            </div>
        </div>
    </div>

    <!-- JAVASCRIPT -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // --- 1. BANCO DE DADOS DA GALERIA ---
            const baseImages = [
                "1513364776144-60967b0f800f", "1579783900882-c0d3dad7b119", "1605721911519-3dfeb3be25e7",
                "1561214115-f2f134cc4912", "1536924430914-91f9e2041b83", "1541961017774-22349e4a1262",
                "1501472312651-726afe119ff1", "1508138221679-760a23a2285b", "1574169208507-84376144848b",
                "1550684848-fac1c5b4e853", "1580136608260-4ebf0ea02fca", "1493219686084-dfa0eb1b2383",
                "1573521193826-58c7dc2e13e3", "1549490349-b02d1a50b0c5", "1518998053901-537628eb9203",
                "1507643179773-3e975d7ac515", "1515405295579-ba7b45403062", "1500462918059-b1a0cb512f1d"
            ];

            const artistProfiles = [
                {
                    name: "Tony Granton",
                    role: "Artista Visual",
                    photo: "tony.png",
                    bio: "Toni Graton (Curitiba, PR) é artista visual e gravador, formado pela Escola de Música e Belas Artes do Paraná (UNESPAR, 2017). Atua principalmente com gravura em metal e cerâmica, desenvolvendo uma produção que combina técnicas tradicionais e recursos digitais."
                },
                {
                    name: "Clara Luz",
                    role: "Escultura Minimalista",
                    photo: "https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=300&h=300&fit=crop&grayscale",
                    bio: "Foca na materialidade do vazio. Suas obras não ocupam espaço, mas parecem dobrar a luz ao seu redor criando quietude."
                },
                {
                    name: "João Bosco",
                    role: "Técnica Mista",
                    photo: "https://images.unsplash.com/photo-1506794778202-cad84cf45f1d?w=300&h=300&fit=crop&grayscale",
                    bio: "Através da sobreposição de imagens e pigmentos naturais, mapeia o apagamento da memória na paisagem urbana moderna."
                },
                {
                    name: "Marina Silva",
                    role: "Arte Geométrica",
                    photo: "https://images.unsplash.com/photo-1544005313-94ddf0286df2?w=300&h=300&fit=crop&grayscale",
                    bio: "Busca o equilíbrio impossível. Seus quadros utilizam cores primárias e linhas retas para questionar a ordem lógica visual."
                },
                {
                    name: "Koji Tanaka",
                    role: "Nanquim Contemporâneo",
                    photo: "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=300&h=300&fit=crop&grayscale",
                    bio: "Mestre na técnica do espaço negativo. Um único traço negro rasga o canvas branco, representando o tempo e a respiração."
                },
                {
                    name: "Elena Rostova",
                    role: "Arte Têxtil",
                    photo: "https://images.unsplash.com/photo-1531746020798-e6953c6e8e04?w=300&h=300&fit=crop&grayscale",
                    bio: "Trabalha com linho cru, cordas e tecelagem orgânica para discutir a relação entre o trabalho manual e a tecnologia."
                },
                {
                    name: "David Osei",
                    role: "Fotografia Arquitetônica",
                    photo: "https://images.unsplash.com/photo-1531384441138-2736e62e0919?w=300&h=300&fit=crop&grayscale",
                    bio: "Fotografa brutalismo ao redor do mundo, isolando blocos de concreto até que pareçam ilhas flutuantes sem contexto de escala."
                },
                {
                    name: "Sofia Mendoza",
                    role: "Cerâmica Desconstruída",
                    photo: "https://images.unsplash.com/photo-1554151228-14d9def656e4?w=300&h=300&fit=crop&grayscale",
                    bio: "Quebra propositalmente seus vasos após a queima, reconstruindo-os com resinas metálicas inspiradas na técnica kintsugi."
                },
                {
                    name: "Lucas Ferrari",
                    role: "Arte Digital Experimental",
                    photo: "https://images.unsplash.com/photo-1500648767791-00dcc994a43e?w=300&h=300&fit=crop&grayscale",
                    bio: "Usa algoritmos e ruído de dados corrompidos para gerar telas que expõem a fragilidade da nossa memória digital."
                },
                {
                    name: "Amara Diop",
                    role: "Retratos de Colagem",
                    photo: "https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=300&h=300&fit=crop&grayscale",
                    bio: "Despedaça revistas de moda antigas para criar retratos hiper-realistas, questionando os padrões estéticos impostos."
                }
            ];

            let allArtworks = [];
            let currentLightboxIndex = 0;

            function generateArtworksForArtist(artistName, artistIndex) {
                const artworks = [];
                const techniques = ["Óleo sobre tela", "Acrílica e areia", "Nanquim sobre papel", "Técnica Mista", "Pigmento mineral", "Impressão Fine Art"];
                
                for (let i = 1; i <= 10; i++) {
                    const imgBaseId = baseImages[(artistIndex * 10 + i) % baseImages.length];
                    const uniqueSig = artistIndex * 10 + i;
                    
                    let imgUrl = `https://images.unsplash.com/photo-${imgBaseId}?auto=format&fit=crop&w=600&h=800&q=80&sig=${uniqueSig}`;
                    
                    if (artistIndex === 0) {
                        const imgNumber = i.toString().padStart(2, '0');
                        imgUrl = `./tonyobra${imgNumber}.webp`;
                    }
                    
                    const artwork = {
                        globalIndex: allArtworks.length, 
                        artist: artistName,
                        title: `Estudo nº ${i} - Série ${(artistIndex % 3) + 1}`,
                        year: `202${Math.floor(Math.random() * 4) + 1}`,
                        technique: techniques[Math.floor(Math.random() * techniques.length)],
                        dimensions: `${100 + (i*5)} x ${120 + (i*2)} cm`,
                        img: imgUrl
                    };
                    
                    artworks.push(artwork);
                    allArtworks.push(artwork); 
                }
                return artworks;
            }

            // --- 2. RENDERIZAÇÃO DA PÁGINA ---
            const container = document.getElementById('artists-container');
            window.isDragging = false;

            artistProfiles.forEach((artist, index) => {
                const artistArtworks = generateArtworksForArtist(artist.name, index);
                let artworksHTML = '';
                
                artistArtworks.forEach(art => {
                    artworksHTML += `
                        <div class="w-[260px] md:w-[320px] flex-shrink-0 snap-start group cursor-pointer artwork-card" 
                             onclick="if(!window.isDragging) openLightbox(${art.globalIndex})">
                            <div class="w-full aspect-[3/4] overflow-hidden bg-gray-100 relative rounded-sm">
                                <img src="${art.img}" alt="${art.title} por ${art.artist}" loading="lazy" 
                                     class="w-full h-full object-cover" draggable="false">
                                <div class="overlay absolute inset-0 flex items-end p-6">
                                    <span class="text-white text-xs tracking-widest uppercase border-b border-white/50 pb-1 font-medium">Ver Detalhes</span>
                                </div>
                            </div>
                            <div class="mt-4 px-1">
                                <h4 class="font-serif text-lg text-gallery-black group-hover:text-gallery-gray transition-colors">${art.title}</h4>
                                <p class="text-xs text-gallery-gray font-sans mt-1.5 uppercase tracking-wider">${art.year} &bull; ${art.technique}</p>
                            </div>
                        </div>
                    `;
                });

                const artistHTML = `
                    <div class="artist-block reveal-up border-b border-gray-100 pb-16 md:pb-24 last:border-0 w-full">
                        <div class="flex flex-col md:flex-row items-start gap-6 md:gap-10 px-6 lg:px-16 mb-8 md:mb-12">
                            <div class="w-24 h-24 md:w-32 md:h-32 flex-shrink-0">
                                <img src="${artist.photo}" alt="Foto de ${artist.name}" class="w-full h-full object-cover rounded-full md:rounded-none grayscale hover:grayscale-0 transition-all duration-500">
                            </div>
                            <div class="flex-1 max-w-2xl pt-2 text-left">
                                <h3 class="text-3xl md:text-4xl font-serif mb-2">${artist.name}</h3>
                                <p class="text-xs uppercase tracking-widest text-gallery-gray font-semibold mb-4">${artist.role}</p>
                                <p class="text-sm md:text-base font-sans font-light text-gray-600 leading-relaxed">${artist.bio}</p>
                            </div>
                        </div>

                        <div class="w-full pl-6 lg:pl-16 text-left">
                            <div class="horizontal-scroll flex gap-4 md:gap-8 pb-8 snap-x snap-mandatory">
                                ${artworksHTML}
                                <!-- Espaçador para o scroll final -->
                                <div class="w-[20px] md:w-[40px] flex-shrink-0"></div>
                            </div>
                        </div>
                    </div>
                `;
                container.insertAdjacentHTML('beforeend', artistHTML);
            });

            // --- DRAG TO SCROLL ---
            const scrollContainers = document.querySelectorAll('.horizontal-scroll');
            scrollContainers.forEach(el => {
                let isDown = false;
                let startX;
                let scrollLeft;

                el.addEventListener('mousedown', (e) => {
                    isDown = true;
                    window.isDragging = false;
                    el.classList.add('is-dragging');
                    startX = e.pageX - el.offsetLeft;
                    scrollLeft = el.scrollLeft;
                });
                
                el.addEventListener('mouseleave', () => {
                    isDown = false;
                    el.classList.remove('is-dragging');
                });
                
                el.addEventListener('mouseup', () => {
                    isDown = false;
                    el.classList.remove('is-dragging');
                });
                
                el.addEventListener('mousemove', (e) => {
                    if (!isDown) return;
                    e.preventDefault();
                    window.isDragging = true;
                    const x = e.pageX - el.offsetLeft;
                    const walk = (x - startX) * 1.5; 
                    el.scrollLeft = scrollLeft - walk;
                });
            });

            // --- 3. LÓGICA DO LIGHTBOX ---
            const lightbox = document.getElementById('lightbox');
            const lbImg = document.getElementById('lb-image');
            
            function updateLightbox() {
                const data = allArtworks[currentLightboxIndex];
                
                lbImg.style.opacity = '0';
                setTimeout(() => {
                    lbImg.src = data.img;
                    lbImg.alt = data.title;
                    document.getElementById('lb-artist').innerText = data.artist;
                    document.getElementById('lb-title').innerText = data.title;
                    document.getElementById('lb-year').innerText = data.year;
                    document.getElementById('lb-technique').innerText = data.technique;
                    document.getElementById('lb-dimensions').innerText = data.dimensions;
                    lbImg.style.opacity = '1';
                }, 200);
            }

            window.openLightbox = function(globalIndex) {
                currentLightboxIndex = globalIndex;
                updateLightbox();
                lightbox.classList.remove('hidden-modal');
                document.body.style.overflow = 'hidden'; 
            }

            window.closeLightbox = function() {
                lightbox.classList.add('hidden-modal');
                document.body.style.overflow = ''; 
            }

            window.nextImage = function(e) {
                if(e) e.stopPropagation();
                currentLightboxIndex = (currentLightboxIndex + 1) % allArtworks.length;
                updateLightbox();
            }

            window.prevImage = function(e) {
                if(e) e.stopPropagation();
                currentLightboxIndex = (currentLightboxIndex - 1 + allArtworks.length) % allArtworks.length;
                updateLightbox();
            }

            // --- 4. MENU MOBILE ---
            const mobileMenu = document.getElementById('mobile-menu');
            window.toggleMobileMenu = function() {
                mobileMenu.classList.toggle('hidden-menu');
                if(!mobileMenu.classList.contains('hidden-menu')) {
                    document.body.style.overflow = 'hidden';
                } else {
                    document.body.style.overflow = '';
                }
            }

            // --- 5. EVENTOS GERAIS ---
            document.addEventListener('keydown', (e) => {
                if (!lightbox.classList.contains('hidden-modal')) {
                    if (e.key === "Escape") closeLightbox();
                    if (e.key === "ArrowRight") nextImage();
                    if (e.key === "ArrowLeft") prevImage();
                }
            });

            const revealElements = document.querySelectorAll('.reveal-up');
            const revealObserver = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('active');
                        observer.unobserve(entry.target);
                    }
                });
            }, { root: null, threshold: 0.1, rootMargin: "0px 0px -50px 0px" });

            revealElements.forEach(el => revealObserver.observe(el));

            // Efeito da Navbar
            const heroImage = document.getElementById('heroImage');
            const navbar = document.getElementById('navbar');
            const navContainer = document.getElementById('nav-container');
            const desktopLinks = document.getElementById('desktop-links');
            const mobileBtn = document.getElementById('mobile-btn');
            const mainLogo = document.getElementById('main-logo');
            let ticking = false;

            window.addEventListener('scroll', () => {
                if (!ticking) {
                    window.requestAnimationFrame(() => {
                        const scrollY = window.scrollY;

                        if (scrollY > 50) {
                            navbar.classList.add('bg-white/90', 'backdrop-blur-md', 'border-b', 'border-gray-200', 'shadow-sm');
                            
                            navContainer.classList.remove('py-5', 'md:py-8');
                            navContainer.classList.add('py-3', 'md:py-4');
                            
                            desktopLinks.classList.remove('mix-blend-difference', 'text-white');
                            desktopLinks.classList.add('text-gallery-black');
                            
                            mobileBtn.classList.remove('mix-blend-difference', 'text-white');
                            mobileBtn.classList.add('text-gallery-black');

                            // Remove o invert para a logo ficar na cor original (preto) no fundo branco
                            mainLogo.classList.remove('invert');
                        } else {
                            navbar.classList.remove('bg-white/90', 'backdrop-blur-md', 'border-b', 'border-gray-200', 'shadow-sm');
                            
                            navContainer.classList.add('py-5', 'md:py-8');
                            navContainer.classList.remove('py-3', 'md:py-4');
                            
                            desktopLinks.classList.add('mix-blend-difference', 'text-white');
                            desktopLinks.classList.remove('text-gallery-black');
                            
                            mobileBtn.classList.add('mix-blend-difference', 'text-white');
                            mobileBtn.classList.remove('text-gallery-black');

                            // Adiciona o invert para a logo ficar branca no topo escuro
                            mainLogo.classList.add('invert');
                        }

                        // Parallax
                        if (scrollY < window.innerHeight) {
                            heroImage.style.transform = `translateY(${scrollY * 0.25}px)`;
                        }
                        ticking = false;
                    });
                    ticking = true;
                }
            });
        });
    </script>
</body>
</html>
