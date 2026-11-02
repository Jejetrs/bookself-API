# Bookshelf API

Bookshelf API adalah RESTful API sederhana untuk mengelola koleksi buku. API ini dibangun menggunakan Express.js dan Node.js sebagai submission project untuk kelas Back-End Developer Dicoding.

## 📋 Fitur

- ✅ Menambahkan buku baru
- ✅ Menampilkan semua buku
- ✅ Menampilkan detail buku berdasarkan ID
- ✅ Mengubah data buku berdasarkan ID
- ✅ Menghapus buku berdasarkan ID
- ✅ Filter buku berdasarkan nama, status reading, dan status finished

## 🛠️ Teknologi yang Digunakan

- **Node.js** - JavaScript runtime
- **Express.js v5** - Web framework
- **nanoid v5** - Generator ID unik
- **ESLint v9** - Linter untuk konsistensi kode

## 📦 Instalasi


### 1. Install Dependencies

```bash
npm install
```

```bash
npm init -y
```

Dependencies yang akan terinstall:
- `express` - Framework web
- `nanoid` - Untuk generate ID unik

```bash
npm install express nanoid
```

Dev Dependencies:
- `eslint` - Code linter
```bash
npm install --save-dev eslint
```

### 2. Konfigurasi (Opsional)

File `eslint.config.js` sudah dikonfigurasi dengan style guide dasar. Jika mengalami error line-ending di Windows, jalankan:

```bash
npx eslint . 
```

Jika error
```bash
npx eslint . --fix
```

## 🚀 Cara Menjalankan

### Development Mode

```bash
npm run start
```

### Production Mode

```bash
npm start
```

Server akan berjalan di `http://localhost:9000`

## 📡 API Endpoints

### 1. Menambahkan Buku

**Endpoint:** `POST /books`

**Request Body:**
```json
{
  "name": "string (required)",
  "year": "number",
  "author": "string",
  "summary": "string",
  "publisher": "string",
  "pageCount": "number",
  "readPage": "number",
  "reading": "boolean"
}
```

**Response Success (201):**
```json
{
  "status": "success",
  "message": "Buku berhasil ditambahkan",
  "data": {
    "bookId": "unique-id"
  }
}
```

**Response Fail (400):**
- Jika `name` tidak diisi:
```json
{
  "status": "fail",
  "message": "Gagal menambahkan buku. Mohon isi nama buku"
}
```

- Jika `readPage` > `pageCount`:
```json
{
  "status": "fail",
  "message": "Gagal menambahkan buku. readPage tidak boleh lebih besar dari pageCount"
}
```

### 2. Menampilkan Semua Buku

**Endpoint:** `GET /books`

**Query Parameters (Opsional):**
- `?name=string` - Filter berdasarkan nama (case-insensitive)
- `?reading=0/1` - Filter berdasarkan status reading
- `?finished=0/1` - Filter berdasarkan status finished

**Response Success (200):**
```json
{
  "status": "success",
  "data": {
    "books": [
      {
        "id": "unique-id",
        "name": "Buku A",
        "publisher": "Penerbit A"
      }
    ]
  }
}
```

### 3. Menampilkan Detail Buku

**Endpoint:** `GET /books/{bookId}`

**Response Success (200):**
```json
{
  "status": "success",
  "data": {
    "book": {
      "id": "unique-id",
      "name": "Buku A",
      "year": 2021,
      "author": "Author A",
      "summary": "Summary A",
      "publisher": "Publisher A",
      "pageCount": 100,
      "readPage": 50,
      "finished": false,
      "reading": true,
      "insertedAt": "2021-03-04T09:11:44.598Z",
      "updatedAt": "2021-03-04T09:11:44.598Z"
    }
  }
}
```

**Response Fail (404):**
```json
{
  "status": "fail",
  "message": "Buku tidak ditemukan"
}
```

### 4. Mengubah Data Buku

**Endpoint:** `PUT /books/{bookId}`

**Request Body:** (sama seperti POST /books)

**Response Success (200):**
```json
{
  "status": "success",
  "message": "Buku berhasil diperbarui"
}
```

**Response Fail:**
- 400: Validasi gagal (sama seperti POST)
- 404: ID tidak ditemukan

### 5. Menghapus Buku

**Endpoint:** `DELETE /books/{bookId}`

**Response Success (200):**
```json
{
  "status": "success",
  "message": "Buku berhasil dihapus"
}
```

**Response Fail (404):**
```json
{
  "status": "fail",
  "message": "Buku gagal dihapus. Id tidak ditemukan"
}
```

## 🧪 Testing

### Menggunakan Postman

1. Download Postman Collection & Environment dari Dicoding
2. Import kedua file ke Postman
3. Jalankan server: `npm start`
4. Run collection untuk testing otomatis

### Menggunakan cURL

**Tambah Buku:**
```bash
curl -X POST http://localhost:9000/books \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Buku Test",
    "year": 2024,
    "author": "Penulis Test",
    "summary": "Ringkasan buku test",
    "publisher": "Penerbit Test",
    "pageCount": 100,
    "readPage": 50,
    "reading": true
  }'
```

**Lihat Semua Buku:**
```bash
curl http://localhost:9000/books
```

## 📝 Code Quality

### Menjalankan ESLint

```bash
npx eslint .
```

### Auto-fix ESLint Issues

```bash
npx eslint . --fix
```

## 📁 Struktur Project

```
bookshelf-api/
├── src/
│   ├── server.js       # Entry point aplikasi
│   ├── routes.js       # Definisi routes
│   └── books.js        # Handler untuk CRUD buku
├── node_modules/
├── package.json
├── eslint.config.js
└── README.md
```

## 🔧 Konfigurasi

### package.json Scripts

- `start` - Menjalankan aplikasi (production)
- `start-dev` - Menjalankan aplikasi dengan nodemon (development)
- `lint` - Menjalankan ESLint

### Port

Aplikasi berjalan di **port 9000** secara default. Untuk mengubah port, edit file `src/server.js`:

```javascript
const PORT = 9000;
```

## 📌 Catatan Penting

- ⚠️ Data disimpan dalam **memory (array)**, bukan database
- ⚠️ Data akan **hilang** ketika server di-restart
- ✅ Tidak menggunakan database eksternal (sesuai requirement submission)
- ✅ Menggunakan ES Module (`"type": "module"` di package.json)

## 👨‍💻 Author

Dibuat sebagai submission project untuk kelas Back-End Developer di Dicoding Indonesia.

## 📄 License

ISC

## 🙏 Acknowledgments

- Dicoding Indonesia - Platform pembelajaran
- Express.js - Web framework
- nanoid - ID generator library