---
title : 'Qucs Intro'
date : 2024-10-08T10:47:02+07:00
toc : true
summary : "Bagian ini adalah tutorial untuk memulai projects dengan qucs"
description : "Bagian ini adalah tutorial untuk memulai projects dengan qucs"
readTime: true
autonumber: true
math: true
tags: ["Electronics", "Qucs"]
showTags: false
hideBackToTop: false

---

# Einleitung

Qucs merupakan salah satu simulator elektronika yang gratis. Dengan lisensi GPL artinya Qucs merupakan opensource yang diperuntukan untuk kebebasan.

Mensimulasikan rangkaian elektronik menjadi penting untuk para mahasiswa, siswa atau penghobi elektronik untuk melihat bentuk sinyal yang muncul dalam rangkaian elektronik tersebut.

# Instalasi 
Saya menggunakan ubuntu 22.04 saat dokument ini ditulis. Sebenarnya Qucs bisa diinstall dalam beragam operating system seperti windows dan macos. Namun dalam dokument ini saya hanya memberikan tutorial dalam menginstalasi dalam ubuntu 22.04.
Karena sudah terdapat dalam repository snapd ubuntu kita bisa langsung menginstallnya dengan command berikut

```bash
sudo snap install qucs-spice --classic
```
Saya juga perlu menginstall octave dan ngspice sebagai toolkit untuk simulasi rangkaian dan operasi matematika atau sinyal processing

```bash
sudo apt-get install ngspice octave
```

# Memulai simulasi pertama
Dalam simulasi pertama kita akan membuat sebuah rangkaian filter yang terdiri dari Capacitor dan resistor. Kita kan melihat nilai frequensi yang mempengaruhi nilai daya rata-rata dari capacitor. Rangkaian filter bisa didesain dengan cara yang sederhana kita bisa mendapatkan pemahaman tentang nilai alternating current dari rangkaian yang akan kita bangun nanti. Pengaruh nilai frequensi yang menentukan nilai reaktansi dari induktor ataupun kapasitor akan bisa kita jelaskan melalui proses simulasi nanti.

![Contoh Simulasi Qucs Sinyal AC](https://faoziaziz.github.io/portofolio/posts/acsimulation.png "Simulasi sinyal AC Qucs")

Gambar diatas adalah hasil dari simulasi dengan menggunakan Qucs untuk sinyal AC.
