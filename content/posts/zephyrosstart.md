---
title : 'Mengingat kembali OS melalui ZephyrOS'
date : 2024-10-12T16:28:24+07:00
summary: "Mengingat kembali materi Operating System melalui ZephyrOS"
description: "Mengingat kembali materi Operating System melalui ZephyrOS"
toc: true
readTime: true
autonumber: true
math: true
tags: ["database", "java"]
showTags: false
hideBackToTop: false
---

Sebagai alternative dari NuttX, ZephyrOS bisa menjadi solusi. Lisensinya GPL bisa jadi opensource. Zephyr merupakan realtime operating system. Saya tertarik karena ada judul buku yang membahas tentang ZephyrOS. Penjelasan bukunya bagus menjelaskan tentang concurency mutex dan juga tentang queue. Buku tersebut terbit tahun 2024 ditulis oleh Andrew Eliasz "Zephyr RTOS Embedded C Programming Using Embedded RTOS POSIX API" terbitan dari Apres.

### Memulai dengan ZephyrOS
```bash
sudo apt update
sudo apt upgrade
```
install Cmake dari Kitware dan sebagainya
```bash
wget https://apt.kitware.com/kitware-archive.sh
sudo bash kitware-archive.sh
```
check versi tools
```bash
cmake --version
python3 --version
dtc --version
```
### Install Python Dependency
Install Python dependency
```bash
sudo apt install python3-venv
```
membuat environtment baru
```bash
python3 -m venv ~/zephyrproject/.venv
```
mengaktivkan enviroment
```bash
source ~/zephyrproject/.venv/bin/activate
```
install west
```bash
pip install west
```
get zephyr source code
```bash
west init ~/zephyrproject
cd ~/zephyrproject
west update
```
export zephyr package
```bash
west zephyr-export
```
install dependency dari python requirement
```bash
pip install -r ~/zephyrproject/zephyr/scripts/requirements.txt
```

### Download SDK ZephyrOS
```bash
cd ~
wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.8/zephyr-sdk-0.16.8_linux-x86_64.tar.xz
wget -O - https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.8/sha256.sum | shasum --check --ignore-missing
```
Extrak ZephyrOS
```bash
tar xvf zephyr-sdk-0.16.8_linux-x86_64.tar.xz
```
Menjalankan Bundle ZephyrOS
```bash
cd zephyr-sdk-0.16.8
./setup.sh
```
install Udev Rules
```bash
sudo cp ~/zephyr-sdk-0.16.8/sysroots/x86_64-pokysdk-linux/usr/share/openocd/contrib/60-openocd.rules /etc/udev/rules.d
sudo udevadm control --reload
```

### Blink Test
Untuk melakukan list pada board yang cocok gunakan perintah berikut.

```bash
west boards | grep esp
```
karena saya menggunakan esp32 saya melakukan list untuk esp32 maka akan muncul list berikut
```bash
$ west boards| grep esp
yd_esp32
olimex_esp32_evb
esp32s3_luatos_core
esp32c3_luatos_core
xiao_esp32c3
xiao_esp32s3
esp32c3_042_oled
esp32s2_franzininho
esp32s3_touch_lcd_1_28
esp32s3_devkitc
esp32_devkitc_wroom
esp32s2_saola
esp32c3_devkitm
esp32_ethernet_kit
esp32c6_devkitc
esp32s3_devkitm
esp8684_devkitm
esp32c3_devkitc
esp_wrover_kit
esp32c3_rust
esp32s3_eye
esp32s2_devkitc
esp32_devkitc_wrover
esp32s2_lolin_mini
```
Saya memilih esp32s3_devkitc karena menggunakan board tersebut. Kemudian masuk ke zephyr direktory dan membuild blink sample

```bash
cd ~/zephyrproject/zephyr
west build -p always -b esp32s3_devkitc samples/basic/blinky
```


# Referensi
1. [Getting Started dengan ZephyrOS](https://docs.zephyrproject.org/latest/develop/getting_started/index.html)

