# Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI
Repository ini akan membahas bagaimana cara menginstall MPI dan cara mengeksekusi program Buble Sort Python menggunakan ubuntu server 22.04 sebagai operating system yang digunakan.

# Cara Install MPI pada Ubuntu Server
## Topologi
![image](https://github.com/feliana444/Eksekusi-Program-Buble-Sort-Python-Menggunakan-MPI/assets/145323449/f8d0a758-04d8-4092-b9a8-b7510e6e417a)

## 1. Langkah Awal
1. Siapkan beberapa komputer dan tentukan satu komputer sebagai master dan beberapa komputer sebagai slave.
2. Pastikan seluruh komputer terhubung dalam satu jaringan.
3. Update dan Upgrade package `sudo apt update && sudo apt upgrade`

## 2. Buat User Baru
>*Lakukan di **Master** dan **Slave***
### 2.1 Buat User 
    sudo adduser <nama user>
### 2.2 Beri Akses Root
    sudo usermod -aG mpiuser
### 2.3 Masuk ke User yang telah dibuat  
    su - mpiuser

## 3. Install MPICH
>*Lakukan di **Master** dan **Slave***
### 3.1 Install MPICH dan Paket Dokumentasi MPICH pada Sistem <br> 
    sudo apt-get install -y mpich-doc mpich
### 3.2 Cek Versi MPI  
    mpirun --version
### 3.3 Testing The Installation 
    mpiexec -n <jumlah core> pyhton3 -m mpi4py.bench helloworld
### 3.4 Install paket python mpi4py menggunakan pip untuk menjalankan python pada MPI 
    pip install mpi4py -U

## 4. Konfigurasi File /etc/hosts
Untuk memeriksa IP Adress pada komputer gunakan perintah *ip a* <br>
`sudo nano /etc/hosts`
1. Untuk **Master** 
```sh
172.20.10.7 master
172.20.10.9 slave1
172.20.10.5 slave2
172.20.10.6 slave3
```
2. Untuk **Slave** <br>
```sh
172.20.10.7 master
172.20.10.9 slave1
```
## 5. Install SSH
>*Lakukan di **Master** dan **Slave***

`sudo apt install openssh-server`
### 5.1 Buat Key <br> Lakukan pada master 
    ssh-keygen -t rsa
### 5.2 Copy key public to client  
    ssh-copy-id <nama user>@<host>
Ganti *nama user* dengan user yang dibuat dan *host* dengan slave, lakukan pada semua slave.

## 6. Jalankan MPI
### Lakukan pada **Master**  
    mpiexec -n <jumlah core> python -m mpi4py.bench helloworld

# Cara Eksekusi Program Buble Sort Python Menggunakan MPI
### 1. Lakukan Penginputan SSH Untuk Semua Slave 
    ssh-copy-id user@hostname_or_ip

### 2. Masukkan Program Buble Sort Python 
Berikut adalah program yang saya gunakan <br>
```sh
from mpi4py import MPI

def BubbleSort(val):
    for passnum in range(len(val) - 1, 0, -1):
        for i in range(passnum):
            if val[i] > val[i+1]:
                temp = val[i]
                val[i] = val[i+1]
                val[i+1] = temp

DaftarAngka = [23, 87, 2, 10, 2004, 24, 43, 12]
BubbleSort(DaftarAngka)
Print(Daftar Angka)
```

### 3. Copy File Python ke Semua Slave
`path$ scp /path/to/locate/bin * user@hostname_or_ip:path/to` <br>
Contohnya seperti ini 
```sh
scp /home/mpiuser/wadah/* mpiuser@slave1:/home/mpiuser
scp /home/mpiuser/wadah/* mpiuser@slave2:/home/mpiuser
scp /home/mpiuser/wadah/* mpiuser@slave3:/home/mpiuser
```

### 4. Run Program
```sh
mpirun -n <jumlah core> -host master,slave1,slave2,slave3 python3 bubble.py
```
output
```sh
[2, 10, 12, 23, 24, 43, 87, 2004]
[2, 10, 12, 23, 24, 43, 87, 2004]
[2, 10, 12, 23, 24, 43, 87, 2004]
```
