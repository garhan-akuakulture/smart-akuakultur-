<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Akuakultur Sistem by Tegar</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Gaya tambahan untuk UI dan Background Interaktif */
        body { 
            font-family: 'Inter', sans-serif; 
            background-color: #0f172a; /* Warna dasar slate-900 */
            color: #f8fafc; /* Teks default terang */
        }
        #interactive-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1; /* Letakkan di belakang semua konten */
        }
        .card { 
            background-color: rgba(255, 255, 255, 0.05); /* Latar belakang semi-transparan */
            backdrop-filter: blur(10px); /* Efek blur untuk tampilan modern */
            -webkit-backdrop-filter: blur(10px);
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
        .status-badge { 
            display:inline-block; 
            padding: 0.5rem 1rem; 
            border-radius: 9999px; 
            font-weight: 600; 
            font-size: 0.875rem;
        }
        .input-icon {
            position: absolute;
            inset-y: 0;
            left: 0;
            display: flex;
            align-items: center;
            padding-left: 0.75rem; /* 12px */
            color: #94a3b8; /* slate-400 */
        }
        .main-button {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
        }
        /* Penyesuaian warna teks dan input untuk tema gelap */
        label { color: #cbd5e1; /* slate-300 */ }
        .card h2, .result-item span { color: #f1f5f9; /* slate-100 */ }
        .result-item span:first-child { color: #94a3b8; /* slate-400 */ }
        input {
            background-color: rgba(15, 23, 42, 0.5) !important; /* bg-slate-900/50 */
            border-color: #334155 !important; /* border-slate-700 */
            color: white !important;
        }
        input:focus {
            border-color: #6366f1 !important; /* focus:border-indigo-500 */
            --tw-ring-color: #6366f1 !important; /* focus:ring-indigo-500 */
        }
    </style>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
</head>
<body class="p-4 md:p-8">
<canvas id="interactive-bg"></canvas>
<div class="max-w-6xl mx-auto relative z-10">
    <div class="text-center mb-10">
        <h1 class="text-4xl md:text-5xl font-extrabold text-white">Smart Akuakultur Sistem</h1>
        <p class="text-lg text-slate-400 mt-2">by Tegar</p>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
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
                    <label for="bobot_awal_tebar" class="block text-sm font-medium mb-1">Total Bobot Awal (kg)</label>
                    <div class="relative">
                        <div class="input-icon">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M3 6l3 1m0 0l-3 9a5.002 5.002 0 006.001 0M6 7l3 9M6 7l6-2m6 2l3-1m-3 1l-3 9a5.002 5.002 0 006.001 0M18 7l3 9m-3-9l-6-2m0-2v2m0 16V5m0 16H9m3 0h3" /></svg>
                        </div>
                        <input type="number" id="bobot_awal_tebar" placeholder="Contoh: 10" class="pl-10 mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                    </div>
                </div>
                <div>
                    <label for="total_pakan" class="block text-sm font-medium mb-1">Total Pakan Dihabiskan (kg)</label>
                    <div class="relative">
                        <div class="input-icon">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" /></svg>
                        </div>
                        <input type="number" id="total_pakan" placeholder="Contoh: 120" class="pl-10 mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                    </div>
                </div>
                <div>
                    <label for="bobot_panen" class="block text-sm font-medium mb-1">Total Bobot Panen (kg)</label>
                    <div class="relative">
                        <div class="input-icon">
                           <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" /></svg>
                        </div>
                        <input type="number" id="bobot_panen" placeholder="Contoh: 110" class="pl-10 mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                    </div>
                </div>
                <div>
                    <label for="jumlah_bibit_awal" class="block text-sm font-medium mb-1">Jumlah Bibit Awal (ekor)</label>
                    <div class="relative">
                        <div class="input-icon">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z" /></svg>
                        </div>
                        <input type="number" id="jumlah_bibit_awal" placeholder="Contoh: 1000" class="pl-10 mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                    </div>
                </div>
                <div>
                    <label for="jumlah_ikan_panen" class="block text-sm font-medium mb-1">Jumlah Ikan Panen (ekor)</label>
                    <div class="relative">
                       <div class="input-icon">
                           <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M15 21v-1a6 6 0 00-1.781-4.121M12 4.354a4 4 0 000 5.292M3 15a4 4 0 014 4v1h4v-1a4 4 0 014-4h3m-4-6a4 4 0 014-4h3" /></svg>
                       </div>
                        <input type="number" id="jumlah_ikan_panen" placeholder="Contoh: 950" class="pl-10 mt-1 block w-full px-3 py-2 rounded-md shadow-sm">
                    </div>
                </div>
            </div>
            <button id="calculate-btn" class="main-button mt-8 w-full bg-indigo-600 text-white font-bold py-3 px-4 rounded-lg hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-all duration-200 transform hover:scale-105">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z" /></svg>
                <span>Hitung Analisis</span>
            </button>
        </div>

        <!-- Kolom Hasil -->
        <div id="result-container" class="space-y-8" style="display: none;">
            <div class="card">
                <h2 class="text-2xl font-bold mb-4 border-b border-slate-700 pb-4 flex items-center gap-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-indigo-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" /></svg>
                    Hasil Analisis
                </h2>
                <div class="space-y-2">
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
                </div>
                <div id="status-fcr" class="mt-6 text-center"></div>
                <div id="status-sr" class="mt-2 text-center"></div>
            </div>

            <div class="card">
                 <h2 class="text-2xl font-bold mb-4 border-b border-slate-700 pb-4 flex items-center gap-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-indigo-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z" /></svg>
                    Perencanaan Pakan
                </h2>
                <div>
                    <label for="target_fcr" class="block text-sm font-medium mb-1">Masukkan Target FCR Baru:</label>
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
    </footer>
</div>

<script>
// --- SCRIPT UNTUK BACKGROUND INTERAKTIF ---
const canvas = document.getElementById('interactive-bg');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particlesArray;

// Posisi mouse
const mouse = {
    x: null,
    y: null,
    radius: (canvas.height/110) * (canvas.width/110)
}

window.addEventListener('mousemove', 
    function(event) {
        mouse.x = event.x;
        mouse.y = event.y;
    }
);

// Class untuk membuat satu partikel
class Particle {
    constructor(x, y, directionX, directionY, size, color) {
        this.x = x;
        this.y = y;
        this.directionX = directionX;
        this.directionY = directionY;
        this.size = size;
        this.color = color;
    }
    // Menggambar partikel
    draw() {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2, false);
        ctx.fillStyle = 'rgba(165, 180, 252, 0.5)'; // Warna indigo-300 dengan transparansi
        ctx.fill();
    }
    // Memperbarui posisi partikel
    update() {
        if (this.x > canvas.width || this.x < 0) {
            this.directionX = -this.directionX;
        }
        if (this.y > canvas.height || this.y < 0) {
            this.directionY = -this.directionY;
        }

        // Cek deteksi tabrakan dengan mouse
        let dx = mouse.x - this.x;
        let dy = mouse.y - this.y;
        let distance = Math.sqrt(dx*dx + dy*dy);
        if (distance < mouse.radius + this.size){
            if (mouse.x < this.x && this.x < canvas.width - this.size * 10) {
                this.x += 5;
            }
            if (mouse.x > this.x && this.x > this.size * 10) {
                this.x -= 5;
            }
            if (mouse.y < this.y && this.y < canvas.height - this.size * 10) {
                this.y += 5;
            }
            if (mouse.y > this.y && this.y > this.size * 10) {
                this.y -= 5;
            }
        }
        // Gerakkan partikel
        this.x += this.directionX;
        this.y += this.directionY;
        // Gambar partikel
        this.draw();
    }
}

// Membuat array partikel
function init() {
    particlesArray = [];
    let numberOfParticles = (canvas.height * canvas.width) / 9000;
    for (let i = 0; i < numberOfParticles; i++) {
        let size = (Math.random() * 2) + 1;
        let x = (Math.random() * ((innerWidth - size * 2) - (size * 2)) + size * 2);
        let y = (Math.random() * ((innerHeight - size * 2) - (size * 2)) + size * 2);
        let directionX = (Math.random() * .4) - 0.2;
        let directionY = (Math.random() * .4) - 0.2;
        let color = '#818cf8';

        particlesArray.push(new Particle(x, y, directionX, directionY, size, color));
    }
}

// Membuat koneksi antar partikel
function connect() {
    let opacityValue = 1;
    for (let a = 0; a < particlesArray.length; a++) {
        for (let b = a; b < particlesArray.length; b++) {
            let distance = ((particlesArray[a].x - particlesArray[b].x) * (particlesArray[a].x - particlesArray[b].x))
            + ((particlesArray[a].y - particlesArray[b].y) * (particlesArray[a].y - particlesArray[b].y));
            if (distance < (canvas.width/7) * (canvas.height/7)) {
                opacityValue = 1 - (distance/20000);
                ctx.strokeStyle = 'rgba(199, 210, 254,' + opacityValue + ')'; // Warna indigo-200
                ctx.lineWidth = 1;
                ctx.beginPath();
                ctx.moveTo(particlesArray[a].x, particlesArray[a].y);
                ctx.lineTo(particlesArray[b].x, particlesArray[b].y);
                ctx.stroke();
            }
        }
    }
}

// Loop animasi
function animate() {
    requestAnimationFrame(animate);
    ctx.clearRect(0,0,innerWidth, innerHeight);

    for (let i = 0; i < particlesArray.length; i++) {
        particlesArray[i].update();
    }
    connect();
}

// Event listener untuk resize window
window.addEventListener('resize',
    function(){
        canvas.width = innerWidth;
        canvas.height = innerHeight;
        mouse.radius = ((canvas.height/110) * (canvas.width/110));
        init();
    }
);

// Event listener untuk mouse out
window.addEventListener('mouseout', 
    function(){
        mouse.x = undefined;
        mouse.y = undefined;
    }
)

init();
animate();


// --- SCRIPT UNTUK LOGIKA KALKULATOR ---
document.addEventListener('DOMContentLoaded', () => {

    // KUMPULKAN SEMUA ELEMEN DOM
    const elements = {
        calculateBtn: document.getElementById('calculate-btn'),
        planBtn: document.getElementById('plan-btn'),
        resultContainer: document.getElementById('result-container'),
        errorMessage: document.getElementById('error-message'),
        planningResultEl: document.getElementById('planning-result'),
        inputs: {
            bobotAwal: document.getElementById('bobot_awal_tebar'),
            totalPakan: document.getElementById('total_pakan'),
            bobotPanen: document.getElementById('bobot_panen'),
            jumlahBibitAwal: document.getElementById('jumlah_bibit_awal'),
            jumlahIkanPanen: document.getElementById('jumlah_ikan_panen'),
            targetFcr: document.getElementById('target_fcr'),
        },
        outputs: {
            pertambahanBobot: document.getElementById('hasil-pertambahan-bobot'),
            fcr: document.getElementById('hasil-fcr'),
            ep: document.getElementById('hasil-ep'),
            sr: document.getElementById('hasil-sr'),
            statusFcr: document.getElementById('status-fcr'),
            statusSr: document.getElementById('status-sr'),
        }
    };
    const appState = { pertambahanBobot: 0, totalPakan: 0 };
    
    // FUNGSI UTAMA KALKULASI
    const handleCalculation = () => {
        // Reset pesan error
        elements.errorMessage.style.display = 'none';
        elements.errorMessage.textContent = '';
        
        const inputs = {
            bobotAwal: parseFloat(elements.inputs.bobotAwal.value),
            totalPakan: parseFloat(elements.inputs.totalPakan.value),
            bobotPanen: parseFloat(elements.inputs.bobotPanen.value),
            jumlahBibitAwal: parseInt(elements.inputs.jumlahBibitAwal.value),
            jumlahIkanPanen: parseInt(elements.inputs.jumlahIkanPanen.value),
        };
        
        // Validasi input
        const validationError = validateInputs(inputs);
        if (validationError) {
            elements.errorMessage.textContent = `Error: ${validationError}`;
            elements.errorMessage.style.display = 'block';
            return;
        }

        // Lakukan kalkulasi
        const results = calculateMetrics(inputs);
        appState.pertambahanBobot = results.pertambahanBobot;
        appState.totalPakan = inputs.totalPakan;
        
        // Perbarui tampilan UI
        updateUI(results);
    };

    // --- (Fungsi-fungsi pembantu lainnya) ---
    const validateInputs=(i)=>{if(Object.values(i).some(isNaN))return"Semua kolom harus diisi angka.";if(i.totalPakan<=0||i.jumlahBibitAwal<=0)return"Total pakan & bibit awal harus > 0.";if(i.bobotPanen<=i.bobotAwal)return"Bobot panen harus > bobot awal.";if(i.jumlahIkanPanen>i.jumlahBibitAwal)return"Ikan panen tidak boleh > bibit awal.";return null;};
    const calculateMetrics=(i)=>{const pB=i.bobotPanen-i.bobotAwal;const fcr=pB>0?i.totalPakan/pB:0;const ep=i.totalPakan>0?(pB/i.totalPakan)*100:0;const sr=(i.jumlahIkanPanen/i.jumlahBibitAwal)*100;return{pertambahanBobot:pB,fcr,ep,sr};};
    const displayStatus=(el,t,bg,c)=>{el.innerHTML=`<span class="status-badge" style="background-color:${bg};color:${c};">${t}</span>`;};
    const updateUI=(r)=>{elements.outputs.pertambahanBobot.textContent=`${r.pertambahanBobot.toFixed(2)} kg`;elements.outputs.fcr.textContent=r.fcr.toFixed(2);elements.outputs.ep.textContent=`${r.ep.toFixed(2)} %`;elements.outputs.sr.textContent=`${r.sr.toFixed(2)} %`;if(r.fcr>0&&r.fcr<1.0){displayStatus(elements.outputs.statusFcr,'🟢 FCR Sangat Efisien','#dcfce7','#166534');}else if(r.fcr<=1.2){displayStatus(elements.outputs.statusFcr,'🔵 FCR Efisien','#dbeafe','#1e40af');}else if(r.fcr<=1.5){displayStatus(elements.outputs.statusFcr,'🟡 FCR Cukup Efisien','#fef9c3','#854d0e');}else{displayStatus(elements.outputs.statusFcr,'🔴 FCR Kurang Efisien','#fee2e2','#991b1b');}if(r.sr>=80){displayStatus(elements.outputs.statusSr,'✅ SR Berhasil (di atas 80%)','#dcfce7','#166534');}else{displayStatus(elements.outputs.statusSr,'⚠️ SR Perlu Evaluasi (di bawah 80%)','#fef9c3','#854d0e');}elements.resultContainer.style.display='block';};
    const handlePlanning=()=>{const tFcr=parseFloat(elements.inputs.targetFcr.value);if(isNaN(tFcr)||tFcr<=0||appState.pertambahanBobot<=0){elements.planningResultEl.innerHTML=`<p class="text-red-400">Hitung analisis terlebih dahulu.</p>`;elements.planningResultEl.style.display='block';return;}const pI=appState.pertambahanBobot*tFcr;const sP=appState.totalPakan-pI;let resHTML=`<p>Dengan target FCR <strong>${tFcr.toFixed(2)}</strong>, pakan idealnya <strong>${pI.toFixed(2)} kg</strong>.</p>`;if(sP>0.01){resHTML+=`<p class="mt-2 font-semibold text-green-400">Anda berpotensi HEMAT pakan ${sP.toFixed(2)} kg.</p>`;}else if(sP<-0.01){const fcrSaatIni=appState.totalPakan/appState.pertambahanBobot;resHTML+=`<p class="mt-2 font-semibold text-blue-400">FCR Anda (${fcrSaatIni.toFixed(2)}) sudah lebih baik dari target.</p>`;}else{resHTML+=`<p class="mt-2 font-semibold">Target FCR sama dengan capaian.</p>`;}elements.planningResultEl.innerHTML=resHTML;elements.planningResultEl.style.display='block';};

    // Tambahkan event listener ke tombol
    elements.calculateBtn.addEventListener('click', handleCalculation);
    elements.planBtn.addEventListener('click', handlePlanning);
});
</script>

</body>
</html>
