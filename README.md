<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kalkulator Analisis Panen</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Gaya tambahan untuk UI yang lebih baik */
        body { 
            background-color: #f1f5f9; 
            font-family: 'Inter', sans-serif; 
        }
        .card { 
            background-color: white; 
            border-radius: 0.75rem; 
            padding: 2rem; 
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1); 
            transition: transform 0.2s ease-in-out;
        }
        .card:hover {
            transform: translateY(-5px);
        }
        .result-item { 
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
            padding: 0.75rem 0; 
            border-bottom: 1px solid #e5e7eb; 
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
        /* Style untuk notifikasi */
        #notification { 
            position: fixed; 
            bottom: -100px; /* Mulai dari luar layar */
            left: 50%; 
            transform: translateX(-50%); 
            padding: 12px 24px; 
            border-radius: 8px; 
            color: white; 
            font-weight: bold; 
            z-index: 1000; 
            opacity: 0; 
            transition: opacity 0.5s, bottom 0.5s; 
        }
        #notification.show { 
            opacity: 1; 
            bottom: 20px; /* Muncul ke dalam layar */
        }
    </style>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
</head>
<body class="p-4 md:p-8">
<div class="max-w-6xl mx-auto">
    <h1 class="text-4xl font-extrabold text-center text-slate-800 mb-8">Kalkulator Analisis & Perencanaan Panen</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <!-- Kolom Input -->
        <div class="card">
            <h2 class="text-2xl font-bold text-gray-700 mb-6 border-b pb-3">Data Siklus Panen</h2>
            <div class="space-y-4">
                <div>
                    <label for="bobot_awal_tebar" class="block text-sm font-medium text-gray-700">Total Bobot Awal (kg)</label>
                    <input type="number" id="bobot_awal_tebar" placeholder="Contoh: 10" class="mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                </div>
                <div>
                    <label for="total_pakan" class="block text-sm font-medium text-gray-700">Total Pakan Dihabiskan (kg)</label>
                    <input type="number" id="total_pakan" placeholder="Contoh: 120" class="mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                </div>
                <div>
                    <label for="bobot_panen" class="block text-sm font-medium text-gray-700">Total Bobot Panen (kg)</label>
                    <input type="number" id="bobot_panen" placeholder="Contoh: 110" class="mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                </div>
                <div>
                    <label for="jumlah_bibit_awal" class="block text-sm font-medium text-gray-700">Jumlah Bibit Awal (ekor)</label>
                    <input type="number" id="jumlah_bibit_awal" placeholder="Contoh: 1000" class="mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                </div>
                <div>
                    <label for="jumlah_ikan_panen" class="block text-sm font-medium text-gray-700">Jumlah Ikan Panen (ekor)</label>
                    <input type="number" id="jumlah_ikan_panen" placeholder="Contoh: 950" class="mt-1 block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                </div>
            </div>
            <button id="calculate-btn" class="mt-8 w-full bg-indigo-600 text-white font-bold py-3 px-4 rounded-lg hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-transform transform hover:scale-105 disabled:bg-indigo-400 disabled:cursor-not-allowed">
                Hitung & Simpan Analisis
            </button>
        </div>

        <!-- Kolom Hasil -->
        <div id="result-container" class="space-y-8" style="display: none;">
            <div class="card">
                <h2 class="text-2xl font-bold text-gray-700 mb-4 border-b pb-3">Hasil Analisis</h2>
                <div class="space-y-2">
                    <div class="result-item">
                        <span class="text-gray-600">Pertambahan Bobot</span>
                        <span id="hasil-pertambahan-bobot" class="font-bold text-lg text-gray-800"></span>
                    </div>
                    <div class="result-item">
                        <span class="text-gray-600">Rasio Konversi Pakan (FCR)</span>
                        <span id="hasil-fcr" class="font-bold text-lg text-gray-800"></span>
                    </div>
                    <div class="result-item">
                        <span class="text-gray-600">Efisiensi Pakan (EP)</span>
                        <span id="hasil-ep" class="font-bold text-lg text-gray-800"></span>
                    </div>
                    <div class="result-item">
                        <span class="text-gray-600">Survival Rate (SR)</span>
                        <span id="hasil-sr" class="font-bold text-lg text-gray-800"></span>
                    </div>
                </div>
                <div id="status-fcr" class="mt-4 text-center"></div>
                <div id="status-sr" class="mt-2 text-center"></div>
            </div>

            <div class="card">
                <h2 class="text-2xl font-bold text-gray-700 mb-4 border-b pb-3">Perencanaan Pakan</h2>
                <div>
                    <label for="target_fcr" class="block text-sm font-medium text-gray-700">Masukkan Target FCR Baru:</label>
                    <div class="flex space-x-2 mt-1">
                        <input type="number" id="target_fcr" value="1.2" step="0.1" class="block w-full px-3 py-2 bg-white border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500">
                        <button id="plan-btn" class="px-4 py-2 bg-gray-600 text-white font-semibold rounded-lg hover:bg-gray-700">Rencanakan</button>
                    </div>
                </div>
                <div id="planning-result" class="mt-4 text-center text-gray-700 bg-gray-50 p-4 rounded-lg" style="display: none;"></div>
            </div>
        </div>
    </div>
    <div id="error-message" class="mt-6 text-center text-red-600 font-semibold"></div>
    <!-- Elemen untuk Notifikasi -->
    <div id="notification"></div>
</div>

<script>
document.addEventListener('DOMContentLoaded', () => {

    // URL WEB APP ANDA SUDAH DIPERBARUI DI SINI
    const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbxYTVTySvme1I2dH1m8mmDtgmVwia9dAjd6ve0FsA2PQkQB-rThJG3XzcFxGis7D40k/exec';

    // KUMPULKAN SEMUA ELEMEN DOM
    const elements = {
        calculateBtn: document.getElementById('calculate-btn'),
        planBtn: document.getElementById('plan-btn'),
        resultContainer: document.getElementById('result-container'),
        errorMessage: document.getElementById('error-message'),
        notification: document.getElementById('notification'),
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
    
    // FUNGSI UNTUK NOTIFIKASI
    const showNotification = (message, isSuccess) => {
        elements.notification.textContent = message;
        elements.notification.style.backgroundColor = isSuccess ? '#22c55e' : '#ef4444';
        elements.notification.classList.add('show');
        setTimeout(() => {
            elements.notification.classList.remove('show');
        }, 3000);
    };

    /*
        CATATAN PENTING UNTUK INTEGRASI GOOGLE SHEET:
        Metode pengiriman data telah diubah agar lebih stabil.
        Anda juga HARUS memperbarui fungsi `doPost(e)` di Google Apps Script Anda.
        Hapus fungsi `doPost(e)` yang lama dan ganti dengan yang ini:

        function doPost(e) {
          try {
            var data = e.parameter;
            // Ganti "Sheet1" jika nama sheet Anda berbeda
            var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Sheet1"); 

            sheet.appendRow([
              new Date(),
              data.bobotAwal,
              data.totalPakan,
              data.bobotPanen,
              data.jumlahBibitAwal,
              data.jumlahIkanPanen,
              data.pertambahanBobot,
              data.fcr,
              data.ep,
              data.sr
            ]);
            
            return ContentService
              .createTextOutput(JSON.stringify({ "status": "sukses", "message": "Data berhasil disimpan!" }))
              .setMimeType(ContentService.MimeType.JSON);

          } catch (error) {
            return ContentService
              .createTextOutput(JSON.stringify({ "status": "gagal", "message": error.toString() }))
              .setMimeType(ContentService.MimeType.JSON);
          }
        }

        Setelah memperbarui script, jangan lupa untuk DEPLOY ULANG sebagai Web App.
    */
    // FUNGSI UNTUK MENGIRIM DATA KE GOOGLE SHEET (METODE BARU YANG LEBIH STABIL)
    const sendDataToGoogleSheet = async (inputs, results) => {
        const payload = { ...inputs, ...results };
        const formData = new FormData();
        for (const key in payload) {
            formData.append(key, payload[key]);
        }
        
        try {
            const response = await fetch(GOOGLE_SCRIPT_URL, {
                method: 'POST',
                mode: 'cors',
                body: new URLSearchParams(formData), // Kirim sebagai application/x-www-form-urlencoded
            });

            if (!response.ok) {
               throw new Error(`Network response was not ok. Status: ${response.status}`);
            }

            const result = await response.json();
            if (result.status === 'sukses') {
                showNotification('✅ Data berhasil tersimpan di Google Sheet!', true);
            } else {
                throw new Error(result.message || 'Eksekusi script gagal.');
            }
        } catch (error) {
            console.error('Error saat mengirim ke Google Sheet:', error);
            showNotification(`❌ Gagal menyimpan data. Error: ${error.message}`, false);
        }
    };

    // FUNGSI UTAMA KALKULASI
    const handleCalculation = async () => {
        // Reset pesan error dan nonaktifkan tombol untuk mencegah klik ganda
        elements.errorMessage.textContent = '';
        elements.calculateBtn.disabled = true;
        elements.calculateBtn.textContent = 'Memproses...';

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
            elements.calculateBtn.disabled = false;
            elements.calculateBtn.textContent = 'Hitung & Simpan Analisis';
            return;
        }

        // Lakukan kalkulasi
        const results = calculateMetrics(inputs);
        appState.pertambahanBobot = results.pertambahanBobot;
        appState.totalPakan = inputs.totalPakan;
        
        // Perbarui tampilan UI
        updateUI(results);

        // KIRIM DATA SETELAH KALKULASI BERHASIL
        await sendDataToGoogleSheet(inputs, results);

        // Aktifkan kembali tombol
        elements.calculateBtn.disabled = false;
        elements.calculateBtn.textContent = 'Hitung & Simpan Analisis';
    };

    // --- (Fungsi-fungsi pembantu lainnya) ---
    const validateInputs=(i)=>{if(Object.values(i).some(isNaN))return"Semua kolom harus diisi angka.";if(i.totalPakan<=0||i.jumlahBibitAwal<=0)return"Total pakan & bibit awal harus > 0.";if(i.bobotPanen<=i.bobotAwal)return"Bobot panen harus > bobot awal.";if(i.jumlahIkanPanen>i.jumlahBibitAwal)return"Ikan panen tidak boleh > bibit awal.";return null;};
    const calculateMetrics=(i)=>{const pB=i.bobotPanen-i.bobotAwal;const fcr=pB>0?i.totalPakan/pB:0;const ep=i.totalPakan>0?(pB/i.totalPakan)*100:0;const sr=(i.jumlahIkanPanen/i.jumlahBibitAwal)*100;return{pertambahanBobot:pB,fcr,ep,sr};};
    const displayStatus=(el,t,bg,c)=>{el.innerHTML=`<span class="status-badge" style="background-color:${bg};color:${c};">${t}</span>`;};
    const updateUI=(r)=>{elements.outputs.pertambahanBobot.textContent=`${r.pertambahanBobot.toFixed(2)} kg`;elements.outputs.fcr.textContent=r.fcr.toFixed(2);elements.outputs.ep.textContent=`${r.ep.toFixed(2)} %`;elements.outputs.sr.textContent=`${r.sr.toFixed(2)} %`;if(r.fcr>0&&r.fcr<1.0){displayStatus(elements.outputs.statusFcr,'🟢 FCR Sangat Efisien','#dcfce7','#166534');}else if(r.fcr<=1.2){displayStatus(elements.outputs.statusFcr,'🔵 FCR Efisien','#dbeafe','#1e40af');}else if(r.fcr<=1.5){displayStatus(elements.outputs.statusFcr,'🟡 FCR Cukup Efisien','#fef9c3','#854d0e');}else{displayStatus(elements.outputs.statusFcr,'🔴 FCR Kurang Efisien','#fee2e2','#991b1b');}if(r.sr>=80){displayStatus(elements.outputs.statusSr,'✅ SR Berhasil (di atas 80%)','#dcfce7','#166534');}else{displayStatus(elements.outputs.statusSr,'⚠️ SR Perlu Evaluasi (di bawah 80%)','#fef9c3','#854d0e');}elements.resultContainer.style.display='block';};
    const handlePlanning=()=>{const tFcr=parseFloat(elements.inputs.targetFcr.value);if(isNaN(tFcr)||tFcr<=0||appState.pertambahanBobot<=0){elements.planningResultEl.innerHTML=`<p class="text-red-600">Hitung analisis terlebih dahulu.</p>`;elements.planningResultEl.style.display='block';return;}const pI=appState.pertambahanBobot*tFcr;const sP=appState.totalPakan-pI;let resHTML=`<p>Dengan target FCR <strong>${tFcr.toFixed(2)}</strong>, pakan idealnya <strong>${pI.toFixed(2)} kg</strong>.</p>`;if(sP>0.01){resHTML+=`<p class="mt-2 font-semibold text-green-700">Anda berpotensi HEMAT pakan ${sP.toFixed(2)} kg.</p>`;}else if(sP<-0.01){const fcrSaatIni=appState.totalPakan/appState.pertambahanBobot;resHTML+=`<p class="mt-2 font-semibold text-blue-700">FCR Anda (${fcrSaatIni.toFixed(2)}) sudah lebih baik dari target.</p>`;}else{resHTML+=`<p class="mt-2 font-semibold">Target FCR sama dengan capaian.</p>`;}elements.planningResultEl.innerHTML=resHTML;elements.planningResultEl.style.display='block';};

    // Tambahkan event listener ke tombol
    elements.calculateBtn.addEventListener('click', handleCalculation);
    elements.planBtn.addEventListener('click', handlePlanning);
});
</script>

</body>
</html>
