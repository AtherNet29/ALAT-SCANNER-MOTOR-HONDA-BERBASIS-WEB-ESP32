<div align="center">
  <img src="https://img.shields.io/badge/Versi-1.0.0-blue?style=for-the-badge&logo=arduino" />
  <img src="https://img.shields.io/badge/Chip-ESP32-black?style=for-the-badge&logo=espressif" />
  <img src="https://img.shields.io/badge/Protocol-Honda_K_Line-green?style=for-the-badge" />
  <br><br>
  <img src="https://img.shields.io/badge/🛠️_Alat_Diagnostik_Otomotif-PENTING-blue" />
</div>

<h1 align="center">🏎️ Scanner Motor Honda</h1>
<p align="center">
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
<p>⚠️ <b>PERINGATAN:</b> Pastikan pengkabelan sesuai dengan konfigurasi di bawah ini agar alat berfungsi dengan baik.</p>

<h3>1. Modul K-Line (ECU)</h3>
<table>
  <tr>
    <th>Pin K-Line</th>
    <th style="text-align: center;">Pin ESP32</th>
    <th>Keterangan</th>
  </tr>
  <tr><td>TX (Kirim)</td><td style="text-align: center;"><b>GPIO 17</b></td><td>Ke RX Modul K-Line</td></tr>
  <tr><td>RX (Terima)</td><td style="text-align: center;"><b>GPIO 16</b></td><td>Dari TX Modul K-Line</td></tr>
  <tr><td>GND</td><td style="text-align: center;"><b>GND</b></td><td>Ground Bersama</td></tr>
</table>
<p><i>* Menggunakan <code>HardwareSerial Serial2</code> dengan baudrate 10400.</i></p>

<h3>2. LCD I2C (16x2)</h3>
<table>
  <tr>
    <th>Pin LCD</th>
    <th style="text-align: center;">Pin ESP32</th>
    <th>Keterangan</th>
  </tr>
  <tr><td>SDA</td><td style="text-align: center;"><b>GPIO 21</b> (Default)</td><td>Jalur Data</td></tr>
  <tr><td>SCL</td><td style="text-align: center;"><b>GPIO 22</b> (Default)</td><td>Jalur Clock</td></tr>
  <tr><td>VCC</td><td style="text-align: center;"><b>5V</b></td><td>Cataya Daya</td></tr>
  <tr><td>GND</td><td style="text-align: center;"><b>GND</b></td><td>Ground Bersama</td></tr>
</table>
<p><i>* Alamat I2C pada kode diset ke <b>0x27</b>. Jika layar tidak menyala, coba ganti ke <code>0x3F</code>.</i></p>

<h3>3. Tombol Navigasi Fisik</h3>
<table>
  <tr>
    <th>Fungsi</th>
    <th style="text-align: center;">Pin ESP32</th>
    <th>Koneksi</th>
  </tr>
  <tr><td>ATAS (UP)</td><td style="text-align: center;"><b>GPIO 26</b></td><td>Tombol → GND (Menggunakan Internal Pull-Up)</td></tr>
  <tr><td>BAWAH (DOWN)</td><td style="text-align: center;"><b>GPIO 32</b></td><td>Tombol → GND (Menggunakan Internal Pull-Up)</td></tr>
  <tr><td>ENTER / PB</td><td style="text-align: center;"><b>GPIO 25</b></td><td>Tombol → GND (Menggunakan Internal Pull-Up)</td></tr>
</table>

<h3>4. Komponen On-Board</h3>
<table>
  <tr>
    <th>Komponen</th>
    <th style="text-align: center;">Pin</th>
    <th>Keterangan</th>
  </tr>
  <tr><td>LED Bawaan (Built-in)</td><td style="text-align: center;"><b>GPIO 2</b></td><td>Indikator Error (Blink jika MAC Address tidak cocok)</td></tr>
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
<div style="background-color: #e6f3ff; padding: 15px; border-left: 5px solid #0055aa;">
  <b>💡 Jika Anda ingin mem-flash firmware ini ke ESP32 lain (bukan unit awal), Anda WAJIB mengubah variabel berikut di dalam kode:</b>
  <ol>
    <li><b>Kunci MAC Address:</b> Ubah <code>String allowedMAC = "8C:94:DF:AA:4A:1C";</code> menjadi MAC Address dari ESP32 baru Anda.</li>
    <li><b>Alamat LCD:</b> Jika LCD Anda berbeda, ubah <code>LiquidCrystal_I2C lcd(0x27, 16, 2);</code> (Biasanya 0x27 atau 0x3F).</li>
  </ol>
</div>

<hr>

<h2>📸 Preview Tampilan</h2>
<p><b>Antarmuka Web Dashboard:</b></p>
<p align="center">
  <img src="LINK_GAMBAR_ANDA_DISINI" width="400" alt="Dashboard Scanner Honda" />
</p>

<hr>

<div align="center">
  <h2>💎 Dapatkan Alat Ini</h2>
  <p>Hubungi saya atau lakukan pemesanan langsung melalui Telegram untuk mendapatkan firmware full version dan bantuan teknis.</p>
  <h3>🛒 Harga: RP 50.000</h3>
  <br>
  <a href="https://t.me/+6283141852690">
  <img src="https://img.shields.io/badge/Buy_Now-Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" />
  </a>
  <br><br>
  <i>Klik tombol di atas untuk chat langsung dengan saya di Telegram.</i>
</div>

<hr>

<div style="background-color: #ffcccc; padding: 15px; border-left: 5px solid #ff0000;">
  <h3>⚖️ Disclaimer</h3>
  <b>PERINGATAN:</b> Alat ini dibuat murni untuk tujuan <i>Diagnostik Otomotif</i> dan <i>Pendidikan</i>. Penggunaan alat ini untuk keperluan modifikasi ilegal atau tindakan yang melanggar hukum daerah setempat <b>BUKAN</b> merupakan tanggung jawab Pengembang.
</div>

<div align="center">
  <br>
  <sub>Dibuat dengan ❤️ untuk Sepeda Motor Honda</sub>
</div>
