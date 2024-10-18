---
title : 'Nuttx dengan Qemu'
date : 2024-10-06T14:21:53+07:00
summary : "Bagian ini adalah catatan tentang menjalankan nuttx dengan Qemu"
description : "Bagian ini adalah catatan tentang menjalankan nuttx dengan Qemu"
readTime: true
autonumber: true
math: true
tags: ["NuttX", "C", "Embedded"]
showTags: false
hideBackToTop: false
---
NuttX merupakan salah satu realtime operating system. Sebenernya ada banyak operating system seperti FreeRTOS, VxWorks, atau openRTOS. Nuttx sering digunakan dalam platform Drone, misalkan FMUv4. Struktur code dari NuttX yang mirip dengan struktur code dari Linux (Seperti kita tahu bahwa linux menggunakan menuconfig dan Kconfig). Settingannya memang mirip ada juga driver untuk tiap processor yang codenya mirip dengan linux. Untuk itu mempelajari linux dengan lebih simple bisa dilakukan dengan menggunakan NuttX. Struktur Code dari NuttX juga dibagi jadi 2 direktori besar yaitu tools dan apps. Dimana kalau kita sambungkan dengan linux ini juga mirip dengan zImage, dan rootfs. zImage dari linux terdiri dari binary code bootloader dan kernel sama dengan direktori tools dari NuttX yang berisi driver hardware dari perangkat. Sedangkan rootFs dari linux yang berisi aplikasi user mirip dengan code pada direktori apps dari NuttX kita bisa mendevelop code yang akan dijalankan user dalam code apps. Ketika kita menjalankan NuttX kita akan melihat bahwa booting dan consolenya, serta struktur bootingnya juga mirip linux. Bahkan kita akan melihat ada struktur direktory seperti /var /home /lib /bin dan sebagainya ketika kita melakukan logging console.

Buat kamu yang belum memiliki hardware untuk menjalankan NuttX dalam hardware kalian. Kalian bisa menggunkan Qemu sebagai alternatif untuk menjalakan program NuttX anda. Qemu merupakan sebuah emulator yang bagus untuk mensimulasikan linux lalu bagaimana jika kita ingin menggunakan NuttX yang dijalanakan melalui Qemu. Oh tentu saja bisa kita bisa membuild code nuttx dan melakukannya berjalan pada emulator Qemu. Seperti halnya membuat program aplikasi dengan menggunakan linux, maksudnya membuild sebuah sistem operating linux kita perlu mendownload code source tools dan apps untuk nuttx. Pertama buat direktori untuk pengerjaan NuttX dengan qemu. 

```bash
mkdir ~/NuttXqemu
cd ~/NuttXqemu
```

Kemudian mendownload code NuttX untuk kita build nanti

```bash
git clone https://github.com/apache/incubator-nuttx.git nuttx
git clone https://github.com/apache/incubator-nuttx-apps apps
```

sebelumnya kita perlu menginstall gcc untuk arm untuk melakukan compile dan linker. 
```bash
sudo apt install gcc-arm-none-eabi.
```
lalu kita build dengan code berikut
```bash
./tools/configure.sh -l qemu-armv7a:nsh
make
```

lalu run dengan code berikut
```bash
qemu-system-arm -cpu cortex-a7 -nographic \
     -machine virt,virtualization=off,gic-version=2 \
     -net none -chardev stdio,id=con,mux=on -serial chardev:con \
     -mon chardev=con,mode=readline -kernel ./nuttx
```
nanti akan muncul code qemu dengan nuttx yang ada didalamnya. Qemu akan mensimulasikan hardware armv7a 

berikut adalah tampilan dari console nuttx yang dijalankan dalam Qemu.

![Gambar Console Qemu](https://faoziaziz.github.io/portofolio/posts/Screenshot_20241006_145954.png "Console Qemu")

untuk mengetahui command apa yang bisa dijalakan gunakan tanda "?" lalu tekan enter.

# Referensi 
1. [Build dengan Qemu](https://nuttx.apache.org/docs/latest/platforms/arm/qemu/boards/qemu-armv7a/index.html)







