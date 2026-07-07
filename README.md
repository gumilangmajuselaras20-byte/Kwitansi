<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kwitansi - PT. GUMILANG MAJU SELARAS</title>
    <style>
        body {
            font-family: 'Courier New', Courier, monospace;
            background-color: #f4f4f4;
            padding: 20px;
            margin: 0;
        }
        .container {
            max-width: 800px;
            margin: auto;
        }
        /* Form Input - Sembunyi saat cetak */
        .form-input {
            background: #fff;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            font-family: Arial, sans-serif;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        .form-group input, .form-group textarea {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        /* Kwitansi Tampilan */
        .kwitansi-box {
            background: #fff;
            padding: 30px;
            border: 2px solid #333;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 3px double #333;
            padding-bottom: 15px;
            margin-bottom: 20px;
        }
        .identitas-perusahaan {
            display: flex;
            align-items: center;
            gap: 20px;
        }
        .logo-perusahaan img {
            width: 80px;
            height: auto;
            object-fit: contain;
        }
        .perusahaan h2 { 
            margin: 0 0 5px 0; 
            text-transform: uppercase; 
            font-size: 18px;
            font-family: Arial, sans-serif;
            font-weight: bold;
        }
        .perusahaan p { 
            margin: 2px 0; 
            font-size: 11px; 
            font-family: Arial, sans-serif;
            color: #333;
            line-height: 1.4;
        }
        .judul { text-align: right; }
        .judul h1 { margin: 0; font-size: 28px; letter-spacing: 2px; }
        .row {
            display: flex;
            margin-bottom: 15px;
            align-items: baseline;
        }
        .label { width: 200px; font-weight: bold; }
        .titik-dua { width: 20px; }
        .konten { flex: 1; border-bottom: 1px dashed #999; padding-bottom: 3px; }
        .terbilang-box { background-color: #e9e9e9; font-style: italic; padding: 8px; font-weight: bold; }
        .footer {
            margin-top: 40px;
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
        }
        .jumlah-bayar {
            border: 2px solid #333;
            padding: 10px 20px;
            font-size: 20px;
            font-weight: bold;
            background-color: #f9f9f9;
        }
        .tanda-tangan { text-align: center; width: 200px; }
        .tanda-tangan .tanggal { margin-bottom: 60px; }
        .tanda-tangan .nama { border-top: 1px solid #333; padding-top: 5px; font-weight: bold; }
        
        .btn-cetak {
            display: block;
            width: 100%;
            padding: 12px;
            background-color: #27ae60;
            color: white;
            text-align: center;
            border: none;
            cursor: pointer;
            font-size: 16px;
            font-family: Arial, sans-serif;
            border-radius: 4px;
            margin-top: 10px;
        }

        /* Aturan Cetak */
        @media print {
            .form-input, .btn-cetak { display: none !important; }
            body { background-color: #fff; padding: 0; }
            .kwitansi-box { border: 2px solid #000; box-shadow: none; padding: 20px; }
        }
    </style>
</head>
<body>

<div class="container">
    <div class="form-input">
        <h3 style="margin-top:0; font-family: Arial;">Isi Data Transaksi Kwitansi</h3>
        <div class="form-group">
            <label>Nomor Kwitansi</label>
            <input type="text" id="inNo" value="KW-2026-001">
        </div>
        <div class="form-group">
            <label>Diterima Dari</label>
            <input type="text" id="inNama" value="Budi Santoso">
        </div>
        <div class="form-group">
            <label>Jumlah Uang (Angka saja)</label>
            <input type="number" id="inUang" value="1500000">
        </div>
        <div class="form-group">
            <label>Untuk Pembayaran</label>
            <textarea id="inUntuk" rows="2">Pembayaran pengadaan barang inventaris kantor</textarea>
        </div>
        <div class="form-group">
            <label>Kota & Tanggal</label>
            <input type="text" id="inTanggal" value="Bandung, 7 Juli 2026">
        </div>
        <button class="btn-cetak" onclick="window.print()">Cetak Kwitansi</button>
    </div>

    <div class="kwitansi-box">
        <div class="header">
            <div class="identitas-perusahaan">
                <div class="logo-perusahaan">
                    <img src="logo.png" alt="Logo PT">
                </div>
                <div class="perusahaan">
                    <h2>PT. GUMILANG MAJU SELARAS</h2>
                    <p>Jl. Kencana Wangi I No. 10, Komplek Pandan Wangi, Bandung 40287</p>
                    <p>HP. 0822 1884 4662 | Email: gumilangmajuselaras@gmail.com</p>
                </div>
            </div>
            <div class="judul">
                <h1>KWITANSI</h1>
                <div id="outNo" style="font-size: 16px; margin-top: 5px;">No. <b>-</b></div>
            </div>
        </div>

        <div class="row">
            <div class="label">Telah Diterima Dari</div>
            <div class="titik-dua">:</div>
            <div class="konten" id="outNama">-</div>
        </div>

        <div class="row">
            <div class="label">Uang Sejumlah</div>
            <div class="titik-dua">:</div>
            <div class="konten terbilang-box" id="outTerbilang">-</div>
        </div>

        <div class="row">
            <div class="label">Untuk Pembayaran</div>
            <div class="titik-dua">:</div>
            <div class="konten" id="outUntuk">-</div>
        </div>

        <div class="footer">
            <div class="jumlah-bayar" id="outUang">
                Rp. 0,-
            </div>
            <div class="tanda-tangan">
                <div class="tanggal" id="outTanggal">-</div>
                <div class="nama">Kasir / Admin</div>
            </div>
        </div>
    </div>
</div>

<script>
    // Fungsi Konversi Angka ke Kata Terbilang Bahasa Indonesia
    function kekata(angka) {
        const bilne = ["", "Satu", "Dua", "Tiga", "Empat", "Lima", "Enam", "Tujuh", "Delapan", "Sembilan", "Sepuluh", "Sebelas"];
        let temp = "";
        if (angka < 12) { temp = " " + bilne[angka]; }
        else if (angka < 20) { temp = kekata(angka - 10) + " Belas"; }
        else if (angka < 100) { temp = kekata(Math.floor(angka / 10)) + " Puluh" + kekata(angka % 10); }
        else if (angka < 200) { temp = " Seratus" + kekata(angka - 100); }
        else if (angka < 1000) { temp = kekata(Math.floor(angka / 100)) + " Ratus" + kekata(angka % 100); }
        else if (angka < 2000) { temp = " Seribu" + kekata(angka - 1000); }
        else if (angka < 1000000) { temp = kekata(Math.floor(angka / 1000)) + " Ribu" + kekata(angka % 1000); }
        else if (angka < 1000000000) { temp = kekata(Math.floor(angka / 1000000)) + " Juta" + kekata(angka % 1000000); }
        return temp;
    }

    function updateKwitansi() {
        // Ambil Nilai Input
        const no = document.getElementById('inNo').value;
        const nama = document.getElementById('inNama').value;
        const uang = parseInt(document.getElementById('inUang').value) || 0;
        const untuk = document.getElementById('inUntuk').value;
        const tanggal = document.getElementById('inTanggal').value;

        // Format Rupiah
        const formatRupiah = "Rp. " + uang.toLocaleString('id-ID') + ",-";
        
        // Terbilang
        const terbilang = uang > 0 ? kekata(uang) + " Rupiah" : "Nol Rupiah";

        // Update ke Tampilan Kwitansi
        document.getElementById('outNo').innerHTML = "No. <b>" + no + "</b>";
        document.getElementById('outNama').innerText = nama;
        document.getElementById('outUntuk').innerText = untuk;
        document.getElementById('outTanggal').innerText = tanggal;
        document.getElementById('outUang').innerText = formatRupiah;
        document.getElementById('outTerbilang').innerText = terbilang.trim();
    }

    // Pasang Event Listener
    const inputs = ['inNo', 'inNama', 'inUang', 'inUntuk', 'inTanggal'];
    inputs.forEach(id => {
        document.getElementById(id).addEventListener('input', updateKwitansi);
    });

    // Jalankan pertama kali saat reload
    updateKwitansi();
</script>

</body>
</html>
