<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kwitansi - Template Fleksibel 1 Halaman</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
            display: flex;
            gap: 20px;
            justify-content: center;
        }

        /* --- Panel Form Pengisian (Sisi Kiri) --- */
        .form-panel {
            width: 320px;
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            height: fit-content;
        }
        .form-panel h3 { margin-top: 0; margin-bottom: 15px; color: #333; }
        .form-group { margin-bottom: 12px; }
        .form-group label { display: block; margin-bottom: 5px; font-weight: bold; font-size: 13px; }
        .form-group input, .form-group textarea {
            width: 100%; padding: 8px; box-sizing: border-box;
            border: 1px solid #ccc; border-radius: 4px; font-family: Arial, sans-serif;
        }
        .btn-cetak {
            display: block; width: 100%; padding: 12px;
            background-color: #27ae60; color: white; text-align: center;
            border: none; cursor: pointer; font-size: 16px; font-weight: bold;
            border-radius: 4px; margin-top: 15px;
        }
        .btn-cetak:hover { background-color: #219150; }

        /* --- Kertas Kwitansi A4 (Sisi Kanan) --- */
        .a4-document {
            width: 210mm;
            height: 297mm; /* Kunci tinggi A4 pas agar tidak overflow ke page 2 */
            background: #fff;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: relative;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        /* --- Kop Gambar Atas: Dibuat Full Menyentuh Sisi Kertas --- */
        .kop-gambar-atas {
            width: 100%;
            margin: 0;
            padding: 0;
        }
        .kop-gambar-atas img {
            width: 100%;
            height: auto;
            display: block;
        }

        /* --- Isi Konten Kwitansi dengan Padding Internal --- */
        .kwitansi-content {
            position: relative;
            z-index: 3;
            flex-grow: 1;
            padding: 10mm 20mm 15mm 20mm; /* Sisi text tetap aman berjarak dari pinggir kertas */
            display: flex;
            flex-direction: column;
        }
        
        .kwitansi-header-detail {
            display: flex;
            justify-content: flex-end;
            align-items: flex-end;
            margin-bottom: 5px;
        }
        
        .judul-kwitansi-box { text-align: right; }
        .judul-kwitansi-box h1 { margin: 0; font-size: 32px; letter-spacing: 2px; color: #333; }
        .judul-kwitansi-box p { margin: 5px 0 0 0; font-size: 14px; font-weight: bold; }

        .garis-pembatas {
            border-top: 1px solid #333; border-bottom: 3px double #333;
            height: 2px; margin: 15px 0 30px 0;
        }

        /* --- Baris Isi Data Transaksi --- */
        .kwitansi-row { display: flex; margin-bottom: 22px; align-items: baseline; }
        .row-label { width: 180px; font-weight: bold; font-size: 15px; color: #222; }
        .row-colon { width: 20px; font-size: 15px; }
        .row-value { flex: 1; border-bottom: 1px dashed #888; padding-bottom: 3px; font-size: 15px; color: #333; }
        
        .box-terbilang { 
            background-color: #f5f5f5; font-style: italic; padding: 12px; 
            font-weight: bold; border-radius: 4px; color: #333; border-left: 4px solid #666;
            font-size: 15px;
        }

        /* --- Bagian Tanda Tangan & Nominal --- */
        .kwitansi-footer {
            margin-top: 40px; 
            display: flex; 
            justify-content: space-between; 
            align-items: flex-end;
            margin-bottom: 30px;
        }
        .box-nominal {
            border: 2px solid #333; padding: 12px 25px; font-size: 24px;
            font-weight: bold; background-color: #f9f9f9; font-family: 'Courier New', monospace;
        }
        .area-ttd { text-align: center; width: 220px; font-size: 15px; }
        .ttd-tanggal { margin-bottom: 75px; }
        .ttd-garis { border-top: 1px solid #333; padding-top: 5px; font-weight: bold; }

        /* --- Slot Gambar Logo Kop Paling Bawah --- */
        .logo-footer-bawah {
            margin-top: auto; /* Mendorong otomatis ke posisi terbawah konten */
            text-align: center;
            width: 100%;
            padding-bottom: 5mm;
        }
        .logo-footer-bawah img {
            max-width: 100%;
            height: auto;
            display: inline-block;
        }

        /* --- Aturan Cetak Presisi --- */
        @media print {
            @page {
                size: A4;
                margin: 0; /* Menghilangkan margin browser agar kop bisa full ke tepi */
            }
            .form-panel { display: none !important; }
            body { background: #fff; padding: 0; margin: 0; justify-content: flex-start; }
            .a4-document { 
                box-shadow: none; 
                width: 210mm;
                height: 297mm;
                page-break-inside: avoid;
            }
        }
    </style>
</head>
<body>

    <div class="form-panel">
        <h3>Input Data Kwitansi</h3>
        <div class="form-group">
            <label>Nomor Kwitansi</label>
            <input type="text" id="inNo" value="KW-2026-001">
        </div>
        <div class="form-group">
            <label>Telah Diterima Dari</label>
            <input type="text" id="inNama" value="Samsuri Sidik">
        </div>
        <div class="form-group">
            <label>Jumlah Uang (Angka)</label>
            <input type="number" id="inUang" value="35000000">
        </div>
        <div class="form-group">
            <label>Untuk Pembayaran</label>
            <textarea id="inUntuk" rows="4">Material dan consumable pada proyek “Pemasangan Instalasi Pipa Air Compressor Sus-304” Berlokasi di SPIN, Jl. Raya Narogong, Bekasi</textarea>
        </div>
        <div class="form-group">
            <label>Kota & Tanggal</label>
            <input type="text" id="inTanggal" value="Bandung, 7 Juli 2026">
        </div>
        <div class="form-group">
            <label>Nama Kasir / Admin</label>
            <input type="text" id="inJabatan" value="Kasir / Admin">
        </div>
        <button class="btn-cetak" onclick="window.print()">Cetak / Simpan PDF</button>
    </div>

    <div class="a4-document">
        
        <div class="kop-gambar-atas">
            <img src="kop.png" alt="Kop Surat Atas">
        </div>
        
        <div class="kwitansi-content">
            <div class="kwitansi-header-detail">
                <div class="judul-kwitansi-box">
                    <h1>KWITANSI</h1>
                    <div id="outNo" style="font-size: 15px; margin-top: 5px;">No. <b>-</b></div>
                </div>
            </div>

            <div class="garis-pembatas"></div>

            <div class="kwitansi-row">
                <div class="row-label">Telah Diterima Dari</div>
                <div class="row-colon">:</div>
                <div class="row-value" id="outNama">-</div>
            </div>

            <div class="kwitansi-row" style="margin-bottom: 10px;">
                <div class="row-label">Uang Sejumlah</div>
                <div class="row-colon">:</div>
                <div class="row-value" style="border: none;"></div>
            </div>
            <div class="box-terbilang" id="outTerbilang">-</div>
            <br>

            <div class="kwitansi-row">
                <div class="row-label">Untuk Pembayaran</div>
                <div class="row-colon">:</div>
                <div class="row-value" id="outUntuk" style="line-height: 1.6;">-</div>
            </div>

            <div class="kwitansi-footer">
                <div class="box-nominal" id="outUang">Rp. 0,-</div>
                <div class="area-ttd">
                    <div class="ttd-tanggal" id="outTanggal">-</div>
                    <div class="ttd-garis" id="outJabatan">Kasir / Admin</div>
                </div>
            </div>

            <div class="logo-footer-bawah">
                <img src="logo kop.png" alt="Footer Logo Bawah">
            </div>
        </div>

    </div>

<script>
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
        const no = document.getElementById('inNo').value;
        const nama = document.getElementById('inNama').value;
        const uang = parseInt(document.getElementById('inUang').value) || 0;
        const untuk = document.getElementById('inUntuk').value;
        const tanggal = document.getElementById('inTanggal').value;
        const jabatan = document.getElementById('inJabatan').value;

        const formatRupiah = "Rp. " + uang.toLocaleString('id-ID') + ",-";
        const terbilang = uang > 0 ? kekata(uang) + " Rupiah" : "Nol Rupiah";

        document.getElementById('outNo').innerHTML = "No. <b>" + no + "</b>";
        document.getElementById('outNama').innerText = nama;
        document.getElementById('outUntuk').innerText = untuk;
        document.getElementById('outTanggal').innerText = tanggal;
        document.getElementById('outJabatan').innerText = jabatan;
        document.getElementById('outUang').innerText = formatRupiah;
        document.getElementById('outTerbilang').innerText = terbilang.trim();
    }

    const inputs = ['inNo', 'inNama', 'inUang', 'inUntuk', 'inTanggal', 'inJabatan'];
    inputs.forEach(id => {
        document.getElementById(id).addEventListener('input', updateKwitansi);
    });

    updateKwitansi();
</script>
</body>
</html>
