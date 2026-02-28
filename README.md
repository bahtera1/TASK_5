# E-Commerce Catalog

Aplikasi katalog e-commerce yang dibangun menggunakan **Vue.js 2** dan terintegrasi dengan **Fake Store API**. Menampilkan produk fashion dengan tampilan dinamis yang berubah sesuai kategori produk.

## Preview

| Men Section | Women Section | Unavailable |
|-------------|---------------|-------------|
| Background biru | Background pink | Background abu-abu |
| Produk men's clothing | Produk women's clothing | Produk non-fashion |

## Fitur

- Fetch produk dari Fake Store API (20 produk)
- 3 tampilan dinamis: Men Section, Women Section, Unavailable
- Class binding otomatis berdasarkan kategori produk
- Tombol Next Product dengan increment index (reset setelah 20)
- Rating visual dengan dot indicator
- Loading skeleton saat fetch data
- Responsive design
- Lazy loading gambar
- Hover effect pada card

## Tech Stack

- **Framework:** Vue.js 2
- **Styling:** Vanilla CSS
- **API:** [Fake Store API](https://fakestoreapi.com)
- **Tools:** Vue CLI, Node.js

## Struktur Project

```
src/
├── assets/
│   └── page.css               # Styling global, tema warna, skeleton
├── components/
│   └── ProductDisplay.vue     # Komponen card produk & unavailable
├── App.vue                    # Logic utama, API call, class binding
└── main.js                    # Entry point
```

## Cara Menjalankan

```bash
# Install dependencies
npm install

# Jalankan development server
npm run serve

# Build untuk production
npm run build
```

Buka `http://localhost:8080` di browser.

## Alur Kerja

1. Halaman dibuka → `mounted()` → fetch produk index 1
2. Cek kategori:
   - `men's clothing` → tampilkan card + tema biru
   - `women's clothing` → tampilkan card + tema pink
   - Lainnya → tampilkan halaman unavailable + tema abu-abu
3. User klik "Next product" → index + 1 → fetch ulang
4. Index > 20 → reset ke 1

## API

Endpoint: `https://fakestoreapi.com/products/{id}`

ID 1–20 mencakup kategori:
- men's clothing (1–4)
- jewelery (5–8)
- electronics (9–14)
- women's clothing (15–20)

## Author

**Naufal Assani Saputra**
- GitHub: [@bahtera1](https://github.com/bahtera1)
- LinkedIn: [naufal-assani](https://www.linkedin.com/in/naufal-assani)
