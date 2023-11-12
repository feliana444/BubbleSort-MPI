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
### 2.2 Beri Akses Root
sudo usermod -aG mpiuser
### 2.3 Masuk ke User yang telah dibuat
su - mpiuser

## 3. Install MPICH
Lakukan di Master dan Slave
### 3.1 Install MPICH dan Paket Dokumentasi MPICH pada Sistem
sudo apt-get install -y mpich-doc mpich
### 3.2 Cek Versi MPI
mpirun --version
### 3.3 Testing The Installation
mpiexec -n <jumlah core> pyhton3 -m mpi4py.bench helloworld
### 3.4 Install paket python mpi4py menggunakan pip untuk menjalankan python pada MPI
pip install mpi4py -U

## 4. Konfigurasi File /etc/hosts
sudo nano /etc/hosts
### 4.1 Untuk Master
![4.3](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/d93c6202-ee4d-446b-8343-2aa5a5484ea5)

### 4.2 Untuk Slave
Slave



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

<img width="404" alt="percobaan" src="https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/8e1d12c1-2d12-4016-afd9-341b1eea56e7">



# Cara Eksekusi Program Buble Sort Python Menggunakan MPI
## 1. Lakukan Penginputan SSH Untuk Semua Slave
ssh-copy-id user@hostname_or_ip

![image](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/ab0015e2-dd64-4d4e-abe3-3571a2b0c5aa)
![image](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/670c8067-f5d0-4a50-9867-00ca8a800476)
<img width="401" alt="copyssh3" src="https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/19f2d4b2-cd3a-4185-8ea3-f54279ca5f95">


## 2. Masukkan Program Buble Sort Python
Berikut adalah kodingan yang kelompok saya gunakan

![G2](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/06f0602c-f77c-4e96-a9cc-2bcae83c3c68)


## 3. Copy File Python ke Semua Slave
~path$ scp /path/to/locate/bin * user@hostname_or_ip:path/to
![image](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/d6455bd1-4c86-41e2-9116-f5648166b92c)


## 4. Hasil Percobaan
![image](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/72d92ade-9125-4b55-b043-add4c0e6ee1f)

