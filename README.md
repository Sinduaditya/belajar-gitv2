# 📌 Git & GitHub Cheatsheet (Ringkas & Praktis)

Dokumen ini berisi rangkuman perintah dan konsep penting Git & GitHub sebagai referensi cepat.

---

## 1. Konsep Dasar

### Git vs VCS Lain (Distributed vs Centralized)

* **Git (Distributed)**: Setiap developer punya salinan repositori lengkap → bisa bekerja offline, lebih cepat.
* **VCS Lain (Centralized)**: Ada satu server pusat → butuh koneksi untuk hampir semua operasi.

### Konsep 3 Pohon (The Three Trees)

1. **Working Directory** → Folder tempat mengedit file.
2. **Staging Area (Index)** → Tempat menandai perubahan sebelum di-*commit*. (`git add`)
3. **Repository (.git)** → Riwayat permanen proyek. (`git commit`)

### Forking vs Cloning

| Kriteria           | Fork (di GitHub)       | Clone (`git clone`)                       |
| :----------------- | :--------------------- | :---------------------------------------- |
| **Lokasi Salinan** | Di akun GitHub Anda    | Di komputer lokal                         |
| **Kepemilikan**    | Jadi pemilik salinan   | Hanya salinan kerja                       |
| **Tujuan Utama**   | Kontribusi open source | Bekerja di repo yang Anda miliki aksesnya |

---

## 2. Alur Kerja Dasar

| Perintah                | Penjelasan                                                       |
| :---------------------- | :--------------------------------------------------------------- |
| `git status`            | Cek status *working dir* & *staging area*.                       |
| `git add <file>`        | Tambahkan perubahan ke *staging area*. (`git add .` untuk semua) |
| `git commit -m "pesan"` | Simpan snapshot ke repo.                                         |
| `git log`               | Lihat riwayat *commit*.                                          |

**Tips Commit:**

* Format: `<tipe>: <subjek>` → `feat: Tambah tombol login`
* Tipe umum: `feat`, `fix`, `docs`, `style`, `refactor`, `chore`
* Gunakan kata kerja bentuk perintah: *Tambah*, *Perbaiki*, *Hapus*.
* Jelaskan **mengapa**, bukan hanya **apa**.

---

## 3. Branching & Merging

| Perintah              | Penjelasan                             |
| :-------------------- | :------------------------------------- |
| `git branch <nama>`   | Buat branch baru.                      |
| `git checkout <nama>` | Pindah branch.                         |
| `git switch <nama>`   | (alternatif modern `checkout`)         |
| `git merge <nama>`    | Gabungkan `<nama>` ke branch saat ini. |

### Jenis Merge

* **Fast-Forward** → Riwayat lurus, tidak ada commit baru.
* **Merge Commit** → Buat commit baru untuk penggabungan.

### Menangani Merge Conflict

1. `git status` → lihat file yang konflik
2. Edit file, hapus tanda `<<< === >>>`
3. `git add <file>`
4. `git commit`

---

## 4. Mengubah Riwayat

⚠️ Jangan lakukan di commit yang sudah di-*push* ke remote publik.

* **Amend (perbaiki commit terakhir)**

  ```bash
  git add .
  git commit --amend --no-edit
  ```

* **Rebase (luruskan riwayat)**

  ```bash
  git checkout feature
  git rebase main
  ```

* **Squash (gabungkan commit kecil)**

  ```bash
  git checkout main
  git merge --squash feature
  git commit -m "Gabungkan perubahan feature"
  ```

---

## 5. Remote (GitHub)

| Perintah                   | Penjelasan                         |
| :------------------------- | :--------------------------------- |
| `git fetch origin`         | Ambil data terbaru (tidak gabung). |
| `git pull origin <branch>` | Fetch + merge.                     |
| `git push origin <branch>` | Kirim commit ke remote.            |

---

## 6. Stash (Simpan Sementara)

| Perintah               | Penjelasan                             |
| :--------------------- | :------------------------------------- |
| `git stash`            | Simpan perubahan tracked files.        |
| `git stash -u`         | Simpan termasuk file baru.             |
| `git stash list`       | Lihat daftar stash.                    |
| `git stash pop`        | Terapkan & hapus stash terakhir.       |
| `git stash apply <id>` | Terapkan stash tertentu (tanpa hapus). |

---

## 7. Kolaborasi di GitHub

* **File Penting**: `README.md`, `CONTRIBUTING.md`, `LICENSE`, `CHANGELOG.md`.
* **GitHub Wiki**: Dokumentasi lebih lengkap.
* **GitHub API**: Automasi lewat REST/GraphQL.
* **Webhooks**: Notifikasi otomatis (misal deploy setelah push).
* **GitHub Apps**: Integrasi otomatis (misal CI/CD).

---

## 8. Pull Request via CLI

Selain membuat PR lewat web GitHub, bisa juga lewat CLI.

### Dengan GitHub CLI (`gh`)

1. Install [GitHub CLI](https://cli.github.com/)
2. Buat PR:

   ```bash
   gh pr create --base main --head feature-branch --title "feat: Tambah login" --body "Menambahkan fitur login"
   ```
3. Buka PR di browser:

   ```bash
   gh pr view --web
   ```

### Dengan Git Saja (Manual)

1. Push branch ke remote:

   ```bash
   git push origin feature-branch
   ```
2. Buka browser ke repo GitHub → Akan muncul tombol **Compare & Pull Request**.

---

