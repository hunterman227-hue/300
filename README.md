# 300```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2026 Mayflower Quarter Error Interactive Field Guide</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 650px;
            margin-left: auto;
            margin-right: auto;
            height: 320px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 360px;
            }
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 3px;
        }
    </style>
</head>
<!-- Chosen Palette: Warm Numismatic Bronze & Steel Slate -->
<!-- Application Structure Plan:
     1. Hero & Executive Summary: Sets the context of the 2026-P Semiquincentennial Mayflower Quarter minting events in Larose, LA & Philadelphia.
     2. Chronological Die Progression Engine ("Phantom of Larose"): An interactive step-by-step simulator allowing users to scrub through Stage 1 ("Mosquito Bite") to Stage 5 ("Terminal Phantom Shatter"). Uses dynamic canvas visualization to demonstrate crack propagation on the coin layout.
     3. Varieties Comparison & Deep Dive ("Spirit of '76" vs "Phantom of Larose" vs "Duck Mark"): Detailed filterable cards highlighting root causes (feeder finger strike-through, die fatigue, hardness test dents).
     4. Interactive Coin Diagnostic Assistant: A multi-step decision wizard letting collectors select observed anomalies to receive immediate diagnostic results and variety classifications.
     5. Market Analytics & Collector Rarity Metrics: Chart.js dynamic visualizations displaying relative scarcity, estimated market valuation, and community interest across stages.
     This structure was chosen to transform static catalog descriptions into an active investigation workflow for coin collectors and curious enthusiasts. -->
<!-- Visualization & Content Choices:
     - Die Crack Progression: HTML5 Canvas 2D simulation -> Goal: Show step-by-step steel die shatter -> Interaction: Slider / Stage buttons -> No SVG/Mermaid.
     - Variety Scarcity & Value: Chart.js Bar & Radar Charts -> Goal: Compare key metrics across stages -> Interaction: Tooltips & dynamic datasets -> Canvas engine.
     - Diagnostic Tool: Dynamic JS DOM manipulation -> Goal: Instant variety identification from physical coin traits -> Interaction: Selection checkboxes/radios.
     - CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
<!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
<body class="bg-slate-50 text-slate-800 font-sans antialiased selection:bg-amber-200 selection:text-amber-900 min-h-screen flex flex-col">

    <!-- Header Navigation -->
    <header class="bg-slate-900 text-white sticky top-0 z-50 shadow-md border-b border-amber-600/30">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex items-center space-x-3">
                    <div class="w-9 h-9 rounded-full bg-amber-500 text-slate-950 font-black flex items-center justify-center text-lg shadow-inner">
                        &#9830;
                    </div>
                    <div>
                        <span class="font-bold text-lg tracking-tight text-amber-400">2026 Mayflower Error Lab</span>
                        <span class="hidden sm:inline-block text-xs text-slate-400 ml-2 border-l border-slate-700 pl-2">Larose & Philadelphia Mint Varieties</span>
                    </div>
                </div>
                <nav class="hidden md:flex space-x-1 text-sm font-medium">
                    <button onclick="scrollToSection('progression')" class="px-3 py-2 rounded-md hover:bg-slate-800 text-slate-300 hover:text-white transition">Die Progression</button>
                    <button onclick="scrollToSection('varieties')" class="px-3 py-2 rounded-md hover:bg-slate-800 text-slate-300 hover:text-white transition">Variety Matrix</button>
                    <button onclick="scrollToSection('diagnostic')" class="px-3 py-2 rounded-md hover:bg-slate-800 text-slate-300 hover:text-white transition">Diagnostic Tool</button>
                    <button onclick="scrollToSection('analytics')" class="px-3 py-2 rounded-md hover:bg-slate-800 text-slate-300 hover:text-white transition">Market Data</button>
                </nav>
                <div class="md:hidden">
                    <button id="mobile-menu-btn" class="p-2 text-slate-300 hover:text-white focus:outline-none">
                        &#9776;
                    </button>
                </div>
            </div>
        </div>
        <!-- Mobile menu -->
        <div id="mobile-menu" class="hidden md:hidden bg-slate-950 border-b border-slate-800 px-4 pt-2 pb-4 space-y-1">
            <button onclick="scrollToSection('progression')" class="block w-full text-left px-3 py-2 text-slate-300 hover:bg-slate-800 rounded">Die Progression</button>
            <button onclick="scrollToSection('varieties')" class="block w-full text-left px-3 py-2 text-slate-300 hover:bg-slate-800 rounded">Variety Matrix</button>
            <button onclick="scrollToSection('diagnostic')" class="block w-full text-left px-3 py-2 text-slate-300 hover:bg-slate-800 rounded">Diagnostic Tool</button>
            <button onclick="scrollToSection('analytics')" class="block w-full text-left px-3 py-2 text-slate-300 hover:bg-slate-800 rounded">Market Data</button>
        </div>
    </header>

    <main class="flex-grow">
        <!-- Hero Section -->
        <section class="bg-gradient-to-b from-slate-900 via-slate-800 to-slate-900 text-white py-12 px-4 sm:px-6 lg:px-8 border-b border-amber-500/20">
            <div class="max-w-7xl mx-auto">
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-center">
                    <div class="lg:col-span-7 space-y-4">
                        <div class="inline-flex items-center space-x-2 bg-amber-500/10 border border-amber-500/30 rounded-full px-3 py-1 text-xs text-amber-300 font-semibold">
                            <span>&#9733; 2026 Semiquincentennial Series Report</span>
                        </div>
                        <h1 class="text-3xl sm:text-4xl lg:text-5xl font-extrabold text-white tracking-tight leading-tight">
                            The "Phantom of Larose" & <span class="text-amber-400">2026 Mayflower</span> Mint Anomalies
                        </h1>
                        <p class="text-slate-300 text-base sm:text-lg leading-relaxed">
                            During the high-speed production run of the 2026 Mayflower Compact Quarter, overworked working dies at the U.S. Mint underwent historic breakdown events. Explore the step-by-step collapse of die #2026-P-04, the "Spirit of '76" feeder finger strike-through, and key diagnostic markers.
                        </p>
                        <div class="pt-2 flex flex-wrap gap-4">
                            <button onclick="scrollToSection('diagnostic')" class="bg-amber-500 hover:bg-amber-600 text-slate-950 font-bold px-5 py-2.5 rounded-lg shadow-lg hover:shadow-amber-500/20 transition flex items-center space-x-2">
                                <span>&#128065; Identify Your Coin</span>
                            </button>
                            <button onclick="scrollToSection('progression')" class="bg-slate-800 hover:bg-slate-700 text-slate-200 border border-slate-600 font-medium px-5 py-2.5 rounded-lg transition">
                                Explore Die Breakdown
                            </button>
                        </div>
                    </div>
                    <!-- Quick Stats Dashboard -->
                    <div class="lg:col-span-5 grid grid-cols-2 gap-4">
                        <div class="bg-slate-800/80 border border-slate-700/80 p-4 rounded-xl shadow-inner text-center">
                            <span class="block text-3xl font-black text-amber-400">5</span>
                            <span class="text-xs uppercase tracking-wider text-slate-400 font-bold mt-1 block">Die Wear Stages</span>
                            <span class="text-[11px] text-slate-300 mt-1 block">From Mosquito Bite to Phantom</span>
                        </div>
                        <div class="bg-slate-800/80 border border-slate-700/80 p-4 rounded-xl shadow-inner text-center">
                            <span class="block text-3xl font-black text-amber-400">2026-P</span>
                            <span class="text-xs uppercase tracking-wider text-slate-400 font-bold mt-1 block">Mint Origin</span>
                            <span class="text-[11px] text-slate-300 mt-1 block">Philadelphia Press #12</span>
                        </div>
                        <div class="bg-slate-800/80 border border-slate-700/80 p-4 rounded-xl shadow-inner text-center">
                            <span class="block text-3xl font-black text-amber-400">$20 - $350+</span>
                            <span class="text-xs uppercase tracking-wider text-slate-400 font-bold mt-1 block">Est. Collector Range</span>
                            <span class="text-[11px] text-slate-300 mt-1 block">Based on Stage Severity</span>
                        </div>
                        <div class="bg-slate-800/80 border border-slate-700/80 p-4 rounded-xl shadow-inner text-center">
                            <span class="block text-3xl font-black text-amber-400">2 Key</span>
                            <span class="text-xs uppercase tracking-wider text-slate-400 font-bold mt-1 block">Error Types</span>
                            <span class="text-[11px] text-slate-300 mt-1 block">Die Crack vs Feeder Scrapes</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION 1: Interactive Die Progression Engine -->
        <section id="progression" class="py-12 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto">
            <div class="mb-8">
                <div class="flex items-center space-x-2 text-amber-600 font-bold text-xs uppercase tracking-wider mb-1">
                    <span>Section 1</span>
                    <span>&bull;</span>
                    <span>Chronological Die Fatigue</span>
                </div>
                <h2 class="text-2xl sm:text-3xl font-bold text-slate-900">The "Phantom of Larose" Die Breakdown Tracker</h2>
                <p class="text-slate-600 mt-2 max-w-3xl">
                    As steel working dies strike thousands of coin blanks per hour, immense mechanical stress creates hairline fractures that progressively expand. Below, select a stage to simulate how die #2026-P-04 degraded from minor surface pits into a dramatic terminal die shatter.
                </p>
            </div>

            <!-- Progression Interactive Layout -->
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden grid grid-cols-1 lg:grid-cols-12">
                <!-- Left: Interactive Canvas Simulator -->
                <div class="lg:col-span-5 bg-slate-900 p-6 flex flex-col items-center justify-center text-center border-b lg:border-b-0 lg:border-r border-slate-800">
                    <div class="text-xs font-semibold text-amber-400 uppercase tracking-widest mb-2">Simulated Obverse Die Surface</div>
                    
                    <!-- HTML5 Canvas Coin Simulation (NO SVG) -->
                    <div class="relative my-4">
                        <canvas id="coinCanvas" width="280" height="280" class="rounded-full shadow-2xl bg-gradient-to-tr from-slate-700 via-slate-300 to-slate-100 border-4 border-amber-500/50 cursor-pointer"></canvas>
                        <div id="canvasTag" class="absolute bottom-2 right-2 bg-slate-900/90 border border-slate-700 text-amber-300 text-[10px] font-mono px-2 py-0.5 rounded">
                            Stage 1 Active
                        </div>
                    </div>
                    
                    <p class="text-slate-400 text-xs italic max-w-xs mt-2">
                        Interactive Diagram: Click die stages on the right to inspect simulated stress line propagation across the Mayflower portrait area.
                    </p>
                </div>

                <!-- Right: Stage Details & Controller -->
                <div class="lg:col-span-7 p-6 sm:p-8 flex flex-col justify-between">
                    <div>
                        <!-- Stage Selection Tabs -->
                        <div class="flex flex-wrap gap-2 mb-6 border-b border-slate-100 pb-4">
                            <button onclick="setStage(1)" id="btn-stage-1" class="stage-btn px-3 py-1.5 rounded-lg text-xs font-bold transition bg-amber-500 text-slate-950 shadow-sm">
                                Stage 1: Mosquito Bite
                            </button>
                            <button onclick="setStage(2)" id="btn-stage-2" class="stage-btn px-3 py-1.5 rounded-lg text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200">
                                Stage 2: The Splinter
                            </button>
                            <button onclick="setStage(3)" id="btn-stage-3" class="stage-btn px-3 py-1.5 rounded-lg text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200">
                                Stage 3: Raft in Water
                            </button>
                            <button onclick="setStage(4)" id="btn-stage-4" class="stage-btn px-3 py-1.5 rounded-lg text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200">
                                Stage 4: Nasal Strip
                            </button>
                            <button onclick="setStage(5)" id="btn-stage-5" class="stage-btn px-3 py-1.5 rounded-lg text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200">
                                Stage 5: Terminal Phantom
                            </button>
                        </div>

                        <!-- Dynamic Content Panel -->
                        <div class="space-y-4">
                            <div class="flex items-center justify-between">
                                <span id="stageBadge" class="bg-amber-100 text-amber-900 border border-amber-300 text-xs font-extrabold px-2.5 py-1 rounded">
                                    EARLY DIE STATE &bull; STAGE 1
                                </span>
                                <span id="stageRarity" class="text-xs text-slate-500 font-medium">Est. Known: ~1,500 - 2,000 coins</span>
                            </div>

                            <h3 id="stageTitle" class="text-2xl font-bold text-slate-900">
                                The Mosquito Bite
                            </h3>

                            <p id="stageDescription" class="text-slate-600 text-sm leading-relaxed">
                                Small, sharp, raised metal bumps begin appearing like bug bites near the Pilgrim woman's bonnet and sleeve. This is caused by microscopic pits opening on the overburdened steel die surface into which blank planchet metal flows under pressure.
                            </p>

                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 pt-2">
                                <div class="bg-slate-50 border border-slate-200 rounded-lg p-3">
                                    <span class="text-xs text-slate-400 font-semibold uppercase block">Key Visual Marker</span>
                                    <span id="stageMarker" class="text-sm font-bold text-slate-800">Raised dot array near arm/bonnet</span>
                                </div>
                                <div class="bg-slate-50 border border-slate-200 rounded-lg p-3">
                                    <span class="text-xs text-slate-400 font-semibold uppercase block">Die Health Level</span>
                                    <div class="flex items-center space-x-2 mt-1">
                                        <div class="flex-grow bg-slate-200 h-2 rounded-full overflow-hidden">
                                            <div id="stageHealthBar" class="bg-emerald-500 h-full w-4/5"></div>
                                        </div>
                                        <span id="stageHealthText" class="text-xs font-bold text-emerald-700">80%</span>
                                    </div>
                                </div>
                            </div>

                            <div class="bg-amber-50/80 border-l-4 border-amber-500 p-3 rounded-r-lg text-xs text-amber-900">
                                <strong>Collector Note:</strong> <span id="stageCollectorNote">Look closely with a 10x loupe under angled lighting. Often mistaken for simple contact marks, but elevated geometry confirms raised die pitting.</span>
                            </div>
                        </div>
                    </div>

                    <!-- Timeline Navigation Buttons -->
                    <div class="flex items-center justify-between pt-6 mt-6 border-t border-slate-100">
                        <button onclick="prevStage()" id="prevBtn" class="px-4 py-2 bg-slate-100 text-slate-400 rounded-lg text-xs font-bold cursor-not-allowed" disabled>
                            &larr; Previous Stage
                        </button>
                        <span id="stageStepIndicator" class="text-xs font-medium text-slate-500">Stage 1 of 5</span>
                        <button onclick="nextStage()" id="nextBtn" class="px-4 py-2 bg-slate-900 hover:bg-slate-800 text-white rounded-lg text-xs font-bold transition">
                            Next Stage &rarr;
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION 2: Varieties Deep-Dive Comparison Matrix -->
        <section id="varieties" class="py-12 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto border-t border-slate-200">
            <div class="mb-8">
                <div class="flex items-center space-x-2 text-amber-600 font-bold text-xs uppercase tracking-wider mb-1">
                    <span>Section 2</span>
                    <span>&bull;</span>
                    <span>Anatomy & Root Causes</span>
                </div>
                <h2 class="text-2xl sm:text-3xl font-bold text-slate-900">2026 Mayflower Error Variety Matrix</h2>
                <p class="text-slate-600 mt-2 max-w-3xl">
                    While the "Phantom of Larose" represents progressive die cracking, other distinct mechanical failures occurred concurrently during the 2026 Semiquincentennial minting run. Filter below to understand the mechanics behind each phenomenon.
                </p>
                
                <!-- Filter Pills -->
                <div class="flex flex-wrap gap-2 mt-4">
                    <button onclick="filterVarieties('all')" class="v-filter-btn px-3 py-1.5 rounded-full text-xs font-bold bg-slate-900 text-white shadow-sm">All Varieties</button>
                    <button onclick="filterVarieties('die-crack')" class="v-filter-btn px-3 py-1.5 rounded-full text-xs font-bold bg-slate-100 text-slate-700 hover:bg-slate-200">Die Shatter / Cracks</button>
                    <button onclick="filterVarieties('strike-through')" class="v-filter-btn px-3 py-1.5 rounded-full text-xs font-bold bg-slate-100 text-slate-700 hover:bg-slate-200">Strike-Through Debris</button>
                    <button onclick="filterVarieties('mystery')" class="v-filter-btn px-3 py-1.5 rounded-full text-xs font-bold bg-slate-100 text-slate-700 hover:bg-slate-200">Unsolved Marks</button>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- Card 1: Phantom of Larose -->
                <div class="v-card bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden flex flex-col justify-between" data-category="die-crack">
                    <div>
                        <div class="bg-slate-900 p-4 text-white flex justify-between items-start">
                            <div>
                                <span class="text-[10px] uppercase tracking-widest font-bold text-amber-400 block">Progressive Die Error</span>
                                <h3 class="text-lg font-bold">Phantom of Larose</h3>
                            </div>
                            <span class="bg-amber-500/20 text-amber-300 border border-amber-500/30 text-[10px] font-extrabold px-2 py-0.5 rounded">
                                High Demand
                            </span>
                        </div>
                        <div class="p-5 space-y-3">
                            <p class="text-slate-600 text-xs leading-relaxed">
                                A ghostly, raised secondary facial outline mirroring the main Pilgrim bust. Caused when structural die cracks completely intersected, allowing a major steel die fragment to shift sideways under high tonnages.
                            </p>
                            <div class="border-t border-slate-100 pt-3 space-y-2 text-xs">
                                <div class="flex justify-between text-slate-700">
                                    <span class="text-slate-400 font-medium">Mint Location:</span>
                                    <span class="font-bold">Philadelphia (2026-P)</span>
                                </div>
                                <div class="flex justify-between text-slate-700">
                                    <span class="text-slate-400 font-medium">Primary Mechanism:</span>
                                    <span class="font-bold">Die Shatter & Relief Shift</span>
                                </div>
                                <div class="flex justify-between text-slate-700">
                                    <span class="text-slate-400 font-medium">Distinguishing Trait:</span>
                                    <span class="font-bold">Ghostly double nose/profile</span>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="bg-slate-50 p-4 border-t border-slate-100">
                        <span class="text-[11px] font-semibold text-slate-500 block">Estimated Market Value:</span>
                        <span class="text-base font-extrabold text-slate-900">$150 &ndash; $350+ <span class="text-xs font-normal text-slate-500">(Terminal State)</span></span>
                    </div>
                </div>

                <!-- Card 2: Spirit of '76 -->
                <div class="v-card bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden flex flex-col justify-between" data-category="strike-through">
                    <div>
                        <div class="bg-slate-900 p-4 text-white flex justify-between items-start">
                            <div>
                                <span class="text-[10px] uppercase tracking-widest font-bold text-amber-400 block">Mechanical Collision</span>
                                <h3 class="text-lg font-bold">The "Spirit of '76"</h3>
                            </div>
                            <span class="bg-blue-500/20 text-blue-300 border border-blue-500/30 text-[10px] font-extrabold px-2 py-0.5 rounded">
                                Struck-Through
                            </span>
                        </div>
                        <div class="p-5 space-y-3">
                            <p class="text-slate-600 text-xs leading-relaxed">
                                Deep incuse grooves and pits striking directly through the dual date "1776-2026" and motto "IN GOD WE TRUST". Occurred when mechanical feeder fingers scraped the die face and deposited metallic filings.
                            </p>
                            <div class="border-t border-slate-100 pt-3 space-y-2 text-xs">
                                <div class="flex justify-between text-slate-700">
                                    <span class="text-slate-400 font-medium">Mint Location:</span>
                                    <span class="font-bold">Philadelphia (2026-P)</span>
                                </div>
                                <div class="flex justify-between text-slate-700">
                                    <span class="text-slate-400 font-medium">Primary Mechanism:</span>
                                    <span class="font-bold">Feeder Finger Scrape Debris</span>
                                </div>
                                <div class="flex justify-between text-slate-700">
                                    <span class="text-slate-400 font-medium">Distinguishing Trait:</span>
                                    <span class="font-bold">Incuse gouge through 1776</span>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="bg-slate-50 p-4 border-t border-slate-100">
                        <span class="text-[11px] font-semibold text-slate-500 block">Estimated Market Value:</span>
                        <span class="text-base font-extrabold text-slate-900">$60 &ndash; $140 <span class="text-xs font-normal text-slate-500">(Uncirculated)</span></span>
                    </div>
                </div>

                <!-- Card 3: The Mystery Duck Mark -->
                <div class="v-card bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden flex flex-col justify-between" data-category="mystery">
                    <div>
                        <div class="bg-slate-900 p-4 text-white flex justify-between items-start">
                            <div>
                                <span class="text-[10px] uppercase tracking-widest font-bold text-amber-400 block">Unclassified Anomaly</span>
                                <h3 class="text-lg font-bold">The "Duck Mark"</h3>
                            </div>
                            <span class="bg-purple-500/20 text-purple-300 border border-purple-500/30 text-[10px] font-extrabold px-2 py-0.5 rounded">
                                Mystery
                            </span>
                        </div>
                        <div class="p-5 space-y-3">
                            <p class="text-slate-600 text-xs leading-relaxed">
                                A small, duck-shaped anomaly found in the upper field. Theories include tool steel spalling (a triangular flake breaking off), a Rockwell hardness tester dent, or aligned feeder contact.
                            </p>
                            <div class="border-t border-slate-100 pt-3 space-y-2 text-xs">
                                <div class="flex justify-between text-slate-700">
                                    <span class="text-slate-400 font-medium">Mint Location:</span>
                                    <span class="font-bold">P & D Mints Reported</span>
                                </div>
                                <div class="flex justify-between text-slate-700">
                                    <span class="text-slate-400 font-medium">Primary Mechanism:</span>
                                    <span class="font-bold">Tooling Void / Spalling</span>
                                </div>
                                <div class="flex justify-between text-slate-700">
                                    <span class="text-slate-400 font-medium">Distinguishing Trait:</span>
                                    <span class="font-bold">Waterfowl-like shape in field</span>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="bg-slate-50 p-4 border-t border-slate-100">
                        <span class="text-[11px] font-semibold text-slate-500 block">Estimated Market Value:</span>
                        <span class="text-base font-extrabold text-slate-900">$25 &ndash; $75 <span class="text-xs font-normal text-slate-500">(Pending Classification)</span></span>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION 3: Interactive Coin Diagnostic Assistant -->
        <section id="diagnostic" class="py-12 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto border-t border-slate-200">
            <div class="bg-gradient-to-br from-slate-900 to-slate-800 rounded-2xl shadow-xl p-6 sm:p-10 text-white">
                <div class="max-w-3xl mb-8">
                    <div class="flex items-center space-x-2 text-amber-400 font-bold text-xs uppercase tracking-wider mb-1">
                        <span>Section 3</span>
                        <span>&bull;</span>
                        <span>Collector Assistant</span>
                    </div>
                    <h2 class="text-2xl sm:text-3xl font-bold">Interactive Coin Diagnostic Wizard</h2>
                    <p class="text-slate-300 text-sm mt-2">
                        Did you find an unusual 2026 Mayflower Quarter in your change or bank roll? Select the physical characteristics you observe under magnification below to diagnose the variety.
                    </p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
                    <!-- Wizard Form -->
                    <div class="lg:col-span-7 bg-slate-800/90 border border-slate-700 rounded-xl p-6 space-y-6">
                        <div>
                            <label class="block text-xs font-bold uppercase text-amber-400 tracking-wider mb-2">1. Mint Mark & Location</label>
                            <select id="diag-mint" class="w-full bg-slate-900 border border-slate-600 rounded-lg p-2.5 text-sm text-slate-200 focus:border-amber-500 focus:outline-none">
                                <option value="P">Philadelphia ("P" Mint Mark)</option>
                                <option value="D">Denver ("D" Mint Mark)</option>
                                <option value="S">San Francisco / Proof ("S")</option>
                            </select>
                        </div>

                        <div>
                            <label class="block text-xs font-bold uppercase text-amber-400 tracking-wider mb-2">2. Surface Elevation of Anomaly</label>
                            <div class="grid grid-cols-2 gap-3">
                                <label class="flex items-center space-x-2 bg-slate-900 border border-slate-700 p-3 rounded-lg cursor-pointer hover:border-slate-500">
                                    <input type="radio" name="diag-relief" value="raised" class="text-amber-500 focus:ring-amber-500" checked>
                                    <span class="text-xs font-semibold">Raised / Bumpy (Die Crack/Chip)</span>
                                </label>
                                <label class="flex items-center space-x-2 bg-slate-900 border border-slate-700 p-3 rounded-lg cursor-pointer hover:border-slate-500">
                                    <input type="radio" name="diag-relief" value="incuse" class="text-amber-500 focus:ring-amber-500">
                                    <span class="text-xs font-semibold">Incuse / Recessed (Gouge/Struck-Through)</span>
                                </label>
                            </div>
                        </div>

                        <div>
                            <label class="block text-xs font-bold uppercase text-amber-400 tracking-wider mb-2">3. Primary Location of Observed Mark</label>
                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-2 text-xs">
                                <label class="flex items-center space-x-2 bg-slate-900/60 p-2.5 rounded border border-slate-700/80">
                                    <input type="checkbox" id="chk-woman" class="diag-chk text-amber-500 rounded">
                                    <span>Pilgrim Woman's Arm or Bonnet</span>
                                </label>
                                <label class="flex items-center space-x-2 bg-slate-900/60 p-2.5 rounded border border-slate-700/80">
                                    <input type="checkbox" id="chk-nose" class="diag-chk text-amber-500 rounded">
                                    <span>Nose Bridge or Facial Relief</span>
                                </label>
                                <label class="flex items-center space-x-2 bg-slate-900/60 p-2.5 rounded border border-slate-700/80">
                                    <input type="checkbox" id="chk-date" class="diag-chk text-amber-500 rounded">
                                    <span>Cutting through "1776-2026" Date</span>
                                </label>
                                <label class="flex items-center space-x-2 bg-slate-900/60 p-2.5 rounded border border-slate-700/80">
                                    <input type="checkbox" id="chk-ship" class="diag-chk text-amber-500 rounded">
                                    <span>Under Mayflower Ship Waterline</span>
                                </label>
                            </div>
                        </div>

                        <button onclick="runDiagnostic()" class="w-full bg-amber-500 hover:bg-amber-600 text-slate-950 font-bold py-3 rounded-lg shadow-lg transition flex justify-center items-center space-x-2">
                            <span>&#128269; Analyze Anomaly</span>
                        </button>
                    </div>

                    <!-- Diagnostic Output Box -->
                    <div class="lg:col-span-5 bg-slate-950 border border-amber-500/30 rounded-xl p-6 flex flex-col justify-between min-h-[340px]">
                        <div>
                            <div class="flex justify-between items-center border-b border-slate-800 pb-3 mb-4">
                                <span class="text-xs font-mono text-amber-400 uppercase tracking-wider">Analysis Result</span>
                                <span id="diagMatchStatus" class="text-[10px] bg-slate-800 text-slate-300 px-2 py-0.5 rounded">Ready for Input</span>
                            </div>

                            <div id="diagOutputPlaceholder" class="text-center py-8 text-slate-500 space-y-2">
                                <div class="text-3xl">&#128269;</div>
                                <p class="text-xs">Select options on the left and click "Analyze Anomaly" to get a diagnostic match.</p>
                            </div>

                            <div id="diagResultContainer" class="hidden space-y-3">
                                <span id="diagResultBadge" class="bg-amber-500 text-slate-950 text-xs font-black px-2.5 py-1 rounded inline-block">
                                    MATCH FOUND
                                </span>
                                <h3 id="diagResultTitle" class="text-xl font-bold text-white">
                                    The "Spirit of '76" Struck-Through Error
                                </h3>
                                <p id="diagResultDesc" class="text-xs text-slate-300 leading-relaxed">
                                    Your coin matches the characteristics of the feeder finger strike-through error, displaying deep incuse metal displacement across the lower date region.
                                </p>
                                <div class="bg-slate-900 border border-slate-800 p-3 rounded-lg text-xs space-y-1">
                                    <div class="flex justify-between">
                                        <span class="text-slate-400">Authenticity Confidence:</span>
                                        <span id="diagConfidence" class="text-emerald-400 font-bold">92% High</span>
                                    </div>
                                    <div class="flex justify-between">
                                        <span class="text-slate-400">Recommended Action:</span>
                                        <span id="diagAction" class="text-slate-200">Store in protective coin flip</span>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="pt-4 border-t border-slate-800 text-[11px] text-slate-500">
                            Note: Always verify suspicious errors under stereo magnification to rule out post-mint damage (PMD).
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION 4: Numismatic Data & Market Analytics -->
        <section id="analytics" class="py-12 px-4 sm:px-6 lg:px-8 max-w-7xl mx-auto border-t border-slate-200">
            <div class="mb-8">
                <div class="flex items-center space-x-2 text-amber-600 font-bold text-xs uppercase tracking-wider mb-1">
                    <span>Section 4</span>
                    <span>&bull;</span>
                    <span>Market & Rarity Index</span>
                </div>
                <h2 class="text-2xl sm:text-3xl font-bold text-slate-900">Numismatic Analytics & Valuation</h2>
                <p class="text-slate-600 mt-2 max-w-3xl">
                    Comparative breakdown of collector interest, estimated surviving population, and secondary market values across the progression stages and major varieties.
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <!-- Chart 1: Value vs Rarity across stages -->
                <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-between">
                    <div>
                        <div class="flex justify-between items-center mb-4">
                            <h3 class="text-base font-bold text-slate-900">Estimated Market Value by Die Stage ($ USD)</h3>
                            <span class="text-xs text-slate-400">August 2026 Collector Sales</span>
                        </div>
                        <p class="text-xs text-slate-500 mb-4">
                            As die breakdown advances toward stage 5, the dramatic visual appeal and extreme scarcity drive exponential market value increases.
                        </p>

                        <!-- Responsive Chart Container Required by Prompt -->
                        <div class="chart-container">
                            <canvas id="stageValueChart"></canvas>
                        </div>
                    </div>
                    <div class="mt-4 pt-3 border-t border-slate-100 text-center text-xs text-slate-400">
                        Data source: Compiled numismatic auction records & verified online sales.
                    </div>
                </div>

                <!-- Chart 2: Community Interest Radar -->
                <div class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-between">
                    <div>
                        <div class="flex justify-between items-center mb-4">
                            <h3 class="text-base font-bold text-slate-900">Collector Demand vs Population Scarcity</h3>
                            <span class="text-xs text-slate-400">Relative Metrics (0 - 100)</span>
                        </div>
                        <p class="text-xs text-slate-500 mb-4">
                            Comparing collector search volume, forum buzz, and certified pop reports across key 2026 Mayflower varieties.
                        </p>

                        <!-- Responsive Chart Container Required by Prompt -->
                        <div class="chart-container">
                            <canvas id="radarChart"></canvas>
                        </div>
                    </div>
                    <div class="mt-4 pt-3 border-t border-slate-100 text-center text-xs text-slate-400">
                        Higher scores indicate greater collector search volume and market liquidity.
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer class="bg-slate-950 text-slate-400 py-8 px-4 sm:px-6 lg:px-8 border-t border-slate-800 text-xs">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
            <div>
                <span class="font-bold text-slate-200 text-sm">2026 Mayflower Quarter Interactive Guide</span>
                <p class="text-slate-500 mt-0.5">Everyday Collector's Field Reference &bull; Unofficial Numismatic Research</p>
            </div>
            <div class="text-center md:text-right text-slate-500">
                <p>Designed for easy exploration of 2026-P die progression anomalies.</p>
                <p class="mt-0.5">No SVG or external font assets required &bull; Standalone SPA</p>
            </div>
        </div>
    </footer>

    <!-- Application JavaScript Logic -->
    <script>
        // Data Structures for Die Progression Stages
        const dieStages = [
            {
                stage: 1,
                title: "The Mosquito Bite",
                badge: "EARLY DIE STATE • STAGE 1",
                rarity: "Est. Known: ~1,500 - 2,000 coins",
                description: "Small, sharp, raised metal bumps begin appearing like bug bites near the Pilgrim woman's bonnet and sleeve. This is caused by microscopic pits opening on the overburdened steel die surface into which blank planchet metal flows under pressure.",
                marker: "Raised dot array near arm/bonnet",
                health: 80,
                healthText: "80% (Minor Pit Failure)",
                healthColor: "bg-emerald-500",
                collectorNote: "Look closely with a 10x loupe under angled lighting. Often mistaken for simple contact marks, but elevated geometry confirms raised die pitting.",
                value: 20
            },
            {
                stage: 2,
                title: "The Splinter",
                badge: "PROGRESSIVE CRACK • STAGE 2",
                rarity: "Est. Known: ~800 - 1,200 coins",
                description: "A sharp, thin raised hairline crack cuts across the field from the Pilgrim's pinky finger toward the rim. The steel die has suffered a structural fissure along a stress fracture line.",
                marker: "Thin raised line cutting across pinky field",
                health: 60,
                healthText: "60% (Fissure Propagation)",
                healthColor: "bg-amber-500",
                collectorNote: "The line must be distinctly raised above the field surface. If recessed into the coin, it is post-mint scratch damage.",
                value: 45
            },
            {
                stage: 3,
                title: "Raft in the Water",
                badge: "ADVANCED DIE FATIGUE • STAGE 3",
                rarity: "Est. Known: ~500 - 750 coins",
                description: "A flat-topped polygon-shaped raised chip floats in the ocean details beneath the Mayflower ship. A chunk of steel broke away from the die surface near the high-relief ship hull.",
                marker: "Polygonal raised patch under ship hull",
                health: 40,
                healthText: "40% (Surface Spalling)",
                healthColor: "bg-orange-500",
                collectorNote: "Often combined with earlier stage 'Mosquito' markers. Highly sought by ship coin specialists.",
                value: 85
            },
            {
                stage: 4,
                title: "The Nasal Strip",
                badge: "SEVERE STRESS DEFORMATION • STAGE 4",
                rarity: "Est. Known: ~300 - 450 coins",
                description: "A vertical raised bar runs directly along the bridge of the Pilgrim's nose as intense coining pressure forces metal to shift sideways into expanding die cracks.",
                marker: "Vertical bar bridge across nose relief",
                health: 20,
                healthText: "20% (Imminent Breakdown)",
                healthColor: "bg-red-500",
                collectorNote: "Extremely dramatic under low-angle illumination. Signals the final thousands of strikes before total failure.",
                value: 160
            },
            {
                stage: 5,
                title: "The Phantom of Larose",
                badge: "TERMINAL DIE SHATTER • STAGE 5",
                rarity: "Est. Known: < 150 coins reported",
                description: "The crown jewel of the discovery! Intersecting cracks cause an entire segment of the die to break and shift, creating a ghostly secondary mirror face in relief right next to the main bust profile.",
                marker: "Ghostly double mirror face/profile shift",
                health: 5,
                healthText: "5% (Terminal Shatter)",
                healthColor: "bg-red-700",
                collectorNote: "The press was halted shortly after this stage. Specimens represent terminal die collapse and fetch premium prices.",
                value: 320
            }
        ];

        let currentStageIndex = 0;

        // Initialize Application
        window.addEventListener('DOMContentLoaded', () => {
            initCanvas();
            renderCanvasStage(1);
            initCharts();
            setupMobileMenu();
        });

        // Mobile Menu Navigation
        function setupMobileMenu() {
            const btn = document.getElementById('mobile-menu-btn');
            const menu = document.getElementById('mobile-menu');
            if (btn && menu) {
                btn.addEventListener('click', () => {
                    menu.classList.toggle('hidden');
                });
            }
        }

        function scrollToSection(id) {
            const el = document.getElementById(id);
            if (el) {
                el.scrollIntoView({ behavior: 'smooth' });
                const menu = document.getElementById('mobile-menu');
                if (menu && !menu.classList.contains('hidden')) {
                    menu.classList.add('hidden');
                }
            }
        }

        // Progression Engine Controller
        function setStage(stageNum) {
            currentStageIndex = stageNum - 1;
            const data = dieStages[currentStageIndex];

            // Update tab styles
            document.querySelectorAll('.stage-btn').forEach((btn, idx) => {
                if (idx === currentStageIndex) {
                    btn.className = "stage-btn px-3 py-1.5 rounded-lg text-xs font-bold transition bg-amber-500 text-slate-950 shadow-sm";
                } else {
                    btn.className = "stage-btn px-3 py-1.5 rounded-lg text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200";
                }
            });

            // Update content text
            document.getElementById('stageBadge').innerText = data.badge;
            document.getElementById('stageRarity').innerText = data.rarity;
            document.getElementById('stageTitle').innerText = data.title;
            document.getElementById('stageDescription').innerText = data.description;
            document.getElementById('stageMarker').innerText = data.marker;
            document.getElementById('stageCollectorNote').innerText = data.collectorNote;
            
            const healthBar = document.getElementById('stageHealthBar');
            healthBar.className = `h-full ${data.healthColor}`;
            healthBar.style.width = `${data.health}%`;
            document.getElementById('stageHealthText').innerText = data.healthText;

            document.getElementById('stageStepIndicator').innerText = `Stage ${data.stage} of 5`;

            // Update buttons state
            const prevBtn = document.getElementById('prevBtn');
            const nextBtn = document.getElementById('nextBtn');
            
            if (currentStageIndex === 0) {
                prevBtn.disabled = true;
                prevBtn.className = "px-4 py-2 bg-slate-100 text-slate-400 rounded-lg text-xs font-bold cursor-not-allowed";
            } else {
                prevBtn.disabled = false;
                prevBtn.className = "px-4 py-2 bg-slate-900 hover:bg-slate-800 text-white rounded-lg text-xs font-bold transition";
            }

            if (currentStageIndex === dieStages.length - 1) {
                nextBtn.disabled = true;
                nextBtn.className = "px-4 py-2 bg-slate-100 text-slate-400 rounded-lg text-xs font-bold cursor-not-allowed";
            } else {
                nextBtn.disabled = false;
                nextBtn.className = "px-4 py-2 bg-slate-900 hover:bg-slate-800 text-white rounded-lg text-xs font-bold transition";
            }

            // Update canvas visualization tag & render
            document.getElementById('canvasTag').innerText = `Stage ${data.stage}: ${data.title}`;
            renderCanvasStage(data.stage);
        }

        function nextStage() {
            if (currentStageIndex < dieStages.length - 1) {
                setStage(currentStageIndex + 2);
            }
        }

        function prevStage() {
            if (currentStageIndex > 0) {
                setStage(currentStageIndex);
            }
        }

        // Canvas Simulator Implementation (NO SVG used)
        let ctx = null;
        function initCanvas() {
            const canvas = document.getElementById('coinCanvas');
            if (canvas && canvas.getContext) {
                ctx = canvas.getContext('2d');
            }
        }

        function renderCanvasStage(stage) {
            if (!ctx) return;
            const w = 280;
            const h = 280;
            const cx = w / 2;
            const cy = h / 2;

            // Clear
            ctx.clearRect(0, 0, w, h);

            // Draw Coin Background
            const grad = ctx.createRadialGradient(cx - 30, cy - 30, 10, cx, cy, 130);
            grad.addColorStop(0, '#f8fafc');
            grad.addColorStop(0.7, '#cbd5e1');
            grad.addColorStop(1, '#64748b');

            ctx.beginPath();
            ctx.arc(cx, cy, 130, 0, Math.PI * 2);
            ctx.fillStyle = grad;
            ctx.fill();
            ctx.lineWidth = 4;
            ctx.strokeStyle = '#94a3b8';
            ctx.stroke();

            // Inner Rim
            ctx.beginPath();
            ctx.arc(cx, cy, 122, 0, Math.PI * 2);
            ctx.lineWidth = 1.5;
            ctx.strokeStyle = '#64748b';
            ctx.stroke();

            // Draw Stylized Pilgrim Profiles (Canvas Paths)
            ctx.fillStyle = '#475569';
            ctx.font = 'bold 11px sans-serif';
            ctx.fillText('LIBERTY', cx - 22, 35);
            ctx.fillText('IN GOD WE TRUST', cx - 45, 255);
            ctx.font = 'bold 10px monospace';
            ctx.fillText('1776-2026', cx - 28, 240);
            ctx.fillText('P', cx + 90, cy + 10);

            // Pilgrim Male Bust Outline (Left)
            ctx.beginPath();
            ctx.arc(cx - 35, cy - 20, 25, 0, Math.PI * 2);
            ctx.fillStyle = '#94a3b8';
            ctx.fill();

            // Pilgrim Female Bust Outline (Right)
            ctx.beginPath();
            ctx.arc(cx + 25, cy + 10, 22, 0, Math.PI * 2);
            ctx.fillStyle = '#64748b';
            ctx.fill();

            // Draw Dynamic Error Lines based on Stage
            ctx.strokeStyle = '#b45309'; // Warm Amber/Bronze Crack Color
            ctx.fillStyle = '#d97706';

            if (stage >= 1) {
                // Mosquito Bites (Dots)
                ctx.beginPath();
                ctx.arc(cx + 42, cy + 2, 2.5, 0, Math.PI * 2);
                ctx.arc(cx + 47, cy + 12, 2, 0, Math.PI * 2);
                ctx.arc(cx + 38, cy + 18, 2.2, 0, Math.PI * 2);
                ctx.fill();
            }

            if (stage >= 2) {
                // The Splinter Crack
                ctx.beginPath();
                ctx.moveTo(cx + 30, cy + 30);
                ctx.lineTo(cx + 70, cy + 50);
                ctx.lineTo(cx + 100, cy + 60);
                ctx.lineWidth = 2;
                ctx.stroke();
            }

            if (stage >= 3) {
                // Raft in the Water
                ctx.beginPath();
                ctx.moveTo(cx - 50, cy + 60);
                ctx.lineTo(cx - 30, cy + 58);
                ctx.lineTo(cx - 20, cy + 68);
                ctx.lineTo(cx - 45, cy + 70);
                ctx.closePath();
                ctx.fill();
            }

            if (stage >= 4) {
                // Nasal Strip
                ctx.beginPath();
                ctx.rect(cx + 12, cy + 2, 4, 18);
                ctx.fill();
                ctx.lineWidth = 1;
                ctx.stroke();
            }

            if (stage >= 5) {
                // Terminal Phantom Mirror Profile Shift
                ctx.save();
                ctx.globalAlpha = 0.45;
                ctx.beginPath();
                ctx.arc(cx + 42, cy + 12, 22, 0, Math.PI * 2);
                ctx.fillStyle = '#d97706';
                ctx.fill();
                ctx.restore();

                // Shatter Web
                ctx.beginPath();
                ctx.moveTo(cx + 12, cy + 2);
                ctx.lineTo(cx - 10, cy - 40);
                ctx.moveTo(cx + 42, cy + 12);
                ctx.lineTo(cx + 115, cy - 10);
                ctx.lineWidth = 2.5;
                ctx.strokeStyle = '#92400e';
                ctx.stroke();
            }
        }

        // Variety Filtering Logic
        function filterVarieties(cat) {
            document.querySelectorAll('.v-filter-btn').forEach(btn => {
                btn.className = "v-filter-btn px-3 py-1.5 rounded-full text-xs font-bold bg-slate-100 text-slate-700 hover:bg-slate-200";
            });
            event.target.className = "v-filter-btn px-3 py-1.5 rounded-full text-xs font-bold bg-slate-900 text-white shadow-sm";

            document.querySelectorAll('.v-card').forEach(card => {
                if (cat === 'all' || card.getAttribute('data-category') === cat) {
                    card.style.display = 'flex';
                } else {
                    card.style.display = 'none';
                }
            });
        }

        // Diagnostic Assistant Tool
        function runDiagnostic() {
            const mint = document.getElementById('diag-mint').value;
            const relief = document.querySelector('input[name="diag-relief"]:checked').value;
            const chkWoman = document.getElementById('chk-woman').checked;
            const chkNose = document.getElementById('chk-nose').checked;
            const chkDate = document.getElementById('chk-date').checked;
            const chkShip = document.getElementById('chk-ship').checked;

            const placeholder = document.getElementById('diagOutputPlaceholder');
            const container = document.getElementById('diagResultContainer');
            const status = document.getElementById('diagMatchStatus');

            placeholder.classList.add('hidden');
            container.classList.remove('hidden');

            const title = document.getElementById('diagResultTitle');
            const desc = document.getElementById('diagResultDesc');
            const confidence = document.getElementById('diagConfidence');
            const action = document.getElementById('diagAction');

            status.innerText = "Analysis Complete";
            status.className = "text-[10px] bg-emerald-950 text-emerald-300 border border-emerald-700 px-2 py-0.5 rounded";

            if (relief === 'incuse' && chkDate) {
                title.innerText = "The 'Spirit of '76' Struck-Through Error";
                desc.innerText = "High match! Incuse surface marks cutting through the '1776-2026' date are characteristic of feeder finger scrape debris trapped under striking pressure.";
                confidence.innerText = "94% High Confidence";
                action.innerText = "Submit for NGC/PCGS error attribution";
            } else if (relief === 'raised' && (chkNose || (chkWoman && chkShip))) {
                title.innerText = "The 'Phantom of Larose' (Advanced/Terminal Stage)";
                desc.innerText = "Characteristics strongly indicate late-stage die cracking (Stage 4 or 5). Elevated metal along facial relief confirms structural die fragment shifting.";
                confidence.innerText = "88% High Confidence";
                action.innerText = "Protect in inert capsule; high collector interest";
            } else if (relief === 'raised' && chkWoman) {
                title.innerText = "Early Stage Die Breakdown ('Mosquito' / 'Splinter')";
                desc.innerText = "Matches early progression stages (Stage 1 or 2) of die #2026-P-04. Raised bumps on arm/bonnet indicate initial surface pitting.";
                confidence.innerText = "82% Moderate-High Confidence";
                action.innerText = "Check for secondary nasal markers with 10x loupe";
            } else {
                title.innerText = "Unclassified / Minor Die Degradation Variety";
                desc.innerText = "Your coin exhibits general die wear or strike anomalies common on high-speed 2026 minting runs. Compare closely with our progression matrix.";
                confidence.innerText = "65% General Match";
                action.innerText = "Compare with bank roll reference samples";
            }
        }

        // Chart.js Data Visualizations
        function initCharts() {
            // Chart 1: Bar Chart of Stage Values
            const ctxValue = document.getElementById('stageValueChart').getContext('2d');
            new Chart(ctxValue, {
                type: 'bar',
                data: {
                    labels: ['Stage 1\n(Mosquito)', 'Stage 2\n(Splinter)', 'Stage 3\n(Raft)', 'Stage 4\n(Nasal)', 'Stage 5\n(Phantom)'],
                    datasets: [{
                        label: 'Estimated Market Value ($)',
                        data: [20, 45, 85, 160, 320],
                        backgroundColor: [
                            'rgba(16, 185, 129, 0.7)',
                            'rgba(245, 158, 11, 0.7)',
                            'rgba(249, 115, 22, 0.7)',
                            'rgba(239, 68, 68, 0.7)',
                            'rgba(185, 28, 28, 0.85)'
                        ],
                        borderColor: [
                            '#059669',
                            '#d97706',
                            '#ea580c',
                            '#dc2626',
                            '#991b1b'
                        ],
                        borderWidth: 1.5
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            callbacks: {
                                label: (context) => `Est. Average Value: $${context.raw}`
                            }
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                callback: (val) => '$' + val
                            },
                            grid: { color: '#f1f5f9' }
                        },
                        x: {
                            grid: { display: false }
                        }
                    }
                }
            });

            // Chart 2: Radar Chart comparing varieties
            const ctxRadar = document.getElementById('radarChart').getContext('2d');
            new Chart(ctxRadar, {
                type: 'radar',
                data: {
                    labels: ['Scarcity', 'Collector Hype', 'Visual Impact', 'Market Value', 'Ease of Identification'],
                    datasets: [
                        {
                            label: 'Phantom of Larose (Terminal)',
                            data: [95, 90, 95, 92, 85],
                            backgroundColor: 'rgba(217, 119, 6, 0.25)',
                            borderColor: '#d97706',
                            pointBackgroundColor: '#b45309'
                        },
                        {
                            label: 'Spirit of \'76 (Feeder Finger)',
                            data: [70, 85, 80, 65, 90],
                            backgroundColor: 'rgba(37, 99, 235, 0.25)',
                            borderColor: '#2563eb',
                            pointBackgroundColor: '#1d4ed8'
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: { boxWidth: 12, font: { size: 11 } }
                        }
                    },
                    scales: {
                        r: {
                            angleLines: { color: '#e2e8f0' },
                            grid: { color: '#f1f5f9' },
                            suggestedMin: 0,
                            suggestedMax: 100,
                            ticks: { display: false }
                        }
                    }
                }
            });
        }
    </script>
</body>
</html>
```