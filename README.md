<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Akuakultur Sistem by Tegar</title>
    <!-- Memuat Tailwind CSS dari CDN, cara ini kompatibel dengan GitHub Pages -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Gaya tambahan untuk UI dan Background Interaktif */
        body { 
            font-family: 'Inter', sans-serif; 
            background-color: #0f172a; /* Warna dasar slate-900 */
            color: #f8fafc; /* Teks default terang */
            overflow-x: hidden; /* Mencegah scroll horizontal */
        }
        #fishery-bg { /* ID Baru untuk background perikanan */
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0; /* Letakkan di belakang konten utama */
        }
        .main-content {
            position: relative;
            z-index: 1; /* Konten utama berada di atas background */
        }
        .card { 
            background-color: rgba(15, 23, 42, 0.75); /* Latar belakang semi-transparan lebih gelap */
            backdrop-filter: blur(12px); /* Efek blur untuk tampilan modern */
            -webkit-backdrop-filter: blur(12px);
            border-radius: 0.75rem; 
            padding: 2rem; 
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
            transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
            border-color: rgba(255, 255, 255, 0.2);
        }
        .main-button {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
        }
        /* Penyesuaian warna teks dan input untuk tema gelap */
        label { color: #cbd5e1; /* slate-300 */ }
        .card h2 { color: #f1f5f9; /* slate-100 */ }
        input, select {
            background-color: rgba(15, 23, 42, 0.5) !important; /* bg-slate-900/50 */
            border-color: #334155 !important; /* border-slate-700 */
            color: white !important;
        }
        input:focus, select:focus {
            border-color: #6366f1 !important; /* focus:border-indigo-500 */
            --tw-ring-color: #6366f1 !important; /* focus:ring-indigo-500 */
        }
        /* Gaya untuk daftar hasil */
        .result-item { 
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
            padding: 1rem 0.5rem; 
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            transition: background-color 0.2s ease-in-out;
        }
        .result-item:hover {
            background-color: rgba(255, 255, 255, 0.05);
        }
        .result-item:last-child { 
            border-bottom: none; 
        }
        .result-item span:first-child {
            color: #94a3b8; /* slate-400 */
        }
        .result-item span:last-child {
            color: #ffffff;
            font-weight: 700;
        }
        .status-badge { 
            display:inline-block; 
            padding: 0.5rem 1rem; 
            border-radius: 9999px; 
            font-weight: 600; 
            font-size: 0.875rem;
        }
    </style>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
</head>
<body class="p-4 md:p-8">
<canvas id="fishery-bg"></canvas>
<div class="main-content max-w-3xl mx-auto">
    <div class="text-center mb-10">
        <h1 class="text-4xl md:text-5xl font-extrabold text-white">Smart Akuakultur Sistem</h1>
        <p class="text-lg text-slate-400 mt-2">by Tegar</p>
    </div>
    
    <div class="space-y-8">
        <!-- Kolom Input -->
        <div class="card">
            <h2 class="text-2xl font-bold mb-6 border-b border-slate-700 pb-4 flex items-center gap-3">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-indigo-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                </svg>
                Data Siklus Panen
            </h2>
            <div class="space-y-5">
                <div>
                    <label for="fish_type" class="block text-sm font-medium mb-1">Pilih Jenis Ikan</label>
                    <select id="fish_type" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                        <option value="lele">Lele</option>
                        <option value="nila">Nila</option>
                        <option value="gurame">Gurame</option>
                        <option value="mas">Ikan Mas</option>
                        <option value="patin">Patin</option>
                        <option value="bawal">Bawal</option>
                    </select>
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label for="weight_unit" class="block text-sm font-medium mb-1">Satuan Bobot (Total)</label>
                        <select id="weight_unit" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                            <option value="kg">Kilogram (kg)</option>
                            <option value="g">Gram (g)</option>
                        </select>
                    </div>
                    <div>
                        <label for="lama_budidaya" class="block text-sm font-medium mb-1">Lama Budidaya (hari)</label>
                        <input type="number" id="lama_budidaya" placeholder="Contoh: 90" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                    </div>
                </div>
                <hr class="border-slate-700">

                <!-- KELOMPOK BOBOT AWAL -->
                <div class="p-4 border border-slate-700 rounded-lg space-y-4">
                    <h3 class="font-semibold text-slate-300">Data Bobot Awal</h3>
                    <div>
                        <label for="bobot_awal_type" class="block text-sm font-medium mb-1">Jenis Input</label>
                        <select id="bobot_awal_type" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                            <option value="total">Total Bobot</option>
                            <option value="rata">Rata-rata Bobot</option>
                        </select>
                    </div>
                    <div>
                        <label id="label_bobot_awal" for="bobot_awal_tebar" class="flex items-center text-sm font-medium mb-1">Total Bobot Awal</label>
                        <input type="number" id="bobot_awal_tebar" placeholder="Contoh: 10" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                    </div>
                </div>

                <!-- KELOMPOK BOBOT PANEN -->
                <div class="p-4 border border-slate-700 rounded-lg space-y-4">
                    <h3 class="font-semibold text-slate-300">Data Bobot Panen</h3>
                    <div>
                        <label for="bobot_panen_type" class="block text-sm font-medium mb-1">Jenis Input</label>
                        <select id="bobot_panen_type" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                            <option value="total">Total Bobot</option>
                            <option value="rata">Rata-rata Bobot</option>
                        </select>
                    </div>
                    <div>
                        <label id="label_bobot_panen" for="bobot_panen" class="flex items-center text-sm font-medium mb-1">Total Bobot Panen</label>
                        <input type="number" id="bobot_panen" placeholder="Contoh: 110" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                    </div>
                </div>

                <!-- INPUT PAKAN -->
                <div>
                    <label for="total_pakan" class="flex items-center text-sm font-medium mb-1">Total Pakan Dihabiskan</label>
                    <input type="number" id="total_pakan" placeholder="Contoh: 120" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                </div>

                <hr class="border-slate-700">

                <!-- KELOMPOK JUMLAH IKAN -->
                <div>
                    <label for="jumlah_bibit_awal" class="flex items-center text-sm font-medium mb-1">Jumlah Bibit Awal (ekor)</label>
                    <input type="number" id="jumlah_bibit_awal" placeholder="Contoh: 1000" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                </div>
                <div>
                    <label for="jumlah_ikan_panen" class="flex items-center text-sm font-medium mb-1">Jumlah Ikan Panen (ekor)</label>
                    <input type="number" id="jumlah_ikan_panen" placeholder="Contoh: 950" class="mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                </div>
            </div>
            <button id="calculate-btn" class="main-button mt-8 w-full bg-indigo-600 text-white font-bold py-3 px-4 rounded-lg hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-all duration-200 transform hover:scale-105">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z" /></svg>
                <span>Hitung Analisis Panen</span>
            </button>
        </div>

        <!-- Kolom Hasil -->
        <div id="result-container" class="space-y-8" style="display: none;">
            <div class="card">
                <h2 class="text-2xl font-bold mb-4 border-b border-slate-700 pb-4 flex items-center gap-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-indigo-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" /></svg>
                    Hasil Analisis
                </h2>
                <div class="mt-4 space-y-2">
                    <div class="result-item">
                        <span>Pertambahan Bobot</span>
                        <span id="hasil-pertambahan-bobot" class="font-bold text-lg"></span>
                    </div>
                    <div class="result-item">
                        <span>Rasio Konversi Pakan (FCR)</span>
                        <span id="hasil-fcr" class="font-bold text-lg"></span>
                    </div>
                    <div class="result-item">
                        <span>Efisiensi Pakan (EP)</span>
                        <span id="hasil-ep" class="font-bold text-lg"></span>
                    </div>
                    <div class="result-item">
                        <span>Survival Rate (SR)</span>
                        <span id="hasil-sr" class="font-bold text-lg"></span>
                    </div>
                    <div class="result-item">
                        <span>Specific Growth Rate (SGR)</span>
                        <span id="hasil-sgr" class="font-bold text-lg"></span>
                    </div>
                    <div class="result-item">
                        <span>Pertumbuhan Rata-rata</span>
                        <span id="hasil-pertumbuhan-rata" class="font-bold text-lg"></span>
                    </div>
                    <div class="result-item">
                        <span>Bobot Rata-rata Panen</span>
                        <span id="hasil-bobot-rata-panen" class="font-bold text-lg"></span>
                    </div>
                    <div class="result-item">
                        <span>Pertumbuhan Harian (ADG)</span>
                        <span id="hasil-adg" class="font-bold text-lg"></span>
                    </div>
                </div>
                <div id="status-fcr" class="mt-6 text-center"></div>
                <div id="status-sr" class="mt-2 text-center"></div>
            </div>

            <div class="card">
                 <h2 class="text-2xl font-bold mb-4 border-b border-slate-700 pb-4 flex items-center gap-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-indigo-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
                    Rekomendasi & Perencanaan
                </h2>
                <!-- Rekomendasi Pakan SNI -->
                <div id="rekomendasi-pakan-container" class="bg-slate-800/50 p-4 rounded-lg">
                    <p class="text-lg font-semibold text-slate-200">Rekomendasi Pakan Harian (SNI)</p>
                    <div id="recommendation-output" class="mt-2 space-y-1 text-sm">
                        <p>Bobot Rata-rata Ikan: <span id="rekomendasi-bobot-rata" class="font-bold"></span></p>
                        <p>Persentase Pakan: <span id="rekomendasi-persentase" class="font-bold"></span> dari biomassa</p>
                        <p>Jumlah Pakan Harian: <span id="rekomendasi-jumlah-pakan" class="font-bold"></span></p>
                    </div>
                </div>
                <!-- Perencanaan Pakan -->
                <div class="mt-6">
                    <label for="target_fcr" class="block text-sm font-medium mb-1">Perencanaan Target FCR (setelah panen)</label>
                    <div class="flex space-x-2 mt-1">
                        <input type="number" id="target_fcr" value="1.2" step="0.1" class="block w-full px-3 py-2 rounded-md shadow-sm">
                        <button id="plan-btn" class="px-4 py-2 bg-slate-600 text-white font-semibold rounded-lg hover:bg-slate-700 transition-colors">Rencanakan</button>
                    </div>
                </div>
                <div id="planning-result" class="mt-4 text-center text-slate-300 bg-slate-800/50 p-4 rounded-lg" style="display: none;"></div>
            </div>
        </div>
    </div>
    <div id="error-message" class="mt-6 text-center text-red-400 font-semibold p-4 bg-red-500/10 rounded-lg" style="display: none;"></div>
    <footer class="text-center mt-12 text-sm text-slate-500">
        <p>&copy; 2025 Smart Akuakultur Sistem by Tegar.</p>
        <p class="mt-1">Kontak: <a href="mailto:tegarraihan211204@gmail.com" class="text-indigo-400 hover:underline">tegarraihan211204@gmail.com</a></p>
    </footer>
</div>

<script>
// --- SCRIPT UNTUK BACKGROUND PERIKANAN INTERAKTIF ---
const canvas = document.getElementById('fishery-bg');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let fishArray = [];
let ripplesArray = [];

const mouse = {
    x: null,
    y: null
};

canvas.addEventListener('mousemove', function(event) {
    mouse.x = event.x;
    mouse.y = event.y;
    if (Math.random() > 0.9) {
        ripplesArray.push(new Ripple(mouse.x, mouse.y));
    }
});
canvas.addEventListener('click', function(event) {
    mouse.x = event.x;
    mouse.y = event.y;
    for (let i = 0; i < 5; i++) {
         ripplesArray.push(new Ripple(mouse.x, mouse.y));
    }
});


class Ripple {
    constructor(x, y) {
        this.x = x;
        this.y = y;
        this.radius = Math.random() * 5 + 1;
        this.maxRadius = Math.random() * 20 + 30;
        this.opacity = 1;
        this.speed = Math.random() * 0.5 + 0.2;
    }
    update() {
        this.radius += this.speed;
        if (this.radius > this.maxRadius) {
            this.opacity -= 0.05;
        }
    }
    draw() {
        ctx.strokeStyle = `rgba(199, 210, 254, ${this.opacity})`; // indigo-200
        ctx.lineWidth = 2;
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
        ctx.stroke();
    }
}

class Fish {
    constructor() {
        this.x = Math.random() * canvas.width;
        this.y = Math.random() * canvas.height;
        this.size = Math.random() * 5 + 8;
        this.speed = Math.random() * 1.5 + 0.5;
        this.angle = Math.random() * 2 * Math.PI;
        this.turnSpeed = Math.random() * 0.04 - 0.02;
        this.color = `hsla(200, 100%, ${Math.random() * 30 + 50}%, 0.6)`;
    }
    update() {
        this.angle += this.turnSpeed;
        this.x += this.speed * Math.cos(this.angle);
        this.y += this.speed * Math.sin(this.angle);

        if (this.x < -this.size) this.x = canvas.width + this.size;
        if (this.x > canvas.width + this.size) this.x = -this.size;
        if (this.y < -this.size) this.y = canvas.height + this.size;
        if (this.y > canvas.height + this.size) this.y = -this.size;
    }
    draw() {
        ctx.save();
        ctx.translate(this.x, this.y);
        ctx.rotate(this.angle);
        ctx.fillStyle = this.color;
        ctx.beginPath();
        ctx.moveTo(0, 0);
        ctx.quadraticCurveTo(this.size * 0.5, this.size * 0.4, this.size, 0);
        ctx.quadraticCurveTo(this.size * 0.5, -this.size * 0.4, 0, 0);
        ctx.moveTo(-this.size * 0.2, 0);
        ctx.lineTo(-this.size * 0.4, -this.size * 0.2);
        ctx.lineTo(-this.size * 0.4, this.size * 0.2);
        ctx.closePath();
        ctx.fill();
        ctx.restore();
    }
}

function init() {
    fishArray = [];
    let numberOfFish = 25;
    for (let i = 0; i < numberOfFish; i++) {
        fishArray.push(new Fish());
    }
}

function animate() {
    const gradient = ctx.createLinearGradient(0, 0, 0, canvas.height);
    gradient.addColorStop(0, '#1e3a8a');
    gradient.addColorStop(1, '#0c4a6e');
    ctx.fillStyle = gradient;
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    ripplesArray.forEach((ripple, index) => {
        ripple.update();
        ripple.draw();
        if (ripple.opacity <= 0) {
            ripplesArray.splice(index, 1);
        }
    });
    fishArray.forEach(fish => {
        fish.update();
        fish.draw();
    });
    requestAnimationFrame(animate);
}

window.addEventListener('resize', function() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    init();
});

init();
animate();


// --- SCRIPT UNTUK LOGIKA KALKULATOR ---
document.addEventListener('DOMContentLoaded', () => {

    const sniData = {
        lele: { name: 'Lele', ranges: [{ limit: 5, min: 7, max: 7 },{ limit: 15, min: 5, max: 5 },{ limit: 50, min: 4, max: 4 },{ limit: 100, min: 3, max: 3 },{ limit: Infinity, min: 2, max: 2 }] },
        nila: { name: 'Nila', ranges: [{ limit: 5, min: 5, max: 7 },{ limit: 20, min: 4, max: 6 },{ limit: 100, min: 3, max: 4 },{ limit: Infinity, min: 2, max: 3 }] },
        gurame: { name: 'Gurame', ranges: [{ limit: 25, min: 5, max: 7 },{ limit: 150, min: 3, max: 4 },{ limit: 500, min: 2, max: 3 },{ limit: Infinity, min: 1, max: 2 }] },
        mas: { name: 'Ikan Mas', ranges: [{ limit: 20, min: 5, max: 5 },{ limit: 100, min: 4, max: 4 },{ limit: Infinity, min: 3, max: 3 }] },
        patin: { name: 'Patin', ranges: [{ limit: 15, min: 5, max: 8 },{ limit: 100, min: 3, max: 5 },{ limit: 500, min: 2, max: 3 },{ limit: Infinity, min: 1, max: 2 }] },
        bawal: { name: 'Bawal', ranges: [{ limit: 20, min: 4, max: 6 },{ limit: 100, min: 3, max: 5 },{ limit: 300, min: 2, max: 4 },{ limit: Infinity, min: 1, max: 3 }] }
    };

    const elements = {
        calculateBtn: document.getElementById('calculate-btn'),
        planBtn: document.getElementById('plan-btn'),
        resultContainer: document.getElementById('result-container'),
        errorMessage: document.getElementById('error-message'),
        planningResultEl: document.getElementById('planning-result'),
        inputs: {
            fishType: document.getElementById('fish_type'),
            weightUnit: document.getElementById('weight_unit'),
            lamaBudidaya: document.getElementById('lama_budidaya'), 
            bobotAwalTebar: document.getElementById('bobot_awal_tebar'),
            bobotPanen: document.getElementById('bobot_panen'),
            totalPakan: document.getElementById('total_pakan'),
            jumlahBibitAwal: document.getElementById('jumlah_bibit_awal'),
            jumlahIkanPanen: document.getElementById('jumlah_ikan_panen'),
            targetFcr: document.getElementById('target_fcr'),
            bobotAwalType: document.getElementById('bobot_awal_type'),
            bobotPanenType: document.getElementById('bobot_panen_type'),
        },
        labels: {
            bobotAwal: document.getElementById('label_bobot_awal'),
            bobotPanen: document.getElementById('label_bobot_panen'),
        },
        outputs: {
            pertambahanBobot: document.getElementById('hasil-pertambahan-bobot'),
            fcr: document.getElementById('hasil-fcr'),
            ep: document.getElementById('hasil-ep'),
            sr: document.getElementById('hasil-sr'),
            sgr: document.getElementById('hasil-sgr'),
            pertumbuhanRata: document.getElementById('hasil-pertumbuhan-rata'),
            bobotRataPanen: document.getElementById('hasil-bobot-rata-panen'),
            adg: document.getElementById('hasil-adg'),
        }
    };
    const appState = { 
        pertambahanBobot: 0,
        totalPakan: 0,
        unit: 'kg'
    };
    
    function updateInputLabels() {
        const unit = elements.inputs.weightUnit.value;
        
        if (elements.inputs.bobotAwalType.value === 'total') {
            elements.labels.bobotAwal.textContent = `Total Bobot Awal (${unit})`;
            elements.inputs.bobotAwalTebar.placeholder = `Contoh: 10`;
        } else {
            elements.labels.bobotAwal.textContent = 'Rata-rata Bobot Awal (g/ekor)';
            elements.inputs.bobotAwalTebar.placeholder = `Contoh: 7`;
        }
        
        if (elements.inputs.bobotPanenType.value === 'total') {
            elements.labels.bobotPanen.textContent = `Total Bobot Panen (${unit})`;
            elements.inputs.bobotPanen.placeholder = `Contoh: 110`;
        } else {
            elements.labels.bobotPanen.textContent = 'Rata-rata Bobot Panen (g/ekor)';
            elements.inputs.bobotPanen.placeholder = `Contoh: 120`;
        }
    }

    const handleCalculation = () => {
        elements.errorMessage.style.display = 'none';
        
        const unit = elements.inputs.weightUnit.value;
        const fishType = elements.inputs.fishType.value;
        const conversionFactor = unit === 'kg' ? 1000 : 1;

        const inputs = {
            lamaBudidaya: parseInt(elements.inputs.lamaBudidaya.value),
            bobotAwal: parseFloat(elements.inputs.bobotAwalTebar.value),
            totalPakan: parseFloat(elements.inputs.totalPakan.value),
            bobotPanen: parseFloat(elements.inputs.bobotPanen.value),
            jumlahBibitAwal: parseInt(elements.inputs.jumlahBibitAwal.value),
            jumlahIkanPanen: parseInt(elements.inputs.jumlahIkanPanen.value),
            bobotAwalType: elements.inputs.bobotAwalType.value,
            bobotPanenType: elements.inputs.bobotPanenType.value,
        };
        
        const validationError = validateInputs(inputs);
        if (validationError) {
            elements.errorMessage.textContent = `Error: ${validationError}`;
            elements.errorMessage.style.display = 'block';
            return;
        }

        let totalBobotAwalGrams = inputs.bobotAwalType === 'total' ? inputs.bobotAwal * conversionFactor : inputs.bobotAwal * inputs.jumlahBibitAwal;
        let totalBobotPanenGrams = inputs.bobotPanenType === 'total' ? inputs.bobotPanen * conversionFactor : inputs.bobotPanen * inputs.jumlahIkanPanen;
        let totalPakanGrams = inputs.totalPakan * conversionFactor;

        const inputsInGrams = {
            bobotAwal: totalBobotAwalGrams,
            totalPakan: totalPakanGrams,
            bobotPanen: totalBobotPanenGrams,
        };

        const results = calculateMetrics(inputsInGrams, inputs.jumlahBibitAwal, inputs.jumlahIkanPanen, inputs.lamaBudidaya);
        
        appState.pertambahanBobot = results.pertambahanBobot;
        appState.totalPakan = inputsInGrams.totalPakan;
        appState.unit = unit;
        
        updateUI(results, unit, inputsInGrams.bobotPanen, inputs.jumlahIkanPanen, fishType);
    };

    const validateInputs=(i)=>{if(Object.values(i).some(val => typeof val === 'number' && isNaN(val)))return"Semua kolom harus diisi angka.";if(i.totalPakan<=0||i.jumlahBibitAwal<=0||i.lamaBudidaya<=0)return"Pakan, bibit awal, dan lama budidaya harus > 0.";if(i.jumlahIkanPanen > i.jumlahBibitAwal)return"Ikan panen tidak boleh > bibit awal.";return null;};
    
    const calculateMetrics=(weightInputs, bibitAwal, ikanPanen, lamaBudidaya)=>{
        const pB = weightInputs.bobotPanen - weightInputs.bobotAwal;
        const fcr = pB > 0 ? weightInputs.totalPakan / pB : 0;
        const ep = weightInputs.totalPakan > 0 ? (pB / weightInputs.totalPakan) * 100 : 0;
        const sr = (ikanPanen / bibitAwal) * 100;
        const w1 = weightInputs.bobotAwal / bibitAwal; 
        const w2 = weightInputs.bobotPanen / ikanPanen;
        let sgr = 0;
        if (w1 > 0 && w2 > 0 && lamaBudidaya > 0) sgr = ((Math.log(w2) - Math.log(w1)) / lamaBudidaya) * 100;
        const pertumbuhanRata = ikanPanen > 0 ? pB / ikanPanen : 0;
        let adg = 0;
        if (lamaBudidaya > 0) adg = (w2 - w1) / lamaBudidaya;
        return { pertambahanBobot: pB, fcr, ep, sr, sgr, pertumbuhanRata, adg, bobotRataPanen: w2 };
    };

    const displayStatus=(el,t,bg,c)=>{el.innerHTML=`<span class="status-badge" style="background-color:${bg};color:${c};">${t}</span>`;};
    
    const updateUI=(r, unit, totalBiomassInGrams, fishCount, fishType)=>{
        let displayWeight = r.pertambahanBobot;
        let displayPertumbuhanRata = r.pertumbuhanRata;
        if (unit === 'kg') {
            displayWeight /= 1000;
            displayPertumbuhanRata /= 1000;
        }

        elements.outputs.pertambahanBobot.textContent = `${displayWeight.toFixed(2)} ${unit}`;
        elements.outputs.fcr.textContent = r.fcr.toFixed(2);
        elements.outputs.ep.textContent = `${r.ep.toFixed(2)} %`;
        elements.outputs.sr.textContent = `${r.sr.toFixed(2)} %`;
        elements.outputs.sgr.textContent = `${r.sgr.toFixed(2)} %/hari`;
        elements.outputs.pertumbuhanRata.textContent = `${displayPertumbuhanRata.toFixed(2)} ${unit}/ekor`;
        elements.outputs.bobotRataPanen.textContent = `${r.bobotRataPanen.toFixed(2)} g/ekor`;
        elements.outputs.adg.textContent = `${r.adg.toFixed(2)} g/ekor/hari`;
        
        const avgWeightInGrams = totalBiomassInGrams / fishCount;
        const selectedSni = sniData[fishType];
        let feedPercentMin, feedPercentMax, percentText;

        for (const range of selectedSni.ranges) {
            if (avgWeightInGrams < range.limit) {
                feedPercentMin = range.min;
                feedPercentMax = range.max;
                percentText = (feedPercentMin === feedPercentMax) ? `${feedPercentMin}%` : `${range.min}% - ${range.max}%`;
                break;
            }
        }

        const minFeed = totalBiomassInGrams * (feedPercentMin / 100);
        const maxFeed = totalBiomassInGrams * (feedPercentMax / 100);
        
        let displayMinFeed = minFeed;
        let displayMaxFeed = maxFeed;
        if (unit === 'kg') {
            displayMinFeed /= 1000;
            displayMaxFeed /= 1000;
        }

        document.getElementById('rekomendasi-bobot-rata').textContent = `${avgWeightInGrams.toFixed(2)} g/ekor`;
        document.getElementById('rekomendasi-persentase').textContent = percentText;
        document.getElementById('rekomendasi-jumlah-pakan').textContent = `${displayMinFeed.toFixed(2)} - ${displayMaxFeed.toFixed(2)} ${unit}/hari`;
        
        const statusFcrEl = document.getElementById('status-fcr');
        const statusSrEl = document.getElementById('status-sr');
        if (statusFcrEl) statusFcrEl.innerHTML = '';
        if (statusSrEl) statusSrEl.innerHTML = '';

        if(r.fcr>0&&r.fcr<1.0)displayStatus(statusFcrEl,'🟢 FCR Sangat Efisien','#dcfce7','#166534');
        else if(r.fcr<=1.2)displayStatus(statusFcrEl,'🔵 FCR Efisien','#dbeafe','#1e40af');
        else if(r.fcr<=1.5)displayStatus(statusFcrEl,'🟡 FCR Cukup Efisien','#fef9c3','#854d0e');
        else displayStatus(statusFcrEl,'🔴 FCR Kurang Efisien','#fee2e2','#991b1b');
        
        if(r.sr>=80)displayStatus(statusSrEl,'✅ SR Berhasil (di atas 80%)','#dcfce7','#166534');
        else displayStatus(statusSrEl,'⚠️ SR Perlu Evaluasi (di bawah 80%)','#fef9c3','#854d0e');
        
        elements.resultContainer.style.display='block';
    };

    const handlePlanning=()=>{
        const tFcr=parseFloat(elements.inputs.targetFcr.value);
        if(isNaN(tFcr)||tFcr<=0||appState.pertambahanBobot<=0){
            elements.planningResultEl.innerHTML=`<p class="text-red-400">Hitung analisis terlebih dahulu.</p>`;
            elements.planningResultEl.style.display='block';
            return;
        }
        
        const unit = appState.unit;
        const pakanIdealInGrams = appState.pertambahanBobot * tFcr;
        const selisihPakanInGrams = appState.totalPakan - pakanIdealInGrams;
        let displayPakanIdeal = pakanIdealInGrams;
        let displaySelisih = selisihPakanInGrams;
        if (unit === 'kg') {
            displayPakanIdeal /= 1000;
            displaySelisih /= 1000;
        }

        let resHTML=`<p>Dengan target FCR <strong>${tFcr.toFixed(2)}</strong>, pakan idealnya <strong>${displayPakanIdeal.toFixed(2)} ${unit}</strong>.</p>`;
        if(displaySelisih > 0.01) resHTML+=`<p class="mt-2 font-semibold text-green-400">Anda berpotensi HEMAT pakan ${displaySelisih.toFixed(2)} ${unit}.</p>`;
        else if(displaySelisih < -0.01) {
            const fcrSaatIni=appState.totalPakan/appState.pertambahanBobot;
            resHTML+=`<p class="mt-2 font-semibold text-blue-400">FCR Anda (${fcrSaatIni.toFixed(2)}) sudah lebih baik dari target.</p>`;
        } else resHTML+=`<p class="mt-2 font-semibold">Target FCR sama dengan capaian.</p>`;
        
        elements.planningResultEl.innerHTML=resHTML;
        elements.planningResultEl.style.display='block';
    };

    elements.inputs.bobotAwalType.addEventListener('change', updateInputLabels);
    elements.inputs.bobotPanenType.addEventListener('change', updateInputLabels);
    elements.inputs.weightUnit.addEventListener('change', updateInputLabels);
    elements.calculateBtn.addEventListener('click', handleCalculation);
    elements.planBtn.addEventListener('click', handlePlanning);
    
    // Panggil sekali di awal untuk inisialisasi
    updateInputLabels();
});
</script>

</body>
</html>
