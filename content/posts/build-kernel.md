---
date : '2024-12-09T11:35:16+07:00'
title : 'Build Kernel Basic'
summary : "Build Kernel basic"
description : "Build kernel basic"
readTime: true
autonumber: true
math: true
tags: ["Electronics", "Qucs"]
showTags: false
hideBackToTop: false
---

Karena biasanya kita membutuhkan cara untuk membuat kernel. Mungkin kita perlu untuk pertama kali bagaimana cara kita untuk membuildnya, kemudian kita mensimulasikannya dengan qemu lalu melakukan modifikasi pada kernel itu sendiri.

## Download kode kernel
```bash
wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.5.tar.xz
```
## extract kode kernel
```bash
tar -xvf linux-6.5.tar.xz
cd linux-6.5
```

## install build toolsnya
```bash
sudo apt update
sudo apt install build-essential libncurses-dev bison flex libssl-dev libelf-dev
```


## configurasinya
karena kita akan memulai untuk membuild terlebih dahulu code awalnya kita buat dengan dasar
```bash
make defconfig

```
## membuildnya dengan jumlah processor
supaya cepat gunakan -j$(jumlahprocessor)
```bash
make -j$(nproc)
```

# Buat Rootfs untuk mengetest 
Kita membutuhkan rootfs untuk mengetest kernel yang kita buat ternyata bisa dijalankan dengan rootfs atau tidak.

## download code rootfs
```bash
mkdir rootfs
cd rootfs
mkdir -p {bin,sbin,etc,proc,sys,usr/{bin,sbin}}

```
## buat file init
gunakan text editor favorit saya menggunakan vim jadi kommandnya seperti berikut

```bash
vim init

```
isinya sebagai berikut
```bash
#!/bin/sh

# INI FILE init pada direktory rootfs
mount -t proc none /proc
mount -t sysfs none /sys
echo "Hello, Kernel is running!"
/bin/busybox sh
mkdir dev
sudo mknod -m 666 dev/null c 1 3
sudo mknod -m 622 dev/console c 5 1
```
## tambahkan busybox
busybox diguanakn untuk memperoleh perintah dasar seperti ls atau init
```bash
wget https://busybox.net/downloads/binaries/1.30.0-i686/busybox
mv busybox bin/busybox
chmod +x bin/busybox
cd bin
ln -s busybox sh
```

## buat initramfs
initramfs diguankan untuk meload rootfs pada ram yang ada kernelnya.
```bash
find . | cpio -o --format=newc > ../initramfs.img
cd ..
```
## run dengan qemu 
```bash
qemu-system-x86_64 -kernel arch/x86/boot/bzImage -initrd initramfs.img -append "console=ttyS0 init=/bin/sh" -nographic
```