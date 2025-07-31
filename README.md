# Catatan Singkat Git & GitHub (Cheatsheet)

Dokumen ini berisi rangkuman perintah dan konsep penting Git & GitHub yang telah kita diskusikan, dirancang untuk menjadi referensi cepat.

---

## 1. Konsep Dasar
Konsep fundamental yang menjadi dasar cara kerja Git dan kolaborasi.

### Git vs VCS Lain (Distributed vs Centralized)
* **Git (Distributed)**: Setiap developer memiliki salinan repositori lengkap. Operasi dilakukan secara lokal dan cepat.
* **VCS Lain (Centralized)**: Ada satu server pusat. Membutuhkan koneksi untuk hampir semua operasi.

### Konsep 3 Pohon (The Three Trees)
1.  **Working Directory**: Folder tempat Anda bekerja dan mengubah file.
2.  **Staging Area (Index)**: Area persiapan untuk mendaftarkan perubahan yang akan di-*commit* (via `git add`).
3.  **Repository (.git)**: "Brankas" tempat riwayat *commit* disimpan permanen (via `git commit`).

### Perbedaan Forking vs. Cloning
| Kriteria | Fork (di GitHub) | Clone (`git clone`) |
| :--- | :--- | :--- |
| **Lokasi Salinan** | Di server GitHub, ke akun Anda. | Dari server ke komputer lokal Anda. |
| **Kepemilikan** | Anda menjadi pemilik salinan. | Anda tidak menjadi pemilik. |
| **Tujuan Utama** | Kontribusi ke proyek orang lain (*open source*). | Bekerja pada proyek yang Anda miliki aksesnya. |

---

## 2. Alur Kerja Dasar
Perintah yang menjadi tulang punggung aktivitas harian.

| Perintah | Penjelasan |
| :--- | :--- |
| `git status` | Menampilkan status *Working Directory* dan *Staging Area*. |
| `git add <file>` | Menambahkan perubahan ke *Staging Area*. `git add .` untuk semua. |
| `git commit -m "Pesan"` | Menyimpan *snapshot* dari *Staging Area* ke *Repository*. |
| `git log` | Menampilkan riwayat *commit*. |

### Tips Menulis Pesan Commit
* **Gunakan Format**: `<tipe>: <subjek>`. Contoh: `feat: Tambah tombol login`. Tipe umum: `feat`, `fix`, `docs`, `style`, `refactor`, `chore`.
* **Gunakan Kalimat Perintah**: "Tambah", "Perbaiki", "Hapus" (bukan "Menambahkan", "Diperbaiki").
* **Jelaskan "Mengapa"**: Jika perlu, gunakan *body* (setelah baris kosong) untuk menjelaskan konteks perubahan.

---

## 3. Branching & Merging
Mengelola berbagai lini pengembangan.

| Perintah | Penjelasan |
| :--- | :--- |
| `git branch <nama>` | Membuat *branch* baru. |
| `git checkout <nama>` | Berpindah ke *branch* lain. |
| `git merge <nama>` | Menggabungkan riwayat dari `<nama>` ke *branch* saat ini. |

### Tipe Merge
* **Fast-Forward**: Terjadi jika *branch* utama tidak berubah. Riwayat tetap lurus.
* **Non-Fast-Forward (Merge Commit)**: Terjadi jika *branch* utama sudah berubah. Membuat *commit* baru yang menandakan adanya penggabungan.

### Penanganan Merge Conflict
1.  `git status` untuk melihat file yang konflik.
2.  Buka file, hapus penanda `<<<`, `===`, `>>>`, dan sisakan kode yang benar.
3.  `git add <file>` untuk menandai konflik selesai.
4.  `git commit` untuk menyelesaikan *merge*.

---

## 4. Mengubah Riwayat (History Rewriting)
⚠️ **Peringatan**: Jangan gunakan perintah di bawah ini pada *commit* yang sudah di-*push* dan dibagikan ke tim!

### Memperbaiki Commit Terakhir (`--amend`)
* **Tujuan**: Menambah atau memperbaiki perubahan pada *commit* terakhir tanpa membuat *commit* baru.
* **Cara**: Lakukan perbaikan -> `git add .` -> `git commit --amend --no-edit`.

### Rebase: Meluruskan Riwayat
* **Tujuan**: Memindahkan titik awal sebuah *branch* ke ujung *branch* lain (`main`) untuk menciptakan riwayat yang lurus.
* **Cara**: `git checkout feature-branch` -> `git rebase main`.

### Squash: Meringkas Riwayat
* **Tujuan**: Menggabungkan beberapa *commit* kecil menjadi satu *commit* tunggal yang rapi.
* **Cara**: `git checkout main` -> `git merge --squash feature-branch` -> `git commit -m "Pesan baru"`.

---

## 5. Bekerja dengan Remote (GitHub)

| Perintah | Penjelasan |
| :--- | :--- |
| `git fetch origin` | **Mengunduh** data baru dari remote, **tidak mengubah** *branch* lokal. |
| `git pull origin <branch>` | **Mengunduh (fetch) DAN menggabungkan (merge)** dalam satu langkah. |
| `git push origin <branch>` | **Mengirim** *commit* dari lokal ke remote. |

---

## 6. Menyimpan Sementara (`stash`)
Menyimpan perubahan yang belum selesai tanpa perlu *commit*.

| Perintah | Penjelasan |
| :--- | :--- |
| `git stash` | Menyimpan perubahan pada file yang sudah di-*track*. |
| `git stash -u` | Menyimpan perubahan, termasuk file baru (*untracked*). |
| `git stash list` | Menampilkan daftar simpanan. |
| `git stash pop` | Menerapkan simpanan terakhir dan menghapusnya dari daftar. |
| `git stash apply <nama>` | Menerapkan simpanan spesifik tanpa menghapusnya. |

---

## 7. Ekosistem & Kolaborasi GitHub

* **Dokumentasi Proyek**: File penting seperti `README.md` (info proyek), `CONTRIBUTING.md` (panduan kontribusi), `LICENSE` (lisensi), dan `CHANGELOG.md` (riwayat perubahan).
* **GitHub Wikis**: Tempat untuk dokumentasi proyek yang lebih luas seperti panduan pengguna, FAQ, dll.
* **GitHub API (REST & GraphQL)**: "Jembatan" yang memungkinkan aplikasi/skrip Anda berinteraksi dengan data GitHub secara otomatis.
* **Webhooks**: Mekanisme notifikasi otomatis. "Jika X terjadi, beri tahu aplikasi saya." Contoh: Memicu *deployment* saat ada *push* baru.
* **GitHub Apps**: Aplikasi pihak ketiga yang berintegrasi dengan GitHub untuk mengotomatiskan tugas dan memperluas fungsionalitas.
