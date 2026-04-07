# LinearLayoutApp
Implementasi Linear Layout pada antarmuka aplikasi Marketplace Bunga 'Akhyar Florist'. Tugas Mata Kuliah Pemrograman Mobile, Teknik Informatika UMNU Kebumen

1. Analisis Komponen & Resource
Dalam pengembangan Android yang baik (Best Practices), kita mengatur tampilan (XML) terpisah dari aset dan nilai-nilai konstan (seperti warna, teks, dan gambar). Pada kode layout Anda, terdapat penggabungan antara resource eksternal kompilasi dan beberapa hardcoded values:
@drawable/bg_rounded_input, @drawable/bg_rounded_button, @drawable/bg_rounded_google: Ini adalah file XML Drawable Sub-component. Alih-alih mendesain kotak secara statis, kita memanggil shape eksternal untuk memberikan efek lengkung (rounded corners radius: 16dp) dan efek warna solid atau garis batas (stroke).
@drawable/ic_google: File vektor eksternal untuk menampilkan logo Google dengan resolusi mandiri (resolution-independent), sehingga tidak akan pecah di layar manapun.
@android:drawable/ic_menu_view: Resource bawaan Android (ikon mata) untuk melihat komponen kata sandi. Keuntungannya adalah kita tidak perlu menambahkan ikon manual karena sistem Android sudah menyediakannya.
Catatan Praktik Terbaik Akademis: Pada kode ini, teks (seperti "Selamat Datang") dan warna (seperti #7CB342) masih terprogram statis (hardcoded). Dalam dunia industri, sangat disarankan untuk mereferensikan warna melalui @color/nama_warna di colors.xml dan teks melalui @string/nama_teks di strings.xml. Pemisahan resource ini mempermudah proses lokalisasi (translasi bahasa) dan menjaga konsistensi tema (Design System) tanpa mengubah layout utama.
2. Logika dan Karakteristik Layout Utama (Linear Layout)
Struktur dokumen ini sepenuhnya bergantung pada paradigma LinearLayout. LinearLayout bekerja seperti "antrean"—ia menyusun semua elemen anak (child views) secara berurutan, baik berbaris ke bawah (Vertikal) maupun berderet ke samping (Horizontal).
Karakteristik & Atribut Kunci yang Digunakan:
android:orientation="vertical": View root (wadah paling luar) memiliki sifat ini. Artinya, setiap komponen UI dari teks sambutan hingga tombol 'Daftar' akan disusun merambat ke bawah dari atas secara linear berurutan.
android:gravity="center": Atribut ini memaksa semua isi konten di dalam root utama tertarik dan tersusun rapi di bagian tengah layar, membuat form login terlihat simetris.
android:orientation="horizontal": Digunakan pada LinearLayout bersarang (Nested Layout) seperti bagian Kata Sandi+Ikon Mata, baris Ingat Sandi+Lupa Sandi, pemisah "ATAU", dan bagian "Belum punya akun? Daftar". Ini menyusun elemennya menyamping dari kiri ke kanan.
android:layout_weight="1" dengan layout_width="0dp": Dapat dilihat pada bagian kolom Password, Space, dan garis Divider. Konsep ini adalah "Weight-based dimension". Dengan memberikan lebar 0dp dan bobot 1, kita menginstruksikan komponen tersebut untuk "memakan" atau mengisi sisa ruang kosong sekecil dan sebesar apapun ukuran layar peranti, memastikan komponen lain (seperti Ikon atau teks "Lupa sandi?") tetap memiliki tempat yang konsisten dipojok layar (Responsive Design).
Margin dan Padding: android:padding="32dp" pada root memberikan ruang bernafas di tepi layar, sedangkan layout_marginBottom digunakan untuk mendorong dan memberi jarak secara presisi antar setiap tumpukan layout/komponen di bawahnya.
3. Anatomi Visual (Pemetaan Antarmuka)
Dari sisi UI (User Interface), anatomi activity_main.xml ini membentuk alur Login Modern yang disederhanakan secara progresif top-down (atas ke bawah):
Header (Bagian Atas Layer):
Terdapat teks sambutan ("Selamat Datang") berukuran besar dan ditambahkan gaya Bold agar langsung menarik fokus User. Di bawahnya ditaruh sub-teks instruktif sekunder ("Masuk untuk melihat koleksi bunga hari ini") berwarna abu-abu halus agar tidak beradu visual terhadap Judul.
User Input Forms (Bagian Tengah):
Satu blok input murni (EditText) untuk Email.
Sebuah bungkus (LinearLayout horizontal) seolah-olah terlihat seperti kotak sandi tunggal berkat resource background bg_rounded_input. Di dalamnya diintegrasikan dua sub-objek: area input sandi (dengan properti textPassword untuk menyembunyikan titik/bintang) dan elemen ikon mata transparan di ujung kanan.
Action Bar Mini (Horizontal) berisi opsi cerdas: Tanda centang ("Ingat Sandi") pada area kiri layar dan tautan tekan ("Lupa Sandi?") yang terdorong elegan ke sebelah kanan layar.
Primary Control (Aksi Utama):
Tombol MASUK Utama: Menggunakan komponen yang ditingkatkan AppCompatButton dengan lebar membentangkan area layar (match_parent), dan background kehijauan bernuansa tegas, dirancang menonjol sebagai call-to-action primer.
Aksi Alternatif (Bagian Bawah):
Sistem pembatas (Divider) halus yang diisi teks "ATAU" diapit dua garis abu horizontal tipis buatan manual dari elemen <View>.
Tombol log-in pihak ketiga (Third-party Login), yaitu Masuk dengan Google. Didesain dengan profil warna terbalik/pucat (latar putih dengan border dan ikon) agar tidak merampas perhatian visual dari Aksi Utama (Tombol Hijau).
Footer (Bagian Dasar):
Sebuah Call-to-Action persuasif di baris terakhir berupa teks "Belum punya akun?" bersanding vertikal dengan tautan "Daftar" berwarna hijau yang konsisten dengan palet tema.
