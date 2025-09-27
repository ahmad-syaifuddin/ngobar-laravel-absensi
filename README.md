# 🚀 Panduan Instalasi Lengkap Laravel Attendance System

## 📋 Overview Project
- **Nama Aplikasi**: `el_presence` atau sesuaikan dengan kemauan kalian misal KalselAttendanceSystem
- **Framework**: Laravel 10
- **Auth**: Laravel Breeze 1.19
- **Styling**: Tailwind CSS 4.1 
- **Icons**: Font Awesome
- **Database**: MySQL
- **Server**: Laragon

---

## 🛠️ Step 1: Persiapan Environment

### Install Laragon
1. Download Laragon dari [https://laragon.org/download/](https://laragon.org/download/)
2. Install dengan setting default
3. Jalankan Laragon sebagai Administrator
4. Klik **Start All** untuk nyalain Apache & MySQL

### Cek Versi yang Dibutuhkan
Buka terminal di Laragon (klik kanan icon Laragon > Terminal):

```bash
# Cek PHP (harus 8.1+)
php -v

# Cek Composer
composer -V

# Cek Node.js (harus 16+)
node -v

# Cek NPM
npm -v
```

> 💡 **Tips**: Kalau ada yang belum terinstall, download manual atau update via Laragon menu.

---

## 🏗️ Step 2: Buat Project Laravel Baru

### 2.1 Buat Project Laravel 10
```bash
# Pindah ke folder www laragon (biasanya C:\laragon\www)
cd C:\laragon\www

# Buat project baru
composer create-project laravel/laravel el_presence "10.*"

# Masuk ke folder project
cd KalselAttendanceSystem
```

### 2.2 Setup Database
1. Buka phpMyAdmin di browser: `http://localhost/phpmyadmin`
2. Buat database baru: `el_presence`
3. Edit file `.env`:

```env
APP_NAME="El Presence System"
APP_ENV=local
APP_KEY=base64:your-app-key-here
APP_DEBUG=true
APP_URL=http://el-presence.test

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=el_presence
DB_USERNAME=root
DB_PASSWORD=
```

### 2.3 Generate App Key
```bash
php artisan key:generate
```

---

## 🔐 Step 3: Install Laravel Breeze

### 3.1 Install Breeze
```bash
# Install breeze versi 1.19
composer require laravel/breeze:^1.19 --dev

# Install breeze dengan blade
php artisan breeze:install blade

# Install dependencies
npm install
```

### 3.2 Migrate Database
```bash
php artisan migrate
```

### 3.3 Buat User Admin Dummy
```bash
php artisan tinker
```

Di dalam tinker, ketik:
```php
App\Models\User::create([
    'name' => 'Admin System',
    'email' => 'admin@gmail.com', 
    'password' => bcrypt('password')
]);
exit
```

---

## 🎨 Step 4: Upgrade ke Tailwind CSS 4.1

### 4.1 Hapus Tailwind v3 (Bawaan Breeze)
```bash
# Uninstall paket lama
npm uninstall tailwindcss postcss autoprefixer @tailwindcss/forms

# Hapus config files
rm -f tailwind.config.js postcss.config.js
```

### 4.2 Install Tailwind v4.1 & Font Awesome
```bash
# Install Tailwind v4
npm install @tailwindcss/cli@next

# Install Font Awesome
npm install @fortawesome/fontawesome-free
```

### 4.3 Update CSS File
Edit `resources/css/app.css` dan replace semua isinya dengan:

```css
@import "tailwind";
@import "@fortawesome/fontawesome-free/css/all.css";

/* Custom styles bisa ditambahin di bawah ini */
body {
    font-family: 'Inter', sans-serif;
}
```

### 4.4 Update Vite Config
Edit `vite.config.js`:

```javascript
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';

export default defineConfig({
    plugins: [
        laravel({
            input: [
                'resources/css/app.css',
                'resources/js/app.js',
            ],
            refresh: true,
        }),
    ],
});
```

---

## 📦 Step 5: Install Extra Packages

### 5.1 Install Packages via Composer
```bash
# Excel export
composer require maatwebsite/excel

# PDF export  
composer require barryvdh/laravel-dompdf
```

### 5.2 Install JavaScript Packages
```bash
# SweetAlert2 untuk notifikasi keren
npm install sweetalert2
```

### 5.3 Update JavaScript (Optional)
Edit `resources/js/app.js` dan tambahkan:

```javascript
import './bootstrap';
import Alpine from 'alpinejs';
import Swal from 'sweetalert2';

// Make SweetAlert2 global
window.Swal = Swal;

window.Alpine = Alpine;
Alpine.start();
```

---

## 🚀 Step 6: Jalankan Project

### 6.1 Build Assets
```bash
# Development mode (auto-reload)
npm run dev
```

Biarkan terminal ini tetap jalan! Buka terminal baru untuk step berikutnya.

### 6.2 Jalankan Laravel Server

**Opsi 1: Pakai Artisan Serve**
```bash
php artisan serve
```
Project akan jalan di: `http://127.0.0.1:8000`

**Opsi 2: Pakai Laragon (Recommended)**
1. Buka Laragon
2. Klik kanan icon Laragon > **Apache** > **Sites Directory**
3. Pastikan folder `el_presence` ada di sana
4. Restart Laragon
5. Buka browser ke: `http://el-presence.test`

---

## 🧪 Step 7: Testing & Verifikasi

### 7.1 Test Basic Laravel
Buka browser ke URL project kamu, seharusnya muncul welcome page Laravel.

### 7.2 Test Authentication
1. Klik **Register** atau **Login**
2. Login pakai admin yang udah dibuat:
   - Email: `admin@gmail.com`
   - Password: `password`

### 7.3 Test Tailwind & Font Awesome
Buat test page simple. Edit `resources/views/dashboard.blade.php`:

```html
<x-app-layout>
    <x-slot name="header">
        <h2 class="font-semibold text-xl text-gray-800 leading-tight">
            <i class="fas fa-tachometer-alt mr-2"></i>
            {{ __('Dashboard') }}
        </h2>
    </x-slot>

    <div class="py-12">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
            <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                <div class="p-6 text-gray-900">
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                        <!-- Card 1 -->
                        <div class="bg-blue-500 text-white p-6 rounded-lg shadow-lg">
                            <div class="flex items-center">
                                <i class="fas fa-users text-3xl mr-4"></i>
                                <div>
                                    <h3 class="text-lg font-semibold">Total Karyawan</h3>
                                    <p class="text-2xl font-bold">150</p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Card 2 -->
                        <div class="bg-green-500 text-white p-6 rounded-lg shadow-lg">
                            <div class="flex items-center">
                                <i class="fas fa-check-circle text-3xl mr-4"></i>
                                <div>
                                    <h3 class="text-lg font-semibold">Hadir Hari Ini</h3>
                                    <p class="text-2xl font-bold">145</p>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Card 3 -->
                        <div class="bg-red-500 text-white p-6 rounded-lg shadow-lg">
                            <div class="flex items-center">
                                <i class="fas fa-times-circle text-3xl mr-4"></i>
                                <div>
                                    <h3 class="text-lg font-semibold">Tidak Hadir</h3>
                                    <p class="text-2xl font-bold">5</p>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Test SweetAlert Button -->
                    <div class="mt-6">
                        <button onclick="testSweetAlert()" 
                                class="bg-purple-500 hover:bg-purple-700 text-white font-bold py-2 px-4 rounded">
                            <i class="fas fa-bell mr-2"></i>
                            Test SweetAlert
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        function testSweetAlert() {
            Swal.fire({
                title: 'Berhasil!',
                text: 'SweetAlert2 sudah berjalan dengan baik!',
                icon: 'success',
                confirmButtonText: 'OK'
            });
        }
    </script>
</x-app-layout>
```

---

## 🐛 Troubleshooting - Error yang Sering Muncul

### Error 1: `npm run dev` gagal
**Solusi:**
```bash
# Clear cache
npm cache clean --force

# Install ulang
rm -rf node_modules package-lock.json
npm install
npm run dev
```

### Error 2: Migration Error
**Solusi:**
```bash
# Reset database
php artisan migrate:fresh

# Kalau masih error, cek koneksi database di .env
```

### Error 3: Class 'App\Models\User' not found
**Solusi:**
```bash
# Clear cache
php artisan cache:clear
php artisan config:clear
composer dump-autoload
```

### Error 4: Tailwind classes tidak muncul
**Solusi:**
1. Pastikan `npm run dev` masih jalan
2. Hard refresh browser (Ctrl+Shift+R)
3. Cek file `resources/css/app.css` sudah benar

### Error 5: Font Awesome icons tidak muncul
**Solusi:**
```bash
# Install ulang Font Awesome
npm uninstall @fortawesome/fontawesome-free
npm install @fortawesome/fontawesome-free

# Restart dev server
npm run dev
```

---

## 🎉 Selamat!

Kalau semua step di atas berhasil, berarti project Laravel Attendance System kamu udah siap! 

**Next Steps:**
- Bikin model & migration untuk Attendance
- Buat CRUD untuk karyawan  
- Implementasi fitur absensi real-time
- Export ke Excel & PDF

**Useful Commands untuk Development:**
```bash
# Jalankan migration
php artisan migrate

# Bikin model baru
php artisan make:model NamaModel -m

# Bikin controller
php artisan make:controller NamaController

# Clear semua cache
php artisan optimize:clear
```

Happy coding! 🚀
