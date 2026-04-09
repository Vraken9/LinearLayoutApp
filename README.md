## Ringkasan Proyek

Pada halaman *Login* project ini, `LinearLayout` digunakan sebagai fondasi
penyusunan elemen karena sifatnya yang mampu mengurutkan desain secara satu arah.
Orientasi utama struktur adalah vertikal (menurun dari atas ke bawah), menampung
elemen-elemen seperti tulisan selamat datang, kolom isian email dan kata sandi,
hingga tombol login. Selain itu, digunakan pula `LinearLayout` horizontal di
bagian dalam (sebagai *nested layout*) untuk menyatukan isian teks bersampingan
dengan ikon mata, serta meratakan kotak centang (*checkbox*) dengan tulisan
"Lupa Sandi?". Properti `layout_weight` merapikan distribusi lebarnya.

## Dokumentasi Teknis

### 1. Penjelasan File Resource Pendukung

Meskipun kerangka letak utamanya berada di `activity_main.xml`, antarmuka tak
akan lengkap tanpa file pendukung. Project ini bergantung pada resource gambar
seperti `@drawable/bg_rounded_input` dan `@drawable/bg_rounded_button`.

-   **Fungsinya:** File drawable bertugas menyuntikkan efek visual melengkung,
    kapsul tombol, hingga bayangan tepi keliling pada komponen.
-   **Mengapa dipisah?:** Pemisahan *styling* ke `res/drawable/` adalah wujud 
    praktik terbaik pemrograman (*best practice*). Dengan begitu, *style* bentuk 
    melengkung dapat digunakan berulang kali (*reusable*) di seluruh layar, serta
    menghindarkan kita dari penulisan kode tampilan yang berulang tanpa ujung.

### 2. Penjelasan Logika Layout Utama (`activity_main.xml`)

Halaman pengisian sandi mutlak berurutan ke bawah, karena itulah **LinearLayout**
beratribut `android:orientation="vertical"` diadopsi penuh sebagai inti.

-   **`padding="32dp"`**: Mengamankan area jarak bernapas antara elemen form
    dengan perbatasan layar, mencegah UI menabrak bezel layar peranti.
-   **`gravity="center"`**: Menarik segenap elemen untuk memusat ke jantung
    ekuador layar, sehingga tata letak tak menggantung kaku di bagian atas.
-   **`layout_weight="1"`**: Menjadi sihir pada kolom sandi (`EditText`) yang
    melar otomatis merampok spasi tersisa, memaksa tombol ikon tergusur rapi
    ke tepi batas pandang tanpa ukuran pasti.

### 3. Alur Visual

Mata pengguna akan dituntun mengalir mengikuti tumpukan balok ke bawah:

1.  **Header Pembuka**: Sebuah *TextView* dominan bertugas menyambut tumpuan mata.
2.  **Blok Pengisian Data**: Turun setingkat, kolom surel (*email*) menduduki 
    baris mandiri, diiringi blok kata sandi (yang menumbangkan format vertikal 
    menjadi horizontal sementara demi menyisipkan ikon visibilitas sandi).
3.  **Fasilitas Tautan Bawah**: Membariskan horizontal centang penanda masuk
    di kiri dan kalimat peringatan lupa sandi meregang ke ujung ufuk paling kanan.
4.  **Tombol Eksekusi Akhir**: Balok besar penutup menghujam dasar bawah sebagai
    titik gerbang konfirmasi perjalanan form pengguna.

