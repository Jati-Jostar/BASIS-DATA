# BASIS-DATA
Iya, insting kamu bener: alurnya **ada yang kurang pas** dan ada yang **ketuker peran**. Tapi tenang, ini bukan salah fatal—cuma perlu dirapihin biar **Level 0 kamu masuk akal** dan nggak bikin dosen nyinyir.

## Yang bermasalah / kurang relevan

### 1) “Status barang” dari **Penyedia Estimasi Pengiriman** itu janggal

Kalau entitas ke-3 kamu namanya **penyedia estimasi**, mestinya dia ngurus:

* harga/ongkir
* estimasi waktu (ETA)

Bukan ngurus **status barang** (pickup, transit, delivered). Status itu biasanya datang dari **sistem tracking/logistik** (atau internal operasi pengiriman).

Kalau kamu tetap maksa penyedia estimasi ngirim “status barang”, dosen bisa nanya:

> “Kok sistem estimasi jadi tau posisi barang?”

Dan kamu bakal bengong.

✅ Solusi aman:

* Entitas ke-3 fokus **estimasi harga & waktu saja**.
* **Status barang** dikelola oleh sistem pengiriman sendiri (via Admin/operasional) atau entitas eksternal lain (Tracking/Carrier).
  Tapi karena kamu cuma mau 3 entitas, paling aman: **status diupdate oleh Admin**.

---

### 2) Admin cuma “cetak resi” itu terlalu kecil perannya

Di dunia nyata, admin/operasional biasanya:

* verifikasi order
* input/update status pengiriman
* (opsional) assign kurir, jadwal pickup
  Kalau admin cuma cetak resi, Admin jadi kayak tombol “Print” doang.

✅ Solusi:
Tambahkan aliran:

* **Admin → Sistem: Update status pengiriman**
* (opsional) **Admin → Sistem: Verifikasi/Proses order**

---

### 3) Customer “Check status barang” itu sebenernya bukan input data

Secara DFD, “check status” itu lebih tepat disebut:

* Customer mengirim **permintaan tracking (No resi)**
  lalu sistem balas status.

✅ Jadi flow-nya:

* Customer → Sistem: **Permintaan tracking (No resi)**
* Sistem → Customer: **Info status pengiriman**

---

## Versi alur Level 0 yang lebih rapi (masih 3 entitas)

### Customer → Sistem

1. **Data pengiriman** (pengirim, penerima, alamat, berat, layanan)
2. **Permintaan estimasi** (asal, tujuan, berat, layanan)
3. **Konfirmasi pesanan / permintaan pickup** (setuju estimasi)
4. **Permintaan tracking** (No resi)

### Sistem → Customer

1. **Hasil estimasi** (harga + estimasi waktu)
2. **Nomor resi / bukti order**
3. **Informasi status pengiriman**

---

### Sistem → Penyedia Estimasi Pengiriman

1. **Request estimasi** (asal, tujuan, berat/volume, layanan)

### Penyedia Estimasi Pengiriman → Sistem

1. **Estimasi harga & estimasi waktu (ETA/SLA)**

> Catatan: buang “status barang” dari entitas ini biar konsisten.

---

### Admin → Sistem

1. **Proses/validasi order** (opsional tapi bagus)
2. **Cetak resi**
3. **Update status pengiriman** (pickup, transit, delivered)

### Sistem → Admin

1. **Data pengiriman/order masuk**
2. **Status pengiriman terakhir / daftar pengiriman aktif**

---

## Kenapa ini lebih efektif?

* Setiap entitas punya kerja yang masuk akal:

  * Customer: input & minta info
  * Penyedia estimasi: hitung ongkir/ETA
  * Admin: operasional & update status
* Status barang jadi “milik” sistem operasional, bukan sistem estimasi
* Flow jadi gampang diturunkan ke Level 1

Kalau kamu mau, aku bisa bantu sekalian bikin **DFD Level 0 dalam format teks siap gambar** (proses tunggal + panah-panah), biar kamu tinggal gambar di Visio/draw.io tanpa salah arah.
