# Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI
Repository ini akan membahas bagaimana cara menginstall MPI dan cara mengeksekusi program Buble Sort Python menggunakan ubuntu server 22.04 sebagai operating system yang digunakan.

# Cara Install MPI pada Ubuntu Server
## Topologi
![image](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/f8d0a758-04d8-4092-b9a8-b7510e6e417a)

## 1. Langkah Awal
1. Siapkan beberapa komputer dan tentukan satu komputer sebagai master dan beberapa komputer sebagai slave.
2. Pastikan seluruh komputer terhubung dalam satu jaringan.
3. Update dan Upgrade package **sudo apt update && sudo apt upgrade**

## 2. Buat User Baru
Lakukan di **Master** dan **Slave**
### 2.1 Buat User <br>
    sudo adduser <nama user>
### 2.2 Beri Akses Root <br>
    sudo usermod -aG mpiuser
### 2.3 Masuk ke User yang telah dibuat <br> 
    su - mpiuser

## 3. Install MPICH
Lakukan di **Master** dan **Slave**
### 3.1 Install MPICH dan Paket Dokumentasi MPICH pada Sistem <br> 
    sudo apt-get install -y mpich-doc mpich
### 3.2 Cek Versi MPI <br> 
    mpirun --version
### 3.3 Testing The Installation <br> 
    mpiexec -n <jumlah core> pyhton3 -m mpi4py.bench helloworld
### 3.4 Install paket python mpi4py menggunakan pip untuk menjalankan python pada MPI <br> 
    pip install mpi4py -U

## 4. Konfigurasi File /etc/hosts
Untuk memeriksa IP Adress pada komputer gunakan perintah *ip a* <br>
**sudo nano /etc/hosts**
1. Untuk **Master** <br>
   ![image1](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/4eebb045-9e2d-4c10-abc1-8cf37bb57704)
2. Untuk **Slave** <br>
   ![Image2](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/1b49e18a-57ec-4284-8dac-daf4ef5a97d6)

## 5. Install SSH
Lakukan di **Master** dan **Slave** <br>
**sudo apt install openssh-server**
### 5.1 Buat Key <br> Lakukan pada master <br>
    ssh-keygen -t rsa
### 5.2 Copy key public to client <br> 
    ssh-copy-id <nama user>@<host>
<br> Ganti <nama user> dengan user yang dibuat dan <host> dengan slave, lakukan pada semua slave.

## 6. Jalankan MPI
### Lakukan pada **Master** <br> 
    mpiexec -n <jumlah core> python -m mpi4py.bench helloworld
<img width="404" alt="percobaan" src="https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/8e1d12c1-2d12-4016-afd9-341b1eea56e7">

# Cara Eksekusi Program Buble Sort Python Menggunakan MPI
### 1. Lakukan Penginputan SSH Untuk Semua Slave 
    ssh-copy-id user@hostname_or_ip

### 2. Masukkan Program Buble Sort Python 
Berikut adalah kodingan yang kelompok saya gunakan <br>
![G2](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/06f0602c-f77c-4e96-a9cc-2bcae83c3c68)

### 3. Copy File Python ke Semua Slave
    path$ scp /path/to/locate/bin * user@hostname_or_ip:path/to
![image](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/d6455bd1-4c86-41e2-9116-f5648166b92c)

### 4. Hasil Percobaan
![image](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/72d92ade-9125-4b55-b043-add4c0e6ee1f)

