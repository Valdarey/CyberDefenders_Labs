# Laporan Investigasi Forensik Jaringan — shoporoma.com

Investigasi *network forensics* atas kompromi web server melalui web shell upload, reverse shell, dan percobaan eksfiltrasi data, berdasarkan analisis berkas tangkapan lalu lintas jaringan (`WebStrike.pcap`).

## Ringkasan

| Atribut | Detail |
|---|---|
| Kategori | Network Forensics |
| Target | shoporoma.com (Web Server) |
| Berkas Bukti | WebStrike.pcap |
| Tools | Wireshark, IP Geolocation Lookup |
| Tingkat Keparahan | **CRITICAL** |
| Lingkungan | Internal Staging / Home Lab |

## Kronologi Serangan

1. Koneksi awal & pengungkapan User-Agent penyerang (`GET /favicon.ico`)
2. Upload web shell (`image.jpg.php`) via `POST /reviews/upload.php` — teknik ekstensi ganda
3. Eksekusi web shell melalui `GET /reviews/uploads/image.jpg.php`
4. Pembukaan reverse shell keluar (outbound) ke mesin penyerang
5. Percobaan eksfiltrasi berkas sistem `/etc/passwd`

## Indikator Kompromi (IOC)

| Indikator | Nilai |
|---|---|
| Alamat IP Penyerang | 117.11.88.124 |
| Lokasi Geografis | Tianjin, Tiongkok |
| User-Agent | Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0 |
| Nama Web Shell | image.jpg.php |
| Direktori Unggahan | /reviews/uploads/ |
| Port Reverse Shell | 8080/TCP |
| Target Eksfiltrasi | /etc/passwd |
| Endpoint Rentan | /reviews/upload.php |

## Metodologi

Analisis statis terhadap `WebStrike.pcap` menggunakan Wireshark:
- Display filter (`http.request.method == POST`) untuk isolasi permintaan upload
- Rekonstruksi sesi via *Follow TCP Stream*
- Verifikasi asal geografis IP melalui layanan IP geolocation

## Struktur Laporan

1. Ringkasan Eksekutif
2. Metodologi Investigasi
3. Kronologi Serangan (Attack Timeline)
4. Temuan Analisis Terperinci (asal geografis, User-Agent, web shell, direktori, port, target eksfiltrasi)
5. Indikator Kompromi (IOC)
6. Kesimpulan
7. Rekomendasi Mitigasi

## Rekomendasi Mitigasi (Ringkas)

**Segera:**
- Blokir IP penyerang pada firewall/WAF
- Blokir port outbound 8080
- Hapus berkas `image.jpg.php`
- Rotasi kredensial & audit akun

**Jangka Panjang:**
- Validasi upload ketat (whitelist ekstensi + validasi MIME-type/isi berkas)
- Nonaktifkan eksekusi skrip pada direktori unggahan
- WAF untuk deteksi pola ekstensi ganda
- Filtering lalu lintas outbound
- Code review modul upload

## Klasifikasi & Distribusi

**Confidential** — Distribusi terbatas hanya untuk tim Keamanan Siber dan Manajemen terkait.

⚠️ Repository ini bersifat **privat**. Laporan berisi IOC nyata (IP, User-Agent, nama file, endpoint) yang tidak seharusnya dipublikasikan secara terbuka.
