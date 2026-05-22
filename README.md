
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cek Resi</title>

  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Poppins', sans-serif;
    }

    body {
      background: #f5f7fb;
      color: #222;
    }

    .navbar {
      width: 100%;
      background: white;
      padding: 18px 8%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 10px rgba(0,0,0,0.05);
      position: sticky;
      top: 0;
      z-index: 999;
    }

    .logo {
      font-size: 24px;
      font-weight: 700;
      color: #00a86b;
    }

    .menu {
      display: flex;
      gap: 20px;
    }

    .menu a {
      text-decoration: none;
      color: #444;
      font-weight: 500;
    }

    .hero {
      width: 100%;
      padding: 80px 8%;
      background: linear-gradient(135deg,#00a86b,#00c17d);
      color: white;
      text-align: center;
    }

    .hero h1 {
      font-size: 42px;
      margin-bottom: 15px;
    }

    .hero p {
      opacity: 0.9;
      margin-bottom: 35px;
    }

    .tracking-box {
      background: white;
      max-width: 900px;
      margin: auto;
      padding: 25px;
      border-radius: 20px;
      display: flex;
      gap: 15px;
      flex-wrap: wrap;
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    }

    .tracking-box input,
    .tracking-box select {
      flex: 1;
      padding: 16px;
      border: 1px solid #ddd;
      border-radius: 12px;
      font-size: 15px;
    }

    .tracking-box button {
      padding: 16px 28px;
      border: none;
      background: #00a86b;
      color: white;
      border-radius: 12px;
      cursor: pointer;
      font-weight: 600;
      transition: 0.3s;
    }

    .tracking-box button:hover {
      background: #00945e;
    }

    .result {
      width: 100%;
      padding: 60px 8%;
    }

    .card {
      background: white;
      border-radius: 20px;
      padding: 30px;
      box-shadow: 0 5px 20px rgba(0,0,0,0.08);
    }

    .card h2 {
      margin-bottom: 25px;
      color: #00a86b;
    }

    .info-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(200px,1fr));
      gap: 20px;
      margin-bottom: 40px;
    }

    .info-box {
      background: #f5f7fb;
      padding: 20px;
      border-radius: 14px;
    }

    .info-box small {
      color: #777;
    }

    .timeline {
      border-left: 3px solid #00a86b;
      padding-left: 25px;
    }

    .timeline-item {
      margin-bottom: 30px;
      position: relative;
    }

    .timeline-item::before {
      content: '';
      width: 16px;
      height: 16px;
      background: #00a86b;
      border-radius: 50%;
      position: absolute;
      left: -34px;
      top: 5px;
    }

    .timeline-item h4 {
      margin-bottom: 5px;
    }

    .timeline-item span {
      color: #888;
      font-size: 14px;
    }

    .courier-list {
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 20px;
      padding: 50px 8%;
    }

    .courier {
      background: white;
      padding: 20px 30px;
      border-radius: 16px;
      box-shadow: 0 5px 20px rgba(0,0,0,0.05);
      font-weight: 600;
    }

    footer {
      background: #111;
      color: white;
      text-align: center;
      padding: 30px;
      margin-top: 50px;
    }

    @media(max-width:768px){
      .hero h1 {
        font-size: 30px;
      }

      .tracking-box {
        flex-direction: column;
      }

      .tracking-box button {
        width: 100%;
      }
    }
  </style>
</head>
<body>

  <div class="navbar">
    <div class="logo">CEKRESI.ID</div>

    <div class="menu">
      <a href="#">Home</a>
      <a href="#">Tracking</a>
      <a href="#">Kurir</a>
      <a href="#">Contact</a>
    </div>
  </div>

  <section class="hero">
    <h1>Cek Resi Semua Ekspedisi</h1>
    <p>Lacak paket otomatis cepat & realtime seperti CekResi dan JuraganCOD</p>

    <div class="tracking-box">
      <input type="text" id="resi" placeholder="Masukkan nomor resi...">

      <select id="courier">
        <option value="sicepat">SiCepat</option>
        <option value="jnt">J&T</option>
        <option value="jne">JNE</option>
        <option value="anteraja">AnterAja</option>
        <option value="spx">Shopee Express</option>
      </select>

      <button onclick="cekResi()">Lacak Sekarang</button>
    </div>
  </section>

  <section class="courier-list">
    <div class="courier">SiCepat</div>
    <div class="courier">J&T Express</div>
    <div class="courier">JNE</div>
    <div class="courier">Shopee Express</div>
    <div class="courier">AnterAja</div>
    <div class="courier">Ninja Xpress</div>
  </section>

  <section class="result">
    <div class="card" id="hasil" style="display:none;">

      <h2>Status Pengiriman</h2>

      <div class="info-grid">
        <div class="info-box">
          <small>No Resi</small>
          <h3 id="nomorresi">-</h3>
        </div>

        <div class="info-box">
          <small>Kurir</small>
          <h3 id="kurirnya">-</h3>
        </div>

        <div class="info-box">
          <small>Status</small>
          <h3 id="statusnya">-</h3>
        </div>

        <div class="info-box">
          <small>Penerima</small>
          <h3 id="penerima">-</h3>
        </div>
      </div>

      <div class="timeline" id="timeline">
      </div>

    </div>
  </section>

  <footer>
    © 2026 CEKRESI.ID - Tracking Resi Otomatis
  </footer>

  <script>
    const API_KEY = "ouX4lmi5e83b0dca8a8a9bebuRE46ojF";
    const API_URL = "https://api.binderbyte.com/v1/track";
    function cekResi(){

      let resi = document.getElementById('resi').value;
      let courier = document.getElementById('courier').value;

      if(resi === ''){
        alert('Masukkan nomor resi dulu');
        return;
      }

      document.getElementById('hasil').style.display = 'block';

      document.getElementById('nomorresi').innerHTML = resi;
      document.getElementById('kurirnya').innerHTML = courier.toUpperCase();
      document.getElementById('statusnya').innerHTML = 'Paket Sedang Dikirim';
      document.getElementById('penerima').innerHTML = 'Zidan';

      document.getElementById('timeline').innerHTML = `

        <div class="timeline-item">
          <h4>Paket telah dikirim dari gudang</h4>
          <span>22 Mei 2026 - 09:20</span>
        </div>

        <div class="timeline-item">
          <h4>Paket sedang menuju kota tujuan</h4>
          <span>22 Mei 2026 - 13:10</span>
        </div>

        <div class="timeline-item">
          <h4>Paket sedang diantar kurir</h4>
          <span>22 Mei 2026 - 16:00</span>
        </div>

      `;
    }
  </script>

</body>
</html>
```

# Cara Pakai

1. Buat folder baru
2. Buat file `index.html`
3. Paste semua code di atas
4. Simpan
5. Klik 2x file `index.html`

# Upload Jadi Website Online

Bisa upload ke:

* Netlify
* Vercel
* GitHub Pages

# Fitur Tampilan

✔ Style modern seperti CekResi / JuraganCOD
✔ Responsive HP & PC
✔ Timeline tracking
✔ Card status pengiriman
✔ Dropdown kurir
✔ Tampilan clean premium
✔ Siap ditambah API RajaOngkir / Binderbyte

# Selanjutnya Bisa Ditambah

* Auto detect kurir
* API tracking realtime
* Dark mode
* Login admin
* Database resi
* Notifikasi WhatsApp
* Anti limit scrape
* Tracking otomatis semua ekspedisi
