# praktikum_3
# Tugas Praktikum { Pertemuan ke 10 } <img src=https://qph.fs.quoracdn.net/main-qimg-648763cc041459725b62108f4fdf5b91 width="110px" >

|**Nama**|**NIM**|**Kelas**|**Matkul**|
|----|---|-----|------|
|Fadzar Surya Wijaya|312310451|TI.23.A5|Basis Data|


# Soal Latihan Praktikum

1. Lakukan penambahan data pada tabel mahasiswa dengan mengisi kd_ds yang belum ada pada data dosen.
dengan menggunakan kode berikut :
```
INSERT INTO dosen (kd_ds, nama) VALUES
('DS001', 'Fajar'),
('DS002', 'Arif'),
('DS003', 'Bagus'),
('DS004', 'Wahyu'),
('DS005', 'Ridho');
```
![alt text](Picture/6.PNG)

***Output :***

![alt text](Picture/6.1.PNG)

2. Hapus satu record data pada tabel dosen yang telah dirujuk pada tabel mahasiswa. 
```
DELETE FROM dosen WHERE kd_ds = 'DS005';
```
***Output :***

![alt text](Picture/7.PNG)

3. Ubah mode menjadi **ON UPDATE CASCADE ON DELETE RESTRICT** 

Untuk mengubah CONSTRAINT FOREIGN KEY menjadi **ON UPDATE CASCADE** dan **ON DELETE RESTRICT**, Anda perlu menambahkan CONSTRAINT dengan opsi yang diinginkan. Berikut adalah langkah-langkahnya:

Tambahkan CONSTRAINT FOREIGN KEY dengan opsi ON UPDATE CASCADE dan ON DELETE RESTRICT:
```
ALTER TABLE mahasiswa
ADD CONSTRAINT fk_dosen
FOREIGN KEY (kd_ds)
REFERENCES dosen (kd_ds)
ON UPDATE CASCADE
ON DELETE RESTRICT;
```
***Output :***

![alt text](Picture/8.PNG)

4. Lakukan perubahan data pada tabel dosen (kd_ds)

Berikut adalah contoh perintah untuk melakukan perubahan data pada tabel "dosen" dengan kolom "kd_ds":
```
UPDATE dosen SET kd_ds = 'DS005' WHERE nama = 'Wahyu';
```
Perintah di atas akan mengubah nilai kolom `"kd_ds" "Wahyu" menjadi "DS005" pada tabel "dosen"`. Anda dapat menyesuaikan nilai yang ingin Anda ubah dan kondisi WHERE sesuai dengan kebutuhan Anda.

Pastikan untuk menjalankan perintah dengan hati-hati dan memastikan bahwa perubahan data yang Anda lakukan sesuai dengan kebutuhan dan kebijakan yang berlaku dalam basis data Anda.

***Output :***

![alt text](Picture/9.PNG)

5. Lakukan penghapusan data pada tabel dosen

Untuk menghapus data dari tabel "dosen" dengan kondisi "kd_ds = 'DS005'", Anda dapat menggunakan perintah DELETE dengan sintaks yang benar. Berikut adalah contoh perintah yang dapat Anda gunakan:
```
DELETE FROM Dosen WHERE kd_ds = 'DS005';
```

***Output :***

![alt text](Picture/10.PNG)

6. Ubah mode menjadi **ON UPDATE CASCADE ON DELETE SET NULL**
```
ALTER TABLE mahasiswa
DROP FOREIGN KEY fk_dosen;
```
```
ALTER TABLE mahasiswa
ADD CONSTRAINT fk_dosen
FOREIGN KEY (kd_ds)
REFERENCES dosen (kd_ds)
ON DELETE SET NULL;
```
***Output :***

![alt text](Picture/11.PNG)

Dengan perubahan di atas, ketika Anda menghapus record dari tabel "dosen" yang memiliki referensi di tabel "mahasiswa", nilai kolom "kd_ds" dalam tabel "mahasiswa" yang mengacu pada record yang dihapus akan diatur menjadi NULL.

Setelah menjalankan perintah di atas, Anda dapat kembali mencoba menghapus record dengan menggunakan perintah berikut:

7. Lakukan penghapusan data pada tabel dosen
```
DELETE FROM dosen WHERE kd_ds = 'DS003';
```
***0utput :***

![alt text](Picture/12.PNG)

![alt text](Picture/12.1.PNG)

Perintah ini akan menghapus record dengan nilai "DS003" dari tabel "dosen", dan karena menggunakan opsi ON DELETE SET NULL, nilai kolom "kd_ds" dalam tabel "mahasiswa" yang mengacu pada record yang dihapus akan diatur menjadi NULL.

# Evaluasi dan Pertanyaan

### Tulis semua perintah-perintah SQL percobaan di atas beserta outputnya!

- Membuat foreign key

Dalam ALTER TABLE:
```
ALTER TABLE mahasiswa
ADD CONSTRAINT fk_dosen
FOREIGN KEY (kd_ds) REFERENCES dosen(kd_ds)
```

Dalam CREATE TABLE:
```
CREATE TABLE mahasiswa(
nim VARCHAR(10) NOT NULL,
nama VARCHAR(100) NOT NULL,
kd_ds VARCHAR(10),
PRIMARY KEY(nim),
CONSTRAINT fk_Dosen FOREIGN KEY (kd_ds)
REFERENCES dosen(kd_ds)
);
```

- Mengubah data
```
UPDATE mahasiswa
SET kd_ds = 'DS001' WHERE nim = 112233445;
```

- Menampilkan CREATE TABLE
```
SHOW CREATE TABLE  mahasiswa;
Mode ON UPDATE CASCADE ON DELETE CASCADE
```
```
ALTER TABLE mahasiswa
DROP FOREIGN KEY fk_mahasiswa_dosen,
ADD CONSTRAINT fk_dosen FOREIGN KEY (kd_ds) REFERENCES dosen(kd_ds) ON UPDATE CASCADE ON DELETE CASCADE;
```

- Menghapus data
```
DELETE FROM dosen WHERE kd_ds = 'DS001';
Mode ON UPDATE CASCADE ON DELETE NOT NULL
```
```
ALTER TABLE <table>
DROP FOREIGN KEY <nama_constraint_lama>,
ADD CONSTRAINT <nama_constraint_baru> FOREIGN KEY (field) REFERENCES <table_references(filed_references)> ON UPDATE CASCADE ON DELETE NOT NULL;
```

- Mengubah data
```
UPDATE dosen
SET kd_ds = 'DS006' WHERE nama = 'Haha Hihi';
```

- Menghapus data
```
DELETE FROM dosen WHERE nim = 'DS003';
```

### Apa bedanya penggunaan RESTRICT dan penggunaan CASCADE

- **RESTRICT:** Ketika Anda menggunakan opsi RESTRICT, itu berarti bahwa tindakan penghapusan atau pembaruan yang Anda lakukan akan ditolak jika ada data yang memiliki hubungan referensial dengan data yang akan dihapus atau diperbarui. Dengan kata lain, RESTRICT menghentikan tindakan tersebut jika menyebabkan konflik referensial. Misalnya, jika Anda mencoba menghapus sebuah baris dalam tabel yang memiliki anak-anak yang terhubung melalui kunci asing, operasi penghapusan akan ditolak jika ada ketergantungan referensial yang berlaku. RESTRICT secara efektif membatasi tindakan Anda agar tidak merusak integritas referensial dalam basis data.

- **CASCADE:** Sebaliknya, ketika Anda menggunakan opsi CASCADE, itu berarti bahwa tindakan penghapusan atau pembaruan yang Anda lakukan akan mempengaruhi semua data yang memiliki hubungan referensial dengan data yang dihapus atau diperbarui. Dengan kata lain, CASCADE akan melakukan tindakan yang sama pada data yang terkait. Misalnya, jika Anda menghapus sebuah baris dalam tabel yang memiliki anak-anak yang terkait melalui kunci asing dengan opsi CASCADE, operasi penghapusan akan mempengaruhi tidak hanya baris yang dihapus tetapi juga semua baris anak yang terkait secara rekursif. Hal ini berguna ketika Anda ingin menghapus semua data terkait dengan entitas utama atau memperbarui nilai di semua tempat yang menggunakan entitas tersebut.

Dalam banyak kasus, pemilihan antara `RESTRICT dan CASCADE `tergantung pada kebutuhan bisnis dan hubungan data dalam basis data. Jika Anda ingin memastikan integritas referensial dan mencegah tindakan yang dapat merusak data, Anda dapat menggunakan RESTRICT. Namun, jika Anda ingin melakukan tindakan yang berdampak luas pada data yang terkait, Anda dapat menggunakan CASCADE.

### Berikan Kesimpulan anda !

- SQL Constraint digunakan untuk menentukan aturan untuk data dalam tabel.

  - Constraint digunakan untuk membatasi jenis data yang bisa masuk ke tabel. Ini memastikan keakuratan dan keandalan data dalam tabel.

  - Constraint dapat berupa level kolom atau level tabel.

  - Constraint level kolom berlaku untuk kolom, dan batasan level tabel berlaku untuk seluruh tabel.

- **RESTRICT** membatasi tindakan penghapusan atau pembaruan jika ada ketergantungan referensial yang akan terganggu. Ini menjaga integritas referensial dalam basis data.

- **CASCADE** melakukan tindakan yang sama pada data yang terkait. Jika Anda menghapus atau memperbarui data, CASCADE akan mempengaruhi semua data terkait, termasuk data anak yang terhubung secara rekursif.  


# Tugas pada Praktikum 2:
• Buat DDL Script berdasarkan skema ERD tersebut diatas.
• Jalankan script DDL tersebut pada DBMS MySQL.

```
Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

Dosen (kd_ds, nama)

Matakuliah (kd_mk, nama, sks)

JadwalMengajar (kd_ds, kd_mk, hari, jam, ruang)

KRSMahasiswa (nim, kd_mk, kd_ds, semester, nilai)
```

**Langkah-langkahnya :**

1. Buat dulu script untuk table Mahasiswa :
![alt text](Picture/1.PNG)

2. Buat Index Key
![alt text](Picture/index.PNG)

3. Buat Foreign Key
![alt text](Picture/foreign.PNG)

4. Buat Tabel Dosen
![alt text](Picture/2.PNG)

**output**

![alt text](Picture/2.1.PNG)

5. Buat Tabel Mata Kuliah
![alt text](Picture/3.PNG)

**output**

![alt text](Picture/3.1.PNG)

6. Buat Tabel Jadwal Mengajar
![alt text](Picture/4.PNG)

**output**

![alt text](Picture/4.1.PNG)

7. Buat Tabel KRSMahasiswa
![alt text](Picture/5.PNG)

**output**

![alt text](Picture/5.1.PNG)


## FINISH
