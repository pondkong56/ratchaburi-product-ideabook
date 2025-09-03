# ratchaburi-product-ideabook
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ideabook: นวัตกรรมผลิตภัณฑ์เกษตร จ.ราชบุรี</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Earthy Harmony -->
    <!-- Application Structure Plan: The application is designed as an interactive product gallery or "Ideabook". The core structure is a filterable grid of product idea cards. A top navigation bar with buttons allows the user to filter ideas by primary raw material (e.g., Coconut, Milk, Rice). This task-oriented design directly addresses the user's goal of exploring new ideas based on available resources. It's more engaging and useful than a static list, encouraging exploration and comparison of different innovation pathways. -->
    <!-- Visualization & Content Choices: 
    - Report Info: Raw material potential (coconut, milk, rice, etc.) -> Goal: Inspire/Organize -> Viz: Interactive Card Grid (HTML/Tailwind) -> Interaction: JS-powered category filtering buttons dynamically show/hide cards with smooth transitions. -> Justification: For presenting distinct, qualitative concepts like product ideas, a visual card grid is superior to data charts. It allows for a richer presentation of information (concept, target market, differentiation) for each idea. The filtering interaction is intuitive and empowers users to focus on materials they are interested in.
    - Report Info: Product concept details -> Goal: Inform -> Viz: Structured text and icons (emojis) within each card -> Interaction: Static (within the card) -> Justification: Emojis add visual appeal without needing image assets, and structured text makes the information scannable and easy to digest.
    - CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Sarabun', sans-serif;
            background-color: #FDFBF8;
            color: #3D352E;
        }
        .filter-btn {
            transition: all 0.3s ease;
            border-bottom: 3px solid transparent;
        }
        .filter-btn.active {
            color: #4A5C3D;
            border-bottom-color: #4A5C3D;
        }
        .product-card {
            transition: opacity 0.4s ease, transform 0.4s ease;
            opacity: 1;
            transform: scale(1);
        }
        .product-card.hidden {
            opacity: 0;
            transform: scale(0.95);
            display: none;
        }
    </style>
</head>
<body class="antialiased">

    <header class="bg-white/80 backdrop-blur-lg shadow-sm sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
            <div class="text-center">
                <h1 class="text-3xl font-bold text-[#4A5C3D]">Product Innovation Ideabook</h1>
                <p class="mt-1 text-lg text-gray-600">แนวคิดผลิตภัณฑ์ใหม่จากวัตถุดิบท้องถิ่นราชบุรี</p>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto py-8 px-4 sm:px-6 lg:px-8">
        
        <div class="mb-12 text-center">
            <p class="text-gray-700 max-w-3xl mx-auto">
                จากวัตถุดิบคุณภาพสู่ผลิตภัณฑ์นวัตกรรมที่ไม่เหมือนใคร ลองเลือกสำรวจแนวคิดผลิตภัณฑ์ใหม่ๆ ที่สร้างสรรค์ขึ้นเพื่อตอบสนองต่อเทรนด์ผู้บริโภคยุคใหม่ โดยใช้วัตถุดิบเด่นของราชบุรีเป็นหัวใจสำคัญ
            </p>
        </div>

        <div id="filter-container" class="flex flex-wrap justify-center gap-4 md:gap-8 mb-10 pb-4 border-b border-gray-200">
            <button class="filter-btn active font-semibold text-lg py-2 px-3" data-category="all">ทั้งหมด</button>
            <button class="filter-btn font-semibold text-lg py-2 px-3" data-category="coconut">🥥 มะพร้าว</button>
            <button class="filter-btn font-semibold text-lg py-2 px-3" data-category="milk">🥛 นมโค</button>
            <button class="filter-btn font-semibold text-lg py-2 px-3" data-category="rice">🌾 ข้าว</button>
            <button class="filter-btn font-semibold text-lg py-2 px-3" data-category="pineapple">🍍 สับปะรด</button>
            <button class="filter-btn font-semibold text-lg py-2 px-3" data-category="pork">🐖 สุกร</button>
        </div>

        <div id="product-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        </div>

    </main>
    
    <footer class="mt-16">
        <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8 border-t border-gray-200 text-center text-gray-500">
            <p>&copy; 2568 Ideabook for Ratchaburi Agricultural Innovation</p>
        </div>
    </footer>

    <script>
    document.addEventListener('DOMContentLoaded', () => {

        const productData = [
            {
                name: 'น้ำมะพร้าวเคเฟอร์ (Coconut Water Kefir)',
                icon: '🥥',
                category: 'coconut',
                color: 'blue',
                concept: 'เครื่องดื่มโปรไบโอติกส์เพื่อสุขภาพลำไส้ ที่เกิดจากการหมักน้ำมะพร้าวน้ำหอมด้วยเกรนส์เคเฟอร์ ให้รสชาติซ่าสดชื่นคล้ายสปาร์คกลิ้ง และมีประโยชน์ต่อร่างกาย',
                materials: ['น้ำมะพร้าวน้ำหอม (GI)', 'เกรนส์เคเฟอร์ (Kefir Grains)'],
                targetMarket: 'กลุ่มคนรักสุขภาพ, กลุ่มผู้บริโภคที่มองหาเครื่องดื่มทางเลือกใหม่, ผู้ที่แพ้นมวัว',
                differentiation: 'แตกต่างจากน้ำมะพร้าวทั่วไปโดยสิ้นเชิง โดยเพิ่มมูลค่าด้านสุขภาพ (โปรไบโอติกส์) และสร้างประสบการณ์การดื่มแบบใหม่ (รสซ่า สดชื่น) ซึ่งเป็นตลาดที่ยังมีคู่แข่งน้อย',
                challenges: 'การควบคุมกระบวนการหมักให้ได้มาตรฐาน, การให้ความรู้ผู้บริโภคเกี่ยวกับเคเฟอร์, อายุการเก็บรักษาสั้นกว่าเครื่องดื่มทั่วไป'
            },
            {
                name: 'ราชบุรีลาบเนะห์ (Ratchaburi Labneh)',
                icon: '🥛',
                category: 'milk',
                color: 'teal',
                concept: 'ผลิตภัณฑ์ชีสสดสไตล์ตะวันออกกลาง เนื้อครีมข้นเนียน ทำจากโยเกิร์ตที่กรองน้ำออกจนเกือบหมด สามารถใช้ทาขนมปัง, เป็นดิป, หรือผสมในสลัดได้',
                materials: ['น้ำนมดิบคุณภาพสูงจาก อ.จอมบึง', 'หัวเชื้อโยเกิร์ต'],
                targetMarket: 'ร้านอาหาร, โรงแรม, คาเฟ่, กลุ่มผู้บริโภคที่ชื่นชอบอาหารตะวันตกและตะวันออกกลาง',
                differentiation: 'เป็นผลิตภัณฑ์นมที่แตกต่างจากนมพาสเจอร์ไรส์หรือโยเกิร์ตทั่วไป สร้างตลาดใหม่ในกลุ่มชีสสดและผลิตภัณฑ์นมพรีเมียม โดยชูจุดเด่นเรื่องความสดใหม่จากฟาร์มคุณภาพ',
                challenges: 'ต้องสร้างการรับรู้ในตลาดให้ผู้บริโภคเข้าใจว่าลาบเนะห์คืออะไรและรับประทานอย่างไร, การควบคุมความสะอาดในกระบวนการผลิต'
            },
            {
                name: 'ข้าวพองกรอบเคลือบคาราเมลมะพร้าว (Coconut Caramel Rice Crisps)',
                icon: '🌾',
                category: 'rice',
                color: 'amber',
                concept: 'ขนมขบเคี้ยวเพื่อสุขภาพ ที่นำข้าวพองจากข้าวหอมมะลิราชบุรี มาคลุกเคล้ากับซอสคาราเมลที่ทำจากน้ำตาลมะพร้าวแท้และกะทิ แล้วอบจนกรอบ',
                materials: ['ข้าวสาร (อ.โพธาราม)', 'น้ำตาลมะพร้าว', 'กะทิ'],
                targetMarket: 'กลุ่มคนทำงาน, เด็ก, นักท่องเที่ยว, ตลาดของฝาก',
                differentiation: 'ยกระดับขนมนางเล็ด/ข้าวแต๋นแบบดั้งเดิมให้ดูทันสมัยขึ้น บรรจุภัณฑ์สวยงาม และใช้คาราเมลจากมะพร้าวแทนน้ำตาลอ้อยเพื่อสร้างกลิ่นหอมและรสชาติที่เป็นเอกลักษณ์ ไม่หวานแหลม',
                challenges: 'การพัฒนาสูตรให้มีความกรอบคงทน, การออกแบบบรรจุภัณฑ์ที่น่าดึงดูดและรักษาคุณภาพสินค้าได้ดี'
            },
            {
                name: 'ช็อตเอนไซม์สับปะรด (Pineapple Enzyme Wellness Shot)',
                icon: '🍍',
                category: 'pineapple',
                color: 'yellow',
                concept: 'เครื่องดื่มช็อตเล็กๆ ขนาด 50-60 ml ที่อุดมไปด้วยเอนไซม์โบรมีเลนจากแกนสับปะรด ช่วยเรื่องการย่อยอาหารและลดการอักเสบ อาจผสมขิงหรือขมิ้นเพื่อเพิ่มสรรพคุณ',
                materials: ['แกนสับปะรด (ผลผลิตพลอยได้)', 'เนื้อสับปะรด', 'สมุนไพรอื่นๆ เช่น ขิง, ขมิ้น'],
                targetMarket: 'กลุ่มคนรักสุขภาพ, ผู้ที่ออกกำลังกายเป็นประจำ, ผู้ที่มีปัญหาระบบย่อยอาหาร',
                differentiation: 'สร้างมูลค่าจาก "ของเหลือทิ้ง" อย่างแกนสับปะรดให้กลายเป็นผลิตภัณฑ์สุขภาพมูลค่าสูง ตอบเทรนด์ Wellness Shot ที่กำลังมาแรงในตลาดโลก',
                challenges: 'กระบวนการสกัดและรักษาคุณค่าของเอนไซม์โบรมีเลน, การสร้างความน่าเชื่อถือและสื่อสารสรรพคุณให้ถูกต้อง'
            },
            {
                name: 'หมูฉีกพร้อมทานซอสมะขาม (Ready-to-Eat Tamarind Pulled Pork)',
                icon: '🐖',
                category: 'pork',
                color: 'red',
                concept: 'เนื้อหมูส่วนสะโพกที่นำไปตุ๋นด้วยไฟอ่อนเป็นเวลานานกับซอสที่เคี่ยวจากมะขามและเครื่องเทศท้องถิ่น จนเปื่อยนุ่มและสามารถใช้ส้อมฉีกเป็นเส้นได้ง่าย บรรจุในถุงสุญญากาศ',
                materials: ['เนื้อสุกร', 'มะขาม', 'น้ำตาลมะพร้าว', 'เครื่องเทศ'],
                targetMarket: 'คนเมืองที่ไม่มีเวลาทำอาหาร, ครอบครัว, ร้านอาหารที่ต้องการวัตถุดิบสำเร็จรูปคุณภาพดี',
                differentiation: 'เปลี่ยนจากหมูแดดเดียวหรือกุนเชียงแบบเดิมๆ มาเป็นผลิตภัณฑ์สไตล์ตะวันตก (Pulled Pork) แต่ใช้รสชาติแบบไทย (ซอสมะขาม) สร้างความแปลกใหม่และสะดวกในการนำไปประกอบอาหารหลากหลายเมนู',
                challenges: 'การควบคุมมาตรฐานของรสชาติและเนื้อสัมผัส, การลงทุนในอุปกรณ์การผลิตและบรรจุภัณฑ์สุญญากาศ'
            },
            {
                name: 'โยเกิร์ตมะพร้าว (Coconut Yogurt)',
                icon: '🥥',
                category: 'coconut',
                color: 'blue',
                concept: 'ผลิตภัณฑ์โยเกิร์ตทางเลือกสำหรับคนแพ้นมวัว ทำจากกะทิคุณภาพดี หมักด้วยเชื้อจุลินทรีย์สำหรับโยเกิร์ต ให้เนื้อสัมผัสเนียนนุ่มและมีกลิ่นหอมของมะพร้าว',
                materials: ['กะทิสด', 'หัวเชื้อโยเกิร์ต (Dairy-free)'],
                targetMarket: 'กลุ่มวีแกน, ผู้ที่แพ้แลคโตส, กลุ่มคนรักสุขภาพ',
                differentiation: 'เจาะตลาด Plant-based ที่กำลังเติบโตอย่างรวดเร็วโดยตรง เป็นผลิตภัณฑ์ที่มีมูลค่าสูงและมีคู่แข่งในประเทศน้อยราย สามารถชูจุดเด่นของมะพร้าวน้ำหอมราชบุรีได้',
                challenges: 'การพัฒนาสูตรให้ได้เนื้อสัมผัสที่คงที่และไม่แยกชั้น, การตลาดเพื่อเข้าถึงกลุ่มลูกค้าเฉพาะกลุ่ม'
            }
        ];

        const productGrid = document.getElementById('product-grid');
        const filterButtons = document.querySelectorAll('.filter-btn');

        function renderProducts(category = 'all') {
            const filteredData = category === 'all' 
                ? productData 
                : productData.filter(p => p.category === category);

            productGrid.innerHTML = ''; 

            filteredData.forEach(product => {
                const card = document.createElement('div');
                card.className = `product-card bg-white p-6 rounded-xl shadow-lg border-t-8 border-${product.color}-500 flex flex-col`;
                card.dataset.category = product.category;
                
                card.innerHTML = `
                    <div class="flex items-start justify-between mb-4">
                        <div>
                            <h3 class="text-2xl font-bold text-gray-800">${product.name}</h3>
                            <p class="font-semibold text-${product.color}-600">แนวคิดผลิตภัณฑ์กลุ่ม${product.category === 'milk' ? 'นมโค' : product.category}</p>
                        </div>
                        <div class="text-5xl">${product.icon}</div>
                    </div>
                    <div class="space-y-4 flex-grow">
                        <div>
                            <h4 class="font-semibold text-gray-700">คอนเซ็ปต์หลัก:</h4>
                            <p class="text-gray-600 text-sm">${product.concept}</p>
                        </div>
                        <div>
                            <h4 class="font-semibold text-gray-700">วัตถุดิบท้องถิ่น:</h4>
                            <p class="text-gray-600 text-sm">${product.materials.join(', ')}</p>
                        </div>
                        <div>
                            <h4 class="font-semibold text-gray-700">กลุ่มเป้าหมาย:</h4>
                            <p class="text-gray-600 text-sm">${product.targetMarket}</p>
                        </div>
                        <div class="p-3 bg-${product.color}-50 rounded-lg mt-2">
                            <h4 class="font-semibold text-${product.color}-800">💡 จุดสร้างความแตกต่าง:</h4>
                            <p class="text-gray-700 text-sm">${product.differentiation}</p>
                        </div>
                         <div>
                            <h4 class="font-semibold text-gray-700">ความท้าทายที่เป็นไปได้:</h4>
                            <p class="text-gray-600 text-sm">${product.challenges}</p>
                        </div>
                    </div>
                `;
                productGrid.appendChild(card);
            });
        }

        filterButtons.forEach(button => {
            button.addEventListener('click', () => {
                const category = button.dataset.category;
                
                filterButtons.forEach(btn => btn.classList.remove('active'));
                button.classList.add('active');

                const allCards = document.querySelectorAll('.product-card');
                allCards.forEach(card => {
                    const cardCategory = card.dataset.category;
                    if (category === 'all' || cardCategory === category) {
                        setTimeout(() => {
                           card.classList.remove('hidden');
                        }, 10);
                    } else {
                        card.classList.add('hidden');
                    }
                });
            });
        });

        renderProducts('all');
    });
    </script>
</body>
</html>
