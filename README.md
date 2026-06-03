<!DOCTYPE html>
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
    
    <!-- Configuração do Tailwind -->
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
        body {
            background-color: #fcfcfc;
            color: #111111;
            overflow-x: hidden;
        }

        /* Ocultar scrollbar vertical principal */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #fcfcfc;
        }
        ::-webkit-scrollbar-thumb {
            background: #e5e5e5;
            border-radius: 10px;
        }

        /* Scroll Horizontal das Mini Galerias */
        .horizontal-scroll {
            overflow-x: auto;
            scroll-behavior: smooth;
            -webkit-overflow-scrolling: touch;
            scrollbar-width: none; /* Firefox */
        }
        .horizontal-scroll::-webkit-scrollbar {
            display: none; /* Chrome/Safari */
        }

        /* Animações de entrada */
        .reveal-up {
            opacity: 0;
            transform: translateY(40px);
            transition: all 1s cubic-bezier(0.16, 1, 0.3, 1);
        }
        .reveal-up.active {
            opacity: 1;
            transform: translateY(0);
        }

        /* Hero Image */
        .hero-img {
            height: 120%;
            width: 100%;
            object-fit: cover;
            transform-origin: center;
        }

        /* Efeito de profundidade nas obras */
        .artwork-card img {
            transition: transform 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);
        }
        .artwork-card:hover img {
            transform: scale(1.04);
        }
        .artwork-card .overlay {
            opacity: 0;
            transition: opacity 0.4s ease;
            background: linear-gradient(to top, rgba(17,17,17,0.8) 0%, rgba(17,17,17,0) 100%);
        }
        .artwork-card:hover .overlay {
            opacity: 1;
        }

        /* Lightbox */
        #lightbox {
            transition: opacity 0.4s ease, visibility 0.4s ease;
        }
        #lightbox.hidden-modal {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }
    </style>
</head>
<body class="antialiased selection:bg-gallery-black selection:text-white">

    <nav class="fixed top-0 w-full z-40 p-6 md:p-10 flex justify-between items-center mix-blend-difference text-white pointer-events-none">
        <div class="text-2xl font-serif tracking-widest pointer-events-auto cursor-pointer" onclick="window.scrollTo(0,0)">GALERIA BOI</div>
        <div class="hidden md:flex gap-8 text-sm font-sans tracking-widest uppercase pointer-events-auto">
            <a href="#acervo" class="hover:opacity-60 transition-opacity">Acervo</a>
            <a href="#sobre" class="hover:opacity-60 transition-opacity">A Galeria</a>
        </div>
        <div class="pointer-events-auto md:hidden">
            <button class="uppercase text-xs tracking-widest">Menu</button>
        </div>
    </nav>

    <!-- Hero Section -->
    <header class="min-h-screen flex flex-col lg:flex-row relative">
        <div class="w-full lg:w-4/12 min-h-screen flex flex-col justify-center px-8 md:px-16 pt-32 lg:pt-0 z-10 bg-gallery-white">
            <div class="max-w-sm">
                <p class="text-gallery-gray text-xs tracking-[0.2em] uppercase mb-4">Acervo Permanente</p>
                <h1 class="text-5xl md:text-6xl font-serif leading-tight mb-8">10 Vozes.<br>100 Obras.</h1>
                <p class="font-sans text-gallery-gray font-light leading-relaxed mb-10 text-sm">
                    Um catálogo imersivo dos artistas mais proeminentes da nossa curadoria. Deslize para baixo para conhecer os criadores e horizontalmente para explorar suas respectivas mini galerias.
                </p>
                <a href="#acervo" class="inline-flex items-center gap-4 text-xs uppercase tracking-widest font-medium group pb-2 border-b border-gallery-black/20 hover:border-gallery-black transition-colors">
                    Explorar Acervo
                    <span class="transform transition-transform group-hover:translate-x-2">↓</span>
                </a>
            </div>
        </div>

        <div class="w-full lg:w-8/12 h-[60vh] lg:h-screen overflow-hidden relative mt-12 lg:mt-0 bg-gray-100">
            <img src="https://images.unsplash.com/photo-1577720580479-7d839d829c73?q=80&w=2000&auto=format&fit=crop" 
                 alt="Interior da Galeria" 
                 class="hero-img" 
                 id="heroImage">
        </div>
    </header>

    <!-- Seção Principal: Artistas e Mini Galerias -->
    <section id="acervo" class="pt-24 pb-16 bg-gallery-white">
        <div class="max-w-[1600px] mx-auto">
            
            <div class="text-center mb-24 px-6 reveal-up">
                <h2 class="text-3xl md:text-4xl font-serif mb-4">Nossos Artistas</h2>
                <p class="font-sans text-gallery-gray font-light text-sm uppercase tracking-widest">Deslize horizontalmente nas obras</p>
            </div>

            <!-- O JavaScript injetará os 10 artistas aqui -->
            <div id="artists-container" class="flex flex-col gap-8"></div>

        </div>
    </section>

    <!-- Rodapé -->
    <footer id="sobre" class="bg-gallery-offwhite py-24 px-6 lg:px-12 mt-24">
        <div class="max-w-screen-2xl mx-auto grid grid-cols-1 md:grid-cols-4 gap-12 font-sans">
            <div class="md:col-span-1">
                <h2 class="text-2xl font-serif tracking-widest mb-6">GALERIA BOI</h2>
                <p class="text-sm text-gallery-gray font-light">Exposições imersivas e curatoriais.</p>
            </div>
            <div class="md:col-span-1">
                <h4 class="uppercase tracking-widest text-xs font-semibold mb-6">Localização</h4>
                <p class="text-sm text-gallery-gray font-light leading-relaxed">
                    Rua Augusta, 2500<br>São Paulo - SP<br>Ter - Sáb, 11h às 19h
                </p>
            </div>
            <div class="md:col-span-1">
                <h4 class="uppercase tracking-widest text-xs font-semibold mb-6">Contato</h4>
                <ul class="text-sm text-gallery-gray font-light space-y-2">
                    <li><a href="#" class="hover:text-gallery-black">contato@galeriaboi.com</a></li>
                    <li><a href="#" class="hover:text-gallery-black">Instagram</a></li>
                </ul>
            </div>
        </div>
    </footer>

    <!-- Modal Tela Cheia (Lightbox) -->
    <div id="lightbox" class="hidden-modal fixed inset-0 z-50 bg-gallery-white flex flex-col lg:flex-row h-screen">
        <button onclick="closeLightbox()" class="absolute top-6 right-6 lg:top-10 lg:right-10 z-50 p-2 group cursor-pointer">
            <span class="block w-6 h-px bg-gallery-black transform rotate-45 translate-y-0.5"></span>
            <span class="block w-6 h-px bg-gallery-black transform -rotate-45 -translate-y-0.5"></span>
        </button>

        <div class="w-full lg:w-3/4 h-[55vh] lg:h-full bg-[#f2f2f2] flex items-center justify-center p-8 lg:p-24 relative select-none">
            <img id="lb-image" src="" alt="Obra" class="max-w-full max-h-full object-contain shadow-2xl transition-opacity duration-300">
            
            <button onclick="prevImage(event)" class="absolute left-4 lg:left-8 top-1/2 -translate-y-1/2 p-4 text-3xl font-serif text-gallery-gray hover:text-gallery-black bg-white/50 rounded-full backdrop-blur-sm lg:bg-transparent lg:backdrop-blur-none transition-all cursor-pointer">←</button>
            <button onclick="nextImage(event)" class="absolute right-4 lg:right-8 top-1/2 -translate-y-1/2 p-4 text-3xl font-serif text-gallery-gray hover:text-gallery-black bg-white/50 rounded-full backdrop-blur-sm lg:bg-transparent lg:backdrop-blur-none transition-all cursor-pointer">→</button>
        </div>

        <div class="w-full lg:w-1/4 h-[45vh] lg:h-full overflow-y-auto p-8 lg:p-12 flex flex-col border-l border-gray-200">
            <span id="lb-artist" class="text-xs tracking-widest uppercase mb-2 block font-sans text-gallery-gray">Artista</span>
            <h2 id="lb-title" class="text-2xl lg:text-3xl font-serif mb-2">Título</h2>
            <p id="lb-year" class="font-sans text-gallery-gray mb-8 text-sm">Ano</p>
            
            <div class="space-y-4 text-sm font-sans text-gallery-gray font-light mb-8 border-t border-gray-200 pt-6">
                <div><strong class="block text-gallery-black uppercase tracking-widest text-[10px] mb-1">Técnica</strong><span id="lb-technique"></span></div>
                <div><strong class="block text-gallery-black uppercase tracking-widest text-[10px] mb-1">Dimensões</strong><span id="lb-dimensions"></span></div>
            </div>

            <div class="mt-auto pt-8">
                <button class="w-full py-4 border border-gallery-black text-xs uppercase tracking-widest font-sans hover:bg-gallery-black hover:text-white transition-colors duration-300 cursor-pointer">
                    Solicitar Valor
                </button>
            </div>
        </div>
    </div>

    <script>
        // --- 1. BANCO DE DADOS DA GALERIA (10 Artistas) ---
        // Para otimização, definimos os artistas e um gerador de obras para criar as 100 imagens dinamicamente.
        
        const baseImages = [
            "1513364776144-60967b0f800f", "1579783900882-c0d3dad7b119", "1605721911519-3dfeb3be25e7",
            "1561214115-f2f134cc4912", "1536924430914-91f9e2041b83", "1541961017774-22349e4a1262",
            "1501472312651-726afe119ff1", "1508138221679-760a23a2285b", "1574169208507-84376144848b",
            "1550684848-fac1c5b4e853", "1580136608260-4ebf0ea02fca", "1493219686084-dfa0eb1b2383"
        ];

        const artistProfiles = [
            {
                name: "Elias Vannucci",
                role: "Pintura Abstrata",
                photo: "https://images.unsplash.com/photo-1551192243-7f2a13cc7f39?w=300&h=300&fit=crop&grayscale",
                bio: "Desafia noções tradicionais de perspectiva. Suas obras exploram a tensão entre o espaço construído e a fluidez do subconsciente."
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

        // Variáveis globais de Estado
        let allArtworks = []; // Armazenará as 100 obras linearmente para o Lightbox global
        let currentLightboxIndex = 0;

        // Função para gerar dados aleatórios realistas de obras
        function generateArtworksForArtist(artistName, artistIndex) {
            const artworks = [];
            const techniques = ["Óleo sobre tela", "Acrílica e areia", "Nanquim sobre papel", "Técnica Mista", "Pigmento mineral"];
            
            for (let i = 1; i <= 10; i++) {
                // Pegar uma imagem base diferente com base no índice para variar a estética
                const imgBaseId = baseImages[(artistIndex + i) % baseImages.length];
                // Mudar parâmetros de corte da URL para a mesma imagem parecer diferente
                const cropParams = `&rect=${i*100},${i*50},800,1000`; 
                const imgUrl = `https://images.unsplash.com/photo-${imgBaseId}?auto=format&fit=crop&w=600&q=80${cropParams}`;
                
                const artwork = {
                    globalIndex: allArtworks.length, 
                    artist: artistName,
                    title: `Estudo nº ${i} - Série ${artistIndex + 1}`,
                    year: `202${Math.floor(Math.random() * 4)}`, // 2020 a 2023
                    technique: techniques[Math.floor(Math.random() * techniques.length)],
                    dimensions: `${100 + (i*10)} x ${120 + (i*5)} cm`,
                    img: imgUrl
                };
                
                artworks.push(artwork);
                allArtworks.push(artwork); 
            }
            return artworks;
        }

        // --- 2. RENDERIZAÇÃO DA PÁGINA ---
        const container = document.getElementById('artists-container');

        artistProfiles.forEach((artist, index) => {
            // Gera as 10 obras deste artista
            const artistArtworks = generateArtworksForArtist(artist.name, index);
            
            // HTML dos Cards das Obras
            let artworksHTML = '';
            artistArtworks.forEach(art => {
                artworksHTML += `
                    <div class="w-[280px] md:w-[320px] flex-shrink-0 snap-start group cursor-pointer artwork-card" 
                         onclick="openLightbox(${art.globalIndex})">
                        <div class="w-full aspect-[3/4] overflow-hidden bg-gray-100 relative">
                            <img src="${art.img}" alt="${art.title}" loading="lazy" 
                                 class="w-full h-full object-cover">
                            <div class="overlay absolute inset-0 flex items-end p-6">
                                <span class="text-white text-xs tracking-widest uppercase border-b border-white/50 pb-1">Ver Detalhes</span>
                            </div>
                        </div>
                        <div class="mt-4">
                            <h4 class="font-serif text-lg text-gallery-black group-hover:text-gallery-gray transition-colors">${art.title}</h4>
                            <p class="text-xs text-gallery-gray font-sans mt-1 uppercase tracking-wider">${art.year} • ${art.technique}</p>
                        </div>
                    </div>
                `;
            });

            // HTML do Bloco do Artista
            const artistHTML = `
                <div class="artist-block reveal-up border-b border-gray-200 pb-24 mb-12 last:border-0">
                    
                    <!-- Cabeçalho do Artista -->
                    <div class="flex flex-col md:flex-row items-start gap-6 px-6 lg:px-12 mb-10">
                        <div class="w-28 h-28 md:w-32 md:h-32 flex-shrink-0">
                            <img src="${artist.photo}" alt="${artist.name}" class="w-full h-full object-cover shadow-sm">
                        </div>
                        <div class="flex-1 max-w-2xl pt-2 text-left">
                            <h3 class="text-3xl font-serif mb-1">${artist.name}</h3>
                            <p class="text-xs uppercase tracking-widest text-gallery-gray font-semibold mb-4">${artist.role}</p>
                            <p class="text-sm font-sans font-light text-gray-700 leading-relaxed">${artist.bio}</p>
                        </div>
                    </div>

                    <!-- Mini Galeria Horizontal -->
                    <div class="w-full pl-6 lg:pl-12 text-left">
                        <div class="horizontal-scroll flex gap-6 pb-6 snap-x">
                            ${artworksHTML}
                        </div>
                    </div>
                </div>
            `;
            container.insertAdjacentHTML('beforeend', artistHTML);
        });

        // --- 3. LÓGICA DO LIGHTBOX ---
        const lightbox = document.getElementById('lightbox');
        const lbImg = document.getElementById('lb-image');
        
        function updateLightbox() {
            const data = allArtworks[currentLightboxIndex];
            
            // Efeito fade out/in para troca suave
            lbImg.style.opacity = '0';
            setTimeout(() => {
                lbImg.src = data.img;
                document.getElementById('lb-artist').innerText = data.artist;
                document.getElementById('lb-title').innerText = data.title;
                document.getElementById('lb-year').innerText = data.year;
                document.getElementById('lb-technique').innerText = data.technique;
                document.getElementById('lb-dimensions').innerText = data.dimensions;
                lbImg.style.opacity = '1';
            }, 150);
        }

        window.openLightbox = function(globalIndex) {
            currentLightboxIndex = globalIndex;
            updateLightbox();
            lightbox.classList.remove('hidden-modal');
            document.body.style.overflow = 'hidden'; 
        }

        window.closeLightbox = function() {
            lightbox.classList.add('hidden-modal');
            document.body.style.overflow = 'auto'; 
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

        // Eventos de teclado
        document.addEventListener('keydown', (e) => {
            if (lightbox.classList.contains('hidden-modal')) return;
            if (e.key === "Escape") closeLightbox();
            if (e.key === "ArrowRight") nextImage();
            if (e.key === "ArrowLeft") prevImage();
        });

        // --- 4. ANIMAÇÕES DE SCROLL E PARALLAX ---
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

        // Parallax na Hero
        const heroImage = document.getElementById('heroImage');
        window.addEventListener('scroll', () => {
            const scrollY = window.scrollY;
            if (scrollY < window.innerHeight) {
                heroImage.style.transform = `translateY(${scrollY * 0.25}px)`;
            }
        });
    </script>
</body>
</html>
