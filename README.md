# 🛍️ VIX E-Commerce Product Display

Aplikasi e-commerce sederhana yang dibangun menggunakan **Vue.js 3** dengan **Options API** dan **Vanilla CSS**. Aplikasi ini menampilkan produk satu per satu dari FakeStore API dengan tema warna berbeda berdasarkan kategori produk.

---

## 📋 Daftar Isi

- [Tentang Proyek](#-tentang-proyek)
- [Fitur Utama](#-fitur-utama)
- [Teknologi yang Digunakan](#-teknologi-yang-digunakan)
- [Struktur Folder](#-struktur-folder)
- [Instalasi dan Menjalankan Proyek](#-instalasi-dan-menjalankan-proyek)
- [Penggunaan API](#-penggunaan-api)
- [Theming Berdasarkan Kategori](#-theming-berdasarkan-kategori)
- [Komponen dan Penjelasan Kode](#-komponen-dan-penjelasan-kode)
- [CSS Variables](#-css-variables)
- [Responsive Design](#-responsive-design)
- [Screenshot](#-screenshot)

---

## 📖 Tentang Proyek

Proyek ini merupakan bagian dari **VIX Front End Core Initiative** yang bertujuan untuk membangun interface e-commerce sederhana. Aplikasi menampilkan produk dari FakeStore API dengan fitur:

- Menampilkan satu produk pada satu waktu
- Navigasi ke produk berikutnya dengan tombol "Next Product"
- Tema warna yang berbeda untuk setiap kategori produk
- Loading spinner saat mengambil data dari API
- Desain responsif untuk desktop dan mobile

---

## ✨ Fitur Utama

| Fitur                      | Deskripsi                                                                                                       |
| -------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Product Display**        | Menampilkan detail produk termasuk gambar, judul, kategori, rating, deskripsi, dan harga                        |
| **Category-Based Theming** | Warna tema berbeda untuk Men's Clothing (biru), Women's Clothing (pink/ungu), dan Unavailable Product (abu-abu) |
| **Loading State**          | Loading spinner yang ditampilkan di dalam product card saat fetch data                                          |
| **Product Navigation**     | Tombol "Next Product" untuk berpindah ke produk berikutnya dengan cycling (20 → 1)                              |
| **Unavailable Products**   | Tampilan khusus untuk produk non-clothing (Electronics, Jewelry) dengan icon sad face                           |
| **Responsive Design**      | Tampilan yang optimal untuk desktop dan mobile                                                                  |
| **Decorative Pattern**     | Pola dekoratif SVG pada background untuk kategori clothing                                                      |

---

## 🛠️ Teknologi yang Digunakan

- **Frontend Framework**: Vue.js 3 (Options API)
- **Build Tool**: Vue CLI 5
- **Styling**: Vanilla CSS dengan CSS Variables
- **API**: [FakeStore API](https://fakestoreapi.com/)
- **Package Manager**: npm
- **Linting**: ESLint dengan plugin Vue

### Dependencies

```json
{
  "dependencies": {
    "core-js": "^3.8.3",
    "vue": "^3.2.13"
  },
  "devDependencies": {
    "@babel/core": "^7.12.16",
    "@babel/eslint-parser": "^7.12.16",
    "@vue/cli-plugin-babel": "~5.0.0",
    "@vue/cli-plugin-eslint": "~5.0.0",
    "@vue/cli-service": "~5.0.0",
    "eslint": "^7.32.0",
    "eslint-plugin-vue": "^8.0.3"
  }
}
```

---

## 📁 Struktur Folder

```
ecommerce/
├── public/
│   ├── favicon.ico
│   └── index.html
├── src/
│   ├── assets/
│   │   ├── style/
│   │   │   └── page.css          # File CSS utama dengan semua styling
│   │   ├── bg-pattern.svg        # Pola dekoratif untuk background
│   │   └── sad-face.svg          # Icon sad face untuk unavailable product
│   ├── components/
│   │   └── ProductDisplay.vue    # Komponen utama untuk menampilkan produk
│   ├── App.vue                   # Root component
│   └── main.js                   # Entry point aplikasi
├── .gitignore
├── babel.config.js
├── jsconfig.json
├── package.json
├── README.md
└── vue.config.js
```

---

## 🚀 Instalasi dan Menjalankan Proyek

### Prasyarat

- Node.js (versi 14 atau lebih baru)
- npm (Node Package Manager)

### Langkah Instalasi

1. **Clone atau download repository**

   ```bash
   cd TASK_5/ecommerce
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Jalankan development server**

   ```bash
   npm run serve
   ```

4. **Buka browser**

   Akses aplikasi di: `http://localhost:8080`

### Build untuk Production

```bash
npm run build
```

Hasil build akan tersedia di folder `dist/`.

### Linting

```bash
npm run lint
```

---

## 🌐 Penggunaan API

Aplikasi ini menggunakan **FakeStore API** untuk mengambil data produk.

### Endpoint yang Digunakan

```
GET https://fakestoreapi.com/products/{id}
```

- `{id}`: Index produk (1-20)

### Contoh Response API

```json
{
  "id": 1,
  "title": "Fjallraven - Foldsack No. 1 Backpack",
  "price": 109.95,
  "description": "Your perfect pack for everyday use...",
  "category": "men's clothing",
  "image": "https://fakestoreapi.com/img/81fPKd-2AYL._AC_SL1500_.jpg",
  "rating": {
    "rate": 3.9,
    "count": 120
  }
}
```

### Kategori Produk

| ID    | Kategori         |
| ----- | ---------------- |
| 1-4   | Men's Clothing   |
| 5-8   | Jewelry          |
| 9-14  | Electronics      |
| 15-20 | Women's Clothing |

---

## 🎨 Theming Berdasarkan Kategori

Aplikasi menerapkan tema warna yang berbeda berdasarkan kategori produk:

### 1. Men's Clothing (Biru)

- **Background**: `#D6E6FF` (light blue)
- **Accent Color**: `#002772` (navy)
- **Pola Dekoratif**: Aktif

### 2. Women's Clothing (Pink/Ungu)

- **Background**: `#FDE2FF` (light pink)
- **Accent Color**: `#720060` (purple)
- **Pola Dekoratif**: Aktif

### 3. Unavailable Products (Abu-abu)

Produk dengan kategori **Electronics** dan **Jewelry** ditampilkan sebagai "Unavailable":

- **Background**: `#DCDCDC` (gray)
- **Pola Dekoratif**: Nonaktif
- **Tampilan**: Icon sad face dengan pesan "This product is unavailable to show"

### 4. Loading State

- **Background**: `#DCDCDC` (gray)
- **Pola Dekoratif**: Nonaktif
- **Tampilan**: Loading spinner di tengah card

---

## 📦 Komponen dan Penjelasan Kode

### 1. ProductDisplay.vue

Komponen utama yang menangani semua logika dan tampilan produk.

#### Data Properties

```javascript
data() {
  return {
    productIndex: 1,    // Index produk saat ini (1-20)
    product: null,      // Data produk dari API
    isLoading: true,    // Status loading
    maxIndex: 20,       // Maksimal index produk
  };
}
```

#### Computed Properties

| Property            | Deskripsi                                              |
| ------------------- | ------------------------------------------------------ |
| `isClothingProduct` | Mengecek apakah produk adalah clothing (men's/women's) |
| `categoryClass`     | Mengembalikan CSS class berdasarkan kategori produk    |
| `containerClass`    | Mengembalikan CSS class untuk background container     |

#### Methods

| Method           | Deskripsi                                                       |
| ---------------- | --------------------------------------------------------------- |
| `fetchProduct()` | Mengambil data produk dari API berdasarkan `productIndex`       |
| `nextProduct()`  | Increment `productIndex` dan fetch produk baru (cycling 20 → 1) |

#### Lifecycle Hook

```javascript
mounted() {
  this.fetchProduct();  // Fetch produk pertama saat komponen dimuat
}
```

### 2. App.vue

Root component yang mengimport dan merender `ProductDisplay` serta file CSS global.

```vue
<template>
  <ProductDisplay />
</template>

<script>
import ProductDisplay from "./components/ProductDisplay.vue";
import "./assets/style/page.css";

export default {
  name: "App",
  components: {
    ProductDisplay,
  },
};
</script>
```

---

## 🎯 CSS Variables

Semua warna dan nilai desain disimpan dalam CSS Variables untuk kemudahan maintenance:

```css
:root {
  /* Primary Colors */
  --color-navy: #002772;
  --color-purple: #720060;

  /* Background Colors */
  --color-pink-bg: #fde2ff;
  --color-blue-bg: #d6e6ff;
  --color-gray-bg: #dcdcdc;

  /* Neutral Colors */
  --color-black: #1e1e1e;
  --color-gray-dark: #3f3f3f;
  --color-gray-light: #dcdcdc;
  --color-white: #ffffff;

  /* Shadows */
  --shadow-card: 0 4px 4px rgba(0, 0, 0, 0.25);
  --shadow-button: 0 4px 15px rgba(0, 0, 0, 0.15);

  /* Border Radius */
  --radius-card: 10px;
  --radius-button: 4px;
  --radius-image: 12px;

  /* Transitions */
  --transition-fast: 0.2s ease;
  --transition-normal: 0.3s ease;
}
```

---

## 📱 Responsive Design

Aplikasi mendukung tampilan responsif dengan breakpoint berikut:

### Desktop (≥ 768px)

- Product card menggunakan layout horizontal (flex-row)
- Gambar di sebelah kiri, detail di sebelah kanan
- Padding lebih besar (40px)

### Mobile (< 480px)

- Product card menggunakan layout vertikal (flex-column)
- Gambar di atas, detail di bawah
- Padding lebih kecil (20px)
- Tombol menggunakan full width
- Font size yang lebih kecil

### Spesifikasi Card (dari Figma)

| Property      | Nilai                      |
| ------------- | -------------------------- |
| Width         | 1034px (max)               |
| Min Height    | 580px                      |
| Border Radius | 10px                       |
| Box Shadow    | 0 4px 4px rgba(0,0,0,0.25) |

---

## 👨‍💻 Dibuat Oleh

**Komara Indra Putra**

Project Based Intern - Front End Developer - Core Initiative X Rakamin Academy

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan pembelajaran dan bootcamp.
