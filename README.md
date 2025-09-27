# 🚀 Panduan Instalasi Lengkap Laravel Attendance System

## 📋 Overview Project
- **Nama Aplikasi**: `el-presence` atau sesuaikan dengan kemauan kalian misal KalselAttendanceSystem
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

## 🗃️ Step 2: Buat Project Laravel Baru

### 2.1 Buat Project Laravel 10
```bash
# Pindah ke folder www laragon (biasanya C:\laragon\www)
cd C:\laragon\www

# Buat project baru
composer create-project laravel/laravel el-presence "10.*"

# Masuk ke folder project
cd el-presence
```

### 2.2 Setup Database
1. Buka phpMyAdmin di browser: `http://localhost/phpmyadmin`
2. Buat database baru: `el_presence`
3. Edit file `.env`:

```env
APP_NAME="EL Presence"
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
    'name' => 'Admin EL Presence',
    'email' => 'admin@gmail.com',
    'password' => bcrypt('password'),
    'role' => 'admin'
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
npm install tailwindcss @tailwindcss/vite

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
3. Pastikan folder `el-presence` ada di sana
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

## 🏗️ Step 8: Rancangan Aplikasi Absensi Karyawan

### 📝 Kriteria Aplikasi

#### 1. Role User

**👑 Admin**
- Login ke sistem
- Mengelola data karyawan (CRUD)
- Melihat laporan absensi per hari/bulan
- Export laporan ke Excel/PDF
- Mengatur jadwal libur (tabel `holidays`)
- Bisa pilih pembuatan record absensi: **otomatis** (by sistem Senin–Jumat) atau **manual**

**👤 Karyawan**
- Login ke sistem (fitur ingat saya untuk memudahkan, old man friendly)
- Absensi **2x sehari**:
  - **Absen Masuk** (default jam 08:00 WITA)
  - **Absen Pulang** (default jam 14:00 WITA)
- Jika absen masuk lewat dari 08:00 → status **Terlambat**
- Jika tidak absen sama sekali → status **Alpa**
- Bisa klik tombol **Izin** dengan input alasan (misal: sakit, urusan keluarga, dll)
- Bisa lihat riwayat absensi miliknya

#### 2. Database Design (Tabel Utama)

**📊 Struktur Tabel:**
- **users** (data login semua user) - id, name, email, password, role (admin/karyawan), remember_token
- **employees** (data karyawan) - id, user_id, nama, jabatan, dll
- **attendances** (data absensi harian) - id, employee_id, date, time_in, time_out, status (Hadir, Terlambat, Izin, Alpa), notes
- **holidays** (data hari libur) - id, date, description

#### 3. Flow Absensi

1. Sistem cek hari → jika Senin–Jumat → auto generate record absensi (kecuali ada di tabel `holidays`)
2. Karyawan login → klik tombol **Hadir** atau **Izin**
   - Jika hadir lewat 08:00 → status **Terlambat**
   - Jika izin → wajib isi alasan
3. Saat jam pulang (14:00) → karyawan klik **Absen Pulang**
4. Jika karyawan tidak melakukan absen sama sekali → status otomatis **Alpa**
5. Admin bisa buka laporan → filter per hari/per bulan, export PDF/Excel

#### 4. Tambahan Konsep

- UI dibuat **simple dan ramah orang tua** (tombol besar, teks jelas, minim ribet)
- Sistem mendukung login multi-user secara bersamaan
- Data absensi real-time tersimpan di database

---

## 🔧 Step 9: Implementasi Database & Model

### 9.1 Modifikasi Migration Users
Edit file `database/migrations/2014_10_12_000000_create_users_table.php`:

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->enum('role', ['admin', 'karyawan'])->default('karyawan');
            $table->boolean('is_active')->default(true);
            $table->rememberToken();
            $table->timestamps();
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('users');
    }
};
```

### 9.2 Buat Migration Employees
```bash
php artisan make:migration create_employees_table
```

Edit file `database/migrations/xxxx_create_employees_table.php`:

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('employees', function (Blueprint $table) {
            $table->id();
            $table->foreignId('user_id')->constrained()->onDelete('cascade');
            $table->string('employee_code')->unique();
            $table->string('full_name');
            $table->string('position')->nullable();
            $table->string('department')->nullable();
            $table->date('hire_date');
            $table->string('phone')->nullable();
            $table->text('address')->nullable();
            $table->enum('status', ['active', 'inactive', 'terminated'])->default('active');
            $table->timestamps();
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('employees');
    }
};
```

### 9.3 Buat Migration Holidays
```bash
php artisan make:migration create_holidays_table
```

Edit file `database/migrations/xxxx_create_holidays_table.php`:

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('holidays', function (Blueprint $table) {
            $table->id();
            $table->date('date');
            $table->string('name');
            $table->text('description')->nullable();
            $table->enum('type', ['national', 'company', 'religious'])->default('company');
            $table->boolean('is_active')->default(true);
            $table->timestamps();

            $table->index('date');
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('holidays');
    }
};
```

### 9.4 Buat Migration Attendances
```bash
php artisan make:migration create_attendances_table
```

Edit file `database/migrations/xxxx_create_attendances_table.php`:

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('attendances', function (Blueprint $table) {
            $table->id();
            $table->foreignId('employee_id')->constrained()->onDelete('cascade');
            $table->date('date');
            $table->time('time_in')->nullable();
            $table->time('time_out')->nullable();
            $table->enum('status', ['Hadir', 'Terlambat', 'Izin', 'Alpa', 'Libur'])->default('Alpa');
            $table->text('notes')->nullable(); // Untuk keterangan izin
            $table->boolean('is_late')->default(false);
            $table->integer('late_minutes')->default(0);
            $table->timestamp('checked_in_at')->nullable();
            $table->timestamp('checked_out_at')->nullable();
            $table->timestamps();

            $table->unique(['employee_id', 'date']); // Satu karyawan satu record per hari
            $table->index(['date', 'status']);
        });
    }

    public function down(): void
    {
        Schema::dropIfExists('attendances');
    }
};
```

### 9.5 Jalankan Migration
```bash
php artisan migrate
```

---

## 📊 Step 10: Buat Model

### 10.1 Update Model User
Edit `app/Models/User.php`:

```php
<?php

namespace App\Models;

use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Laravel\Sanctum\HasApiTokens;

class User extends Authenticatable
{
    use HasApiTokens, HasFactory, Notifiable;

    protected $fillable = [
        'name',
        'email',
        'password',
        'role',
        'is_active',
    ];

    protected $hidden = [
        'password',
        'remember_token',
    ];

    protected $casts = [
        'email_verified_at' => 'datetime',
        'password' => 'hashed',
        'is_active' => 'boolean',
    ];

    // Relationships
    public function employee()
    {
        return $this->hasOne(Employee::class);
    }

    // Scopes
    public function scopeAdmin($query)
    {
        return $query->where('role', 'admin');
    }

    public function scopeKaryawan($query)
    {
        return $query->where('role', 'karyawan');
    }

    public function scopeActive($query)
    {
        return $query->where('is_active', true);
    }

    // Helper Methods
    public function isAdmin()
    {
        return $this->role === 'admin';
    }

    public function isKaryawan()
    {
        return $this->role === 'karyawan';
    }
}
```

### 10.2 Buat Model Employee
```bash
php artisan make:model Employee
```

Edit `app/Models/Employee.php`:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Carbon\Carbon;

class Employee extends Model
{
    use HasFactory;

    protected $fillable = [
        'user_id',
        'employee_code',
        'full_name',
        'position',
        'department',
        'hire_date',
        'phone',
        'address',
        'status',
    ];

    protected $casts = [
        'hire_date' => 'date',
    ];

    // Relationships
    public function user()
    {
        return $this->belongsTo(User::class);
    }

    public function attendances()
    {
        return $this->hasMany(Attendance::class);
    }

    // Scopes
    public function scopeActive($query)
    {
        return $query->where('status', 'active');
    }

    public function scopeByDepartment($query, $department)
    {
        return $query->where('department', $department);
    }

    // Helper Methods
    public function getTodayAttendance()
    {
        return $this->attendances()
            ->where('date', Carbon::today())
            ->first();
    }

    public function getAttendanceByDate($date)
    {
        return $this->attendances()
            ->where('date', $date)
            ->first();
    }

    public function hasCheckedInToday()
    {
        $attendance = $this->getTodayAttendance();
        return $attendance && $attendance->time_in;
    }

    public function hasCheckedOutToday()
    {
        $attendance = $this->getTodayAttendance();
        return $attendance && $attendance->time_out;
    }

    public function getWorkingDays($startDate, $endDate)
    {
        return $this->attendances()
            ->whereBetween('date', [$startDate, $endDate])
            ->whereIn('status', ['Hadir', 'Terlambat'])
            ->count();
    }
}
```

### 10.3 Buat Model Holiday
```bash
php artisan make:model Holiday
```

Edit `app/Models/Holiday.php`:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Carbon\Carbon;

class Holiday extends Model
{
    use HasFactory;

    protected $fillable = [
        'date',
        'name',
        'description',
        'type',
        'is_active',
    ];

    protected $casts = [
        'date' => 'date',
        'is_active' => 'boolean',
    ];

    // Scopes
    public function scopeActive($query)
    {
        return $query->where('is_active', true);
    }

    public function scopeByYear($query, $year)
    {
        return $query->whereYear('date', $year);
    }

    public function scopeUpcoming($query)
    {
        return $query->where('date', '>=', Carbon::today());
    }

    // Helper Methods
    public static function isHoliday($date)
    {
        return self::where('date', $date)
            ->where('is_active', true)
            ->exists();
    }

    public static function getHolidaysInRange($startDate, $endDate)
    {
        return self::whereBetween('date', [$startDate, $endDate])
            ->where('is_active', true)
            ->get();
    }
}
```

### 10.4 Buat Model Attendance
```bash
php artisan make:model Attendance
```

Edit `app/Models/Attendance.php`:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Carbon\Carbon;

class Attendance extends Model
{
    use HasFactory;

    protected $fillable = [
        'employee_id',
        'date',
        'time_in',
        'time_out',
        'status',
        'notes',
        'is_late',
        'late_minutes',
        'checked_in_at',
        'checked_out_at',
    ];

    protected $casts = [
        'date' => 'date',
        'time_in' => 'datetime:H:i',
        'time_out' => 'datetime:H:i',
        'is_late' => 'boolean',
        'checked_in_at' => 'datetime',
        'checked_out_at' => 'datetime',
    ];

    // Constants
    const STATUS_HADIR = 'Hadir';
    const STATUS_TERLAMBAT = 'Terlambat';
    const STATUS_IZIN = 'Izin';
    const STATUS_ALPA = 'Alpa';
    const STATUS_LIBUR = 'Libur';

    const WORK_START_TIME = '08:00:00';
    const WORK_END_TIME = '14:00:00';

    // Relationships
    public function employee()
    {
        return $this->belongsTo(Employee::class);
    }

    // Scopes
    public function scopeByDate($query, $date)
    {
        return $query->where('date', $date);
    }

    public function scopeByStatus($query, $status)
    {
        return $query->where('status', $status);
    }

    public function scopeByDateRange($query, $startDate, $endDate)
    {
        return $query->whereBetween('date', [$startDate, $endDate]);
    }

    public function scopeToday($query)
    {
        return $query->where('date', Carbon::today());
    }

    public function scopeThisMonth($query)
    {
        return $query->whereMonth('date', Carbon::now()->month)
            ->whereYear('date', Carbon::now()->year);
    }

    // Helper Methods
    public function checkIn($time = null)
    {
        $currentTime = $time ?: Carbon::now()->format('H:i:s');
        $workStartTime = self::WORK_START_TIME;
        
        $this->time_in = $currentTime;
        $this->checked_in_at = Carbon::now();
        
        // Check if late
        if ($currentTime > $workStartTime) {
            $this->is_late = true;
            $this->status = self::STATUS_TERLAMBAT;
            
            // Calculate late minutes
            $start = Carbon::createFromFormat('H:i:s', $workStartTime);
            $checkin = Carbon::createFromFormat('H:i:s', $currentTime);
            $this->late_minutes = $start->diffInMinutes($checkin);
        } else {
            $this->is_late = false;
            $this->status = self::STATUS_HADIR;
            $this->late_minutes = 0;
        }
        
        $this->save();
    }

    public function checkOut($time = null)
    {
        $currentTime = $time ?: Carbon::now()->format('H:i:s');
        
        $this->time_out = $currentTime;
        $this->checked_out_at = Carbon::now();
        $this->save();
    }

    public function setPermission($reason)
    {
        $this->status = self::STATUS_IZIN;
        $this->notes = $reason;
        $this->save();
    }

    public function getWorkingHours()
    {
        if ($this->time_in && $this->time_out) {
            $timeIn = Carbon::createFromFormat('H:i:s', $this->time_in);
            $timeOut = Carbon::createFromFormat('H:i:s', $this->time_out);
            return $timeIn->diffInHours($timeOut);
        }
        return 0;
    }

    public function getStatusColor()
    {
        return match($this->status) {
            self::STATUS_HADIR => 'green',
            self::STATUS_TERLAMBAT => 'yellow',
            self::STATUS_IZIN => 'blue',
            self::STATUS_ALPA => 'red',
            self::STATUS_LIBUR => 'gray',
            default => 'gray'
        };
    }

    public function getStatusIcon()
    {
        return match($this->status) {
            self::STATUS_HADIR => 'fas fa-check-circle',
            self::STATUS_TERLAMBAT => 'fas fa-exclamation-triangle',
            self::STATUS_IZIN => 'fas fa-info-circle',
            self::STATUS_ALPA => 'fas fa-times-circle',
            self::STATUS_LIBUR => 'fas fa-calendar',
            default => 'fas fa-question-circle'
        };
    }
}
```

---

## 🎮 Step 11: Buat Controller

### 11.1 Admin Controller
```bash
php artisan make:controller Admin/AdminController
php artisan make:controller Admin/EmployeeController --resource
php artisan make:controller Admin/AttendanceController
php artisan make:controller Admin/HolidayController --resource
php artisan make:controller Admin/ReportController
```

Edit `app/Http/Controllers/Admin/AdminController.php`:

```php
<?php

namespace App\Http\Controllers\Admin;

use App\Http\Controllers\Controller;
use App\Models\Employee;
use App\Models\Attendance;
use App\Models\Holiday;
use Carbon\Carbon;

class AdminController extends Controller
{
    public function dashboard()
    {
        $today = Carbon::today();
        
        $stats = [
            'total_employees' => Employee::active()->count(),
            'present_today' => Attendance::today()
                ->whereIn('status', ['Hadir', 'Terlambat'])
                ->count(),
            'absent_today' => Attendance::today()
                ->where('status', 'Alpa')
                ->count(),
            'on_leave_today' => Attendance::today()
                ->where('status', 'Izin')
                ->count(),
            'late_today' => Attendance::today()
                ->where('status', 'Terlambat')
                ->count(),
        ];

        $recent_attendances = Attendance::with('employee.user')
            ->today()
            ->latest('checked_in_at')
            ->limit(10)
            ->get();

        $upcoming_holidays = Holiday::upcoming()
            ->active()
            ->limit(5)
            ->get();

        return view('admin.dashboard', compact('stats', 'recent_attendances', 'upcoming_holidays'));
    }

    public function generateAttendanceRecords()
    {
        $today = Carbon::today();
        
        // Skip weekends
        if ($today->isWeekend()) {
            return back()->with('info', 'Hari libur, tidak ada record absensi yang dibuat.');
        }

        // Skip holidays
        if (Holiday::isHoliday($today)) {
            return back()->with('info', 'Hari libur nasional, tidak ada record absensi yang dibuat.');
        }

        $employees = Employee::active()->get();
        $created = 0;

        foreach ($employees as $employee) {
            $existing = Attendance::where('employee_id', $employee->id)
                ->where('date', $today)
                ->first();

            if (!$existing) {
                Attendance::create([
                    'employee_id' => $employee->id,
                    'date' => $today,
                    'status' => 'Alpa',
                ]);
                $created++;
            }
        }

        return back()->with('success', "Berhasil membuat {$created} record absensi untuk hari ini.");
    }
}
```

Edit `app/Http/Controllers/Admin/EmployeeController.php`:

```php
<?php

namespace App\Http\Controllers\Admin;

use App\Http\Controllers\Controller;
use App\Models\Employee;
use App\Models\User;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Facades\Hash;
use Illuminate\Validation\Rule;

class EmployeeController extends Controller
{
    public function index()
    {
        $employees = Employee::with('user')
            ->when(request('search'), function ($query, $search) {
                $query->where('full_name', 'like', "%{$search}%")
                    ->orWhere('employee_code', 'like', "%{$search}%")
                    ->orWhere('position', 'like', "%{$search}%");
            })
            ->when(request('department'), function ($query, $department) {
                $query->where('department', $department);
            })
            ->when(request('status'), function ($query, $status) {
                $query->where('status', $status);
            })
            ->paginate(15);

        $departments = Employee::select('department')
            ->distinct()
            ->whereNotNull('department')
            ->pluck('department');

        return view('admin.employees.index', compact('employees', 'departments'));
    }

    public function create()
    {
        return view('admin.employees.create');
    }

    public function store(Request $request)
    {
        $request->validate([
            'name' => 'required|string|max:255',
            'email' => 'required|string|email|max:255|unique:users',
            'password' => 'required|string|min:8|confirmed',
            'full_name' => 'required|string|max:255',
            'employee_code' => 'required|string|max:20|unique:employees',
            'position' => 'nullable|string|max:100',
            'department' => 'nullable|string|max:100',
            'hire_date' => 'required|date',
            'phone' => 'nullable|string|max:20',
            'address' => 'nullable|string',
        ]);

        DB::transaction(function () use ($request) {
            $user = User::create([
                'name' => $request->name,
                'email' => $request->email,
                'password' => Hash::make($request->password),
                'role' => 'karyawan',
            ]);

            Employee::create([
                'user_id' => $user->id,
                'employee_code' => $request->employee_code,
                'full_name' => $request->full_name,
                'position' => $request->position,
                'department' => $request->department,
                'hire_date' => $request->hire_date,
                'phone' => $request->phone,
                'address' => $request->address,
            ]);
        });

        return redirect()->route('admin.employees.index')
            ->with('success', 'Karyawan berhasil ditambahkan.');
    }

    public function show(Employee $employee)
    {
        $employee->load('user', 'attendances');
        $attendanceStats = [
            'total_days' => $employee->attendances()->thisMonth()->count(),
            'present_days' => $employee->attendances()->thisMonth()
                ->whereIn('status', ['Hadir', 'Terlambat'])->count(),
            'late_days' => $employee->attendances()->thisMonth()
                ->where('status', 'Terlambat')->count(),
            'absent_days' => $employee->attendances()->thisMonth()
                ->where('status', 'Alpa')->count(),
            'leave_days' => $employee->attendances()->thisMonth()
                ->where('status', 'Izin')->count(),
        ];

        return view('admin.employees.show', compact('employee', 'attendanceStats'));
    }

    public function edit(Employee $employee)
    {
        $employee->load('user');
        return view('admin.employees.edit', compact('employee'));
    }

    public function update(Request $request, Employee $employee)
    {
        $request->validate([
            'name' => 'required|string|max:255',
            'email' => ['required', 'string', 'email', 'max:255', 
                Rule::unique('users')->ignore($employee->user_id)],
            'password' => 'nullable|string|min:8|confirmed',
            'full_name' => 'required|string|max:255',
            'employee_code' => ['required', 'string', 'max:20', 
                Rule::unique('employees')->ignore($employee->id)],
            'position' => 'nullable|string|max:100',
            'department' => 'nullable|string|max:100',
            'hire_date' => 'required|date',
            'phone' => 'nullable|string|max:20',
            'address' => 'nullable|string',
            'status' => 'required|in:active,inactive,terminated',
        ]);

        DB::transaction(function () use ($request, $employee) {
            $userData = [
                'name' => $request->name,
                'email' => $request->email,
            ];

            if ($request->filled('password')) {
                $userData['password'] = Hash::make($request->password);
            }

            $employee->user()->update($userData);

            $employee->update([
                'employee_code' => $request->employee_code,
                'full_name' => $request->full_name,
                'position' => $request->position,
                'department' => $request->department,
                'hire_date' => $request->hire_date,
                'phone' => $request->phone,
                'address' => $request->address,
                'status' => $request->status,
            ]);
        });

        return redirect()->route('admin.employees.index')
            ->with('success', 'Data karyawan berhasil diperbarui.');
    }

    public function destroy(Employee $employee)
    {
        DB::transaction(function () use ($employee) {
            $employee->attendances()->delete();
            $employee->user()->delete();
            $employee->delete();
        });

        return redirect()->route('admin.employees.index')
            ->with('success', 'Karyawan berhasil dihapus.');
    }
}
```

Edit `app/Http/Controllers/Admin/AttendanceController.php`:

```php
<?php

namespace App\Http\Controllers\Admin;

use App\Http\Controllers\Controller;
use App\Models\Attendance;
use App\Models\Employee;
use Carbon\Carbon;
use Illuminate\Http\Request;

class AttendanceController extends Controller
{
    public function index(Request $request)
    {
        $date = $request->get('date', Carbon::today()->format('Y-m-d'));
        $department = $request->get('department');
        $status = $request->get('status');

        $attendances = Attendance::with(['employee.user'])
            ->byDate($date)
            ->when($department, function ($query, $department) {
                $query->whereHas('employee', function ($q) use ($department) {
                    $q->where('department', $department);
                });
            })
            ->when($status, function ($query, $status) {
                $query->where('status', $status);
            })
            ->get();

        $departments = Employee::select('department')
            ->distinct()
            ->whereNotNull('department')
            ->pluck('department');

        $stats = [
            'total' => $attendances->count(),
            'present' => $attendances->whereIn('status', ['Hadir', 'Terlambat'])->count(),
            'late' => $attendances->where('status', 'Terlambat')->count(),
            'absent' => $attendances->where('status', 'Alpa')->count(),
            'leave' => $attendances->where('status', 'Izin')->count(),
        ];

        return view('admin.attendance.index', compact(
            'attendances', 'departments', 'stats', 'date', 'department', 'status'
        ));
    }

    public function update(Request $request, Attendance $attendance)
    {
        $request->validate([
            'status' => 'required|in:Hadir,Terlambat,Izin,Alpa,Libur',
            'time_in' => 'nullable|date_format:H:i',
            'time_out' => 'nullable|date_format:H:i',
            'notes' => 'nullable|string|max:500',
        ]);

        $attendance->update([
            'status' => $request->status,
            'time_in' => $request->time_in,
            'time_out' => $request->time_out,
            'notes' => $request->notes,
        ]);

        return back()->with('success', 'Data absensi berhasil diperbarui.');
    }

    public function bulkUpdate(Request $request)
    {
        $request->validate([
            'attendance_ids' => 'required|array',
            'attendance_ids.*' => 'exists:attendances,id',
            'bulk_status' => 'required|in:Hadir,Terlambat,Izin,Alpa,Libur',
        ]);

        Attendance::whereIn('id', $request->attendance_ids)
            ->update(['status' => $request->bulk_status]);

        return back()->with('success', 'Bulk update berhasil dilakukan.');
    }
}
```

Edit `app/Http/Controllers/Admin/HolidayController.php`:

```php
<?php

namespace App\Http\Controllers\Admin;

use App\Http\Controllers\Controller;
use App\Models\Holiday;
use Illuminate\Http\Request;
use Carbon\Carbon;

class HolidayController extends Controller
{
    public function index()
    {
        $holidays = Holiday::when(request('year'), function ($query, $year) {
                $query->byYear($year);
            }, function ($query) {
                $query->byYear(Carbon::now()->year);
            })
            ->orderBy('date')
            ->paginate(15);

        $years = Holiday::selectRaw('YEAR(date) as year')
            ->distinct()
            ->orderBy('year', 'desc')
            ->pluck('year');

        return view('admin.holidays.index', compact('holidays', 'years'));
    }

    public function create()
    {
        return view('admin.holidays.create');
    }

    public function store(Request $request)
    {
        $request->validate([
            'date' => 'required|date|unique:holidays,date',
            'name' => 'required|string|max:255',
            'description' => 'nullable|string|max:500',
            'type' => 'required|in:national,company,religious',
        ]);

        Holiday::create($request->all());

        return redirect()->route('admin.holidays.index')
            ->with('success', 'Hari libur berhasil ditambahkan.');
    }

    public function edit(Holiday $holiday)
    {
        return view('admin.holidays.edit', compact('holiday'));
    }

    public function update(Request $request, Holiday $holiday)
    {
        $request->validate([
            'date' => 'required|date|unique:holidays,date,' . $holiday->id,
            'name' => 'required|string|max:255',
            'description' => 'nullable|string|max:500',
            'type' => 'required|in:national,company,religious',
            'is_active' => 'boolean',
        ]);

        $holiday->update($request->all());

        return redirect()->route('admin.holidays.index')
            ->with('success', 'Hari libur berhasil diperbarui.');
    }

    public function destroy(Holiday $holiday)
    {
        $holiday->delete();

        return redirect()->route('admin.holidays.index')
            ->with('success', 'Hari libur berhasil dihapus.');
    }
}
```

### 11.2 Employee/Karyawan Controller
```bash
php artisan make:controller Employee/EmployeeDashboardController
php artisan make:controller Employee/AttendanceController
```

Edit `app/Http/Controllers/Employee/EmployeeDashboardController.php`:

```php
<?php

namespace App\Http\Controllers\Employee;

use App\Http\Controllers\Controller;
use App\Models\Attendance;
use App\Models\Holiday;
use Carbon\Carbon;
use Illuminate\Http\Request;

class EmployeeDashboardController extends Controller
{
    public function dashboard()
    {
        $employee = auth()->user()->employee;
        $today = Carbon::today();
        $currentMonth = Carbon::now();

        // Today's attendance
        $todayAttendance = $employee->getTodayAttendance();

        // Monthly stats
        $monthlyStats = [
            'total_days' => Attendance::where('employee_id', $employee->id)
                ->whereMonth('date', $currentMonth->month)
                ->whereYear('date', $currentMonth->year)
                ->count(),
            'present_days' => Attendance::where('employee_id', $employee->id)
                ->whereMonth('date', $currentMonth->month)
                ->whereYear('date', $currentMonth->year)
                ->whereIn('status', ['Hadir', 'Terlambat'])
                ->count(),
            'late_days' => Attendance::where('employee_id', $employee->id)
                ->whereMonth('date', $currentMonth->month)
                ->whereYear('date', $currentMonth->year)
                ->where('status', 'Terlambat')
                ->count(),
            'absent_days' => Attendance::where('employee_id', $employee->id)
                ->whereMonth('date', $currentMonth->month)
                ->whereYear('date', $currentMonth->year)
                ->where('status', 'Alpa')
                ->count(),
            'leave_days' => Attendance::where('employee_id', $employee->id)
                ->whereMonth('date', $currentMonth->month)
                ->whereYear('date', $currentMonth->year)
                ->where('status', 'Izin')
                ->count(),
        ];

        // Recent attendances
        $recentAttendances = Attendance::where('employee_id', $employee->id)
            ->latest('date')
            ->limit(7)
            ->get();

        // Upcoming holidays
        $upcomingHolidays = Holiday::upcoming()
            ->active()
            ->limit(3)
            ->get();

        // Check if today is workday
        $isWorkday = !$today->isWeekend() && !Holiday::isHoliday($today);

        return view('employee.dashboard', compact(
            'employee', 'todayAttendance', 'monthlyStats', 
            'recentAttendances', 'upcomingHolidays', 'isWorkday'
        ));
    }

    public function attendanceHistory(Request $request)
    {
        $employee = auth()->user()->employee;
        $month = $request->get('month', Carbon::now()->format('Y-m'));
        
        [$year, $monthNum] = explode('-', $month);

        $attendances = Attendance::where('employee_id', $employee->id)
            ->whereYear('date', $year)
            ->whereMonth('date', $monthNum)
            ->orderBy('date', 'desc')
            ->paginate(20);

        return view('employee.attendance-history', compact('attendances', 'month'));
    }
}
```

Edit `app/Http/Controllers/Employee/AttendanceController.php`:

```php
<?php

namespace App\Http\Controllers\Employee;

use App\Http\Controllers\Controller;
use App\Models\Attendance;
use App\Models\Holiday;
use Carbon\Carbon;
use Illuminate\Http\Request;

class AttendanceController extends Controller
{
    public function checkIn(Request $request)
    {
        $employee = auth()->user()->employee;
        $today = Carbon::today();
        $now = Carbon::now();

        // Check if today is workday
        if ($today->isWeekend()) {
            return back()->with('error', 'Tidak bisa absen di hari libur.');
        }

        if (Holiday::isHoliday($today)) {
            return back()->with('error', 'Hari ini adalah hari libur.');
        }

        // Get or create today's attendance record
        $attendance = Attendance::firstOrCreate([
            'employee_id' => $employee->id,
            'date' => $today,
        ], [
            'status' => 'Alpa',
        ]);

        // Check if already checked in
        if ($attendance->time_in) {
            return back()->with('error', 'Anda sudah melakukan absen masuk hari ini.');
        }

        // Perform check in
        $attendance->checkIn();

        $message = $attendance->is_late 
            ? "Absen masuk berhasil! Anda terlambat {$attendance->late_minutes} menit."
            : 'Absen masuk berhasil!';

        return back()->with('success', $message);
    }

    public function checkOut(Request $request)
    {
        $employee = auth()->user()->employee;
        $today = Carbon::today();

        $attendance = Attendance::where('employee_id', $employee->id)
            ->where('date', $today)
            ->first();

        if (!$attendance) {
            return back()->with('error', 'Anda belum melakukan absen masuk hari ini.');
        }

        if (!$attendance->time_in) {
            return back()->with('error', 'Anda harus absen masuk terlebih dahulu.');
        }

        if ($attendance->time_out) {
            return back()->with('error', 'Anda sudah melakukan absen pulang hari ini.');
        }

        $attendance->checkOut();

        return back()->with('success', 'Absen pulang berhasil!');
    }

    public function requestLeave(Request $request)
    {
        $request->validate([
            'reason' => 'required|string|max:500',
        ]);

        $employee = auth()->user()->employee;
        $today = Carbon::today();

        // Check if today is workday
        if ($today->isWeekend()) {
            return back()->with('error', 'Tidak bisa mengajukan izin di hari libur.');
        }

        if (Holiday::isHoliday($today)) {
            return back()->with('error', 'Hari ini adalah hari libur.');
        }

        // Get or create today's attendance record
        $attendance = Attendance::firstOrCreate([
            'employee_id' => $employee->id,
            'date' => $today,
        ], [
            'status' => 'Alpa',
        ]);

        // Check if already has attendance record for today
        if ($attendance->time_in || $attendance->status !== 'Alpa') {
            return back()->with('error', 'Anda sudah memiliki record absensi untuk hari ini.');
        }

        $attendance->setPermission($request->reason);

        return back()->with('success', 'Permohonan izin berhasil diajukan.');
    }
}
```

### 11.3 Report Controller
Edit `app/Http/Controllers/Admin/ReportController.php`:

```php
<?php

namespace App\Http\Controllers\Admin;

use App\Http\Controllers\Controller;
use App\Models\Attendance;
use App\Models\Employee;
use Carbon\Carbon;
use Illuminate\Http\Request;
use Maatwebsite\Excel\Facades\Excel;
use App\Exports\AttendanceExport;
use Barryvdh\DomPDF\Facade\Pdf;

class ReportController extends Controller
{
    public function index(Request $request)
    {
        $startDate = $request->get('start_date', Carbon::now()->startOfMonth()->format('Y-m-d'));
        $endDate = $request->get('end_date', Carbon::now()->endOfMonth()->format('Y-m-d'));
        $department = $request->get('department');
        $employee_id = $request->get('employee_id');

        $query = Attendance::with(['employee.user'])
            ->whereBetween('date', [$startDate, $endDate]);

        if ($department) {
            $query->whereHas('employee', function ($q) use ($department) {
                $q->where('department', $department);
            });
        }

        if ($employee_id) {
            $query->where('employee_id', $employee_id);
        }

        $attendances = $query->orderBy('date', 'desc')->paginate(20);

        // Summary statistics
        $summary = [
            'total_records' => $query->count(),
            'present' => $query->clone()->whereIn('status', ['Hadir', 'Terlambat'])->count(),
            'late' => $query->clone()->where('status', 'Terlambat')->count(),
            'absent' => $query->clone()->where('status', 'Alpa')->count(),
            'leave' => $query->clone()->where('status', 'Izin')->count(),
        ];

        $departments = Employee::select('department')
            ->distinct()
            ->whereNotNull('department')
            ->pluck('department');

        $employees = Employee::with('user')
            ->when($department, function ($q) use ($department) {
                $q->where('department', $department);
            })
            ->get();

        return view('admin.reports.index', compact(
            'attendances', 'summary', 'departments', 'employees',
            'startDate', 'endDate', 'department', 'employee_id'
        ));
    }

    public function exportExcel(Request $request)
    {
        $filters = $request->only(['start_date', 'end_date', 'department', 'employee_id']);
        
        return Excel::download(
            new AttendanceExport($filters), 
            'laporan-absensi-' . date('Y-m-d') . '.xlsx'
        );
    }

    public function exportPdf(Request $request)
    {
        $startDate = $request->get('start_date', Carbon::now()->startOfMonth()->format('Y-m-d'));
        $endDate = $request->get('end_date', Carbon::now()->endOfMonth()->format('Y-m-d'));
        $department = $request->get('department');
        $employee_id = $request->get('employee_id');

        $query = Attendance::with(['employee.user'])
            ->whereBetween('date', [$startDate, $endDate]);

        if ($department) {
            $query->whereHas('employee', function ($q) use ($department) {
                $q->where('department', $department);
            });
        }

        if ($employee_id) {
            $query->where('employee_id', $employee_id);
        }

        $attendances = $query->orderBy('date', 'desc')->get();

        $pdf = Pdf::loadView('admin.reports.pdf', compact('attendances', 'startDate', 'endDate'));
        
        return $pdf->download('laporan-absensi-' . date('Y-m-d') . '.pdf');
    }
}
```

---

## 📊 Step 12: Buat Export Class

### 12.1 Buat Export Class untuk Excel
```bash
php artisan make:export AttendanceExport
```

Edit `app/Exports/AttendanceExport.php`:

```php
<?php

namespace App\Exports;

use App\Models\Attendance;
use Maatwebsite\Excel\Concerns\FromCollection;
use Maatwebsite\Excel\Concerns\WithHeadings;
use Maatwebsite\Excel\Concerns\WithMapping;
use Maatwebsite\Excel\Concerns\WithStyles;
use PhpOffice\PhpSpreadsheet\Worksheet\Worksheet;

class AttendanceExport implements FromCollection, WithHeadings, WithMapping, WithStyles
{
    protected $filters;

    public function __construct($filters)
    {
        $this->filters = $filters;
    }

    public function collection()
    {
        $query = Attendance::with(['employee.user'])
            ->whereBetween('date', [
                $this->filters['start_date'] ?? now()->startOfMonth(),
                $this->filters['end_date'] ?? now()->endOfMonth()
            ]);

        if (isset($this->filters['department'])) {
            $query->whereHas('employee', function ($q) {
                $q->where('department', $this->filters['department']);
            });
        }

        if (isset($this->filters['employee_id'])) {
            $query->where('employee_id', $this->filters['employee_id']);
        }

        return $query->orderBy('date', 'desc')->get();
    }

    public function headings(): array
    {
        return [
            'Tanggal',
            'Nama Karyawan',
            'Kode Karyawan',
            'Jam Masuk',
            'Jam Pulang',
            'Status',
            'Terlambat (Menit)',
            'Keterangan',
        ];
    }

    public function map($attendance): array
    {
        return [
            $attendance->date->format('d/m/Y'),
            $attendance->employee->full_name,
            $attendance->employee->employee_code,
            $attendance->time_in ? $attendance->time_in->format('H:i') : '-',
            $attendance->time_out ? $attendance->time_out->format('H:i') : '-',
            $attendance->status,
            $attendance->late_minutes,
            $attendance->notes ?? '-',
        ];
    }

    public function styles(Worksheet $sheet)
    {
        return [
            1 => ['font' => ['bold' => true]],
        ];
    }
}
```

---

## 🛠️ Troubleshooting - Error yang Sering Muncul

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

## 🎯 Step 13: Setup Routes

### 13.1 Tambahkan Routes
Edit `routes/web.php`:

```php
<?php

use App\Http\Controllers\ProfileController;
use App\Http\Controllers\Admin\AdminController;
use App\Http\Controllers\Admin\EmployeeController;
use App\Http\Controllers\Admin\AttendanceController as AdminAttendanceController;
use App\Http\Controllers\Admin\HolidayController;
use App\Http\Controllers\Admin\ReportController;
use App\Http\Controllers\Employee\EmployeeDashboardController;
use App\Http\Controllers\Employee\AttendanceController;
use Illuminate\Support\Facades\Route;

/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
*/

Route::get('/', function () {
    return view('welcome');
});

Route::get('/dashboard', function () {
    if (auth()->user()->isAdmin()) {
        return redirect()->route('admin.dashboard');
    }
    return redirect()->route('employee.dashboard');
})->middleware(['auth', 'verified'])->name('dashboard');

Route::middleware('auth')->group(function () {
    Route::get('/profile', [ProfileController::class, 'edit'])->name('profile.edit');
    Route::patch('/profile', [ProfileController::class, 'update'])->name('profile.update');
    Route::delete('/profile', [ProfileController::class, 'destroy'])->name('profile.destroy');
});

// Admin Routes
Route::middleware(['auth', 'role:admin'])->prefix('admin')->name('admin.')->group(function () {
    Route::get('/dashboard', [AdminController::class, 'dashboard'])->name('dashboard');
    Route::post('/generate-attendance', [AdminController::class, 'generateAttendanceRecords'])
        ->name('generate.attendance');
    
    // Employee Management
    Route::resource('employees', EmployeeController::class);
    
    // Attendance Management
    Route::get('/attendance', [AdminAttendanceController::class, 'index'])->name('attendance.index');
    Route::patch('/attendance/{attendance}', [AdminAttendanceController::class, 'update'])
        ->name('attendance.update');
    Route::post('/attendance/bulk-update', [AdminAttendanceController::class, 'bulkUpdate'])
        ->name('attendance.bulk-update');
    
    // Holiday Management
    Route::resource('holidays', HolidayController::class);
    
    // Reports
    Route::get('/reports', [ReportController::class, 'index'])->name('reports.index');
    Route::get('/reports/excel', [ReportController::class, 'exportExcel'])->name('reports.excel');
    Route::get('/reports/pdf', [ReportController::class, 'exportPdf'])->name('reports.pdf');
});

// Employee Routes
Route::middleware(['auth', 'role:karyawan'])->prefix('employee')->name('employee.')->group(function () {
    Route::get('/dashboard', [EmployeeDashboardController::class, 'dashboard'])->name('dashboard');
    Route::get('/attendance-history', [EmployeeDashboardController::class, 'attendanceHistory'])
        ->name('attendance.history');
    
    // Attendance Actions
    Route::post('/check-in', [AttendanceController::class, 'checkIn'])->name('attendance.checkin');
    Route::post('/check-out', [AttendanceController::class, 'checkOut'])->name('attendance.checkout');
    Route::post('/request-leave', [AttendanceController::class, 'requestLeave'])->name('attendance.leave');
});

require __DIR__.'/auth.php';
```

### 13.2 Buat Middleware untuk Role
```bash
php artisan make:middleware RoleMiddleware
```

Edit `app/Http/Middleware/RoleMiddleware.php`:

```php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class RoleMiddleware
{
    public function handle(Request $request, Closure $next, string $role): Response
    {
        if (!auth()->check() || auth()->user()->role !== $role) {
            abort(403, 'Unauthorized access.');
        }

        return $next($request);
    }
}
```

Daftarkan middleware di `app/Http/Kernel.php`:

```php
protected $middlewareAliases = [
    // ... middleware lainnya
    'role' => \App\Http\Middleware\RoleMiddleware::class,
];
```

---

## 🖥️ Step 14: Buat Views (Blade Templates)

### 14.1 Layout Admin
Buat file `resources/views/layouts/admin.blade.php`:

```html
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="csrf-token" content="{{ csrf_token() }}">
    <title>@yield('title', 'Admin') - {{ config('app.name', 'EL Presence') }}</title>
    @vite(['resources/css/app.css', 'resources/js/app.js'])
</head>
<body class="font-sans antialiased bg-gray-100">
    <!-- Navigation -->
    <nav class="bg-white shadow-lg border-b border-gray-200">
        <div class="max-w-7xl mx-auto px-4">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <h1 class="text-xl font-bold text-gray-800">
                            <i class="fas fa-users-cog mr-2"></i>
                            Admin Panel
                        </h1>
                    </div>
                    <div class="hidden space-x-8 sm:-my-px sm:ml-10 sm:flex">
                        <x-nav-link :href="route('admin.dashboard')" :active="request()->routeIs('admin.dashboard')">
                            <i class="fas fa-tachometer-alt mr-1"></i> Dashboard
                        </x-nav-link>
                        <x-nav-link :href="route('admin.employees.index')" :active="request()->routeIs('admin.employees.*')">
                            <i class="fas fa-users mr-1"></i> Karyawan
                        </x-nav-link>
                        <x-nav-link :href="route('admin.attendance.index')" :active="request()->routeIs('admin.attendance.*')">
                            <i class="fas fa-clipboard-check mr-1"></i> Absensi
                        </x-nav-link>
                        <x-nav-link :href="route('admin.holidays.index')" :active="request()->routeIs('admin.holidays.*')">
                            <i class="fas fa-calendar mr-1"></i> Hari Libur
                        </x-nav-link>
                        <x-nav-link :href="route('admin.reports.index')" :active="request()->routeIs('admin.reports.*')">
                            <i class="fas fa-chart-bar mr-1"></i> Laporan
                        </x-nav-link>
                    </div>
                </div>
                <div class="hidden sm:flex sm:items-center sm:ml-6">
                    <x-dropdown align="right" width="48">
                        <x-slot name="trigger">
                            <button class="inline-flex items-center px-3 py-2 text-sm leading-4 font-medium rounded-md text-gray-500 bg-white hover:text-gray-700 focus:outline-none transition ease-in-out duration-150">
                                <div>{{ Auth::user()->name }}</div>
                                <div class="ml-1"><svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" /></svg></div>
                            </button>
                        </x-slot>
                        <x-slot name="content">
                            <x-dropdown-link :href="route('profile.edit')">{{ __('Profile') }}</x-dropdown-link>
                            <form method="POST" action="{{ route('logout') }}">
                                @csrf
                                <x-dropdown-link :href="route('logout')" onclick="event.preventDefault(); this.closest('form').submit();">
                                    {{ __('Log Out') }}
                                </x-dropdown-link>
                            </form>
                        </x-slot>
                    </x-dropdown>
                </div>
            </div>
        </div>
    </nav>

    <!-- Page Content -->
    <main class="py-6">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
            @if (session('success'))
                <div class="mb-4 bg-green-100 border border-green-400 text-green-700 px-4 py-3 rounded relative" role="alert">
                    <span class="block sm:inline">{{ session('success') }}</span>
                </div>
            @endif

            @if (session('error'))
                <div class="mb-4 bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative" role="alert">
                    <span class="block sm:inline">{{ session('error') }}</span>
                </div>
            @endif

            @yield('content')
        </div>
    </main>
</body>
</html>
```

### 14.2 Layout Employee
Buat file `resources/views/layouts/employee.blade.php`:

```html
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="csrf-token" content="{{ csrf_token() }}">
    <title>@yield('title', 'Karyawan') - {{ config('app.name', 'EL Presence') }}</title>
    @vite(['resources/css/app.css', 'resources/js/app.js'])
</head>
<body class="font-sans antialiased bg-gray-50">
    <!-- Navigation -->
    <nav class="bg-blue-600 shadow-lg">
        <div class="max-w-4xl mx-auto px-4">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <h1 class="text-xl font-bold text-white">
                            <i class="fas fa-user-clock mr-2"></i>
                            EL Presence
                        </h1>
                    </div>
                    <div class="hidden space-x-8 sm:-my-px sm:ml-10 sm:flex">
                        <a href="{{ route('employee.dashboard') }}" 
                           class="text-white hover:text-blue-200 px-3 py-2 rounded-md text-sm font-medium {{ request()->routeIs('employee.dashboard') ? 'bg-blue-700' : '' }}">
                            <i class="fas fa-home mr-1"></i> Beranda
                        </a>
                        <a href="{{ route('employee.attendance.history') }}" 
                           class="text-white hover:text-blue-200 px-3 py-2 rounded-md text-sm font-medium {{ request()->routeIs('employee.attendance.history') ? 'bg-blue-700' : '' }}">
                            <i class="fas fa-history mr-1"></i> Riwayat
                        </a>
                    </div>
                </div>
                <div class="flex items-center">
                    <div class="relative">
                        <button onclick="toggleDropdown()" class="flex items-center text-white hover:text-blue-200 px-3 py-2 rounded-md text-sm font-medium">
                            <i class="fas fa-user mr-2"></i>
                            {{ Auth::user()->name }}
                            <i class="fas fa-chevron-down ml-2"></i>
                        </button>
                        <div id="userDropdown" class="hidden absolute right-0 mt-2 w-48 bg-white rounded-md shadow-lg py-1 z-50">
                            <a href="{{ route('profile.edit') }}" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">
                                <i class="fas fa-user mr-2"></i> Profil
                            </a>
                            <form method="POST" action="{{ route('logout') }}">
                                @csrf
                                <button type="submit" class="w-full text-left block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">
                                    <i class="fas fa-sign-out-alt mr-2"></i> Keluar
                                </button>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </nav>

    <!-- Page Content -->
    <main class="py-6">
        <div class="max-w-4xl mx-auto px-4">
            @if (session('success'))
                <div class="mb-4 bg-green-100 border-l-4 border-green-500 text-green-700 p-4" role="alert">
                    <div class="flex">
                        <div class="flex-shrink-0">
                            <i class="fas fa-check-circle"></i>
                        </div>
                        <div class="ml-3">
                            <p class="text-sm">{{ session('success') }}</p>
                        </div>
                    </div>
                </div>
            @endif

            @if (session('error'))
                <div class="mb-4 bg-red-100 border-l-4 border-red-500 text-red-700 p-4" role="alert">
                    <div class="flex">
                        <div class="flex-shrink-0">
                            <i class="fas fa-exclamation-triangle"></i>
                        </div>
                        <div class="ml-3">
                            <p class="text-sm">{{ session('error') }}</p>
                        </div>
                    </div>
                </div>
            @endif

            @yield('content')
        </div>
    </main>

    <script>
        function toggleDropdown() {
            document.getElementById('userDropdown').classList.toggle('hidden');
        }
        
        // Close dropdown when clicking outside
        window.onclick = function(event) {
            if (!event.target.matches('.dropdown-toggle')) {
                var dropdowns = document.getElementsByClassName("dropdown-content");
                for (var i = 0; i < dropdowns.length; i++) {
                    var openDropdown = dropdowns[i];
                    if (!openDropdown.classList.contains('hidden')) {
                        openDropdown.classList.add('hidden');
                    }
                }
            }
        }
    </script>
</body>
</html>
```

### 14.3 Dashboard Admin
Buat file `resources/views/admin/dashboard.blade.php`:

```html
@extends('layouts.admin')

@section('title', 'Dashboard Admin')

@section('content')
<div class="space-y-6">
    <!-- Page Header -->
    <div class="bg-white overflow-hidden shadow rounded-lg">
        <div class="px-4 py-5 sm:p-6">
            <div class="flex items-center justify-between">
                <div>
                    <h1 class="text-2xl font-bold text-gray-900">Dashboard Admin</h1>
                    <p class="text-gray-600">Selamat datang, {{ auth()->user()->name }}</p>
                </div>
                <div>
                    <form method="POST" action="{{ route('admin.generate.attendance') }}">
                        @csrf
                        <button type="submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                            <i class="fas fa-plus mr-2"></i>
                            Generate Absensi Hari Ini
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <!-- Stats Cards -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
        <div class="bg-white overflow-hidden shadow rounded-lg">
            <div class="p-5">
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <div class="w-8 h-8 bg-blue-500 rounded-full flex items-center justify-center">
                            <i class="fas fa-users text-white text-sm"></i>
                        </div>
                    </div>
                    <div class="ml-5 w-0 flex-1">
                        <dl>
                            <dt class="text-sm font-medium text-gray-500 truncate">Total Karyawan</dt>
                            <dd class="text-lg font-medium text-gray-900">{{ $stats['total_employees'] }}</dd>
                        </dl>
                    </div>
                </div>
            </div>
        </div>

        <div class="bg-white overflow-hidden shadow rounded-lg">
            <div class="p-5">
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <div class="w-8 h-8 bg-green-500 rounded-full flex items-center justify-center">
                            <i class="fas fa-check-circle text-white text-sm"></i>
                        </div>
                    </div>
                    <div class="ml-5 w-0 flex-1">
                        <dl>
                            <dt class="text-sm font-medium text-gray-500 truncate">Hadir Hari Ini</dt>
                            <dd class="text-lg font-medium text-gray-900">{{ $stats['present_today'] }}</dd>
                        </dl>
                    </div>
                </div>
            </div>
        </div>

        <div class="bg-white overflow-hidden shadow rounded-lg">
            <div class="p-5">
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <div class="w-8 h-8 bg-red-500 rounded-full flex items-center justify-center">
                            <i class="fas fa-times-circle text-white text-sm"></i>
                        </div>
                    </div>
                    <div class="ml-5 w-0 flex-1">
                        <dl>
                            <dt class="text-sm font-medium text-gray-500 truncate">Tidak Hadir</dt>
                            <dd class="text-lg font-medium text-gray-900">{{ $stats['absent_today'] }}</dd>
                        </dl>
                    </div>
                </div>
            </div>
        </div>

        <div class="bg-white overflow-hidden shadow rounded-lg">
            <div class="p-5">
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <div class="w-8 h-8 bg-yellow-500 rounded-full flex items-center justify-center">
                            <i class="fas fa-info-circle text-white text-sm"></i>
                        </div>
                    </div>
                    <div class="ml-5 w-0 flex-1">
                        <dl>
                            <dt class="text-sm font-medium text-gray-500 truncate">Izin Hari Ini</dt>
                            <dd class="text-lg font-medium text-gray-900">{{ $stats['on_leave_today'] }}</dd>
                        </dl>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Recent Attendance & Upcoming Holidays -->
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- Recent Attendance -->
        <div class="bg-white shadow rounded-lg">
            <div class="px-4 py-5 sm:p-6">
                <h3 class="text-lg leading-6 font-medium text-gray-900 mb-4">
                    <i class="fas fa-clock mr-2"></i>
                    Absensi Terbaru Hari Ini
                </h3>
                <div class="flow-root">
                    <ul class="divide-y divide-gray-200">
                        @forelse($recent_attendances as $attendance)
                        <li class="py-3">
                            <div class="flex items-center space-x-4">
                                <div class="flex-shrink-0">
                                    <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium
                                        @if($attendance->status == 'Hadir') bg-green-100 text-green-800
                                        @elseif($attendance->status == 'Terlambat') bg-yellow-100 text-yellow-800
                                        @elseif($attendance->status == 'Izin') bg-blue-100 text-blue-800
                                        @else bg-red-100 text-red-800 @endif">
                                        {{ $attendance->status }}
                                    </span>
                                </div>
                                <div class="flex-1 min-w-0">
                                    <p class="text-sm font-medium text-gray-900 truncate">
                                        {{ $attendance->employee->full_name }}
                                    </p>
                                    <p class="text-sm text-gray-500">
                                        @if($attendance->checked_in_at)
                                            {{ $attendance->checked_in_at->format('H:i') }}
                                        @endif
                                    </p>
                                </div>
                            </div>
                        </li>
                        @empty
                        <li class="py-3">
                            <p class="text-gray-500 text-center">Belum ada absensi hari ini</p>
                        </li>
                        @endforelse
                    </ul>
                </div>
                <div class="mt-4">
                    <a href="{{ route('admin.attendance.index') }}" 
                       class="text-blue-600 hover:text-blue-500 text-sm font-medium">
                        Lihat semua absensi →
                    </a>
                </div>
            </div>
        </div>

        <!-- Upcoming Holidays -->
        <div class="bg-white shadow rounded-lg">
            <div class="px-4 py-5 sm:p-6">
                <h3 class="text-lg leading-6 font-medium text-gray-900 mb-4">
                    <i class="fas fa-calendar mr-2"></i>
                    Hari Libur Mendatang
                </h3>
                <div class="flow-root">
                    <ul class="divide-y divide-gray-200">
                        @forelse($upcoming_holidays as $holiday)
                        <li class="py-3">
                            <div class="flex items-center space-x-4">
                                <div class="flex-shrink-0">
                                    <div class="w-10 h-10 bg-gray-100 rounded-lg flex items-center justify-center">
                                        <span class="text-sm font-medium text-gray-600">
                                            {{ $holiday->date->format('d') }}
                                        </span>
                                    </div>
                                </div>
                                <div class="flex-1 min-w-0">
                                    <p class="text-sm font-medium text-gray-900">{{ $holiday->name }}</p>
                                    <p class="text-sm text-gray-500">{{ $holiday->date->format('d M Y') }}</p>
                                </div>
                            </div>
                        </li>
                        @empty
                        <li class="py-3">
                            <p class="text-gray-500 text-center">Tidak ada hari libur mendatang</p>
                        </li>
                        @endforelse
                    </ul>
                </div>
                <div class="mt-4">
                    <a href="{{ route('admin.holidays.index') }}" 
                       class="text-blue-600 hover:text-blue-500 text-sm font-medium">
                        Kelola hari libur →
                    </a>
                </div>
            </div>
        </div>
    </div>
</div>
@endsection
```

### 14.4 Dashboard Employee
Buat file `resources/views/employee/dashboard.blade.php`:

```html
@extends('layouts.employee')

@section('title', 'Dashboard Karyawan')

@section('content')
<div class="space-y-6">
    <!-- Welcome Section -->
    <div class="bg-white rounded-lg shadow-md overflow-hidden">
        <div class="px-6 py-4 bg-gradient-to-r from-blue-500 to-blue-600">
            <div class="flex items-center justify-between text-white">
                <div>
                    <h1 class="text-2xl font-bold">Selamat datang, {{ $employee->full_name }}</h1>
                    <p class="text-blue-100">{{ $employee->position }} - {{ $employee->department }}</p>
                </div>
                <div class="text-right">
                    <p class="text-blue-100">{{ now()->format('l, d M Y') }}</p>
                    <p class="text-xl font-bold">{{ now()->format('H:i') }} WITA</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Attendance Actions -->
    @if($isWorkday)
    <div class="bg-white rounded-lg shadow-md p-6">
        <h2 class="text-xl font-semibold mb-4">
            <i class="fas fa-clock mr-2 text-blue-500"></i>
            Absensi Hari Ini
        </h2>
        
        @if($todayAttendance)
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <!-- Status Card -->
                <div class="bg-gray-50 rounded-lg p-4">
                    <div class="text-center">
                        <div class="w-16 h-16 mx-auto mb-2 rounded-full flex items-center justify-center
                            @if($todayAttendance->status == 'Hadir') bg-green-100
                            @elseif($todayAttendance->status == 'Terlambat') bg-yellow-100
                            @elseif($todayAttendance->status == 'Izin') bg-blue-100
                            @else bg-red-100 @endif">
                            <i class="{{ $todayAttendance->getStatusIcon() }}
                                @if($todayAttendance->status == 'Hadir') text-green-500
                                @elseif($todayAttendance->status == 'Terlambat') text-yellow-500
                                @elseif($todayAttendance->status == 'Izin') text-blue-500
                                @else text-red-500 @endif text-2xl"></i>
                        </div>
                        <p class="font-semibold">{{ $todayAttendance->status }}</p>
                        @if($todayAttendance->late_minutes > 0)
                            <p class="text-sm text-yellow-600">Terlambat {{ $todayAttendance->late_minutes }} menit</p>
                        @endif
                    </div>
                </div>

                <!-- Check In -->
                <div class="bg-gray-50 rounded-lg p-4">
                    <div class="text-center">
                        @if($todayAttendance->time_in)
                            <div class="text-green-500 mb-2">
                                <i class="fas fa-check-circle text-2xl"></i>
                            </div>
                            <p class="font-semibold">Masuk: {{ $todayAttendance->time_in->format('H:i') }}</p>
                            <p class="text-sm text-gray-600">Sudah absen masuk</p>
                        @else
                            @if($todayAttendance->status == 'Izin')
                                <div class="text-blue-500 mb-2">
                                    <i class="fas fa-info-circle text-2xl"></i>
                                </div>
                                <p class="font-semibold text-blue-600">Izin</p>
                                <p class="text-sm text-gray-600">{{ $todayAttendance->notes }}</p>
                            @else
                                <form method="POST" action="{{ route('employee.attendance.checkin') }}">
                                    @csrf
                                    <button type="submit" 
                                            class="w-full bg-green-500 hover:bg-green-600 text-white font-bold py-3 px-4 rounded-lg transition duration-200">
                                        <i class="fas fa-sign-in-alt mr-2"></i>
                                        Absen Masuk
                                    </button>
                                </form>
                            @endif
                        @endif
                    </div>
                </div>

                <!-- Check Out -->
                <div class="bg-gray-50 rounded-lg p-4">
                    <div class="text-center">
                        @if($todayAttendance->time_out)
                            <div class="text-blue-500 mb-2">
                                <i class="fas fa-check-circle text-2xl"></i>
                            </div>
                            <p class="font-semibold">Pulang: {{ $todayAttendance->time_out->format('H:i') }}</p>
                            <p class="text-sm text-gray-600">Sudah absen pulang</p>
                        @elseif($todayAttendance->time_in && $todayAttendance->status != 'Izin')
                            <form method="POST" action="{{ route('employee.attendance.checkout') }}">
                                @csrf
                                <button type="submit" 
                                        class="w-full bg-blue-500 hover:bg-blue-600 text-white font-bold py-3 px-4 rounded-lg transition duration-200">
                                    <i class="fas fa-sign-out-alt mr-2"></i>
                                    Absen Pulang
                                </button>
                            </form>
                        @else
                            <div class="text-gray-400 mb-2">
                                <i class="fas fa-clock text-2xl"></i>
                            </div>
                            <p class="text-gray-500">Belum bisa absen pulang</p>
                        @endif
                    </div>
                </div>
            </div>

            <!-- Leave Request -->
            @if(!$todayAttendance->time_in && $todayAttendance->status == 'Alpa')
                <div class="mt-4 pt-4 border-t">
                    <button onclick="showLeaveModal()" 
                            class="w-full bg-orange-500 hover:bg-orange-600 text-white font-bold py-3 px-4 rounded-lg transition duration-200">
                        <i class="fas fa-hand-paper mr-2"></i>
                        Ajukan Izin
                    </button>
                </div>
            @endif
        @else
            <!-- No attendance record yet -->
            <div class="text-center py-8">
                <div class="mb-4">
                    <i class="fas fa-calendar-times text-6xl text-gray-300"></i>
                </div>
                <p class="text-gray-500 mb-4">Belum ada record absensi untuk hari ini</p>
                <div class="space-y-2">
                    <form method="POST" action="{{ route('employee.attendance.checkin') }}" class="inline-block mr-2">
                        @csrf
                        <button type="submit" 
                                class="bg-green-500 hover:bg-green-600 text-white font-bold py-3 px-6 rounded-lg transition duration-200">
                            <i class="fas fa-sign-in-alt mr-2"></i>
                            Absen Masuk
                        </button>
                    </form>
                    <button onclick="showLeaveModal()" 
                            class="bg-orange-500 hover:bg-orange-600 text-white font-bold py-3 px-6 rounded-lg transition duration-200">
                        <i class="fas fa-hand-paper mr-2"></i>
                        Ajukan Izin
                    </button>
                </div>
            </div>
        @endif
    </div>
    @else
        <!-- Holiday/Weekend -->
        <div class="bg-gray-100 rounded-lg p-6 text-center">
            <div class="mb-4">
                <i class="fas fa-calendar text-6xl text-gray-400"></i>
            </div>
            <h2 class="text-xl font-semibold text-gray-600 mb-2">Hari Libur</h2>
            <p class="text-gray-500">Selamat beristirahat! Tidak ada absensi hari ini.</p>
        </div>
    @endif

    <!-- Monthly Statistics -->
    <div class="bg-white rounded-lg shadow-md p-6">
        <h2 class="text-xl font-semibold mb-4">
            <i class="fas fa-chart-bar mr-2 text-blue-500"></i>
            Statistik Bulan Ini
        </h2>
        <div class="grid grid-cols-2 md:grid-cols-5 gap-4">
            <div class="text-center p-4 bg-blue-50 rounded-lg">
                <div class="text-2xl font-bold text-blue-600">{{ $monthlyStats['total_days'] }}</div>
                <div class="text-sm text-gray-600">Total Hari</div>
            </div>
            <div class="text-center p-4 bg-green-50 rounded-lg">
                <div class="text-2xl font-bold text-green-600">{{ $monthlyStats['present_days'] }}</div>
                <div class="text-sm text-gray-600">Hadir</div>
            </div>
            <div class="text-center p-4 bg-yellow-50 rounded-lg">
                <div class="text-2xl font-bold text-yellow-600">{{ $monthlyStats['late_days'] }}</div>
                <div class="text-sm text-gray-600">Terlambat</div>
            </div>
            <div class="text-center p-4 bg-orange-50 rounded-lg">
                <div class="text-2xl font-bold text-orange-600">{{ $monthlyStats['leave_days'] }}</div>
                <div class="text-sm text-gray-600">Izin</div>
            </div>
            <div class="text-center p-4 bg-red-50 rounded-lg">
                <div class="text-2xl font-bold text-red-600">{{ $monthlyStats['absent_days'] }}</div>
                <div class="text-sm text-gray-600">Alpa</div>
            </div>
        </div>
    </div>

    <!-- Recent Attendance History -->
    <div class="bg-white rounded-lg shadow-md p-6">
        <div class="flex items-center justify-between mb-4">
            <h2 class="text-xl font-semibold">
                <i class="fas fa-history mr-2 text-blue-500"></i>
                Riwayat Terakhir
            </h2>
            <a href="{{ route('employee.attendance.history') }}" 
               class="text-blue-600 hover:text-blue-800 font-medium">
                Lihat Semua →
            </a>
        </div>
        <div class="overflow-hidden">
            <table class="min-w-full">
                <thead class="bg-gray-50">
                    <tr>
                        <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tanggal</th>
                        <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                        <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Jam Masuk</th>
                        <th class="px-4 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Jam Pulang</th>
                    </tr>
                </thead>
                <tbody class="divide-y divide-gray-200">
                    @forelse($recentAttendances as $attendance)
                    <tr>
                        <td class="px-4 py-2 text-sm text-gray-900">{{ $attendance->date->format('d/m/Y') }}</td>
                        <td class="px-4 py-2">
                            <span class="inline-flex px-2 py-1 text-xs font-semibold rounded-full
                                @if($attendance->status == 'Hadir') bg-green-100 text-green-800
                                @elseif($attendance->status == 'Terlambat') bg-yellow-100 text-yellow-800
                                @elseif($attendance->status == 'Izin') bg-blue-100 text-blue-800
                                @else bg-red-100 text-red-800 @endif">
                                {{ $attendance->status }}
                            </span>
                        </td>
                        <td class="px-4 py-2 text-sm text-gray-900">
                            {{ $attendance->time_in ? $attendance->time_in->format('H:i') : '-' }}
                        </td>
                        <td class="px-4 py-2 text-sm text-gray-900">
                            {{ $attendance->time_out ? $attendance->time_out->format('H:i') : '-' }}
                        </td>
                    </tr>
                    @empty
                    <tr>
                        <td colspan="4" class="px-4 py-8 text-center text-gray-500">
                            Belum ada riwayat absensi
                        </td>
                    </tr>
                    @endforelse
                </tbody>
            </table>
        </div>
    </div>

    <!-- Upcoming Holidays -->
    @if($upcomingHolidays->count() > 0)
    <div class="bg-white rounded-lg shadow-md p-6">
        <h2 class="text-xl font-semibold mb-4">
            <i class="fas fa-calendar mr-2 text-blue-500"></i>
            Hari Libur Mendatang
        </h2>
        <div class="space-y-3">
            @foreach($upcomingHolidays as $holiday)
            <div class="flex items-center p-3 bg-gray-50 rounded-lg">
                <div class="flex-shrink-0">
                    <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                        <span class="text-sm font-semibold text-blue-600">
                            {{ $holiday->date->format('d') }}
                        </span>
                    </div>
                </div>
                <div class="ml-4">
                    <div class="font-medium text-gray-900">{{ $holiday->name }}</div>
                    <div class="text-sm text-gray-500">{{ $holiday->date->format('l, d M Y') }}</div>
                </div>
            </div>
            @endforeach
        </div>
    </div>
    @endif
</div>

<!-- Leave Request Modal -->
<div id="leaveModal" class="hidden fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50">
    <div class="relative top-20 mx-auto p-5 border w-11/12 md:w-1/2 lg:w-1/3 shadow-lg rounded-md bg-white">
        <div class="mt-3">
            <div class="flex items-center justify-between mb-4">
                <h3 class="text-lg font-medium text-gray-900">Ajukan Permohonan Izin</h3>
                <button onclick="hideLeaveModal()" class="text-gray-400 hover:text-gray-600">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <form method="POST" action="{{ route('employee.attendance.leave') }}">
                @csrf
                <div class="mb-4">
                    <label for="reason" class="block text-sm font-medium text-gray-700 mb-2">
                        Alasan Izin <span class="text-red-500">*</span>
                    </label>
                    <textarea name="reason" id="reason" rows="4" required
                              class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                              placeholder="Contoh: Sakit demam, Urusan keluarga, dll..."></textarea>
                </div>
                <div class="flex justify-end space-x-3">
                    <button type="button" onclick="hideLeaveModal()"
                            class="px-4 py-2 bg-gray-300 text-gray-700 rounded-md hover:bg-gray-400">
                        Batal
                    </button>
                    <button type="submit"
                            class="px-4 py-2 bg-orange-500 text-white rounded-md hover:bg-orange-600">
                        <i class="fas fa-paper-plane mr-2"></i>
                        Ajukan Izin
                    </button>
                </div>
            </form>
        </div>
    </div>
</div>

<script>
function showLeaveModal() {
    document.getElementById('leaveModal').classList.remove('hidden');
}

function hideLeaveModal() {
    document.getElementById('leaveModal').classList.add('hidden');
}

// Auto refresh clock
function updateClock() {
    const now = new Date();
    const timeString = now.toLocaleTimeString('id-ID', { 
        hour: '2-digit', 
        minute: '2-digit',
        timeZone: 'Asia/Makassar'
    });
    const clockElements = document.querySelectorAll('.current-time');
    clockElements.forEach(el => el.textContent = timeString + ' WITA');
}

setInterval(updateClock, 1000);
</script>
@endsection
```

---

## 🎯 Step 15: Seeder dan Factory

### 15.1 Buat Seeder
```bash
php artisan make:seeder DatabaseSeeder
php artisan make:seeder AdminUserSeeder
php artisan make:seeder EmployeeSeeder
php artisan make:seeder HolidaySeeder
```

Edit `database/seeders/AdminUserSeeder.php`:

```php
<?php

namespace Database\Seeders;

use App\Models\User;
use App\Models\Employee;
use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\Hash;

class AdminUserSeeder extends Seeder
{
    public function run(): void
    {
        // Create Admin User
        User::create([
            'name' => 'Administrator',
            'email' => 'admin@gmail.com',
            'password' => Hash::make('admin123'),
            'role' => 'admin',
            'is_active' => true,
        ]);

        // Create Sample Employees
        $employees = [
            [
                'name' => 'Budi Santoso',
                'email' => 'budi@gmail.com',
                'employee_code' => 'EMP001',
                'full_name' => 'Budi Santoso',
                'position' => 'Manager',
                'department' => 'IT',
            ],
            [
                'name' => 'Siti Nurhaliza',
                'email' => 'siti@gmail.com',
                'employee_code' => 'EMP002',
                'full_name' => 'Siti Nurhaliza',
                'position' => 'Staff',
                'department' => 'HR',
            ],
            [
                'name' => 'Ahmad Fauzi',
                'email' => 'ahmad@gmail.com',
                'employee_code' => 'EMP003',
                'full_name' => 'Ahmad Fauzi',
                'position' => 'Developer',
                'department' => 'IT',
            ],
        ];

        foreach ($employees as $employeeData) {
            $user = User::create([
                'name' => $employeeData['name'],
                'email' => $employeeData['email'],
                'password' => Hash::make('password'),
                'role' => 'karyawan',
                'is_active' => true,
            ]);

            Employee::create([
                'user_id' => $user->id,
                'employee_code' => $employeeData['employee_code'],
                'full_name' => $employeeData['full_name'],
                'position' => $employeeData['position'],
                'department' => $employeeData['department'],
                'hire_date' => now()->subMonths(rand(1, 24)),
                'phone' => '081234567' . sprintf('%03d', rand(100, 999)),
                'address' => 'Jl. Contoh No. ' . rand(1, 100) . ', Banjarmasin',
            ]);
        }
    }
}
```

Edit `database/seeders/HolidaySeeder.php`:

```php
<?php

namespace Database\Seeders;

use App\Models\Holiday;
use Illuminate\Database\Seeder;
use Carbon\Carbon;

class HolidaySeeder extends Seeder
{
    public function run(): void
    {
        $holidays = [
            [
                'date' => '2025-01-01',
                'name' => 'Tahun Baru Masehi',
                'type' => 'national'
            ],
            [
                'date' => '2025-02-12',
                'name' => 'Imlek',
                'type' => 'national'
            ],
            [
                'date' => '2025-03-14',
                'name' => 'Hari Raya Nyepi',
                'type' => 'national'
            ],
            [
                'date' => '2025-03-29',
                'name' => 'Wafat Isa Almasih',
                'type' => 'national'
            ],
            [
                'date' => '2025-04-01',
                'name' => 'Isra Miraj',
                'type' => 'national'
            ],
            [
                'date' => '2025-05-01',
                'name' => 'Hari Buruh',
                'type' => 'national'
            ],
            [
                'date' => '2025-05-29',
                'name' => 'Kenaikan Isa Almasih',
                'type' => 'national'
            ],
            [
                'date' => '2025-06-01',
                'name' => 'Hari Pancasila',
                'type' => 'national'
            ],
            [
                'date' => '2025-08-17',
                'name' => 'Hari Kemerdekaan RI',
                'type' => 'national'
            ],
        ];

        foreach ($holidays as $holiday) {
            Holiday::create([
                'date' => $holiday['date'],
                'name' => $holiday['name'],
                'description' => 'Hari libur ' . $holiday['name'],
                'type' => $holiday['type'],
                'is_active' => true,
            ]);
        }
    }
}
```

Edit `database/seeders/DatabaseSeeder.php`:

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    public function run(): void
    {
        $this->call([
            AdminUserSeeder::class,
            HolidaySeeder::class,
        ]);
    }
}
```

### 15.2 Jalankan Seeder
```bash
php artisan db:seed
```

---

## 🚧 Step 16: Command untuk Auto Generate Attendance

### 16.1 Buat Command
```bash
php artisan make:command GenerateDailyAttendance
```

Edit `app/Console/Commands/GenerateDailyAttendance.php`:

```php
<?php

namespace App\Console\Commands;

use App\Models\Employee;
use App\Models\Attendance;
use App\Models\Holiday;
use Carbon\Carbon;
use Illuminate\Console\Command;

class GenerateDailyAttendance extends Command
{
    protected $signature = 'attendance:generate {date?}';
    protected $description = 'Generate daily attendance records for all active employees';

    public function handle()
    {
        $date = $this->argument('date') ? Carbon::parse($this->argument('date')) : Carbon::today();
        
        $this->info("Generating attendance records for: " . $date->format('Y-m-d'));

        // Skip weekends
        if ($date->isWeekend()) {
            $this->warn('Skipping weekend date: ' . $date->format('l, Y-m-d'));
            return;
        }

        // Skip holidays
        if (Holiday::isHoliday($date)) {
            $holiday = Holiday::where('date', $date)->first();
            $this->warn('Skipping holiday: ' . $holiday->name . ' (' . $date->format('Y-m-d') . ')');
            return;
        }

        $employees = Employee::active()->get();
        $created = 0;
        $existing = 0;

        foreach ($employees as $employee) {
            $attendance = Attendance::where('employee_id', $employee->id)
                ->where('date', $date)
                ->first();

            if (!$attendance) {
                Attendance::create([
                    'employee_id' => $employee->id,
                    'date' => $date,
                    'status' => 'Alpa',
                ]);
                $created++;
            } else {
                $existing++;
            }
        }

        $this->info("✅ Created: {$created} records");
        $this->info("ℹ️  Existing: {$existing} records");
        $this->info("Total employees: " . $employees->count());
    }
}
```

### 16.2 Schedule Command
Edit `app/Console/Kernel.php`:

```php
<?php

namespace App\Console;

use Illuminate\Console\Scheduling\Schedule;
use Illuminate\Foundation\Console\Kernel as ConsoleKernel;

class Kernel extends ConsoleKernel
{
    protected function schedule(Schedule $schedule): void
    {
        // Generate attendance records every workday at 6 AM
        $schedule->command('attendance:generate')
            ->weekdays()
            ->at('06:00')
            ->withoutOverlapping()
            ->appendOutputTo(storage_path('logs/attendance.log'));
    }

    protected function commands(): void
    {
        $this->load(__DIR__.'/Commands');

        require base_path('routes/console.php');
    }
}
```

### 16.3 Test Command
```bash
# Generate untuk hari ini
php artisan attendance:generate

# Generate untuk tanggal tertentu
php artisan attendance:generate 2025-09-28
```

---

## ✅ Step 17: Final Setup & Testing

### 17.1 Jalankan Migration & Seeder
```bash
# Reset database dan jalankan seeder
php artisan migrate:fresh --seed
```

### 17.2 Test Login
1. **Admin Login:**
   - Email: `admin@gmail.com`
   - Password: `admin123`

2. **Karyawan Login:**
   - Email: `budi@gmail.com`
   - Password: `password`

### 17.3 Generate Attendance Records
```bash
# Generate record absensi untuk hari ini
php artisan attendance:generate

# Atau lewat admin panel
# Login sebagai admin → klik "Generate Absensi Hari Ini"
```

---

## 🎉 Selamat! Aplikasi EL Presence Sudah Siap!

### ✨ Fitur yang Sudah Tersedia:

**🔐 Authentication & Authorization:**
- ✅ Login/Register dengan Laravel Breeze
- ✅ Role-based access (Admin & Karyawan)
- ✅ Remember me functionality

**👑 Admin Features:**
- ✅ Dashboard dengan statistik real-time
- ✅ CRUD Karyawan lengkap
- ✅ Management absensi harian
- ✅ Management hari libur
- ✅ Laporan dengan export Excel/PDF
- ✅ Auto-generate attendance records

**👤 Employee Features:**
- ✅ Dashboard ramah orang tua (big buttons)
- ✅ Absen masuk/pulang dengan validasi waktu
- ✅ Status terlambat otomatis
- ✅ Pengajuan izin dengan alasan
- ✅ Riwayat absensi pribadi
- ✅ Statistik bulanan

**🎯 Business Logic:**
- ✅ Auto-generate absensi Senin-Jumat
- ✅ Skip weekend & hari libur
- ✅ Validasi waktu masuk (terlambat > 08:00)
- ✅ Status otomatis: Hadir, Terlambat, Izin, Alpa
- ✅ Real-time data dengan proper relationships

**🎨 UI/UX:**
- ✅ Tailwind CSS 4.1 dengan design modern
- ✅ Font Awesome icons
- ✅ SweetAlert2 notifications
- ✅ Responsive design
- ✅ Old-man friendly interface

### 📝 Useful Commands:

```bash
# Development
npm run dev              # Watch mode untuk assets
php artisan serve        # Local development server

# Database
php artisan migrate:fresh --seed  # Reset DB dengan sample data
php artisan attendance:generate   # Generate absensi manual

# Cache Clear
php artisan optimize:clear       # Clear all cache

# Production
npm run build                   # Build assets untuk production
php artisan config:cache        # Cache config untuk performance
```

### 🚀 Next Development Ideas:

1. **Mobile App** dengan Flutter/React Native
2. **Geolocation** untuk absen berdasarkan lokasi
3. **Face Recognition** untuk absensi
4. **Push Notifications** reminder absen
5. **Overtime Management** sistem lembur
6. **Leave Request** workflow approval
7. **Performance Dashboard** untuk manager
8. **API Integration** dengan payroll system

Happy coding! Semoga aplikasi EL Presence bermanfaat! 🎯


konsep aplikasi 
rancangan aplikasi absensi karyawan berbasis web dengan kriteria berikut:
1. Role User
* Admin
   * Login ke sistem
   * Mengelola data karyawan (CRUD)
   * Melihat laporan absensi per hari/bulan
   * Export laporan ke Excel/PDF
   * Mengatur jadwal libur (tabel holidays)
   * Bisa pilih pembuatan record absensi: otomatis (by sistem Senin–Jumat) atau manual
* Karyawan
   * Login ke sistem (fitur ingat saya untuk memudahkan, old man friendly)
   * Absensi 2x sehari:
      * Absen Masuk (default jam 08:00 WITA)
      * Absen Pulang (default jam 14:00 WITA)
   * Jika absen masuk lewat dari 08:00 → status Terlambat
   * Jika tidak absen sama sekali → status Alpa
   * Bisa klik tombol Izin dengan input alasan (misal: sakit, urusan keluarga, dll)
   * Bisa lihat riwayat absensi miliknya
2. Database Design (Tabel Utama)
* users (data login semua user)
   * id, name, email, password, role (admin/karyawan), remember_token
* employees (data karyawan)
   * id, user_id, nama, jabatan, dll
* attendances (data absensi harian)
   * id, employee_id, date, time_in, time_out, status (Hadir, Terlambat, Izin, Alpa), notes
* holidays (data hari libur)
   * id, date, description
3. Flow Absensi
1. Sistem cek hari → jika Senin–Jumat → auto generate record absensi (kecuali ada di tabel holidays).
2. Karyawan login → klik tombol Hadir atau Izin.
   * Jika hadir lewat 08:00 → status Terlambat.
   * Jika izin → wajib isi alasan.
3. Saat jam pulang (14:00) → karyawan klik Absen Pulang.
4. Jika karyawan tidak melakukan absen sama sekali → status otomatis Alpa.
5. Admin bisa buka laporan → filter per hari/per bulan, export PDF/Excel.
4. Tambahan Konsep
* UI dibuat simple dan ramah orang tua (tombol besar, teks jelas, minim ribet).
* Sistem mendukung login multi-user secara bersamaan.
* Data absensi real-time tersimpan di database.
