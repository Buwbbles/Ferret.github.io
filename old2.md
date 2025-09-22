<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Holistic Ferret: A Natural Care Guide</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Earthy Neutrals -->
    <!-- Application Structure Plan: A home-page-first, section-based structure was chosen for a more guided user flow. The landing page acts as a hub, introducing the core philosophy and offering clear navigation to all major content areas (Diet, Grooming, etc.). Clicking a link now hides the home page and reveals a single, focused content section, mimicking a multi-page app within one HTML file. This prevents information overload and provides a clear path for the user. A "Back to Home" button on each content page offers a consistent way to return to the main hub. The top navigation bar is now always visible and allows direct jumps between sections, improving efficiency. New sections for a shopping list and household hazards were integrated to provide a more comprehensive resource. -->
    <!-- Visualization & Content Choices: Report Info: 80/10/10 raw diet ratio -> Goal: Inform & Emphasize -> Viz/Method: Donut Chart -> Interaction: Static visualization with clear labels -> Justification: A donut chart provides an immediate, easy-to-understand visual breakdown of the most critical concept in the guide—the species-appropriate diet. It acts as a powerful visual anchor for the entire nutrition section. Report Info: DIY recipes for food, grooming, and cleaning -> Goal: Organize & Instruct -> Method: Styled HTML cards -> Interaction: Content toggles/accordions -> Justification: Hiding detailed recipes until clicked keeps the main layout clean and scannable, allowing users to focus on one recipe at a time without clutter. This supports the user task of finding a specific solution quickly. All diagrams and icons are rendered with Unicode characters or structured HTML/CSS to maintain the no-SVG constraint. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FDFBF8;
            color: #4A4A4A;
        }
        .nav-link {
            transition: color 0.3s ease, border-bottom-color 0.3s ease;
            border-bottom: 2px solid transparent;
        }
        .nav-link.active {
            color: #8C6E4A;
            border-bottom-color: #8C6E4A;
        }
        .section-title {
            color: #8C6E4A;
        }
        .card {
            background-color: #FFFFFF;
            border: 1px solid #F0EBE5;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
        }
        .btn-primary {
            background-color: #A47E54;
            color: white;
            transition: background-color 0.3s ease;
        }
        .btn-primary:hover {
            background-color: #8C6E4A;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 400px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .recipe-toggle {
            cursor: pointer;
        }
        .recipe-content {
            max-height: 0;
            overflow: hidden;
            opacity: 0;
            transition: max-height 0.5s ease-out, opacity 0.5s ease-out;
        }
    </style>
</head>
<body class="antialiased">

    <header class="bg-white/80 backdrop-blur-md sticky top-0 z-50 shadow-sm border-b border-gray-200">
        <nav class="container mx-auto px-6 py-4 flex justify-center md:justify-between items-center">
            <div id="main-title" class="text-2xl font-bold text-gray-800 md:block">
                🐾 The Holistic Ferret
            </div>
            <div id="nav-sections" class="flex space-x-4 md:space-x-8 hidden">
                <button class="nav-link text-gray-600 font-semibold pb-1 active" data-target="home-content">Home</button>
                <button class="nav-link text-gray-600 font-semibold pb-1" data-target="diet-content">Diet</button>
                <button class="nav-link text-gray-600 font-semibold pb-1" data-target="grooming-content">Grooming</button>
                <button class="nav-link text-gray-600 font-semibold pb-1" data-target="house-and-play-content">House & Play</button>
                <button class="nav-link text-gray-600 font-semibold pb-1" data-target="facts-content">Ferret Facts</button>
                <button class="nav-link text-gray-600 font-semibold pb-1" data-target="bonding-content">Bonding</button>
                <button class="nav-link text-gray-600 font-semibold pb-1" data-target="health-content">Health</button>
                <button class="nav-link text-gray-600 font-semibold pb-1" data-target="shopping-content">Shopping List</button>
            </div>
        </nav>
    </header>

    <main class="container mx-auto px-6 py-12">
        <div id="home-content" class="content-section">
            <section class="text-center mb-12">
                <h1 class="text-4xl md:text-5xl font-bold text-gray-800 mb-4">A Natural Guide to Ferret Wellness</h1>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto">
                    Welcome to your complete guide for raising a happy, healthy ferret the natural way. This guide focuses on a holistic approach, emphasizing a species-appropriate diet, gentle grooming, and a stimulating, chemical-free environment.
                </p>
            </section>
            <section class="mb-20">
                <h2 class="text-3xl font-bold section-title mb-8 text-center">Explore the Guide</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <button data-target="diet-content" class="card p-6 rounded-lg text-left hover:shadow-lg transition-shadow">
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">🥩 Diet & Nutrition</h3>
                        <p class="text-gray-600">The most important factor in your ferret's health: the 80/10/10 raw diet, transitioning methods, and DIY recipes.</p>
                    </button>
                    <button data-target="grooming-content" class="card p-6 rounded-lg text-left hover:shadow-lg transition-shadow">
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">🛁 Grooming & Odor</h3>
                        <p class="text-gray-600">Learn why less is more with bathing, how to care for nails and ears, and why diet is key to odor control.</p>
                    </button>
                    <button data-target="house-and-play-content" class="card p-6 rounded-lg text-left hover:shadow-lg transition-shadow">
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">🏡 House & Play</h3>
                        <p class="text-gray-600">Discover how to create a safe, clean, and enriching environment with natural cleaners and fun DIY toys.</p>
                    </button>
                    <button data-target="facts-content" class="card p-6 rounded-lg text-left hover:shadow-lg transition-shadow">
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">💡 Ferret Facts</h3>
                        <p class="text-gray-600">Essential knowledge about ferret behavior, sleep habits, sounds, and how to build a strong bond.</p>
                    </button>
                    <button data-target="bonding-content" class="card p-6 rounded-lg text-left hover:shadow-lg transition-shadow">
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">🤝 Building a Bond</h3>
                        <p class="text-gray-600">Learn how to build trust, reduce nipping, and form a deep connection with your ferret through play and positive reinforcement.</p>
                    </button>
                    <button data-target="health-content" class="card p-6 rounded-lg text-left hover:shadow-lg transition-shadow">
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">❤️ Health & Vets</h3>
                        <p class="text-gray-600">Understand the role of preventative care and why a relationship with an exotics vet is vital for your ferret's long-term health.</p>
                    </button>
                     <button data-target="shopping-content" class="card p-6 rounded-lg text-left hover:shadow-lg transition-shadow">
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">🛒 Shopping List</h3>
                        <p class="text-gray-600">A curated list of all the essential items you need for a happy and healthy ferret home.</p>
                    </button>
                </div>
            </section>

            <section class="mb-20">
                <h2 class="text-3xl font-bold section-title mb-8 text-center">A Companion for the Curious</h2>
                <div class="grid md:grid-cols-2 gap-12 items-center">
                    <div class="text-gray-600">
                        <p class="mb-4">
                            Ferrets are mischievous, intelligent, and endlessly entertaining companions. Their unique blend of playful energy and deep, lazy sleep makes them truly captivating pets. They form strong bonds with their owners and will keep you laughing with their silly "weasel war dances" and soft "dooking" sounds. For the right person, a ferret offers a rewarding and affectionate friendship unlike any other.
                        </p>
                         <h4 class="font-bold text-xl text-gray-800 mb-2">Why a Ferret Might Be Right For You:</h4>
                         <ul class="list-disc list-inside space-y-2 mb-8">
                             <li>They are highly social and playful, constantly exploring and getting into harmless mischief.</li>
                             <li>They are quiet and don't bark, making them suitable for apartment living.</li>
                             <li>Ferrets are very clean and can be litter-box trained.</li>
                             <li>They are small and adaptable, thriving in indoor environments.</li>
                         </ul>
                         
                    </div>
                    <div class="card p-8 rounded-lg bg-red-50 border-red-200 shadow-md">
                        <h3 class="text-xl font-bold text-red-800 mb-4">The Realities of Ferret Ownership</h3>
                        <p class="text-red-700 mb-4">
                            While incredibly fun, ferrets are not the right pet for everyone. It's crucial to understand their needs and challenges before bringing one home.
                        </p>
                        <ul class="list-disc list-inside space-y-3 text-red-700">
                            <li><strong>High Maintenance:</strong> Ferrets require extensive daily playtime (at least 4 hours) and daily cleaning of their habitat to manage odor and messes.</li>
                            <li><strong>Specialized Diet & Health:</strong> They are obligate carnivores with very specific dietary needs. They also require an exotics vet and are prone to certain health conditions like adrenal disease and insulinoma.</li>
                            <li><strong>Natural Instincts:</strong> Their natural instincts to dig, chew, and burrow mean they can be destructive. Your home must be thoroughly "ferret-proofed" to ensure their safety and protect your belongings.</li>
                        </ul>
                    </div>
                </div>
            </section>
        </div>

        <div id="diet-content" class="content-section hidden">
            <section class="mb-20">
                <h2 class="text-3xl font-bold section-title mb-8 text-center">🥩 The Carnivore's Kitchen: Diet & Nutrition</h2>
                <div class="grid md:grid-cols-2 gap-12 items-center">
                    <div class="card p-8 rounded-lg">
                        <h3 class="text-2xl font-bold text-gray-800 mb-4">The 80/10/10 Raw Diet Rule</h3>
                        <p class="text-gray-600 mb-4">
                            Ferrets are obligate carnivores. Their short digestive tract is designed for a raw meat diet. The cornerstone of natural ferret health is the 80/10/10 formula, which mimics their natural prey and provides optimal nutrition. A proper diet is the single most important factor in reducing odor and preventing common health issues.
                        </p>
                        <ul class="space-y-2 text-gray-700">
                            <li><span class="font-bold text-green-700">80% Muscle Meat:</span> Heart, tongue, gizzards, and general muscle tissue. Provides essential proteins and fats.</li>
                            <li><span class="font-bold text-blue-700">10% Raw Edible Bone:</span> Non-weight-bearing bones from poultry. Provides calcium and phosphorus, crucial for bone health, and naturally cleans teeth.</li>
                            <li><span class="font-bold text-red-700">10% Organ Meat:</span> 5% liver, 5% other secreting organs (kidney, spleen). These are nature's multivitamins, packed with essential nutrients.</li>
                        </ul>
                    </div>
                    <div class="chart-container">
                        <canvas id="dietChart"></canvas>
                    </div>
                </div>
                <div class="card p-8 rounded-lg mt-12">
                    <div class="recipe-toggle flex justify-between items-center">
                        <h3 class="text-2xl font-bold text-gray-800">DIY Raw Food "Grind" Recipe (10lb Batch)</h3>
                        <span class="text-2xl font-bold transform transition-transform duration-300">▼</span>
                    </div>
                    <div class="recipe-content mt-4 border-t pt-4">
                        <p class="text-gray-600 mb-4">This recipe provides a balanced mix that can be frozen in portions for easy feeding. Always use fresh, human-grade meats.</p>
                        <h4 class="font-bold text-lg mb-2">Ingredients:</h4>
                        <ul class="list-disc list-inside text-gray-700 space-y-2 mb-4">
                            <li><strong>8 lbs (128 oz) Muscle Meat:</strong>
                                <ul class="list-disc list-inside ml-6">
                                    <li>4 lbs Chicken Thighs (with bone)</li>
                                    <li>2 lbs Chicken Hearts/Gizzards</li>
                                    <li>2 lbs Pork Shoulder or Beef Roast (cubed)</li>
                                </ul>
                            </li>
                            <li><strong>1 lb (16 oz) Raw Edible Bone:</strong> The bones in the chicken thighs should cover this. If using boneless, substitute with 1lb chicken wings or necks.</li>
                            <li><strong>1 lb (16 oz) Organ Meat:</strong>
                                <ul class="list-disc list-inside ml-6">
                                    <li>0.5 lb (8 oz) Chicken or Beef Liver</li>
                                    <li>0.5 lb (8 oz) Other Organs (Beef Kidney, Pork Spleen)</li>
                                </ul>
                            </li>
                        </ul>
                        <h4 class="font-bold text-lg mb-2">Instructions:</h4>
                        <ol class="list-decimal list-inside text-gray-700 space-y-2">
                            <li><strong>Prepare Meats:</strong> Partially freeze all meat and bones for about 2-3 hours. This makes grinding much easier and safer. Cut larger pieces into strips that fit your grinder.</li>
                            <li><strong>Grind:</strong> Using a quality meat grinder, grind all ingredients together. A double grind ensures the bone is finely incorporated and safe for consumption.</li>
                            <li><strong>Mix:</strong> In a large bowl or tub, thoroughly mix all the ground components by hand to ensure the 80/10/10 ratio is consistent in every serving.</li>
                            <li><strong>Portion & Freeze:</strong> Portion the mix into daily or multi-day servings using ice cube trays, silicone molds, or small containers. Freeze immediately. A typical ferret eats 2-4 ounces per day, split into two meals.</li>
                        </ol>
                    </div>
                </div>
            </section>
        </div>

        <div id="grooming-content" class="content-section hidden">
            <section class="mb-20">
                <h2 class="text-3xl font-bold section-title mb-8 text-center">🛁 Gentle Grooming & Odor Control</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto text-center mb-12">
                    A ferret's natural musky scent comes from their skin oils, not dirt. Over-bathing strips these oils, causing the glands to overproduce and worsen the odor. A proper diet is the primary way to reduce odor; grooming should be minimal and gentle.
                </p>
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Bathing: Less is More</h3>
                        <p class="text-gray-600">Bathe your ferret only 1-3 times per YEAR. Frequent bathing is a leading cause of odor problems. Use a simple, non-stripping solution.</p>
                        <div class="recipe-toggle mt-4 bg-gray-50 p-3 rounded-lg flex justify-between items-center">
                            <h4 class="font-semibold text-gray-700">DIY Oatmeal Bath Recipe</h4>
                            <span class="text-lg transform transition-transform duration-300">▸</span>
                        </div>
                        <div class="recipe-content mt-2">
                            <ol class="list-decimal list-inside text-sm text-gray-700 space-y-1">
                                <li>Grind 1/2 cup of plain, uncooked oatmeal into a fine powder.</li>
                                <li>Place the powder in a sock or cheesecloth and tie it off.</li>
                                <li>Fill a sink with a few inches of lukewarm water and let the oatmeal sock steep, squeezing it to release the milky, soothing liquid.</li>
                                <li>Gently bathe your ferret in the water, avoiding their head. No harsh rubbing needed. Rinse lightly with clean, lukewarm water.</li>
                            </ol>
                        </div>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Nail & Ear Care</h3>
                        <p class="text-gray-600">Trim nails every 2-3 weeks. A dab of salmon oil on their belly can be a great distraction. Clean ears weekly with a cotton swab, only cleaning the parts you can see. Never go deep into the canal.</p>
                         <div class="recipe-toggle mt-4 bg-gray-50 p-3 rounded-lg flex justify-between items-center">
                            <h4 class="font-semibold text-gray-700">DIY Gentle Ear Cleaner</h4>
                            <span class="text-lg transform transition-transform duration-300">▸</span>
                        </div>
                        <div class="recipe-content mt-2">
                            <p class="text-sm text-gray-700">Mix equal parts organic apple cider vinegar and distilled water. Dampen a cotton ball (do not soak) and gently wipe the outer ear folds.</p>
                        </div>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Odor: Separating Fact from Fiction</h3>
                        <p class="text-gray-600 mb-4">
                            Ferrets have two main sources of odor: their natural musk from scent glands and the smell of a dirty environment.
                        </p>
                        <ul class="list-disc list-inside text-gray-700 space-y-2">
                            <li><strong>Musk:</strong> This is the natural, slightly musky smell of a ferret's coat and skin. It's a natural smell that can be managed by a high-quality diet. Most people become accustomed to this smell over time.</li>
                            <li><strong>Glandular Scent:</strong> Ferrets have anal scent glands. They will "poof" or "scoot" when startled or scared. The scent is extremely strong and foul but dissipates quickly. These glands should not be removed as a routine procedure.</li>
                            <li><strong>Dirty Cage:</strong> The most common source of a "bad" smell is a dirty cage or litter box. Ferrets have a fast metabolism and need their space cleaned daily. A clean habitat is the single most effective way to eliminate bad smells.</li>
                        </ul>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Brushing & Dental Care</h3>
                        <p class="text-gray-600">Brushing their fur, especially during shedding seasons, helps prevent hairballs that can cause dangerous blockages. Use a soft brush and make it part of your routine.</p>
                        <p class="text-gray-600 mt-4">Dental hygiene is critical. A raw diet with edible bones provides the best natural cleaning. However, you can also brush their teeth with a ferret-safe toothpaste and a small toothbrush or cotton swab. Aim for weekly brushing to prevent dental disease.</p>
                    </div>
                </div>
            </section>
        </div>

        <div id="house-and-play-content" class="content-section hidden">
            <section class="mb-20">
                <h2 class="text-3xl font-bold section-title mb-8 text-center">🏡 House, Cleaning & Enrichment</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto text-center mb-12">
                    A clean, stimulating environment is crucial for a ferret's physical and mental health. Use natural, ferret-safe products to avoid exposing them to harsh chemicals.
                </p>
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Cleaning Schedule & DIY Solutions</h3>
                        <ul class="space-y-3 text-gray-700">
                            <li><strong>Daily:</strong> Scoop litter box(es) 1-2 times. Spot clean any accidents.</li>
                            <li><strong>Weekly:</strong> Wash all bedding (hammocks, sleep sacks) and soft toys. Do a full litter box change and scrub.</li>
                            <li><strong>Monthly:</strong> Deep clean the entire cage and play areas.</li>
                        </ul>
                        <div class="recipe-toggle mt-4 bg-gray-50 p-3 rounded-lg flex justify-between items-center">
                            <h4 class="font-semibold text-gray-700">All-Purpose Cage Cleaner Recipe</h4>
                            <span class="text-lg transform transition-transform duration-300">▸</span>
                        </div>
                        <div class="recipe-content mt-2">
                            <p class="text-sm text-gray-700">In a spray bottle, mix a 50/50 solution of white vinegar and water. This is excellent for scrubbing cage bars, floors, and litter boxes. It disinfects and neutralizes odors safely. For stubborn messes, a paste of baking soda and water works well as a gentle abrasive.</p>
                        </div>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Enrichment & Playtime</h3>
                         <p class="text-gray-600 mb-4">Ferrets sleep deeply but play hard. They need at least 4 hours of supervised playtime outside their cage daily. Rotate toys to keep them interested.</p>
                        <ul class="space-y-3 text-gray-700">
                            <li><strong>Passive Toys:</strong> Tunnels and tubes are a must-have. Cardboard boxes, crinkle balls, and sturdy plastic toys are great for solo play.</li>
                            <li><strong>Interactive Play:</strong> Engage them with teaser wands (like for cats) or by hiding treats in a dig box.</li>
                             <li><strong>DIY Dig Box:</strong> Fill a large storage bin with uncooked rice, dried beans, or biodegradable packing peanuts. Bury some of their favorite toys inside for a fun foraging activity.</li>
                        </ul>
                    </div>
                     <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Ferrets and Your Home</h3>
                         <p class="text-gray-600 mb-4">Ferrets are masters of mischief. Always supervise them outside their cage. Common household hazards include:
                        <ul class="space-y-3 text-gray-700">
                            <li><span class="font-bold text-red-700">Toxic Chemicals:</span> Any household cleaner, pesticide, or medicine.</li>
                            <li><span class="font-bold text-red-700">Tiny Objects:</span> Rubber bands, foam, erasers, and other small items that can cause intestinal blockages.</li>
                             <li><span class="font-bold text-red-700">Recliners and Sofas:</span> They can easily be crushed or trapped in the moving parts of furniture.</li>
                        </ul>
                    </div>
                     <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Toy Types for Ferrets</h3>
                        <p class="text-gray-600 mb-4">When buying toys, look for durable, ferret-safe materials that can't be chewed up and swallowed.</p>
                        <ul class="list-disc list-inside space-y-2 text-gray-700">
                            <li><strong>Tubes and Tunnels:</strong> These cater to their natural burrowing instinct. Choose durable plastic or fabric tunnels.</li>
                            <li><strong>Interactive Toys:</strong> Feather wands and puzzle toys for cats can be a hit, promoting mental stimulation.</li>
                            <li><strong>Digging Toys:</strong> A dig box filled with uncooked rice or shredded paper satisfies their urge to dig.</li>
                            <li><strong>Hard Plastic Toys:</strong> Sturdy plastic balls, keys, and rings are great for batting around, but avoid soft plastic or rubber that can be ingested.</li>
                            <li><strong>Plush Toys:</strong> Small, durable stuffed animals can be safe if they are not prone to being torn apart.</li>
                        </ul>
                    </div>
                </div>
            </section>
        </div>
        
        <div id="facts-content" class="content-section hidden">
            <section class="mb-20">
                <h2 class="text-3xl font-bold section-title mb-8 text-center">💡 Ferret Facts & Vital Knowledge</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto text-center mb-12">
                    Beyond diet and grooming, understanding your ferret's unique behaviors and needs is key to a strong bond and a happy life together.
                </p>
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">The "Ferret Business"</h3>
                        <p class="text-gray-600">A group of ferrets is called a "business." They often live in groups and thrive with companions, though they are also very bonded to their humans. Consider having a pair if your lifestyle allows.</p>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">The Ferret Nap</h3>
                        <p class="text-gray-600">Ferrets sleep up to 75% of the day! During their deep sleep, they can be limp and unresponsive. This "ferret dead sleep" is completely normal. Don't panic—just enjoy the peaceful moment.</p>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">The "Dook" & Weasel War Dance</h3>
                        <p class="text-gray-600">When excited or playful, ferrets make a soft chuckling sound called "dooking." They might also perform the "weasel war dance," a series of uncoordinated hops and bumps, often accompanied by a puffed-up tail. It's a sign of pure happiness.</p>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Harness & Leash Safety</h3>
                        <p class="text-gray-600">Ferrets can be walked on a leash! Always use a figure-8 harness designed for ferrets, as they can easily slip out of a traditional collar. This allows for safe, supervised outdoor time for fresh air and new smells.</p>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Digging & Burrowing Instincts</h3>
                        <p class="text-gray-600">Ferrets have a powerful instinct to dig and burrow. Provide them with safe outlets for this behavior, like a dig box or a pile of blankets, to prevent them from tearing up furniture or carpets.</p>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Understanding Their Bite</h3>
                        <p class="text-gray-600">Kits (baby ferrets) often nip as a way to play and explore. With consistent and gentle training, this can be corrected. Never hit or scold a ferret; instead, use a consistent method like a scruff and a firm "no."</p>
                    </div>
                </div>
            </section>
        </div>

        <div id="bonding-content" class="content-section hidden">
            <section class="mb-20">
                <h2 class="text-3xl font-bold section-title mb-8 text-center">🤝 Building a Bond: Trust & Training</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto text-center mb-12">
                    A ferret's bond with its human is built on trust, consistency, and plenty of positive interaction. By understanding their behavior and using gentle training techniques, you can forge a deep and lasting friendship.
                </p>
                <div class="grid md:grid-cols-2 gap-8">
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">The Importance of Playtime</h3>
                        <p class="text-gray-600 mb-4">
                            Ferrets are not content to sit still. Daily, supervised playtime is the most critical element of bonding. When they are out of the cage, get down to their level, engage them with toys, and let them explore. This shows them that you are a part of their world and a source of fun.
                        </p>
                        <ul class="list-disc list-inside space-y-2 text-gray-700">
                            <li><strong>Follow their lead:</strong> Let them sniff and explore you at their own pace.</li>
                            <li><strong>Use treats:</strong> Offer a small amount of a ferret-safe treat (like salmon oil or freeze-dried meat) to build positive associations.</li>
                            <li><strong>Respect their boundaries:</strong> If they seem uninterested or want to be left alone, let them be.</li>
                        </ul>
                    </div>
                     <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Training with Positive Reinforcement</h3>
                        <p class="text-gray-600 mb-4">
                            Ferrets are highly intelligent and can be trained to respond to their name, come when called, and even learn simple tricks.
                        </p>
                        <ul class="list-disc list-inside space-y-2 text-gray-700">
                            <li><strong>Litter Training:</strong> Ferrets naturally choose a corner to do their business. Place a litter box there and reward them when they use it correctly. If they go outside the box, gently place them inside the box to reinforce the behavior.</li>
                            <li><strong>Bite Inhibition:</strong> Never punish your ferret. Instead, use a "time out" method. When they bite too hard, give a firm "no" and place them in a small carrier or a non-fun area for 3-5 minutes. This teaches them that biting ends the fun.</li>
                            <li><strong>Target Training:</strong> Use a simple clicker or sound and a target stick. When they touch the stick with their nose, give a treat. This can be expanded to teach them to come to you or go into their cage.</li>
                        </ul>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Creating a Safe Space</h3>
                        <p class="text-gray-600 mb-4">
                            A ferret that feels secure is more likely to trust and bond with you. Their cage and play areas should be a refuge for them.
                        </p>
                        <ul class="list-disc list-inside space-y-2 text-gray-700">
                            <li><strong>Provide safe bedding:</strong> Old t-shirts, blankets, and towels that smell like you can make their cage feel more comforting.</li>
                            <li><strong>Hiding spots:</strong> Ferrets love to burrow and hide. Provide plenty of sleep sacks, tunnels, and hideaways where they can feel safe.</li>
                            <li><strong>Respect sleep:</strong> Never wake a ferret suddenly. Allow them to wake up on their own terms.</li>
                        </ul>
                    </div>
                </div>
            </section>
        </div>

        <div id="shopping-content" class="content-section hidden">
            <section class="mb-20">
                <h2 class="text-3xl font-bold section-title mb-8 text-center">🛒 The Holistic Ferret Shopping List</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto text-center mb-12">
                    A curated list of essential items for your ferret's natural lifestyle. Focus on quality over quantity and avoid products with harmful chemicals.
                </p>
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Food & Supplements</h3>
                        <ul class="list-disc list-inside space-y-2 text-gray-700">
                            <li>Fresh, human-grade meats (chicken, turkey, beef)</li>
                            <li>Edible raw bones (chicken wings, necks)</li>
                            <li>Organ meats (liver, heart, kidney)</li>
                            <li>Salmon oil or other omega-3 supplements</li>
                            <li>Ferret-safe treat (raw meat strips)</li>
                        </ul>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Habitat & Home</h3>
                        <ul class="list-disc list-inside space-y-2 text-gray-700">
                            <li>Multi-level cage with a solid bottom (no wire floors)</li>
                            <li>Litter box and ferret-safe litter (pelleted paper or wood)</li>
                            <li>Bedding (old t-shirts, blankets, towels)</li>
                            <li>Food and water dishes (ceramic or stainless steel)</li>
                            <li>Water bottle with a guard or a bowl for hydration</li>
                        </ul>
                    </div>
                    <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Grooming & Health</h3>
                        <ul class="list-disc list-inside space-y-2 text-gray-700">
                            <li>Blunt-tipped nail clippers</li>
                            <li>Cotton swabs</li>
                            <li>Oatmeal (plain, uncooked) for baths</li>
                            <li>Organic apple cider vinegar</li>
                            <li>Ferret-safe flea preventative (consult your vet)</li>
                        </ul>
                    </div>
                     <div class="card p-6 rounded-lg">
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Toys & Playtime</h3>
                        <ul class="list-disc list-inside space-y-2 text-gray-700">
                            <li>Hard plastic toys (avoid soft rubber)</li>
                            <li>PVC pipes or dryer vent tubing for tunnels</li>
                            <li>Dig box (with clean soil or uncooked rice)</li>
                            <li>Teaser wands (cat toys with feathers)</li>
                            <li>Old socks and blankets for burrowing</li>
                        </ul>
                    </div>
                </div>
            </section>
        </div>

        <div id="health-content" class="content-section hidden">
            <section>
                <h2 class="text-3xl font-bold section-title mb-8 text-center">❤️ A Note on Health & Vets</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto text-center mb-12">
                    The goal of a natural lifestyle is not to *avoid* the vet, but to build a foundation of robust health that makes vet visits for illness less likely. Preventative care at home is your most powerful tool. However, it is not a replacement for professional medical care when needed.
                </p>
                 <div class="bg-yellow-100 border-l-4 border-yellow-500 text-yellow-800 p-6 rounded-r-lg card">
                    <h3 class="text-xl font-bold mb-2">Vets are Vital Partners</h3>
                    <p>
                    An annual check-up with an experienced exotics vet is crucial for monitoring health, even for a seemingly healthy ferret. Accidents and sudden illnesses can happen. This guide empowers you to provide the best daily care, but a vet is an irreplaceable partner in your ferret's lifelong health journey. Ferrets are experts at hiding illness, so professional check-ups are key to early detection.
                    </p>
                </div>
            </section>
        </div>
    </main>

    <footer class="bg-gray-800 text-white mt-20">
        <div class="container mx-auto px-6 py-8 text-center">
            <p>This guide provides information for natural ferret care. Always consult with a qualified exotics veterinarian for medical advice.</p>
            <p class="mt-2 text-sm text-gray-400">The Holistic Ferret © 2025</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            // Function to initialize the diet chart
            const initDietChart = () => {
                const dietData = {
                    labels: ['Muscle Meat', 'Raw Edible Bone', 'Organ Meat'],
                    datasets: [{
                        label: 'Diet Composition',
                        data: [80, 10, 10],
                        backgroundColor: [
                            '#2E8B57',
                            '#4682B4',
                            '#B22222'
                        ],
                        borderColor: '#FDFBF8',
                        borderWidth: 4,
                        hoverOffset: 4
                    }]
                };

                const dietConfig = {
                    type: 'doughnut',
                    data: dietData,
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: {
                                position: 'top',
                                labels: {
                                    color: '#4A4A4A',
                                    font: {
                                        size: 14,
                                        weight: '600'
                                    }
                                }
                            },
                            tooltip: {
                                callbacks: {
                                    label: function(context) {
                                        let label = context.label || '';
                                        if (label) {
                                            label += ': ';
                                        }
                                        if (context.parsed !== null) {
                                            label += context.parsed + '%';
                                        }
                                        return label;
                                    }
                                }
                            }
                        },
                        cutout: '60%'
                    }
                };
                
                // Get the canvas element and ensure it exists before creating the chart
                const dietChartCtx = document.getElementById('dietChart');
                if (dietChartCtx) {
                    new Chart(dietChartCtx, dietConfig);
                }
            };


            const navButtons = document.querySelectorAll('.nav-link');
            const homeButtons = document.querySelectorAll('#home-content button[data-target]');
            const allButtons = [...navButtons, ...homeButtons];
            const contentSections = document.querySelectorAll('.content-section');
            const navSectionsDiv = document.getElementById('nav-sections');
            const mainTitle = document.getElementById('main-title');

            const showContent = (targetId) => {
                contentSections.forEach(section => {
                    section.classList.add('hidden');
                });
                document.getElementById(targetId).classList.remove('hidden');
                window.scrollTo({ top: 0, behavior: 'smooth' });

                if (targetId === 'home-content') {
                    navSectionsDiv.classList.add('hidden');
                    if (mainTitle) mainTitle.classList.remove('hidden');
                } else {
                    navSectionsDiv.classList.remove('hidden');
                    if (mainTitle) mainTitle.classList.add('hidden');
                }

                // Initialize the chart only when the diet-content section is shown
                if (targetId === 'diet-content') {
                    initDietChart();
                }
            };

            const setActiveLink = (targetId) => {
                navButtons.forEach(btn => {
                    btn.classList.remove('active');
                    if (btn.dataset.target === targetId) {
                        btn.classList.add('active');
                    }
                });
            };

            allButtons.forEach(button => {
                button.addEventListener('click', () => {
                    const targetId = button.dataset.target;
                    showContent(targetId);
                    setActiveLink(targetId);
                });
            });

            const recipeToggles = document.querySelectorAll('.recipe-toggle');
            recipeToggles.forEach(toggle => {
                toggle.addEventListener('click', () => {
                    const content = toggle.nextElementSibling;
                    const icon = toggle.querySelector('span');
                    
                    const isCollapsed = content.style.maxHeight === '0px' || content.style.maxHeight === '';

                    if (isCollapsed) {
                        content.style.maxHeight = content.scrollHeight + 'px';
                        content.style.opacity = '1';
                        if(icon) icon.style.transform = 'rotate(90deg)';
                    } else {
                        content.style.maxHeight = '0px';
                        content.style.opacity = '0';
                        if(icon) icon.style.transform = 'rotate(0deg)';
                    }
                });
            });
            
            // Set initial state
            showContent('home-content');
            setActiveLink('home-content');
        });
    </script>
</body>
</html>
