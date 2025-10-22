### Kode HTML dengan Sistem Login

```html
<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Portal-web dasar Perekonomian Indonesia</title>
  <meta name="description" content="Situs tematik ekonomi: indikator, berita singkat, dan analisis sederhana. HTML & CSS murni." />
  <style>
    /* ... (style yang sudah ada) ... */
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="brand">
        <div class="logo">K4</div>
        <div>
          <h1>Portal Ekonomi</h1>
          <p>Indikator • Analisis • Berita</p>
        </div>
      </div>
      <nav>
        <a href="#utama" class="active">Beranda</a>
        <a href="#indikator">Indikator</a>
        <a href="#analisis">Analisis</a>
        <a href="#berita">Berita</a>
        <a href="#langganan">Langganan</a>
        <a href="#tentang-kami">Tentang Kami</a>
        <button id="btnLogin">Login</button>
        <button id="btnLogout" style="display:none;">Logout</button>
      </nav>
    </header>

    <main>
      <!-- ... (konten yang sudah ada) ... -->
    </main>

    <footer>© 2025 Portal Ekonomi — Dibuat oleh mahasiswa Universitas Indraprasta PGRI</footer>
  </div>

  <!-- Modal Login -->
  <div id="modal" style="display:none;">
    <div>
      <h2>Masuk</h2>
      <form id="loginForm">
        <input type="email" id="loginEmail" placeholder="Email" required />
        <input type="password" id="loginPass" placeholder="Kata sandi" required />
        <button type="submit">Masuk</button>
      </form>
      <button id="closeModal">Tutup</button>
    </div>
  </div>

  <script>
    const modal = document.getElementById('modal');
    const btnLogin = document.getElementById('btnLogin');
    const btnLogout = document.getElementById('btnLogout');
    const closeModalBtn = document.getElementById('closeModal');

    // Modal open/close
    function openModal() {
      modal.style.display = 'block';
    }
    function closeModal() {
      modal.style.display = 'none';
    }

    btnLogin.addEventListener('click', openModal);
    closeModalBtn.addEventListener('click', closeModal);

    // LocalStorage helpers
    function saveSession(email) { localStorage.setItem('user', email); }
    function getSession() { return localStorage.getItem('user'); }
    function clearSession() { localStorage.removeItem('user'); }

    function updateAuthUI() {
      const email = getSession();
      if (email) {
        btnLogin.style.display = 'none';
        btnLogout.style.display = '';
      } else {
        btnLogin.style.display = '';
        btnLogout.style.display = 'none';
      }
    }

    // Login
    document.getElementById('loginForm').addEventListener('submit', (event) => {
      event.preventDefault();
      const email = document.getElementById('loginEmail').value.trim();
      const pass = document.getElementById('loginPass').value.trim();
      if (!email || !pass) return alert('Lengkapi email dan kata sandi.');

      const users = JSON.parse(localStorage.getItem('users') || '[]');
      const found = users.find(u => u.email === email && u.pass === pass);
      if (!found) return alert('Email atau kata sandi salah.');

      saveSession(email);
      updateAuthUI();
      closeModal();
    });

    // Logout
    btnLogout.addEventListener('click', () => {
      clearSession();
      updateAuthUI();
    });

    // Init
    updateAuthUI();
  </script>
</body>
</html>
```

### Penjelasan Kode
1. **Modal Login**: Ditambahkan modal untuk login yang berisi form untuk memasukkan email dan kata sandi.
2. **LocalStorage**: Menggunakan `localStorage` untuk menyimpan sesi pengguna. Pengguna yang berhasil login akan disimpan di `localStorage`.
3. **Event Listeners**: Menambahkan event listeners untuk tombol login, logout, dan form login.
4. **Update UI**: Fungsi `updateAuthUI` untuk memperbarui tampilan berdasarkan status login pengguna.

### Catatan
- Pastikan Anda memiliki data pengguna yang disimpan di `localStorage` dalam format JSON. Anda dapat menambahkan pengguna dengan cara yang sama seperti pada kode register yang ada di bagian lain dari aplikasi Anda.
- Anda dapat menyesuaikan gaya modal sesuai dengan desain yang ada di halaman Anda.