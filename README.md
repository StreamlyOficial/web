<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Streamly - Plataformas de Streaming</title>
    <!-- Tailwind CSS desde CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        background: 'var(--background)',
                        foreground: 'var(--foreground)',
                        purple: {
                            50: '#f5f3ff',
                            100: '#ede9fe',
                            200: '#ddd6fe',
                            300: '#c4b5fd',
                            400: '#a78bfa',
                            500: '#8b5cf6',
                            600: '#7c3aed',
                            700: '#6d28d9',
                            800: '#5b21b6',
                            900: '#4c1d95',
                            950: '#2e1065',
                        },
                    }
                }
            }
        }
    </script>
    <style>
        :root {
            --background: #ffffff;
            --foreground: #000000;
        }
        
        .dark {
            --background: #121212;
            --foreground: #ffffff;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
        }
        
        .sr-only {
            position: absolute;
            width: 1px;
            height: 1px;
            padding: 0;
            margin: -1px;
            overflow: hidden;
            clip: rect(0, 0, 0, 0);
            white-space: nowrap;
            border-width: 0;
        }
    </style>
</head>
<body class="flex min-h-screen flex-col bg-background text-foreground">
    <!-- Header -->
    <header class="sticky top-0 z-50 w-full border-b bg-background/95 backdrop-blur supports-[backdrop-filter]:bg-background/60">
        <div class="container mx-auto flex h-16 items-center justify-between px-4">
            <div class="flex items-center gap-2">
                <button id="menu-toggle" class="md:hidden rounded-md p-2 hover:bg-gray-100 dark:hover:bg-gray-800">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="h-6 w-6">
                        <line x1="4" x2="20" y1="12" y2="12"></line>
                        <line x1="4" x2="20" y1="6" y2="6"></line>
                        <line x1="4" x2="20" y1="18" y2="18"></line>
                    </svg>
                    <span class="sr-only">Toggle menu</span>
                </button>
                <a href="#" class="flex items-center gap-2 font-bold text-xl">
                    Streamly
                </a>
            </div>
            <nav id="mobile-menu" class="fixed inset-0 z-50 hidden flex-col bg-background p-6 md:hidden">
                <div class="flex items-center justify-between">
                    <a href="#" class="flex items-center gap-2 font-bold text-xl">
                        Streamly
                    </a>
                    <button id="close-menu" class="rounded-md p-2 hover:bg-gray-100 dark:hover:bg-gray-800">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="h-6 w-6">
                            <path d="M18 6 6 18"></path>
                            <path d="m6 6 12 12"></path>
                        </svg>
                        <span class="sr-only">Close menu</span>
                    </button>
                </div>
                <div class="mt-6 flex flex-col gap-4">
                    <a href="#plataformas" class="hover:text-purple-600">Plataformas</a>
                    <a href="#beneficios" class="hover:text-purple-600">Beneficios</a>
                    <a href="#faq" class="hover:text-purple-600">FAQ</a>
                    <a href="#contacto" class="hover:text-purple-600">Contacto</a>
                </div>
            </nav>
            <nav class="hidden md:flex items-center gap-6">
                <a href="#plataformas" class="hover:text-purple-600">Plataformas</a>
                <a href="#beneficios" class="hover:text-purple-600">Beneficios</a>
                <a href="#faq" class="hover:text-purple-600">FAQ</a>
                <a href="#contacto" class="hover:text-purple-600">Contacto</a>
            </nav>
            <div class="flex items-center gap-2">
                <button id="theme-toggle" class="rounded-md p-2 hover:bg-gray-100 dark:hover:bg-gray-800 mr-2">
                    <svg id="sun-icon" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="h-5 w-5 hidden dark:block">
                        <circle cx="12" cy="12" r="4"></circle>
                        <path d="M12 2v2"></path>
                        <path d="M12 20v2"></path>
                        <path d="m4.93 4.93 1.41 1.41"></path>
                        <path d="m17.66 17.66 1.41 1.41"></path>
                        <path d="M2 12h2"></path>
                        <path d="M20 12h2"></path>
                        <path d="m6.34 17.66-1.41 1.41"></path>
                        <path d="m19.07 4.93-1.41 1.41"></path>
                    </svg>
                    <svg id="moon-icon" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="h-5 w-5 dark:hidden">
                        <path d="M12 3a6 6 0 0 0 9 9 9 9 0 1 1-9-9Z"></path>
                    </svg>
                    <span class="sr-only">Toggle theme</span>
                </button>
                <a href="https://wa.me/+51929676778" target="_blank" class="rounded-md bg-green-600 px-4 py-2 text-white hover:bg-green-700">
                    <span class="flex items-center">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="mr-2" viewBox="0 0 16 16">
                            <path d="M13.601 2.326A7.854 7.854 0 0 0 7.994 0C3.627 0 .068 3.558.064 7.926c0 1.399.366 2.76 1.057 3.965L0 16l4.204-1.102a7.933 7.933 0 0 0 3.79.965h.004c4.368 0 7.926-3.558 7.93-7.93A7.898 7.898 0 0 0 13.6 2.326zM7.994 14.521a6.573 6.573 0 0 1-3.356-.92l-.24-.144-2.494.654.666-2.433-.156-.251a6.56 6.56 0 0 1-1.007-3.505c0-3.626 2.957-6.584 6.591-6.584a6.56 6.56 0 0 1 4.66 1.931 6.557 6.557 0 0 1 1.928 4.66c-.004 3.639-2.961 6.592-6.592 6.592zm3.615-4.934c-.197-.099-1.17-.578-1.353-.646-.182-.065-.315-.099-.445.099-.133.197-.513.646-.627.775-.114.133-.232.148-.43.05-.197-.1-.836-.308-1.592-.985-.59-.525-.985-1.175-1.103-1.372-.114-.198-.011-.304.088-.403.087-.088.197-.232.296-.346.1-.114.133-.198.198-.33.065-.134.034-.248-.015-.347-.05-.099-.445-1.076-.612-1.47-.16-.389-.323-.335-.445-.34-.114-.007-.247-.007-.38-.007a.729.729 0 0 0-.529.247c-.182.198-.691.677-.691 1.654 0 .977.71 1.916.81 2.049.098.133 1.394 2.132 3.383 2.992.47.205.84.326 1.129.418.475.152.904.129 1.246.08.38-.058 1.171-.48 1.338-.943.164-.464.164-.86.114-.943-.049-.084-.182-.133-.38-.232z"/>
                        </svg>
                        WhatsApp
                    </span>
                </a>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="flex-1">
        <!-- Hero Section -->
        <section class="w-full py-12 md:py-24 lg:py-32 bg-gradient-to-b from-purple-50 to-white dark:from-gray-900 dark:to-background">
            <div class="container mx-auto px-4 md:px-6">
                <div class="grid gap-6 lg:grid-cols-2 lg:gap-12 xl:grid-cols-2">
                    <div class="flex flex-col justify-center space-y-4">
                        <div class="space-y-2">
                            <h1 class="text-3xl font-bold tracking-tighter sm:text-5xl xl:text-6xl/none">
                                Todas tus plataformas favoritas en un solo lugar
                            </h1>
                            <p class="max-w-[600px] text-gray-500 md:text-xl dark:text-gray-400">
                                Accede a las mejores plataformas de streaming con nuestros planes económicos y sin contratos a largo plazo.
                            </p>
                        </div>
                        <div class="flex flex-col gap-2 min-[400px]:flex-row">
                            <a href="#plataformas" class="inline-flex items-center justify-center rounded-md bg-purple-600 px-4 py-2 text-sm font-medium text-white hover:bg-purple-700">
                                Ver plataformas
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="ml-2 h-4 w-4">
                                    <path d="M5 12h14"></path>
                                    <path d="m12 5 7 7-7 7"></path>
                                </svg>
                            </a>
                            <a href="https://wa.me/+51929676778" target="_blank" class="inline-flex items-center justify-center rounded-md border border-gray-200 bg-white px-4 py-2 text-sm font-medium dark:border-gray-800 dark:bg-gray-950">
                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="mr-2" viewBox="0 0 16 16">
                                    <path d="M13.601 2.326A7.854 7.854 0 0 0 7.994 0C3.627 0 .068 3.558.064 7.926c0 1.399.366 2.76 1.057 3.965L0 16l4.204-1.102a7.933 7.933 0 0 0 3.79.965h.004c4.368 0 7.926-3.558 7.93-7.93A7.898 7.898 0 0 0 13.6 2.326zM7.994 14.521a6.573 6.573 0 0 1-3.356-.92l-.24-.144-2.494.654.666-2.433-.156-.251a6.56 6.56 0 0 1-1.007-3.505c0-3.626 2.957-6.584 6.591-6.584a6.56 6.56 0 0 1 4.66 1.931 6.557 6.557 0 0 1 1.928 4.66c-.004 3.639-2.961 6.592-6.592 6.592zm3.615-4.934c-.197-.099-1.17-.578-1.353-.646-.182-.065-.315-.099-.445.099-.133.197-.513.646-.627.775-.114.133-.232.148-.43.05-.197-.1-.836-.308-1.592-.985-.59-.525-.985-1.175-1.103-1.372-.114-.198-.011-.304.088-.403.087-.088.197-.232.296-.346.1-.114.133-.198.198-.33.065-.134.034-.248-.015-.347-.05-.099-.445-1.076-.612-1.47-.16-.389-.323-.335-.445-.34-.114-.007-.247-.007-.38-.007a.729.729 0 0 0-.529.247c-.182.198-.691.677-.691 1.654 0 .977.71 1.916.81 2.049.098.133 1.394 2.132 3.383 2.992.47.205.84.326 1.129.418.475.152.904.129 1.246.08.38-.058 1.171-.48 1.338-.943.164-.464.164-.86.114-.943-.049-.084-.182-.133-.38-.232z"/>
                                </svg>
                                Contactar soporte
                            </a>
                        </div>
                    </div>
                    <div class="flex items-center justify-center">
                        <img alt="Streaming Services" class="aspect-video overflow-hidden rounded-xl object-cover object-center" height="310" src="../img/Marco.png" width="550" />
                    </div>
                </div>
            </div>
        </section>

        <!-- Platforms Section -->
        <section class="w-full py-12 md:py-24 lg:py-32" id="plataformas">
            <div class="container mx-auto px-4 md:px-6">
                <div class="flex flex-col items-center justify-center space-y-4 text-center">
                    <div class="space-y-2">
                        <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">Plataformas Disponibles</h2>
                        <p class="max-w-[900px] text-gray-500 md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed dark:text-gray-400">
                            Ofrecemos acceso a las mejores plataformas de streaming del mercado a precios increíbles.
                        </p>
                    </div>
                </div>
                <div class="mx-auto grid max-w-5xl grid-cols-1 gap-6 py-12 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
                    <!-- Platform Cards -->
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-red-600"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/netflix.png" alt="Netflix" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Netflix</h3>
                                <div class="text-xl font-bold text-red-600">S/ 9.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Netflix" target="_blank" class="mt-2 w-full rounded-md bg-red-600 px-3 py-2 text-sm font-medium text-white hover:bg-red-700">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-blue-700"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/disney.png" alt="Disney+" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Disney+</h3>
                                <div class="text-xl font-bold text-blue-700">S/ 7.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Disney+" target="_blank" class="mt-2 w-full rounded-md bg-blue-700 px-3 py-2 text-sm font-medium text-white hover:bg-blue-800">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-purple-700"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/max.png" alt="Max" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Max</h3>
                                <div class="text-xl font-bold text-purple-700">S/ 5.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Max" target="_blank" class="mt-2 w-full rounded-md bg-purple-700 px-3 py-2 text-sm font-medium text-white hover:bg-purple-800">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-blue-500"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/prime.png" alt="Prime Video" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Prime Video</h3>
                                <div class="text-xl font-bold text-blue-500">S/ 5.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Prime%20Video" target="_blank" class="mt-2 w-full rounded-md bg-blue-500 px-3 py-2 text-sm font-medium text-white hover:bg-blue-600">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-green-600"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/spotify.png" alt="Spotify" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Spotify</h3>
                                <div class="text-xl font-bold text-green-600">S/ 12.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Spotify" target="_blank" class="mt-2 w-full rounded-md bg-green-600 px-3 py-2 text-sm font-medium text-white hover:bg-green-700">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-red-700"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/yt.png" alt="YouTube Premium" class="rounded-lg mb-2" />
                                <h3 class="font-medium">YouTube Premium</h3>
                                <div class="text-xl font-bold text-red-700">S/ 5.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20YouTube%20Premium" target="_blank" class="mt-2 w-full rounded-md bg-red-700 px-3 py-2 text-sm font-medium text-white hover:bg-red-800">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-blue-800"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/canva.png" alt="Paramount+" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Canva Pro Edu</h3>
                                <div class="text-xl font-bold text-blue-800">S/ 9.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Paramount+" target="_blank" class="mt-2 w-full rounded-md bg-blue-800 px-3 py-2 text-sm font-medium text-white hover:bg-blue-900">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-orange-600"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/chunchy.png" alt="Crunchyroll" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Crunchyroll</h3>
                                <div class="text-xl font-bold text-orange-600">S/ 3.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Crunchyroll" target="_blank" class="mt-2 w-full rounded-md bg-orange-600 px-3 py-2 text-sm font-medium text-white hover:bg-orange-700">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-gray-700"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/iptv.png" alt="IPTV" class="rounded-lg mb-2" />
                                <h3 class="font-medium">IPTV</h3>
                                <div class="text-xl font-bold text-gray-700">S/ 7.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20IPTV" target="_blank" class="mt-2 w-full rounded-md bg-gray-700 px-3 py-2 text-sm font-medium text-white hover:bg-gray-800">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-teal-600"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/dgo.png" alt="DGO" class="rounded-lg mb-2" />
                                <h3 class="font-medium">DGO</h3>
                                <div class="text-xl font-bold text-teal-600">S/ 25.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20DGO" target="_blank" class="mt-2 w-full rounded-md bg-teal-600 px-3 py-2 text-sm font-medium text-white hover:bg-teal-700">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-red-500"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/claro.png" alt="Claro Video" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Claro Video</h3>
                                <div class="text-xl font-bold text-red-500">S/ 20.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Claro%20Video" target="_blank" class="mt-2 w-full rounded-md bg-red-500 px-3 py-2 text-sm font-medium text-white hover:bg-red-600">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-yellow-600"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/vix.png" alt="Vix" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Vix</h3>
                                <div class="text-xl font-bold text-yellow-600">S/ 6.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Vix" target="_blank" class="mt-2 w-full rounded-md bg-yellow-600 px-3 py-2 text-sm font-medium text-white hover:bg-yellow-700">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-green-700"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/play.png" alt="Movistar Play" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Movistar Play</h3>
                                <div class="text-xl font-bold text-green-700">S/ 20.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Movistar%20Play" target="_blank" class="mt-2 w-full rounded-md bg-green-700 px-3 py-2 text-sm font-medium text-white hover:bg-green-800">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-pink-600"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/viki.png" alt="Viki" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Viki</h3>
                                <div class="text-xl font-bold text-pink-600">S/ 6.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Viki" target="_blank" class="mt-2 w-full rounded-md bg-pink-600 px-3 py-2 text-sm font-medium text-white hover:bg-pink-700">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-indigo-600"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/chat.png" alt="Star+" class="rounded-lg mb-2" />
                                <h3 class="font-medium">ChatGpt Plus</h3>
                                <div class="text-xl font-bold text-indigo-600">S/ 12.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%20Star+" target="_blank" class="mt-2 w-full rounded-md bg-indigo-600 px-3 py-2 text-sm font-medium text-white hover:bg-indigo-700">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                    <div class="overflow-hidden rounded-lg border border-gray-200 transition-all hover:shadow-lg dark:border-gray-800">
                        <div class="h-2 bg-gray-800"></div>
                        <div class="p-4">
                            <div class="flex flex-col items-center justify-center gap-2 text-center">
                                <img src="../img/paramont.png" alt="Contenido Adulto" class="rounded-lg mb-2" />
                                <h3 class="font-medium">Paramount+</h3>
                                <div class="text-xl font-bold text-gray-800">S/ 6.00</div>
                                <a href="https://wa.me/+51929676778?text=Me%20interesa%Paramount%20plus" target="_blank" class="mt-2 w-full rounded-md bg-gray-800 px-3 py-2 text-sm font-medium text-white hover:bg-gray-900">
                                    Comprar ahora
                                </a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Benefits Section -->
        <section class="w-full py-12 md:py-24 lg:py-32" id="beneficios">
            <div class="container mx-auto px-4 md:px-6">
                <div class="flex flex-col items-center justify-center space-y-4 text-center">
                    <div class="space-y-2">
                        <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">¿Por qué elegirnos?</h2>
                        <p class="max-w-[900px] text-gray-500 md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed dark:text-gray-400">
                            Descubre las ventajas de nuestro servicio frente a la competencia.
                        </p>
                    </div>
                </div>
                <div class="mx-auto grid max-w-5xl grid-cols-1 gap-6 py-12 md:grid-cols-2 lg:grid-cols-3">
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">Precios Competitivos</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                Ofrecemos los mejores precios del mercado, con planes adaptados a todas las necesidades y
                                presupuestos.
                            </p>
                        </div>
                    </div>
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">Soporte 24/7</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                Nuestro equipo de soporte está disponible las 24 horas del día, los 7 días de la semana para
                                resolver cualquier duda.
                            </p>
                        </div>
                    </div>
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">Sin Contratos</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                No te atamos a contratos de permanencia. Puedes cancelar tu suscripción cuando quieras sin
                                penalizaciones.
                            </p>
                        </div>
                    </div>
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">Calidad Garantizada</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                Garantizamos la mejor calidad de streaming, con opciones de hasta 4K UHD en los planes compatibles.
                            </p>
                        </div>
                    </div>
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">Múltiples Dispositivos</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                Accede a tus plataformas favoritas desde múltiples dispositivos: Smart TV, móvil, tablet,
                                ordenador...
                            </p>
                        </div>
                    </div>
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">Actualizaciones Constantes</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                Añadimos nuevas plataformas y contenidos regularmente para ofrecerte siempre lo mejor del
                                entretenimiento.
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- FAQ Section -->
        <section class="w-full py-12 md:py-24 lg:py-32 bg-gray-50 dark:bg-gray-900" id="faq">
            <div class="container mx-auto px-4 md:px-6">
                <div class="flex flex-col items-center justify-center space-y-4 text-center">
                    <div class="space-y-2">
                        <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">Preguntas Frecuentes</h2>
                        <p class="max-w-[900px] text-gray-500 md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed dark:text-gray-400">
                            Resolvemos tus dudas más comunes sobre nuestro servicio.
                        </p>
                    </div>
                </div>
                <div class="mx-auto max-w-3xl space-y-4 py-12">
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">¿Cómo funciona el servicio?</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                Una vez realices tu compra, recibirás las credenciales de acceso a las plataformas que hayas
                                seleccionado. Podrás acceder a ellas desde cualquier dispositivo compatible.
                            </p>
                        </div>
                    </div>
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">¿Puedo cambiar las plataformas que he elegido?</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                Sí, puedes cambiar las plataformas seleccionadas una vez al mes sin coste adicional. Para ello,
                                contacta con nuestro servicio de atención al cliente.
                            </p>
                        </div>
                    </div>
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">¿Cuáles son los métodos de pago aceptados?</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>Aceptamos pagos con tarjeta de crédito/débito, PayPal, transferencia bancaria y criptomonedas.</p>
                        </div>
                    </div>
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">¿Qué hago si tengo problemas técnicos?</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                Nuestro equipo de soporte técnico está disponible 24/7. Puedes contactarnos a través de WhatsApp
                                para una respuesta inmediata.
                            </p>
                        </div>
                    </div>
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950">
                        <div class="p-6">
                            <h3 class="text-lg font-bold">¿Puedo compartir mi cuenta con amigos o familiares?</h3>
                        </div>
                        <div class="p-6 pt-0">
                            <p>
                                Dependiendo del plan que elijas, podrás compartir tu cuenta con un número determinado de
                                dispositivos simultáneos. Consulta los detalles de cada plan.
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Contact Section -->
        <section class="w-full py-12 md:py-24 lg:py-32 bg-purple-50 dark:bg-purple-950/20" id="contacto">
            <div class="container mx-auto px-4 md:px-6">
                <div class="flex flex-col items-center justify-center space-y-4 text-center">
                    <div class="space-y-2">
                        <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">Contacta con Nosotros</h2>
                        <p class="max-w-[900px] text-gray-500 md:text-xl/relaxed lg:text-base/relaxed xl:text-xl/relaxed dark:text-gray-400">
                            Estamos aquí para ayudarte. No dudes en contactarnos para cualquier consulta.
                        </p>
                    </div>
                </div>
                <div class="mx-auto flex flex-col items-center justify-center max-w-5xl py-12">
                    <div class="rounded-lg border border-gray-200 bg-white shadow-sm dark:border-gray-800 dark:bg-gray-950 p-8 w-full max-w-md">
                        <div class="text-center mb-6">
                            <h3 class="text-xl font-bold mb-2">¿Tienes alguna pregunta?</h3>
                            <p class="text-gray-500 dark:text-gray-400">
                                Contáctanos directamente por WhatsApp para una respuesta inmediata
                            </p>
                        </div>
                        <a href="https://wa.me/+51929676778" target="_blank" class="flex items-center justify-center w-full rounded-md bg-green-600 px-6 py-3 text-lg font-medium text-white hover:bg-green-700 transition-colors">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" class="mr-3" viewBox="0 0 16 16">
                                <path d="M13.601 2.326A7.854 7.854 0 0 0 7.994 0C3.627 0 .068 3.558.064 7.926c0 1.399.366 2.76 1.057 3.965L0 16l4.204-1.102a7.933 7.933 0 0 0 3.79.965h.004c4.368 0 7.926-3.558 7.93-7.93A7.898 7.898 0 0 0 13.6 2.326zM7.994 14.521a6.573 6.573 0 0 1-3.356-.92l-.24-.144-2.494.654.666-2.433-.156-.251a6.56 6.56 0 0 1-1.007-3.505c0-3.626 2.957-6.584 6.591-6.584a6.56 6.56 0 0 1 4.66 1.931 6.557 6.557 0 0 1 1.928 4.66c-.004 3.639-2.961 6.592-6.592 6.592zm3.615-4.934c-.197-.099-1.17-.578-1.353-.646-.182-.065-.315-.099-.445.099-.133.197-.513.646-.627.775-.114.133-.232.148-.43.05-.197-.1-.836-.308-1.592-.985-.59-.525-.985-1.175-1.103-1.372-.114-.198-.011-.304.088-.403.087-.088.197-.232.296-.346.1-.114.133-.198.198-.33.065-.134.034-.248-.015-.347-.05-.099-.445-1.076-.612-1.47-.16-.389-.323-.335-.445-.34-.114-.007-.247-.007-.38-.007a.729.729 0 0 0-.529.247c-.182.198-.691.677-.691 1.654 0 .977.71 1.916.81 2.049.098.133 1.394 2.132 3.383 2.992.47.205.84.326 1.129.418.475.152.904.129 1.246.08.38-.058 1.171-.48 1.338-.943.164-.464.164-.86.114-.943-.049-.084-.182-.133-.38-.232z"/>
                            </svg>
                            Contactar por WhatsApp
                        </a>
                        <div class="mt-6 text-center">
                            <p class="text-gray-500 dark:text-gray-400">
                                Horario de atención: 24/7, todos los días del año
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer class="w-full border-t bg-background py-6">
        <div class="container mx-auto px-4 md:px-6">
            <div class="grid gap-8 md:grid-cols-2 lg:grid-cols-4">
                <div class="space-y-4">
                    <h3 class="text-lg font-bold">Streamly</h3>
                    <p class="text-sm text-gray-500 dark:text-gray-400">
                        Tu portal de acceso a las mejores plataformas de streaming a precios increíbles.
                    </p>
                </div>
                <div class="space-y-4">
                    <h3 class="text-lg font-bold">Enlaces rápidos</h3>
                    <ul class="space-y-2 text-sm">
                        <li>
                            <a href="#plataformas" class="text-gray-500 hover:text-purple-600 dark:text-gray-400 dark:hover:text-purple-500">
                                Plataformas
                            </a>
                        </li>
                        <li>
                            <a href="#beneficios" class="text-gray-500 hover:text-purple-600 dark:text-gray-400 dark:hover:text-purple-500">
                                Beneficios
                            </a>
                        </li>
                        <li>
                            <a href="#faq" class="text-gray-500 hover:text-purple-600 dark:text-gray-400 dark:hover:text-purple-500">
                                FAQ
                            </a>
                        </li>
                    </ul>
                </div>
                <div class="space-y-4">
                    <h3 class="text-lg font-bold">Legal</h3>
                    <ul class="space-y-2 text-sm">
                        <li>
                            <a href="#" class="text-gray-500 hover:text-purple-600 dark:text-gray-400 dark:hover:text-purple-500">
                                Términos y condiciones
                            </a>
                        </li>
                        <li>
                            <a href="#" class="text-gray-500 hover:text-purple-600 dark:text-gray-400 dark:hover:text-purple-500">
                                Política de privacidad
                            </a>
                        </li>
                        <li>
                            <a href="#" class="text-gray-500 hover:text-purple-600 dark:text-gray-400 dark:hover:text-purple-500">
                                Política de cookies
                            </a>
                        </li>
                        <li>
                            <a href="#" class="text-gray-500 hover:text-purple-600 dark:text-gray-400 dark:hover:text-purple-500">
                                Aviso legal
                            </a>
                        </li>
                    </ul>
                </div>
                <div class="space-y-4">
                    <h3 class="text-lg font-bold">Contacto</h3>
                    <ul class="space-y-2 text-sm">
                        <li class="text-gray-500 dark:text-gray-400">WhatsApp: +51 929676778</li>
                        <li class="text-gray-500 dark:text-gray-400">Horario: 24/7</li>
                    </ul>
                </div>
            </div>
            <div class="mt-8 border-t pt-4 text-center text-sm text-gray-500 dark:text-gray-400">
                <p>© <script>document.write(new Date().getFullYear())</script> Streamly. Todos los derechos reservados.</p>
            </div>
        </div>
    </footer>

    <!-- JavaScript -->
    <script>
        // Theme Toggle
        const themeToggle = document.getElementById('theme-toggle');
        const html = document.documentElement;
        
        // Check for saved theme preference or use system preference
        const savedTheme = localStorage.getItem('theme');
        if (savedTheme) {
            html.classList.toggle('dark', savedTheme === 'dark');
        } else if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
            html.classList.add('dark');
        }
        
        // Toggle theme
        themeToggle.addEventListener('click', () => {
            html.classList.toggle('dark');
            localStorage.setItem('theme', html.classList.contains('dark') ? 'dark' : 'light');
        });
        
        // Mobile Menu
        const menuToggle = document.getElementById('menu-toggle');
        const closeMenu = document.getElementById('close-menu');
        const mobileMenu = document.getElementById('mobile-menu');
        
        menuToggle.addEventListener('click', () => {
            mobileMenu.classList.remove('hidden');
        });
        
        closeMenu.addEventListener('click', () => {
            mobileMenu.classList.add('hidden');
        });
        
        // Close mobile menu when clicking on a link
        const mobileLinks = mobileMenu.querySelectorAll('a');
        mobileLinks.forEach(link => {
            link.addEventListener('click', () => {
                mobileMenu.classList.add('hidden');
            });
        });
    </script>
</body>
</html>
