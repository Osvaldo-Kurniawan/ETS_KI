# DES Encryption/Decryption in C++

## Overview

Ini adalah implementasi algoritma **DES (Data Encryption Standard)** menggunakan bahasa **C++**. DES adalah algoritma cipher blok simetris yang digunakan untuk mengenkripsi dan mendekripsi blok data 64-bit menggunakan kunci 64-bit (56-bit efektif, 8-bit untuk parity).

Program ini menyediakan dua mode:
- **Mode interaktif**: input plaintext (a-z, 8 karakter) dan kunci heksadesimal 16 digit.
- **Mode default**: menggunakan plaintext `0123456789ABCDEF` dan key `133457799BBCDFF1`.

Fitur yang didukung:
- Konversi heksadesimal ke biner dan sebaliknya
- Pembuatan kunci (key schedule)
- Permutasi awal dan akhir
- Ekspansi (E), substitusi S-box, dan permutasi P
- Proses round Feistel (1 round atau bisa diubah ke 16)
- Dekripsi (menggunakan urutan kunci terbalik)

---

## Struktur File

- `main.cpp` - Source code utama untuk enkripsi dan dekripsi DES.

---

## Cara Kerja

### 1. Input Pesan & Kunci

- User dapat memasukkan 8 karakter plaintext (huruf kecil a-z).
- Setiap karakter dikonversi ke ASCII hex (contoh: `'a'` → `"61"`).
- Kunci harus 16 digit hex **uppercase** (misal: `133457799BBCDFF1`).

### 2. Key Scheduling

- Kunci 64-bit dikurangi menjadi 56-bit dengan **PC-1**.
- Kunci dibagi menjadi 2 bagian 28-bit.
- Rotasi dilakukan berdasarkan **rotating schedule**.
- **PC-2** digunakan untuk memilih 48-bit kunci per round.
- Untuk enkripsi: urutan normal.
- Untuk dekripsi: urutan dibalik.

### 3. Algoritma DES

Blok pesan 64-bit melalui proses berikut:

1. **Initial Permutation (IP)**
2. **16 Round Feistel** (hanya 1 round diaktifkan di kode):
    - Ekspansi (E) dari 32-bit → 48-bit
    - XOR dengan round key
    - Substitusi dengan 8 S-box (output 32-bit)
    - Permutasi (P-box)
    - Pertukaran (swap) L dan R
3. **Inverse Initial Permutation (IP⁻¹)**
4. Konversi ke bentuk heksadesimal

---

## Fitur

- Input dan output interaktif
- Enkripsi dan dekripsi
- Konversi biner ↔ heksadesimal
- Menampilkan hasil antar langkah:
  - Expanded message
  - Round keys
  - XOR result
  - Output S-box
  - Pesan permutasi
  - Hasil akhir

---

## Contoh Eksekusi

```text
Do you want to put plaintext?(y/n): y
Type the plain text 8 characters long(a to z): password
Enter the hex key (all upper case, type quit to quit) <16-bits>: 133457799BBCDFF1
Finally!! Hex Encrypted Message: 85E813540F0AB405
Want to see decryption?(y/n): y
Decryption Starts:
Finally!! DES Decrypted Hex Message: 70617373776F7264
Decrypted plain text is: password
