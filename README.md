# Toko Buku API

- **Nama:** Naufal Rifqi Herliansyah
- **NIM:** 24 0504 0046
- **Program Studi:** Teknik Informatika, Universitas Muhammadiyah Magelang

REST API katalog buku (kategori dan buku) dengan Laravel. Praktikum Teknologi Web Service, Pertemuan 1 (RPS Pekan 9).

## Kebutuhan
- PHP 8.3+
- Composer

## Instalasi
```
git clone https://github.com/naufalambons-hue/toko-buku.git
cd toko-buku
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan serve
```
API berjalan di `http://127.0.0.1:8000/api`.

Di Windows (CMD), perintah `cp .env.example .env` diganti dengan `copy .env.example .env`.

## Aturan umum
- Kirim header `Accept: application/json` di setiap request.
- Data dikirim di dalam kunci `data`. Error punya `message`, error validasi punya `errors`.
- Status code: 200 berhasil, 201 data dibuat, 204 berhasil tanpa isi, 404 tidak ada, 409 bentrok dengan data lain, 422 input salah.

## Endpoint

| Method | URL | Keterangan | Status |
|--------|-----|------------|--------|
| GET | /api/categories | Daftar kategori | 200 |
| POST | /api/categories | Buat kategori | 201 / 422 |
| GET | /api/categories/{id} | Detail kategori | 200 / 404 |
| PUT | /api/categories/{id} | Ubah kategori | 200 / 422 |
| DELETE | /api/categories/{id} | Hapus kategori | 204 / 409 |
| GET | /api/books | Daftar buku | 200 |
| POST | /api/books | Buat buku | 201 / 422 |
| GET | /api/books/{id} | Detail buku | 200 / 404 |
| PUT | /api/books/{id} | Ubah buku (boleh sebagian) | 200 / 422 |
| DELETE | /api/books/{id} | Hapus buku | 204 |

## Contoh body

POST /api/categories
```json
{"name": "Novel"}
```

POST /api/books
```json
{
  "category_id": 1,
  "title": "Laskar Pelangi",
  "author": "Andrea Hirata",
  "isbn": "9789793062792",
  "price": 89000,
  "stock": 12,
  "description": "Novel tentang anak-anak Belitung"
}
```
`isbn` boleh kosong, tetapi jika diisi harus unik.

## Catatan
- Kategori tidak bisa dihapus selama masih ada bukunya (409).
- Tugas pertemuan ini: kolom `isbn` pada buku (migration, `$fillable`, validasi, dan `BookResource`).