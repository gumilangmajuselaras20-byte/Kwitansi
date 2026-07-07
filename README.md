<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kwitansi - PT. GUMILANG MAJU SELARAS</title>
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
            min-height: 297mm;
            background: #fff;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            position: relative;
            box-sizing: border-box;
            padding: 40mm 20mm 20mm 20mm; /* Jarak atas disisakan untuk Kop */
            display: flex;
            flex-direction: column;
        }

        /* --- Desain Kop Surat Kreatif (Tanpa Gambar File) --- */
        .kop-wave {
            position: absolute;
            top: 0; left: 0; right: 0;
            height: 130px;
            background: linear-gradient(135deg, #a2d2bb 0%, #8ec3a7 60%, #ffffff 100%);
            border-bottom-left-radius: 50% 30px;
            border-bottom-right-radius: 100% 15px;
            z-index: 1;
        }
        .kop-logo-container {
            position: absolute;
            top: 25px; right: 40px;
            z-index: 2;
            text-align: center;
        }
        .kop-logo-container img {
            width: 65px; height: auto;
        }
        .kop-logo-container .nama-pt-mini {
            display: block; font-size: 10px; font-weight: bold;
            color: #1e4631; margin-top: 2px; line-height: 1.1;
        }

        /* --- Isi Konten Kwitansi --- */
        .kwitansi-content {
            position: relative;
            z-index: 3;
            flex-grow: 1;
        }
        .kwitansi-header-detail {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            margin-bottom: 5px;
        }
        .info-pt h2 { margin: 0 0 5px 0; font-size: 20px; color: #1e4631; }
        .info-pt p { margin: 2px 0; font-size: 11px; color: #444; }
        
        .judul-kwitansi-box { text-align: right; }
        .judul-kwitansi-box h1 { margin: 0; font-size: 28px; letter-spacing: 2px; color: #333; }
        .judul-kwitansi-box p { margin: 5px 0 0 0; font-size: 14px; font-weight: bold; }

        .garis-pembatas {
            border-top: 1px solid #333; border-bottom: 3px double #333;
            height: 2px; margin: 15px 0 25px 0;
        }

        /* --- Baris Isi --- */
        .kwitansi-row { display: flex; margin-bottom: 18px; align-items: baseline; }
        .row-label { width: 180px; font-weight: bold; font-size: 14px; color: #222; }
        .row-colon { width: 20px; font-size: 14px; }
        .row-value { flex: 1; border-bottom: 1px dashed #888; padding-bottom: 3px; font-size: 14px; color: #333; }
        
        .box-terbilang { 
            background-color: #eaedd7; font-style: italic; padding: 10px; 
            font-weight: bold; border-radius: 4px; color: #1e4631; border-left: 4px solid #8ec3a7;
        }

        /* --- Bagian Tanda Tangan & Nominal --- */
        .kwitansi-footer {
            margin-top: 50px; display: flex; justify-content: space-between; align-items: flex-end;
        }
        .box-nominal {
            border: 2px solid #333; padding: 12px 25px; font-size: 22px;
            font-weight: bold; background-color: #f9f9f9; font-family: 'Courier New', monospace;
        }
        .area-ttd { text-align: center; width: 220px; font-size: 14px; }
        .ttd-tanggal { margin-bottom: 70px; }
        .ttd-garis { border-top: 1px solid #333; padding-top: 5px; font-weight: bold; }

        /* --- Footer Dokumen Resmi --- */
        .dokumen-footer {
            border-top: 1px solid #ccc; padding-top: 5px; margin-top: 40px;
            text-align: center; font-size: 10px; color: #666; line-height: 1.4;
        }

        /* --- Aturan Khusus Saat Tombol Cetak Ditekan --- */
        @media print {
            .form-panel { display: none !important; }
            body { background: #fff; padding: 0; margin: 0; justify-content: flex-start; }
            .a4-document { box-shadow: none; padding-top: 40mm; }
        }
    </style>
</head>
<body>

    <!-- PANEL EDIT MANUAL (Hanya tampil di layar) -->
    <div class="form-panel">
        <h3>Edit Data Kwitansi</h3>
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
        <button class="btn-cetak" onclick="window.print()">Cetak / Simpan PDF</button>
    </div>

    <!-- KERTAS PRINTER KWITANSI A4 -->
    <div class="a4-document">
        <!-- Latar Belakang Gelombang Atas Hijau -->
        <div class="kop-wave"></div>
        
        <!-- Logo Kanan Atas -->
        <div class="kop-logo-container">
            <img src="logo.png" alt="Logo">
            <span class="nama-pt-mini">PT. GUMILANG<br>MAJU SELARAS</span>
        </div>

        <div class="kwitansi-content">
            <!-- Header Info Perusahaan -->
            <div class="kwitansi-header-detail">
                <div class="info-pt">
                    <h2>PT. GUMILANG MAJU SELARAS</h2>
                    <p>Jl. Kencana Wangi I No. 10, Komplek Pandan Wangi, Bandung 40287</p>
                    <p>HP. 0822 1884 4662 | Email: gumilangmajuselaras@gmail.com</p>
                </div>
                <div class="judul-kwitansi-box">
                    <h1>KWITANSI</h1>
                    <div id="outNo" style="font-size: 14px; margin-top: 5px;">No. <b>-</b></div>
                </div>
            </div>

            <div class="garis-pembatas"></div>

            <!-- Konten Baris Data -->
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
                <div class="row-value" id="outUntuk" style="line-height: 1.5;">-</div>
            </div>

            <!-- Footer Tanda Tangan & Uang -->
            <div class="kwitansi-footer">
                <div class="box-nominal" id="outUang">Rp. 0,-</div>
                <div class="area-ttd">
                    <div class="ttd-tanggal" id="outTanggal">-</div>
                    <div class="ttd-garis">Kasir / Admin</div>
                </div>
            </div>

            <!-- Catatan Kaki/Footer Lembaga Resmi -->
            <div class="dokumen-footer">
                PT. Gumilang Maju Selaras<br>
                Kencana Wangi I No. 10, Bandung | Email: gumilangmajuselaras@gmail.com | Phone: 022-7313361
            </div>
        </div>
    </div>

<script>
    // System Otomatis Merubah Angka ke Huruf Indonesia
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

        const formatRupiah = "Rp. " + uang.toLocaleString('id-ID') + ",-";
        const terbilang = uang > 0 ? kekata(uang) + " Rupiah" : "Nol Rupiah";

        document.getElementById('outNo').innerHTML = "No. <b>" + no + "</b>";
        document.getElementById('outNama').innerText = nama;
        document.getElementById('outUntuk').innerText = untuk;
        document.getElementById('outTanggal').innerText = tanggal;
        document.getElementById('outUang').innerText = formatRupiah;
        document.getElementById('outTerbilang').innerText = terbilang.trim();
    }

    const inputs = ['inNo', 'inNama', 'inUang', 'inUntuk', 'inTanggal'];
    inputs.forEach(id => {
        document.getElementById(id).addEventListener('input', updateKwitansi);
    });

    updateKwitansi();
</script>
</body>
</html>
