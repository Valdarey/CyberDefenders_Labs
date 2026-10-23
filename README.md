<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0b1f3a,100:2f6bff&height=220&section=header&text=Blue%20Team%20Write-Ups&fontSize=50&fontColor=ffffff&fontAlignY=38&desc=CyberDefenders%20Lab%20Walkthroughs&descSize=20&descAlignY=60&animation=fadeIn" width="100%" alt="Banner">

<img src="cyberlogo.png" alt="CyberDefenders Logo" width="450">

<br><br>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1200&color=2F6BFF&center=true&vCenter=true&width=700&lines=Blue+Team+%7C+Digital+Forensics;Network+Forensics+%7C+Threat+Intelligence;Follow+the+packets.+Find+the+story.;Defend+Smarter%2C+Not+Harder!" alt="Typing SVG">

<br><br>

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-1f3a8a?style=for-the-badge&logo=hackthebox&logoColor=white)
![Focus](https://img.shields.io/badge/Focus-Blue%20Team-2f6bff?style=for-the-badge&logo=shield&logoColor=white)
![Write-ups](https://img.shields.io/badge/Write--ups-2-2ea043?style=for-the-badge)
![Language](https://img.shields.io/badge/Language-ID%20%7C%20EN-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Actively%20Updated-brightgreen?style=for-the-badge)

<br>

Repositori ini berisi kumpulan write-up penyelesaian lab **Blue Team** dan **Digital Forensics** dari CyberDefenders, lengkap dengan analisis dan langkah penyelesaiannya. Seluruh artikel lengkap dipublikasikan di Medium.

<br>

<a href="https://medium.com/@prabaswaradaffa2">
  <img src="https://img.shields.io/badge/📖%20Baca%20Write--Up%20Lengkap%20di%20Medium-000000?style=for-the-badge&logo=medium&logoColor=white" alt="Baca di Medium" height="42">
</a>

</div>

<br>

<div align="center">

[📚 Daftar Write-Up](#-daftar-write-up) · [🧭 Metodologi](#-metodologi-analisis) · [🧰 Tools & Skills](#-tools--skills) · [🗺️ Roadmap](#%EF%B8%8F-roadmap) · [🤝 Kontak](#-connect-with-me)

</div>

<img src="https://capsule-render.vercel.app/api?type=rect&color=0:0b1f3a,100:2f6bff&height=3&section=header" width="100%" alt="divider">

## 📚 Daftar Write-Up

| Lab Name | Category | Link |
|:---------|:--------:|:----:|
| 🕸️ [**WebStrike Lab**](https://medium.com/@prabaswaradaffa2/webstrike-cyberdefenders-labs-5796e6784fd1) | ![Network Forensics](https://img.shields.io/badge/Network%20Forensics-1f6feb?style=flat-square) | [![Read](https://img.shields.io/badge/Read%20Write--Up%20→-000000?style=flat-square&logo=medium&logoColor=white)](https://medium.com/@prabaswaradaffa2/webstrike-cyberdefenders-labs-5796e6784fd1) |
| 🛒 [**RetailBreach Lab**](https://medium.com/@prabaswaradaffa2/retailbreach-cyberdefenders-labs-287255a9315c) | ![Network Forensics](https://img.shields.io/badge/Network%20Forensics-1f6feb?style=flat-square) | [![Read](https://img.shields.io/badge/Read%20Write--Up%20→-000000?style=flat-square&logo=medium&logoColor=white)](https://medium.com/@prabaswaradaffa2/retailbreach-cyberdefenders-labs-287255a9315c) |

> [!NOTE]
> Write-up baru akan terus ditambahkan seiring lab yang saya selesaikan. Beri ⭐ pada repository ini agar tidak ketinggalan!

### 🔎 Sekilas Isi Setiap Write-Up

<details>
<summary><b>🕸️ WebStrike</b>: dari upload berkas hingga reverse shell</summary>

<br>

Menelusuri sebuah web server yang dikompromikan lewat berkas pcap: bagaimana penyerang masuk, apa yang ia jalankan, dan ke mana ia mengirim datanya.

**Teknik yang dibahas:** display filter HTTP · rekonstruksi sesi dengan *Follow TCP Stream* · analisis payload multipart · geolocation IP

</details>

<details>
<summary><b>🛒 RetailBreach</b>: XSS, pembajakan sesi, dan path traversal</summary>

<br>

Menghubungkan pengintaian, injeksi skrip, pencurian sesi admin, dan penyalahgunaan halaman admin menjadi satu linimasa serangan yang utuh.

**Teknik yang dibahas:** deteksi brute-force direktori · korelasi waktu antar-paket · pelacakan cookie sesi · deteksi path traversal

</details>

> [!WARNING]
> Write-up memuat jawaban lab. Kalau Anda sedang mengerjakan lab yang sama, coba selesaikan sendiri dulu, lalu gunakan write-up ini sebagai pembanding.

<img src="https://capsule-render.vercel.app/api?type=rect&color=0:0b1f3a,100:2f6bff&height=3&section=header" width="100%" alt="divider">

## 🧭 Metodologi Analisis

Alur berpikir yang saya pakai di hampir setiap lab network forensics:

```mermaid
flowchart LR
    A([📦 Buka PCAP]) --> B[🔎 Identifikasi<br/>host & protokol]
    B --> C[🎯 Terapkan<br/>display filter]
    C --> D[🧵 Follow Stream<br/>baca isi lengkap]
    D --> E[⏱️ Korelasikan<br/>waktu & alur]
    E --> F([✅ Susun kronologi<br/>& jawaban])

    style A fill:#0b1f3a,stroke:#2f6bff,color:#fff
    style F fill:#1a7f37,stroke:#2ea043,color:#fff
    style B fill:#1f3a8a,stroke:#2f6bff,color:#fff
    style C fill:#1f3a8a,stroke:#2f6bff,color:#fff
    style D fill:#1f3a8a,stroke:#2f6bff,color:#fff
    style E fill:#1f3a8a,stroke:#2f6bff,color:#fff
```

<img src="https://capsule-render.vercel.app/api?type=rect&color=0:0b1f3a,100:2f6bff&height=3&section=header" width="100%" alt="divider">

## 🧰 Tools & Skills

<div align="center">

![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white)
![Network Forensics](https://img.shields.io/badge/Network%20Forensics-0b1f3a?style=for-the-badge)
![Web Attack Analysis](https://img.shields.io/badge/Web%20Attack%20Analysis-b91c1c?style=for-the-badge)
![Incident Investigation](https://img.shields.io/badge/Incident%20Investigation-6d28d9?style=for-the-badge)
![Timeline Analysis](https://img.shields.io/badge/Timeline%20Analysis-0f766e?style=for-the-badge)
![Technical Writing](https://img.shields.io/badge/Technical%20Writing-b45309?style=for-the-badge)

</div>

<img src="https://capsule-render.vercel.app/api?type=rect&color=0:0b1f3a,100:2f6bff&height=3&section=header" width="100%" alt="divider">

## 🗺️ Roadmap

- [x] Network Forensics
- [ ] Threat Intelligence
- [ ] Endpoint Forensics
- [ ] Malware Analysis
- [ ] Threat Hunting
- [ ] SOC / Log Analysis
- [ ] Memory Forensics

<img src="https://capsule-render.vercel.app/api?type=rect&color=0:0b1f3a,100:2f6bff&height=3&section=header" width="100%" alt="divider">

<div align="center">

## 🤝 Connect with Me

[![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://instagram.com/USERNAME)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/USERNAME)
[![Medium](https://img.shields.io/badge/Medium-000000?style=for-the-badge&logo=medium&logoColor=white)](https://medium.com/@prabaswaradaffa2)

<br>

![Visitors](https://komarev.com/ghpvc/?username=Valdarey&label=Visitors&color=2f6bff&style=for-the-badge)

<sub>Seluruh write-up dibuat untuk tujuan edukasi. Lab dan materi asli adalah milik CyberDefenders, dan repository ini tidak berafiliasi dengan mereka.</sub>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0b1f3a,100:2f6bff&height=140&section=footer" width="100%" alt="footer">

</div>
