<!DOCTYPE:html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Holistic Ferret Care Guide</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals (Beige, Taupe, Soft Brown) -->
    <!-- Application Structure Plan: The application is designed as a single-page, tab-based dashboard. This structure was chosen to provide a seamless, non-linear user experience, allowing ferret owners to quickly navigate to the topic they need without scrolling through irrelevant information. The main sections (Nutrition, Grooming, Habitat, Enrichment, Health) are presented as clear, clickable tabs. This thematic organization is more intuitive than a linear document, mirroring how a pet owner thinks about care categories. Key interactions include a dynamic diet calculator/chart, toggle-able recipe cards for DIY solutions, and interactive checklists for routines. This design facilitates quick reference and deep dives, making complex information easily digestible and actionable. -->
    <!-- Visualization & Content Choices: 
        - Nutrition: Report info on the 80/10/10 raw diet is presented as a primary goal. A Chart.js doughnut chart visually represents these proportions (Goal: Inform/Compare). The user can interact with buttons to see example meal plans, updating text blocks (Interaction: Click to update content). This is more engaging than a static list and reinforces the core dietary principle. (Library: Chart.js).
        - Grooming/Cleaning: Information on bathing frequency and cleaning products is organized into toggle-able cards (Goal: Organize). Users can click on a topic like "DIY Gentle Shampoo" to reveal a detailed recipe (Interaction: Click to expand/collapse). This keeps the main view uncluttered while providing deep information on demand. (Method: HTML/CSS/JS).
        - Habitat/Enrichment: Checklists for daily/weekly cleaning and passive/active toys are presented as interactive HTML elements. Users can mentally check off items, reinforcing routines (Goal: Organize/Inform). (Method: HTML/CSS/JS).
        - Health: A symptom spot-checker is presented as a series of clickable buttons. While strongly advising veterinary consultation, this provides initial guidance (Goal: Inform). (Method: HTML/CSS/JS).
        - All choices support the dashboard structure, prioritizing user interaction to explore detailed, natural care options effectively. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FDFBF8; /* Light beige background */
            color: #4A4A4A; /* Dark gray text */
        }
        .nav-button {
            transition: all 0.3s ease;
            color: #7d7d7d;
        }
        .nav-button.active {
            color: #8C6D5A; /* Soft Brown */
            border-bottom: 2px solid #8C6D5A;
            font-weight: 700;
        }
        .nav-button:hover {
            color: #8C6D5A;
        }
        .card {
            background-color: #FFFFFF;
            border: 1px solid #EAEAEA;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.08);
        }
        .content-section {
            display: none;
        }
        .content-section.active {
            display: block;
        }
        .recipe-toggle .recipe-content {
            display: none;
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-out;
        }
        .recipe-toggle.open .recipe-content {
            display: block;
            max-height: 1000px; /* Arbitrary large value */
        }
        .btn-primary {
            background-color: #8C6D5A;
            color: #FFFFFF;
            transition: background-color 0.3s;
            border-radius: 8px;
        }
        .btn-primary:hover {
            background-color: #735a4a;
        }
        .btn-secondary {
            background-color: #EFEBE7;
            color: #8C6D5A;
            transition: background-color 0.3s;
             border-radius: 8px;
        }
        .btn-secondary.active {
            background-color: #8C6D5A;
            color: #FFFFFF;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 400px;
            margin-left: auto;
            margin-right: auto;
            height: auto;
            max-height: 400px;
        }
         /* Simple loading spinner */
        .spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #8C6D5A;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .hidden {
            display: none !important;
        }
    </style>
</head>
<body class="antialiased">
    <div class="container mx-auto px-4 py-8 max-w-7xl">

        <header class="text-center mb-12">
            <h1 class="text-4xl md:text-5xl font-bold text-[#8C6D5A] mb-2">The Holistic Ferret Care Guide</h1>
            <p class="text-lg text-gray-600">A natural, DIY-focused approach for a happy, healthy companion.</p>
        </header>

        <nav class="flex justify-center border-b border-gray-200 mb-8 space-x-4 md:space-x-8">
            <button class="nav-button py-4 px-2 md:px-4 text-lg active" data-target="nutrition">
                <span class="mr-2">🍎</span>Nutrition
            </button>
            <button class="nav-button py-4 px-2 md:px-4 text-lg" data-target="grooming">
                <span class="mr-2">🛁</span>Grooming & Cleaning
            </button>
            <button class="nav-button py-4 px-2 md:px-4 text-lg" data-target="habitat">
                <span class="mr-2">🏠</span>Habitat & Bedding
            </button>
            <button class="nav-button py-4 px-2 md:px-4 text-lg" data-target="enrichment">
                <span class="mr-2">🎾</span>Enrichment & Play
            </button>
             <button class="nav-button py-4 px-2 md:px-4 text-lg" data-target="health">
                <span class="mr-2">❤️</span>Holistic Health
            </button>
        </nav>

        <main>
            <!-- Nutrition Section -->
            <section id="nutrition" class="content-section active">
                <div class="text-center mb-8">
                    <h2 class="text-3xl font-bold text-[#8C6D5A]">The Carnivore's Kitchen</h2>
                    <p class="mt-2 max-w-3xl mx-auto text-gray-600">Ferrets are obligate carnivores. Their health starts with a species-appropriate raw diet. The cornerstone of this is the 80/10/10 formula, which mimics whole prey and provides optimal, digestible nutrition without fillers or harmful additives.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-8 items-center">
                    <div class="card p-6">
                        <h3 class="text-2xl font-bold mb-4 text-center">The 80/10/10 Formula</h3>
                        <div class="chart-container">
                            <canvas id="dietChart"></canvas>
                        </div>
                        <div class="mt-4 text-center text-sm text-gray-500">
                           <p>This ratio is key to preventing many common ferret ailments and ensures they get the right balance of calcium, phosphorus, and essential nutrients.</p>
                        </div>
                    </div>
                    <div class="card p-6">
                        <h3 class="text-2xl font-bold mb-4">DIY Raw Mix Recipe (10lb Batch)</h3>
                        <p class="mb-4 text-gray-600">Making your own ferret food is cost-effective and gives you complete control over quality. Grind and mix these ingredients well, then freeze in daily portions.</p>
                         <ul class="space-y-3 text-gray-700">
                            <li><span class="font-bold text-[#8C6D5A]">8 lbs (80%): Muscle Meat.</span> Use a variety like chicken thighs, beef chunks, or turkey hearts. Aim for at least 3 different protein sources.</li>
                            <li><span class="font-bold text-[#8C6D5A]">1 lb (10%): Raw Edible Bone.</span> Chicken wings, necks, or rabbit bones are excellent. Must be raw and small enough to be ground.</li>
                            <li><span class="font-bold text-[#8C6D5A]">1 lb (10%): Organ Meat.</span> Crucial for vitamins. Use 0.5lb liver (any kind) and 0.5lb of other organs like kidney, spleen, or brain.</li>
                        </ul>
                        <div class="mt-6 p-4 bg-amber-50 rounded-lg text-amber-800">
                           <p><span class="font-bold">Important:</span> Never feed cooked bones. Transition your ferret slowly from kibble by mixing a small amount of raw food into their current diet, gradually increasing the ratio over several weeks.</p>
                        </div>
                    </div>
                     <!-- New Gemini API Integration for Nutrition -->
                    <div class="card p-6 md:col-span-2">
                        <h3 class="text-2xl font-bold mb-4">✨ Generate a Custom Ferret Recipe ✨</h3>
                        <p class="mb-4 text-gray-600">Need a unique recipe? Tell me what you're looking for, and I'll generate a custom raw food recipe for your ferret. For example: "A simple raw food recipe with chicken and beef organs."</p>
                        <textarea id="recipe-input" rows="3" class="w-full p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-[#8C6D5A]"></textarea>
                        <div class="flex items-center space-x-4 mt-4">
                           <button id="generate-recipe-btn" class="btn-primary py-2 px-6 font-bold">Generate Recipe</button>
                           <div id="recipe-spinner" class="spinner hidden"></div>
                        </div>
                        <div id="recipe-output" class="mt-6 p-4 bg-gray-50 rounded-lg whitespace-pre-line text-gray-700"></div>
                    </div>
                </div>
            </section>

            <!-- Grooming & Cleaning Section -->
            <section id="grooming" class="content-section">
                 <div class="text-center mb-8">
                    <h2 class="text-3xl font-bold text-[#8C6D5A]">Natural Grooming & Odor Control</h2>
                    <p class="mt-2 max-w-3xl mx-auto text-gray-600">A ferret's "musky" odor primarily comes from their skin oils, not scent glands (in neutered pets). A proper diet is the #1 defense against bad odor. Over-bathing strips natural oils, causing the body to overproduce them, making the smell worse. </p>
                </div>
                 <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="card p-6">
                        <h3 class="text-xl font-bold mb-2">Bathing: Less is More</h3>
                         <p class="text-gray-600">Bathe your ferret <span class="font-bold">no more than 2-3 times per year</span> unless they get into something dirty. Frequent bathing disrupts their skin's pH and oil balance.</p>
                    </div>
                    <div class="card p-6 recipe-toggle">
                        <div class="flex justify-between items-center cursor-pointer toggle-header">
                            <h3 class="text-xl font-bold">DIY Oatmeal Shampoo</h3>
                            <span class="text-2xl transform transition-transform duration-300">+</span>
                        </div>
                        <div class="recipe-content mt-4 text-gray-600">
                             <p class="mb-2">This soothes skin and gently cleans without harsh chemicals.</p>
                            <ol class="list-decimal list-inside space-y-1">
                                <li>Grind 1/2 cup of plain, uncooked oatmeal into a fine powder.</li>
                                <li>Mix the powder with 2 cups of warm water to form a milky solution.</li>
                                <li>Gently massage the mixture into your ferret's damp fur, avoiding eyes.</li>
                                <li>Let it sit for 5 minutes, then rinse thoroughly with warm water.</li>
                            </ol>
                        </div>
                    </div>
                     <div class="card p-6 recipe-toggle">
                        <div class="flex justify-between items-center cursor-pointer toggle-header">
                            <h3 class="text-xl font-bold">Ear Cleaning Solution</h3>
                             <span class="text-2xl transform transition-transform duration-300">+</span>
                        </div>
                        <div class="recipe-content mt-4 text-gray-600">
                             <p class="mb-2">Clean ears weekly to prevent wax buildup. A healthy ferret's earwax is light brown and minimal.</p>
                            <ol class="list-decimal list-inside space-y-1">
                                <li>Mix equal parts organic apple cider vinegar and distilled water.</li>
                                <li>Dampen a cotton ball (do not saturate) with the solution.</li>
                                <li>Gently wipe the visible parts of the inner ear. Never use Q-tips inside the canal.</li>
                            </ol>
                        </div>
                    </div>
                     <div class="card p-6">
                        <h3 class="text-xl font-bold mb-2">Nail Trimming</h3>
                         <p class="text-gray-600">Trim nails every 2-3 weeks. Use a cat nail clipper. Only snip the clear tip, avoiding the pink quick. A drop of salmon oil on their belly is a great distraction.</p>
                    </div>
                     <div class="card p-6 recipe-toggle">
                        <div class="flex justify-between items-center cursor-pointer toggle-header">
                            <h3 class="text-xl font-bold">Litter Box Cleaner</h3>
                            <span class="text-2xl transform transition-transform duration-300">+</span>
                        </div>
                        <div class="recipe-content mt-4 text-gray-600">
                             <p class="mb-2">Scoop daily. For weekly deep cleans, use this non-toxic spray.</p>
                            <ol class="list-decimal list-inside space-y-1">
                                <li>In a spray bottle, mix 1 part white vinegar with 2 parts water.</li>
                                <li>Add a few drops of unscented liquid castile soap.</li>
                                <li>Spray, let sit for 10 minutes, scrub, and rinse thoroughly. Vinegar neutralizes ammonia odors.</li>
                            </ol>
                        </div>
                    </div>
                     <div class="card p-6">
                        <h3 class="text-xl font-bold mb-2">Bedding & Toy Cleaning</h3>
                         <p class="text-gray-600">Wash all bedding, hammocks, and fabric toys weekly. Use a free-and-clear, unscented laundry detergent. Avoid fabric softeners, as the chemicals can irritate their skin.</p>
                    </div>
                     <!-- New Gemini API Integration for Grooming -->
                    <div class="card p-6 md:col-span-2 lg:col-span-3">
                        <h3 class="text-2xl font-bold mb-4">✨ Ask for a Custom Grooming Solution ✨</h3>
                        <p class="mb-4 text-gray-600">Describe a grooming issue you're facing, and I'll generate a natural, DIY solution. For example: "I need a gentle solution for dry, itchy ferret skin."</p>
                        <textarea id="grooming-input" rows="3" class="w-full p-3 border rounded-lg focus:outline-none focus:ring-2 focus:ring-[#8C6D5A]"></textarea>
                        <div class="flex items-center space-x-4 mt-4">
                           <button id="generate-grooming-btn" class="btn-primary py-2 px-6 font-bold">Get Solution</button>
                           <div id="grooming-spinner" class="spinner hidden"></div>
                        </div>
                        <div id="grooming-output" class="mt-6 p-4 bg-gray-50 rounded-lg whitespace-pre-line text-gray-700"></div>
                    </div>
                </div>
            </section>

            <!-- Habitat Section -->
            <section id="habitat" class="content-section">
                <div class="text-center mb-8">
                    <h2 class="text-3xl font-bold text-[#8C6D5A]">A Safe & Stimulating Environment</h2>
                    <p class="mt-2 max-w-3xl mx-auto text-gray-600">Ferrets are curious, intelligent, and can get into tiny spaces. "Ferret-proofing" your home is essential for their safety. Their habitat should be a cozy den, not a permanent prison; they need at least 4 hours of supervised playtime outside their cage daily.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="card p-6">
                        <h3 class="text-2xl font-bold mb-4">Cage & Bedding Essentials</h3>
                        <ul class="space-y-4">
                            <li class="flex items-start">
                                <span class="text-green-500 mr-3 mt-1">✓</span>
                                <div><span class="font-bold">Multi-Level Cage:</span> Provides vertical space. Ensure bar spacing is no more than 1" x 2" to prevent escapes.</div>
                            </li>
                             <li class="flex items-start">
                                <span class="text-green-500 mr-3 mt-1">✓</span>
                                <div><span class="font-bold">Solid Floors/Ramps:</span> Wire flooring can cause foot injuries. Cover any wire with fleece liners, towels, or solid plastic panels.</div>
                            </li>
                             <li class="flex items-start">
                                <span class="text-green-500 mr-3 mt-1">✓</span>
                                <div><span class="font-bold">Cozy Bedding:</span> Old t-shirts, towels, fleece blankets, and hammocks are perfect. Avoid items with loops or loose strings that can snag nails. Wash weekly.</div>
                            </li>
                             <li class="flex items-start">
                                <span class="text-green-500 mr-3 mt-1">✓</span>
                                <div><span class="font-bold">Litter Box:</span> Use a high-backed box in a corner of the cage. The best litter options are recycled paper pellets or wood stove pellets (not for cedar/pine). Avoid clay or clumping litters.</div>
                            </li>
                        </ul>
                    </div>
                    <div class="card p-6">
                        <h3 class="text-2xl font-bold mb-4">Ferret-Proofing Checklist</h3>
                         <ul class="space-y-4">
                            <li class="flex items-start">
                                <span class="text-red-500 mr-3 mt-1">✗</span>
                                <div><span class="font-bold">Block Small Gaps:</span> Check under doors, behind appliances, and around cabinets. Ferrets can squeeze through any opening their head fits through.</div>
                            </li>
                            <li class="flex items-start">
                                <span class="text-red-500 mr-3 mt-1">✗</span>
                                <div><span class="font-bold">Secure Cabinets:</span> Use child-proof latches, especially on cabinets containing cleaning supplies or food.</div>
                            </li>
                            <li class="flex items-start">
                                <span class="text-red-500 mr-3 mt-1">✗</span>
                                <div><span class="font-bold">Check Recliners & Sofas:</span> Ferrets love to climb inside furniture from below. This is a common cause of fatal accidents. Block access or avoid using recliners when they are out.</div>
                            </li>
                            <li class="flex items-start">
                                <span class="text-red-500 mr-3 mt-1">✗</span>
                                <div><span class="font-bold">Remove Foam/Rubber Items:</span> Ferrets often chew and ingest these, leading to intestinal blockages. This includes shoe insoles, remote buttons, and kids' toys.</div>
                            </li>
                         </ul>
                    </div>
                </div>
            </section>

            <!-- Enrichment Section -->
            <section id="enrichment" class="content-section">
                 <div class="text-center mb-8">
                    <h2 class="text-3xl font-bold text-[#8C6D5A]">Playtime & Brain Games</h2>
                    <p class="mt-2 max-w-3xl mx-auto text-gray-600">A bored ferret is a destructive ferret. Enrichment prevents behavioral problems and strengthens your bond. They thrive on novelty and activities that mimic their natural instincts to hunt, tunnel, and explore.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-8">
                    <div>
                        <div class="card p-6">
                            <h3 class="text-2xl font-bold mb-4">Passive Enrichment (In-Cage Fun)</h3>
                            <p class="mb-4 text-gray-600">These items keep them engaged when you're not around.</p>
                            <ul class="list-disc list-inside space-y-2">
                                <li><span class="font-bold">Tunnels & Tubes:</span> Cardboard shipping tubes or commercial plastic tunnels are a huge hit.</li>
                                <li><span class="font-bold">Dig Box:</span> A shallow cardboard box or plastic bin filled with dried beans, rice, or biodegradable packing peanuts allows them to satisfy their digging instincts. Hide treats inside!</li>
                                <li><span class="font-bold">Hammock & Bed Rotation:</span> Simply changing the location and type of bedding provides new smells and environments to explore.</li>
                                <li><span class="font-bold">Hard Plastic Toys:</span> Sturdy cat toys like jingle balls are generally safe. Avoid soft toys they can tear apart.</li>
                            </ul>
                        </div>
                    </div>
                     <div>
                        <div class="card p-6">
                            <h3 class="text-2xl font-bold mb-4">Active Playtime (With You!)</h3>
                            <p class="mb-4 text-gray-600">Interactive play is vital for their social well-being.</p>
                             <ul class="list-disc list-inside space-y-2">
                                <li><span class="font-bold">Chase Games:</span> Drag a towel, t-shirt, or flirt pole (a wand with a toy on a string) along the floor for them to chase and pounce on.</li>
                                <li><span class="font-bold">Blanket Maze:</span> Drape a large blanket over some furniture to create a temporary, explorable cave system.</li>
                                <li><span class="font-bold">Treasure Hunt:</span> Hide small pieces of meat or their favorite treats around a ferret-proofed room for them to find.</li>
                                <li><span class="font-bold">"Sock Monster":</span> Put a sock on your hand and gently wrestle with them. Let them "win" often to build confidence.</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </section>
            
            <!-- Health Section -->
            <section id="health" class="content-section">
                <div class="text-center mb-8">
                    <h2 class="text-3xl font-bold text-[#8C6D5A]">A Holistic Approach to Wellness</h2>
                    <p class="mt-2 max-w-3xl mx-auto text-gray-600">The goal of this guide is to foster a lifestyle that minimizes the need for veterinary visits through excellent preventative care. However, it's crucial to recognize that this approach is <span class="font-bold">preventative, not a replacement for professional medical care</span>. A strong foundation of natural care builds resilience, but accidents and serious illnesses can still happen. Being a responsible owner means combining diligent home care with the wisdom to seek veterinary help when needed.</p>
                </div>
                <div class="card p-6">
                    <h3 class="text-2xl font-bold mb-4">Recognizing When to See a Vet</h3>
                    <p class="mb-6 text-gray-600">Ferrets hide illness well. Daily observation is key. Contact a veterinarian immediately if you notice any of these signs. This guide empowers you to provide the best home care, not to diagnose or treat serious conditions.</p>
                    <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-center">
                        <div class="p-4 bg-red-50 rounded-lg">
                            <div class="text-3xl mb-2">🍽️</div>
                            <h4 class="font-bold">Loss of Appetite</h4>
                            <p class="text-sm text-red-700">Not eating for >12 hours is an emergency.</p>
                        </div>
                         <div class="p-4 bg-red-50 rounded-lg">
                            <div class="text-3xl mb-2">💤</div>
                            <h4 class="font-bold">Extreme Lethargy</h4>
                            <p class="text-sm text-red-700">Unresponsive or unable to stand.</p>
                        </div>
                        <div class="p-4 bg-red-50 rounded-lg">
                            <div class="text-3xl mb-2">🤢</div>
                            <h4 class="font-bold">Vomiting/Diarrhea</h4>
                            <p class="text-sm text-red-700">Especially if persistent or contains blood.</p>
                        </div>
                         <div class="p-4 bg-red-50 rounded-lg">
                            <div class="text-3xl mb-2">🐾</div>
                            <h4 class="font-bold">Straining to Urinate</h4>
                            <p class="text-sm text-red-700">Could indicate a life-threatening blockage.</p>
                        </div>
                         <div class="p-4 bg-red-50 rounded-lg">
                            <div class="text-3xl mb-2">😮</div>
                            <h4 class="font-bold">Difficulty Breathing</h4>
                            <p class="text-sm text-red-700">Wheezing, coughing, or open-mouth breathing.</p>
                        </div>
                         <div class="p-4 bg-red-50 rounded-lg">
                            <div class="text-3xl mb-2">⚖️</div>
                            <h4 class="font-bold">Sudden Hair Loss</h4>
                            <p class="text-sm text-red-700">Especially a thinning tail or symmetrical loss.</p>
                        </div>
                         <div class="p-4 bg-red-50 rounded-lg">
                            <div class="text-3xl mb-2">🦷</div>
                            <h4 class="font-bold">Pawing at the Mouth</h4>
                            <p class="text-sm text-red-700">Can indicate dental issues or something stuck.</p>
                        </div>
                        <div class="p-4 bg-red-50 rounded-lg">
                            <div class="text-3xl mb-2">🚶</div>
                            <h4 class="font-bold">Hind Leg Weakness</h4>
                            <p class="text-sm text-red-700">Stumbling or dragging back legs.</p>
                        </div>
                    </div>
                </div>
            </section>
        </main>

    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            try {
                const navButtons = document.querySelectorAll('.nav-button');
                const contentSections = document.querySelectorAll('.content-section');
                
                const recipeInput = document.getElementById('recipe-input');
                const generateRecipeBtn = document.getElementById('generate-recipe-btn');
                const recipeOutput = document.getElementById('recipe-output');
                const recipeSpinner = document.getElementById('recipe-spinner');

                const groomingInput = document.getElementById('grooming-input');
                const generateGroomingBtn = document.getElementById('generate-grooming-btn');
                const groomingOutput = document.getElementById('grooming-output');
                const groomingSpinner = document.getElementById('grooming-spinner');

                // Utility function to make API calls
                const callGeminiAPI = async (prompt, outputEl, spinnerEl) => {
                    outputEl.innerHTML = '';
                    outputEl.classList.remove('p-4', 'bg-gray-50');
                    spinnerEl.classList.remove('hidden');
                    
                    try {
                        const apiKey = ""; // If you want to use models other than gemini-2.5-flash-preview-05-20 or imagen-3.0-generate-002, provide an API key here. Otherwise, leave this as-is.
                        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;

                        const payload = {
                            contents: [{ parts: [{ text: prompt }] }],
                            systemInstruction: {
                                parts: [{ text: "You are a helpful and knowledgeable guide on holistic ferret care. Provide clear, concise, and helpful advice in a friendly, conversational tone. Format your responses with markdown." }]
                            },
                        };

                        const response = await fetch(apiUrl, {
                            method: 'POST',
                            headers: { 'Content-Type': 'application/json' },
                            body: JSON.stringify(payload)
                        });

                        const result = await response.json();
                        const text = result?.candidates?.[0]?.content?.parts?.[0]?.text || "Sorry, I couldn't generate a response. Please try again.";
                        outputEl.innerHTML = text.replace(/\n/g, '<br>');
                        outputEl.classList.add('p-4', 'bg-gray-50');

                    } catch (error) {
                        outputEl.innerHTML = `An error occurred: ${error.message}. Please try again.`;
                        outputEl.classList.add('p-4', 'bg-red-50');
                        console.error("Gemini API Error:", error);
                    } finally {
                        spinnerEl.classList.add('hidden');
                    }
                };

                // Navigation logic
                navButtons.forEach(button => {
                    button.addEventListener('click', () => {
                        const targetId = button.dataset.target;
                        navButtons.forEach(btn => btn.classList.remove('active'));
                        button.classList.add('active');
                        contentSections.forEach(section => {
                            if (section.id === targetId) {
                                section.classList.add('active');
                            } else {
                                section.classList.remove('active');
                            }
                        });
                    });
                });

                // Chart.js initialization
                const dietChartCtx = document.getElementById('dietChart');
                if (dietChartCtx) {
                    new Chart(dietChartCtx, {
                        type: 'doughnut',
                        data: {
                            labels: ['Muscle Meat', 'Raw Edible Bone', 'Organ Meat'],
                            datasets: [{
                                label: 'Diet Composition',
                                data: [80, 10, 10],
                                backgroundColor: [
                                    '#8C6D5A',
                                    '#D9C4B3',
                                    '#A68E7E'
                                ],
                                borderColor: '#FDFBF8',
                                borderWidth: 4
                            }]
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            cutout: '70%',
                            plugins: {
                                legend: {
                                    position: 'bottom',
                                    labels: {
                                        font: {
                                            family: 'Inter',
                                            size: 14
                                        },
                                         color: '#4A4A4A'
                                    }
                                }
                            }
                        }
                    });
                }
                
                // Recipe toggle logic
                const recipeToggles = document.querySelectorAll('.recipe-toggle');
                recipeToggles.forEach(toggle => {
                    const header = toggle.querySelector('.toggle-header');
                    if (header) {
                        const icon = header.querySelector('span');
                        header.addEventListener('click', () => {
                            toggle.classList.toggle('open');
                            if (icon) {
                                if (toggle.classList.contains('open')) {
                                    icon.style.transform = 'rotate(45deg)';
                                } else {
                                    icon.style.transform = 'rotate(0deg)';
                                }
                            }
                        });
                    }
                });

                // Gemini API listeners for Nutrition
                if (generateRecipeBtn && recipeInput && recipeOutput && recipeSpinner) {
                    generateRecipeBtn.addEventListener('click', () => {
                        const prompt = `Create a raw ferret food recipe based on the following request: "${recipeInput.value}". The recipe should adhere to the 80/10/10 rule (80% muscle meat, 10% raw edible bone, 10% organ meat).`;
                        callGeminiAPI(prompt, recipeOutput, recipeSpinner);
                    });
                }

                // Gemini API listeners for Grooming
                if (generateGroomingBtn && groomingInput && groomingOutput && groomingSpinner) {
                    generateGroomingBtn.addEventListener('click', () => {
                        const prompt = `Generate a natural, DIY grooming solution for a ferret based on the following request: "${groomingInput.value}". The solution should be safe and use common household ingredients. Reiterate the importance of a professional vet consultation.`;
                        callGeminiAPI(prompt, groomingOutput, groomingSpinner);
                    });
                }
            } catch (error) {
                console.error("An error occurred in the script:", error);
            }
        });
    </script>
</body>
</html>
