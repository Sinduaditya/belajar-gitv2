# Catatan Singkat Git (Git Cheatsheet) untuk Belajar

Dokumen ini berisi rangkuman perintah dan konsep penting Git yang telah kita diskusikan, dirancang untuk menjadi referensi cepat.

---

## Konsep Dasar
Konsep fundamental yang menjadi dasar cara kerja Git.

### Git vs VCS Lain (Distributed vs Centralized)
* **Git (Distributed/Terdistribusi)**: Setiap developer memiliki salinan repositori yang lengkap. Operasi seperti `commit` dan `branch` dilakukan secara lokal dan cepat. Tidak ada *single point of failure*.
* **VCS Lain (Centralized/Terpusat)**: Ada satu server pusat. Developer harus terhubung ke server untuk melakukan hampir semua operasi. Alur kerjanya cenderung linear.

### Konsep 3 Pohon (The Three Trees)
Git memisahkan pekerjaan Anda ke dalam tiga "area" utama:
1.  **Working Directory**: Folder tempat Anda bekerja dan mengubah file secara langsung.
2.  **Staging Area (Index)**: Area persiapan tempat Anda mendaftarkan perubahan yang ingin Anda simpan di *commit* selanjutnya (menggunakan `git add`).
3.  **Repository (.git)**: "Brankas" tempat Git menyimpan semua riwayat *commit* Anda secara permanen (menggunakan `git commit`).

---

## Alur Kerja Dasar Sehari-hari
Perintah yang menjadi tulang punggung penggunaan Git.

| Perintah | Penjelasan |
| :--- | :--- |
| `git status` | Menampilkan status *Working Directory* dan *Staging Area*. Perintah terpenting untuk mengetahui apa yang sedang terjadi. |
| `git add <file>` | Menambahkan perubahan file ke *Staging Area*. Gunakan `git add .` untuk menambahkan semua perubahan. |
| `git commit -m "Pesan"` | Menyimpan *snapshot* dari *Staging Area* secara permanen ke *Repository*. |
| `git log` | [cite_start]Menampilkan riwayat *commit* dari yang terbaru hingga terlama. [cite: 1] |

---

## Bekerja dengan Branch
Mengelola berbagai lini pengembangan secara paralel.

| Perintah | Penjelasan |
| :--- | :--- |
| `git branch <nama>` | Membuat *branch* baru. |
| `git checkout <nama>` | Berpindah ke *branch* lain. |
| `git merge <nama>` | Menggabungkan riwayat dari `<nama>` ke *branch* Anda saat ini. |

### Penanganan Merge Conflict
Terjadi saat Git tidak bisa menggabungkan perubahan secara otomatis.
1.  Jalankan `git status` untuk melihat file yang konflik.
2.  Buka file tersebut, hapus penanda `<<<<<<<`, `=======`, `>>>>>>>`, dan sisakan hanya kode akhir yang Anda inginkan.
3.  Jalankan `git add <file>` untuk menandai konflik telah selesai.
4.  Jalankan `git commit` untuk menyelesaikan proses *merge*.

---

## Bekerja dengan Remote (GitHub, dll.)
Berinteraksi dan berkolaborasi dengan repositori di server.

| Perintah | Penjelasan |
| :--- | :--- |
| `git clone <url>` | Mengunduh salinan repositori dari remote ke lokal. |
| `git push origin <branch>` | [cite_start]Mengirim *commit* dari *branch* lokal ke remote. [cite: 1] |
| `git pull origin <branch>` | [cite_start]Mengambil (`fetch`) perubahan dari remote DAN langsung menggabungkannya (`merge`). [cite: 1] |
| `git fetch origin` | Hanya mengambil perubahan dari remote tanpa menggabungkannya ke *branch* kerja Anda. |

### Mengakses Branch Remote Baru
1.  `git fetch origin`: Ambil semua informasi terbaru dari remote.
2.  `git checkout <nama-branch-baru>`: Git akan otomatis membuat *branch* lokal yang terhubung ke *branch* remote tersebut.

---

## Memperbaiki & Menyimpan Sementara

### Memperbaiki Commit Terakhir (`--amend`)
Digunakan untuk merevisi *commit* terakhir jika ada yang ketinggalan atau salah ketik. [cite_start]**Peringatan**: Jangan gunakan pada *commit* yang sudah di-*push*. [cite: 1]
```bash
# Lakukan perbaikan pada file
git add <file-yang-diperbaiki>
git commit --amend --no-edit
```

### Menyimpan Pekerjaan Sementara (`stash`)
Menyimpan perubahan yang belum selesai tanpa perlu *commit*.
| Perintah | Penjelasan |
| :--- | :--- |
| `git stash` | Menyimpan perubahan pada file yang sudah di-*track*. |
| `git stash -u` | Menyimpan perubahan, termasuk file baru yang belum di-*track* (*untracked*). |
| `git stash list` | Menampilkan semua daftar simpanan. |
| `git stash pop` | Menerapkan simpanan terakhir dan menghapusnya dari daftar. |
| `git stash apply <nama>` | Menerapkan simpanan spesifik tanpa menghapusnya dari daftar. |
| `git stash drop <nama>` | Menghapus simpanan spesifik dari daftar. |

---

## Praktik Terbaik (Best Practices)
* **Commit Sering, Push Saat Siap**: Lakukan `commit` secara lokal sesering mungkin untuk menyimpan progres. Lakukan `push` ketika sebuah fitur sudah selesai atau di akhir hari kerja.
* **Satu Commit, Satu Perubahan Logis**: Usahakan setiap *commit* mewakili satu perubahan yang utuh dan logis (misal: "Menambahkan Fitur A"). Ini membuat riwayat proyek mudah dibaca dan dikelola.
