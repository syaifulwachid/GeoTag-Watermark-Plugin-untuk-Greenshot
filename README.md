# GeoTag Watermark Plugin untuk Greenshot

Plugin untuk menambahkan watermark geotag (koordinat dan informasi lokasi) pada screenshot Greenshot.

## Fitur Utama

### 🔍 Auto Deteksi Koordinat dari Clipboard
- **Real-time monitoring** clipboard untuk perubahan koordinat
- **Multi-format support** untuk berbagai format koordinat
- **Auto-update** koordinat saat terdeteksi
- **Rate limiting** untuk mencegah spam requests

### 📍 Auto Grab Lokasi Alamat
- **Reverse geocoding** otomatis dari koordinat
- **Dual API support**: Google Maps dan OpenStreetMap
- **Bahasa Indonesia** untuk hasil alamat
- **Caching** untuk performa yang lebih baik

### 🎯 Format Koordinat yang Didukung

#### Decimal Degrees
```
-8.22363, 113.214628
-8.22363,113.214628
8.22363, -113.214628
```

#### Degrees, Minutes, Seconds (DMS)
```
-8°13'25.1"S 113°12'52.7"E
8°13'25.1"N 113°12'52.7"W
```

#### Direction First
```
S 8°13'25.1" E 113°12'52.7"
N 8°13'25.1" W 113°12'52.7"
```

#### Decimal with Degree Symbol
```
-8.22363° 113.214628°
8.22363° -113.214628°
```

#### Labeled Coordinates
```
lat: -8.22363, lng: 113.214628
latitude: -8.22363, longitude: 113.214628
LAT: -8.22363, LNG: 113.214628
```

#### Google Maps URL
```
https://maps.google.com/@-8.22363,113.214628,15z
https://maps.google.com/?q=-8.22363,113.214628
https://maps.google.com/?ll=-8.22363,113.214628
https://maps.google.com/?center=-8.22363,113.214628
```

## Instalasi

### 1. Build Plugin
```powershell
# Navigate ke direktori src
cd greenshot-release-1.3/src

# Build plugin
.\Greenshot.Plugin.GeoTagWatermark\build-and-test.ps1 -Clean -Test
```

### 2. Install Plugin
1. Copy file `Greenshot.Plugin.GeoTagWatermark.dll` dari `bin\Debug\net472\` ke direktori plugins Greenshot
2. Restart Greenshot
3. Plugin akan muncul di menu Tools > GeoTag Watermark

## Konfigurasi

### 1. Buka Konfigurasi
- Buka Greenshot
- Klik kanan icon Greenshot di system tray
- Pilih **Tools > GeoTag Watermark > Configure**

### 2. Pengaturan Dasar
- **Enabled**: Aktifkan/nonaktifkan plugin
- **Location Name**: Nama lokasi default
- **Address**: Alamat default
- **Latitude/Longitude**: Koordinat default

### 3. Pengaturan Auto-Detection
- **Enable Clipboard Monitoring**: Aktifkan monitoring clipboard
- **Clipboard Monitoring Interval**: Interval monitoring (500-10000ms)
- **Auto Grab Location**: Otomatis ambil info lokasi

### 4. Pengaturan API
- **API Provider**: Pilih Google Maps atau OpenStreetMap
- **Google Maps API Key**: Masukkan API key jika menggunakan Google Maps
- **Use OpenStreetMap**: Gunakan OpenStreetMap (gratis)

### 5. Pengaturan Tampilan
- **Show Google Maps**: Tampilkan overlay Google Maps
- **Show Info Box**: Tampilkan box informasi
- **Font Size**: Ukuran font teks
- **Text Color**: Warna teks
- **Background Color**: Warna background
- **Opacity**: Transparansi overlay

## Cara Penggunaan

### 1. Auto Deteksi Koordinat
1. Copy koordinat ke clipboard (format apapun yang didukung)
2. Plugin akan otomatis mendeteksi dan update koordinat
3. Jika Auto Grab Location aktif, alamat akan diambil otomatis
4. Notification akan muncul di pojok kanan atas

### 2. Manual Update Koordinat
1. Buka konfigurasi plugin
2. Klik tombol **Auto Detect** untuk mendeteksi dari clipboard
3. Atau masukkan koordinat manual
4. Klik **Auto Grab Lokasi** untuk mengambil info alamat

### 3. Ambil Screenshot dengan Watermark
1. Pastikan koordinat sudah terdeteksi
2. Ambil screenshot seperti biasa dengan Greenshot
3. Watermark akan otomatis ditambahkan dengan informasi lokasi

### 4. Hotkey Auto-Grab
1. Tekan hotkey yang dikonfigurasi (default: Ctrl+Shift+G)
2. Plugin akan auto-detect koordinat dari clipboard
3. Auto-grab lokasi jika diaktifkan
4. Ambil screenshot otomatis

## Troubleshooting

### Koordinat Tidak Terdeteksi
- ✅ Pastikan format koordinat sesuai dengan yang didukung
- ✅ Periksa apakah koordinat valid (latitude: -90 to 90, longitude: -180 to 180)
- ✅ Coba copy ulang koordinat ke clipboard
- ✅ Periksa apakah clipboard monitoring aktif

### Auto Grab Lokasi Gagal
- ✅ Periksa koneksi internet
- ✅ Untuk Google Maps, pastikan API key valid
- ✅ Untuk OpenStreetMap, pastikan tidak melebihi rate limit
- ✅ Coba ganti API provider

### Plugin Tidak Muncul
- ✅ Pastikan DLL sudah di-copy ke direktori plugins yang benar
- ✅ Restart Greenshot
- ✅ Periksa log file untuk error

### Performance Issues
- ✅ Kurangi interval clipboard monitoring
- ✅ Nonaktifkan auto-grab location jika tidak diperlukan
- ✅ Gunakan OpenStreetMap untuk performa lebih baik

## API Configuration

### Google Maps API
1. Dapatkan API key dari [Google Cloud Console](https://console.cloud.google.com/)
2. Aktifkan Geocoding API
3. Masukkan API key di konfigurasi plugin

### OpenStreetMap (Gratis)
- Tidak memerlukan API key
- Rate limit: 1 request per detik
- Cocok untuk penggunaan personal

## Logging

Plugin menggunakan log4net untuk logging. Log file dapat ditemukan di:
- `%APPDATA%\Greenshot\logs\` (Windows)
- `~/.config/Greenshot/logs/` (Linux/macOS)

Level logging dapat diatur di konfigurasi Greenshot.

## Development

### Build Requirements
- Visual Studio 2019/2022 atau .NET SDK
- .NET Framework 4.7.2
- PowerShell 5.1+

### Dependencies
- **Newtonsoft.Json**: JSON parsing
- **log4net**: Logging
- **System.Net.Http**: HTTP requests
- **System.Text.RegularExpressions**: Pattern matching

### Testing
```powershell
# Run tests
.\Greenshot.Plugin.GeoTagWatermark\build-and-test.ps1 -Test -Verbose
```

## Changelog

### v1.3 (2025)
- ✅ **Perbaikan Service Auto Deteksi Koordinat**
  - Rate limiting untuk mencegah spam
  - Support untuk 8+ format koordinat
  - Validasi koordinat otomatis
  - Error handling yang lebih baik

- ✅ **Perbaikan Service Auto Grab Lokasi**
  - Rate limiting untuk API calls
  - Support bahasa Indonesia
  - Better error recovery
  - Proper JSON parsing

- ✅ **Fitur Baru**
  - Real-time coordinate detection
  - Auto-close notifications
  - Better user feedback
  - Thread-safe operations

### v1.2 (2024)
- Initial release dengan fitur dasar
- Support Google Maps dan OpenStreetMap
- Basic coordinate detection

## Support

Untuk bantuan dan support:
- **Email**: syaiful.wachid@fiberhome.com
- **LinkedIn**: [Syaiful Wachid](https://www.linkedin.com/in/syaiful-wachid-5373n/)
- **GitHub**: [Issues](https://github.com/greenshot/greenshot/issues)

## License

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 1 of the License, or
(at your option) any later version.

## Credits

- **Created by**: Syaiful Wachid
- **Senior Project Designer**: Fiberhome Indonesia
- **Based on**: Greenshot Screenshot Tool 
