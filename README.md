# TugasPaktikum2
# Tugas Praktikum { Pertemuan ke 7 } <img src=https://qph.fs.quoracdn.net/main-qimg-648763cc041459725b62108f4fdf5b91 width="110px" >


|**Nama**|**NIM**|**Kelas**|**Matkul**|
|----|---|-----|------|
|Wawan Suwandi|312310457|TI.23.A5|Basis Data|

# Soal Latihan Praktikum
## Data Model Mapping

```
Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

Dosen (kd_ds, nama)

Matakuliah (kd_mk, nama, sks)

JadwalMengajar (kd_ds, kd_mk, hari, jam, ruang)

KRSMahasiswa (nim, kd_mk, kd_ds, semester, nilai)
```
- Buat DDL Script berdasarkan skema ERD tersebut diatas. 
- Jalankan script DDL tersebut pada DBMS MySQL.

**Langkah-langkahnya :**

**1. Buat dulu script untuk table Mahasiswa :**

```
create table Mahasiswa (
    nim varchar(10) PRIMARY KEY,
    nama varchar(25) NOT NULL,
    jenis_kelamin ENUM('Laki-Laki', 'Perempuan'),
    tgl_lahir DATE,
    jalan varchar(15) NOT NULL,
    kota varchar(15) NOT NULL,
    kodepos varchar(5) NOT NULL,
    no_hp varchar(15) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```


![ss1](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/03e20de6-f4a2-481a-a666-c4f2c28bd085)


**Tampilkan hasil table :**

`desc Mahasiswa;`

![ss2](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/40377b1f-7698-45a3-b021-2d2115dd144c)



**2. Buat script untuk table Dosen :**
```
create table Dosen (
    kd_ds varchar(10) PRIMARY KEY,
    nama varchar(35) NOT NULL
    );
```

![ss3](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/16d8a9be-fd1a-408f-8a86-d1d94d79ec26)


**Tampilkan tabel :**

`desc Dosen;`
![ss4](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/4f584f75-3c53-4eb1-8737-80a3915c9029)


**3. Buat script untuk Mata kuliah :**
```
create table Matakuliah (
    kd_mk varchar(10) PRIMARY KEY,
    nama varchar(30) NOT NULL,
    sks INT NOT NULL
    );
```
![ss5](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/04c6ed4b-2e62-48ce-8017-5252079fc873)



**Tampilkan table :**

`desc Matakuliah;`

![ss6](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/a411c0bc-e5de-4792-a209-e03060070f21)


**4. Buat script untuk jadwal mengajar :**
```
create table JadwalMengajar (
    kd_ds varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    hari ENUM('Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu', 'Minggu') NOT NULL,
    jam TIME NOT NULL,
    ruang varchar(555) NOT NULL,
    PRIMARY KEY (kd_ds, kd_mk, hari, jam),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk)
    ); 
```
![ss7](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/05b8ef7f-c008-4467-9d61-b91252c980fb)



**Tampilkan table :**

`desc JadwalMengajar;`

![ss8](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/3a0c2731-a3c2-4a5f-9241-0205740c05ba)


**5. Buat script untuk KRSMahasiswa :**
```
CREATE TABLE KRSMahasiswa (
    nim varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    semester varchar(10) NOT NULL,
    nilai FLOAT NOT NULL,
    PRIMARY KEY (nim, kd_mk),
    FOREIGN KEY (nim) REFERENCES Mahasiswa(nim),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```
![ss9](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/75d59953-7f4d-411e-8a2b-41ac4e1042f6)


**Tampilkan table :**

`desc KRSMahasiswa;`

![ss10](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/672274cc-fc68-496f-90ef-bd2305e250eb)


# Soal Latihan Praktikum

Berdasarkan table Mahasiswa pada praktikum sebelumnya: (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

***Isi data pada table tersebut sebanyak minimal 5 record data. Tampilkan semua isi/record tabel!***

- Ubah data tanggal lahir Mahasiswa yang bernama Ari menjadi: 1979-08-31!

- Tampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja!

- Hapus Mahasiswa yang bernama Dina!

- Tampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita!

- Tampilkan data nama dan alamat Mahasiswa saja dari tabel tersebut

- Tampilkan data Mahasiswa terurut berdasarkan nama.

**1. Mengisi tabel dengan minimal 5 record data :**
```
insert into Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds) values 
-> (11223344,"ari santoso","Laki-laki","1998-10-12","","Bekasi","","",""), 
-> (11223345,"ario talib","Laki-laki","1999-11-16","","Cikarang","","",""), 
-> (11223346,"dina marlina","Perempuan","1997-12-01","","Karawang","","",""), 
-> (11223347,"lisa ayu","perempuan","1996-01-02","","Bekasi","","",""), 
-> (11223348,"tiara wahidah","perempuan","1980-02-05","","Bekasi","","",""), 
-> (11223349,"anton sinaga","laki-laki","1988-03-10","","Cikarang","","","");
```

![ss11](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/af48d668-3539-4387-a5d1-45dd82aa163c)


**2. Menampilkan semua isi/record pada tabel bisa menggunakan kode berikut :**

`select*from Mahasiswa;`

![ss12](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/948435d8-f7b3-4999-b4db-6448800dd280)


**3. Mengubah data tanggal lahir Mahasiswa yang bernama Ari menjadi : 1979-08-31 menggunakan kode berikut :**

`update Mahasiswa set tgl_lahir='1979-08-31' where nim=11223344;`

![ss13](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/f43c2082-9bf6-413c-ac05-07b19cec9f18)


**4. Menampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja dengan cara sebagai berikut :**

`select*from Mahasiswa where nim=11223344;`

![ss14](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/2f0a319b-ef85-46ee-b72b-5214452ffa85)


**5. Menghapus Mahasiswa yang bernama Dina dengan cara sebagai berikut:**

`delete from Mahasiswa where nim=11223346;`

![ss15](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/3608d38d-5d94-485f-b7f9-fdd9abcdc7e5)


**6. Menampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2 dengan cara sebagai berikut :**

`select*from Mahasiswa where tgl_lahir<='1996-1-2';`

![ss16](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/d2136905-c55e-4c0a-877f-c65d65a9755b)


**7. Menampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan dengan cara sebagai berikut :**

`select*from Mahasiswa where kota='bekasi' and jenis_kelamin='Perempuan';`

![ss17](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/301d7ac1-4ffa-4f80-9748-1ed36c54dc4f)


**8. Menampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita dengan cara sebagai berikut :**
```
select * from Mahasiswa where kota='Bekasi' and jenis_kelamin='Laki-laki' 
or tgl_lahir<='2002-4-22' 
and jenis_kelamin='Perempuan';
```

![ss18](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/a031802b-7cda-45b0-a2cf-04a6eb0f9767)


**9. Menampilkan data nama dan jalan Mahasiswa saja dari tabel tersebut dengan cara sebagai berikut :**

`select nama, jalan from Mahasiswa;`

![ss19](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/81b5d85a-40c0-4dd7-af97-3d04d38efffc)


**10. Menampilkan data Mahasiswa terurut berdasarkan nama dengan cara sebagai berikut :**

`select*from Mahasiswa -> order by nama asc;`

![ss20](https://github.com/Ws529/Basis-data-Pertemuan7/assets/147570983/c39e71fe-67b7-44ff-bd8f-b34ea619941b)


# Evaluasi dan Pertanyaan

***Tulis semua perintah-perintah SQL percobaan di atas beserta outputnya!***

**1. Menambah data :**

`INSERT INTO <table> (field1, ..., fieldn) VALUE (value1, ..., valuen)`

*Contoh :*

`INSERT INTO biodata (nim, nama, alamat) VALUE ('312310451','fadzar','Bekasi'),
('312310487', 'thanos sinaga', 'Jakarta');


**2. Menampilkan data :**

`SELECT * FROM <table> SELECT [field1, ..., fieldn] FROM <table>`

*Contoh :*

`SELECT*FROM biodata;`


**3. Mengubah data :**

`UPDATE <table> SET field1=val1, ..., fieldn=valn WHERE <kondisi>;`

*Contoh :*

UPDATE biodata SET nama='udap', alamat='planet lain' WHERE nim='312310487';


**4. Menghapus data :**

`DELETE FROM <table> WHERE <kondisi>`

*Contoh :*

DELETE FROM biodata WHERE nim='312310487';


***Apa bedanya penggunaan BETWEEN dan penggunaan operator >= dan <= ?***

- (misal: tgl_lahir BETWEEN '1990-10-10' AND '1992-10-11')

- (misal: tgl_lahir >= '1990-10-10' AND tgl_lahir <= '1992-10-11')

**Jawaban nya :**

Operator BETWEEN ini untuk menangani operasi “jangkauan” sedangkan operator >= dan <= termasuk pada operator relasional. Operator yang digunakan untuk perbandingan antara dua buah nilai. Jenis dari operator ini adalah: = , >, <, >=, <=, <>

***Berikan kesimpulan anda!***

Data Manipulation Language (DML) adalah bahasa pemrograman yang digunakan untuk mengakses, memanipulasi, dan mengelola data dalam sebuah database. DML memungkinkan pengguna untuk melakukan operasi seperti penyisipan data baru, pembaruan data yang sudah ada, penghapusan data, dan kueri data untuk pengambilan informasi yang diperlukan.

Dalam DML, pengguna dapat menggunakan perintah SQL (Structured Query Language) untuk mengakses data. SQL adalah bahasa standar untuk mengakses dan mengelola data dalam database relasional. Perintah SQL yang digunakan dalam DML termasuk menambah, mengubah, menghapus, dan menampilkan data seperti yang telah dipraktekkan diatas.




