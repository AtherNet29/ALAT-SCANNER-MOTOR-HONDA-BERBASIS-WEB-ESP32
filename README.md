<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Scanner Motor Honda - README</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            line-height: 1.6;
            color: #24292e;
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
            background-color: #ffffff;
        }
        hr {
            border: 0;
            height: 1px;
            background-image: linear-gradient(to right, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.75), rgba(0, 0, 0, 0));
            margin: 30px 0;
        }
        table {
            border-collapse: collapse;
            width: 100%;
            margin-bottom: 20px;
        }
        th, td {
            border: 1px solid #dfe2e5;
            padding: 8px 12px;
            text-align: left;
        }
        th {
            background-color: #f6f8fa;
            font-weight: 600;
        }
        .text-center {
            text-align: center;
        }
        .info-box {
            background-color: #e6f3ff;
            padding: 15px;
            border-left: 5px solid #0055aa;
            margin: 20px 0;
        }
        .warning-box {
            background-color: #ffcccc;
            padding: 15px;
            border-left: 5px solid #ff0000;
            margin: 20px 0;
        }
        .note-box {
            background-color: #fff3cd;
            padding: 10px;
            border-left: 4px solid #ffc107;
            margin-bottom: 15px;
            font-size: 0.9em;
        }
        a {
            color: #0366d6;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
        code {
            background-color: #f6f8fa;
            padding: 2px 6px;
            border-radius: 4px;
            font-family: SFMono-Regular, Consolas, "Liberation Mono", Menlo, monospace;
            font-size: 0.9em;
        }
    </style>
</head>
<body>

<div class="text-center">
  <img src="https://img.shields.io/badge/Versi-1.0.0-blue?style=for-the-badge&logo=arduino" />
  <img src="https://img.shields.io/badge/Chip-ESP32-black?style=for-the-badge&logo=espressif" />
  <img src="https://img.shields.io/badge/Protocol-Honda_K_Line-green?style=for-the-badge" />
  <br><br>
  <img src="https://img.shields.io/badge/🛠️_Alat_Diagnostik_Otomotif-PENTING-blue" />
</div>

<h1 class="text-center">🏎️ Scanner Motor Honda</h1>
<p class="text-center">
  <b>Alat Diagnostik ECU Profesional via Protokol K-Line</b><br>
  <i>Pemantauan data real-time, Pembaca DTC, dan Live Data yang ditampilkan pada LCD & Web Dashboard.</i>
</p>

<hr>

<h2>🎯 Fitur Utama</h2>
<ul>
  <li><b>Dukungan Multi-ECU:</b> Mendukung berbagai tipe ECU Honda (Tipe 10, 11, 17, dan 17 ESP).</li>
  <li><b>Pemantauan Data Real-time (Live Data):</b> Menampilkan data real-time seperti RPM, TPS, ECT, EOT, IAT, MAP, Sensor O2, CKP, Injektor, dan Kecepatan.</li>
  <li><b>Pembaca Kode Error (DTC):</b> Membaca dan menampilkan error pada sensor MAP, EOT, ECT, TPS, dan Injektor.</li>
  <li><b>Hapus Kode Error (Clear DTC):</b> Fitur untuk menghapus kode error yang tersimpan di ECU.</li>
  <li><b>Antarmuka Ganda (Dual Interface):</b> 
    <ul>
      <li><i>Offline:</i> Navigasi menu via LCD 16x2 dan 3 tombol fisik.</li>
      <li><i>Online:</i> Web Dashboard modern yang responsif (Captive Portal WiFi).</li>
    </ul>
  </li>
  <li><b>Pembaruan OTA (Over-The-Air):</b> Update firmware langsung dari browser tanpa kabel USB.</li>
  <li><b>Keamanan MAC Address:</b> Firmware terkunci dan hanya dapat digunakan pada satu MAC Address ESP32 tertentu.</li>
</ul>

<hr>

<h2>🛠️ Spesifikasi Hardware & Pinout</h2>
<p><b>⚠️ PERINGATAN:</b> Pastikan pengkabelan sesuai dengan konfigurasi di bawah ini agar alat berfungsi dengan baik.</p>

<h3>1. Modul K-Line (ECU)</h3>
<table>
  <tr>
    <th>Pin K-Line</th>
    <th class="text-center">Pin ESP32</th>
    <th>Keterangan</th>
  </tr>
  <tr><td>TX (Kirim)</td><td class="text-center"><b>GPIO 17</b></td><td>Ke RX Modul K-Line</td></tr>
  <tr><td>RX (Terima)</td><td class="text-center"><b>GPIO 16</b></td><td>Dari TX Modul K-Line</td></tr>
  <tr><td>GND</td><td class="text-center"><b>GND</b></td><td>Ground Bersama</td></tr>
</table>
<div class="note-box">
  <i>* Menggunakan <code>HardwareSerial Serial2</code> dengan baudrate 10400.</i>
</div>

<h3>2. LCD I2C (16x2)</h3>
<table>
  <tr>
    <th>Pin LCD</th>
    <th class="text-center">Pin ESP32</th>
    <th>Keterangan</th>
  </tr>
  <tr><td>SDA</td><td class="text-center"><b>GPIO 21</b> (Default)</td><td>Jalur Data</td></tr>
  <tr><td>SCL</td><td class="text-center"><b>GPIO 22</b> (Default)</td><td>Jalur Clock</td></tr>
  <tr><td>VCC</td><td class="text-center"><b>5V</b></td><td>Cataya Daya</td></tr>
  <tr><td>GND</td><td class="text-center"><b>GND</b></td><td>Ground Bersama</td></tr>
</table>
<div class="note-box">
  <i>* Alamat I2C pada kode diset ke <b>0x27</b>. Jika layar tidak menyala, coba ganti ke <code>0x3F</code>.</i>
</div>

<h3>3. Tombol Navigasi Fisik</h3>
<table>
  <tr>
    <th>Fungsi</th>
    <th class="text-center">Pin ESP32</th>
    <th>Koneksi</th>
  </tr>
  <tr><td>ATAS (UP)</td><td class="text-center"><b>GPIO 26</b></td><td>Tombol → GND (Menggunakan Internal Pull-Up)</td></tr>
  <tr><td>BAWAH (DOWN)</td><td class="text-center"><b>GPIO 32</b></td><td>Tombol → GND (Menggunakan Internal Pull-Up)</td></tr>
  <tr><td>ENTER / PB</td><td class="text-center"><b>GPIO 25</b></td><td>Tombol → GND (Menggunakan Internal Pull-Up)</td></tr>
</table>

<h3>4. Komponen On-Board</h3>
<table>
  <tr>
    <th>Komponen</th>
    <th class="text-center">Pin</th>
    <th>Keterangan</th>
  </tr>
  <tr><td>LED Bawaan (Built-in)</td><td class="text-center"><b>GPIO 2</b></td><td>Indikator Error (Blink jika MAC Address tidak cocok)</td></tr>
</table>

<hr>

<h2>📦 Cara Menggunakan</h2>

<h3>1. Koneksi Web Dashboard (WiFi)</h3>
<ol>
  <li>Hubungkan Scanner ke socket OBD / ECU motor Honda.</li>
  <li>Nyalakan kontak motor (tidak perlu menghidupkan mesin).</li>
  <li>Buka WiFi di HP/Laptop, cari SSID: <b>SCANNER MOTOR HONDA</b>.</li>
  <li>Hubungkan (Tidak ada password WiFi, menggunakan fitur Captive Portal).</li>
  <li>Jika halaman login tidak muncul otomatis, buka browser dan ketik: <b>http://8.8.8.8</b></li>
  <li>Masukkan Password sistem: <code>88888888</code></li>
  <li>Anda akan masuk ke Dashboard Live Data untuk memantau sensor secara real-time.</li>
</ol>

<h3>2. Navigasi LCD (Offline)</h3>
<ul>
  <li>Gunakan tombol <b>ATAS</b> dan <b>BAWAH</b> untuk berganti halaman parameter (RPM, TPS, ECT, DTC, dll).</li>
  <li>Gunakan tombol <b>ENTER</b> untuk masuk ke sub-menu (seperti melihat DTC, menghapus DTC, atau info Update OTA).</li>
</ul>

<h3>3. Mode Tersembunyi (Advanced)</h3>
<ul>
  <li><b>Maintenance Mode:</b> Tekan dan tahan tombol <code>ENTER (PB)</code> saat alat sedang booting.</li>
  <li><b>EEPROM Mode:</b> Tekan dan tahan tombol <code>ATAS + BAWAH</code> saat booting (Untuk setting tipe ECU Keihin/Shindengen & ubah Flash Count).</li>
</ul>

<hr>

<h2>⚙️ Konfigurasi & Kustomisasi</h2>
<div class="info-box">
  Jika Anda ingin mem-flash firmware ini ke ESP32 lain (bukan unit awal), Anda <b>WAJIB</b> mengubah variabel berikut di dalam kode:
  <ol>
    <li><b>Kunci MAC Address:</b> Ubah <code>String allowedMAC = "8C:94:DF:AA:4A:1C";</code> menjadi MAC Address dari ESP32 baru Anda.</li>
    <li><b>Alamat LCD:</b> Jika LCD Anda berbeda, ubah <code>LiquidCrystal_I2C lcd(0x27, 16, 2);</code> (Biasanya 0x27 atau 0x3F).</li>
  </ol>
</div>

<hr>

<div class="warning-box">
  <h3>⚖️ Disclaimer</h3>
  <b>PERINGATAN:</b> Alat ini dibuat murni untuk tujuan <i>Diagnostik Otomotif</i> dan <i>Pendidikan</i>. Penggunaan alat ini untuk keperluan modifikasi ilegal atau tindakan yang melanggar hukum daerah setempat <b>BUKAN</b> merupakan tanggung jawab Pengembang.
</div>

<div class="text-center">
  <br>
  <sub>Dibuat dengan ❤️ untuk Sepeda Motor Honda</sub>
</div>

</body>
</html>
