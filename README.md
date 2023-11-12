# Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI
Repository ini akan membahas bagaimana cara menginstall MPI dan cara mengeksekusi program Buble Sort Python menggunakan ubuntu server 22.04 sebagai operating system yang digunakan.

# Cara Install MPI pada Ubuntu Server
## Topologi
![Topologi](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/f43765be-5ec9-4ce7-977f-b9264035b25d)

## 1. Langkah Awal
1. Siapkan beberapa komputer dan tentukan satu komputer sebagai master dan beberapa komputer sebagai slave.
2. Pastikan seluruh komputer terhubung dalam satu jaringan.
3. Update dan Upgrade package 'sudo apt update && sudo apt upgrade'.

## 2. Buat User Baru
Lakukan di Master dan Slave
### 2.1 Buat User
sudo adduser <nama user>
![User1](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/c099b279-c267-4974-a398-a7db44696f3b)
### 2.2 Beri Akses Root
sudo usermod -aG mpiuser
### 2.3 Masuk ke User yang telah dibuat
su - mpiuser
![User2](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/119fd0cb-09e3-46d8-9234-ee53cbb5fc89)

## 3. Install MPICH
Lakukan di Master dan Slave
### 3.1 Install MPICH dan Paket Dokumentasi MPICH pada Sistem
sudo apt-get install -y mpich-doc mpich
![MPICH](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/c45360ad-cd87-4a76-b77b-c34ad2f1c904)
### 3.2 Cek Versi MPI
mpirun --version
![MPIrun](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/a0565b0e-73b1-4b9a-8105-55e6d87ea6a4)
### 3.3 Testing The Installation
mpiexec -n <jumlah core> pyhton3 -m mpi4py.bench helloworld
![3.3](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/28f624f5-3dca-4bd6-ac80-f625191988ac)
### 3.4 Install paket python mpi4py menggunakan pip untuk menjalankan python pada MPI
pip install mpi4py -U
![3.4](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/6e08850e-475e-4d8d-8aa1-00cb60b1f17e)

## 4. Konfigurasi File /etc/hosts
sudo nano /etc/hosts
### 4.1 Untuk Master
![4.1](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/971e7ce4-ac66-4be1-81ad-d8c8abfcc9be)
### 4.2 Untuk Slave
Slave
![4.2](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/02b97841-45d5-4517-8e99-cca4950f84a9)

## 5. Install SSH
Lakukan di Master dan Slave
sudo apt install openssh-server
### 5.1 Buat Key
Lakukan pada master
ssh-keygen -t rsa
### 5.2 Copy key public to client
ssh-copy-id <nama user>@<host>
Ganti <nama user> dengan user yang dibuat dan <host> dengan slave, lakukan pada semua slave.

## 6. Jalankan MPI
Lakukan pada master
mpiexec -n <jumlah core> python -m mpi4py.bench helloworld
![6](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/acf5cc49-7c82-42ce-857f-1de872c0fda5)


# Cara Eksekusi Program Buble Sort Python Menggunakan MPI
## 1. Lakukan Penginputan SSH Untuk Semua Slave
ssh-copy-id user@hostname_or_ip
Slave 1
![Slave1](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/7c446076-7900-45ee-a072-c3b4dbbdab56)
![Slave2](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/38920fb0-b450-42cb-bc30-a98b6df7de9c)
![Slave3](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/e3200e46-1179-43c2-92b4-f3c3c1da8d72)

## 2. Masukkan Program Buble Sort Python
Berikut adalah kodingan yang kelompok saya gunakan
![2.2](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/dbad251f-d8a9-4612-affc-e663b7933637)

## 3. Copy File Python ke Semua Slave
~path$ scp /path/to/locate/bin * user@hostname_or_ip:path/to
![2.3](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/2f8475d3-04ff-4cee-a797-af48ea5c4547)

## 4. Hasil Percobaan
![2.4](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/d1966178-fb3d-45b6-bcc1-3b4527a0bf10)
