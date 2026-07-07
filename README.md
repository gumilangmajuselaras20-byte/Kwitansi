<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kwitansi PT. GUMILANG MAJU SELARAS dengan Kop Surat</title>
    <style>
        @media print {
            body { margin: 0; padding: 0; }
            .no-print { display: none !important; }
            .a4-page { box-shadow: none; border: none; }
        }
        
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 20px;
            padding: 0;
            display: flex;
            justify-content: center;
        }

        .no-print-container {
            position: fixed;
            top: 20px;
            left: 20px;
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            z-index: 1000;
        }

        .a4-page {
            width: 210mm;
            min-height: 297mm;
            padding: 20mm;
            margin: 0;
            background: white;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            position: relative;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
        }

        /* --- STYLING KOP SURAT (IMAGE 3) --- */
        .letterhead-header {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 40mm; /* Atur tinggi agar pas */
            overflow: hidden;
            z-index: 1;
        }
        
        .letterhead-header img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            object-position: top center;
        }

        .letterhead-logo-container {
            position: absolute;
            top: 15mm; /* Sesuaikan dengan gambar */
            right: 20mm; /* Sesuaikan dengan margin */
            z-index: 2;
            text-align: right;
        }

        .letterhead-logo-container img {
            height: 15mm; /* Sesuaikan ukuran logo */
            width: auto;
        }

        .letterhead-logo-container .company-name-text {
            display: block;
            font-size: 10pt;
            color: #333;
            margin-top: 2mm;
            font-weight: bold;
        }

        /* Konten utama di bawah kop surat */
        .page-content {
            margin-top: 45mm; /* Memberi ruang untuk kop */
            position: relative;
            z-index: 2;
            flex-grow: 1;
        }

        /* --- STYLING KWITANSI (IMAGE 2) --- */
        .kwitansi-header-row {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            margin-bottom: 20px;
            padding-bottom: 10px;
        }

        .company-info {
            flex-grow: 1;
            padding-left: 20px; /* Ruang untuk logo di kop */
        }

        .company-info h1 {
            font-size: 18pt;
            margin: 0 0 5px 0;
            font-weight: bold;
            color: #333;
        }

        .company-info p {
            font-size: 9pt;
            margin: 2px 0;
            color: #555;
            line-height: 1.3;
        }

        .kwitansi-title-box {
            text-align: right;
        }

        .kwitansi-title-box h2 {
            font-size: 20pt;
            margin: 0;
            font-weight: normal;
            color: #333;
        }

        .kwitansi-title-box p {
            font-size: 10pt;
            margin: 5px 0 0 0;
            color: #555;
        }

        .separator-line {
            border-top: 2px solid #333;
            margin-bottom: 10px;
        }

        .double-separator-line {
            border-top: 1px solid #333;
            border-bottom: 1px solid #333;
            height: 3px;
            margin-bottom: 20px;
        }

        .data-row {
            display: flex;
            margin-bottom: 15px;
            font-size: 10pt;
        }

        .label {
            width: 180px;
            font-weight: bold;
            color: #333;
        }

        .colon {
            width: 15px;
        }

        .value {
            flex-grow: 1;
            border-bottom: 1px dashed #999;
            padding-bottom: 3px;
            color: #555;
        }

        .terbilang-box {
            background-color: #f2f2f2;
            padding: 10px;
            margin-top: 5px;
            font-style: italic;
            font-weight: bold;
            border-radius: 4px;
            color: #333;
        }

        .footer-row {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            margin-top: 40px;
        }

        .amount-box {
            border: 2px solid #333;
            padding: 10px 20px;
            font-size: 16pt;
            font-weight: bold;
            color: #333;
        }

        .signature-box {
            text-align: center;
            font-size: 10pt;
            color: #333;
        }

        .date-text {
            margin-bottom: 60px;
        }

        .signature-line {
            border-top: 1px solid #333;
            width: 200px;
            margin: 0 auto;
        }

        .signatory-title {
            margin-top: 5px;
            font-weight: bold;
        }

        /* --- STYLING FOOTER KOP SURAT (IMAGE 3) --- */
        .letterhead-footer {
            position: absolute;
            bottom: 10mm;
            left: 20mm;
            right: 20mm;
            z-index: 1;
            text-align: center;
        }

        .letterhead-footer-line {
            border-top: 1px solid #666;
            margin-bottom: 5px;
        }

        .letterhead-footer-text {
            font-size: 8pt;
            color: #666;
            line-height: 1.4;
        }

        .letterhead-footer-text a {
            color: #0066cc;
            text-decoration: none;
        }
    </style>
</head>
<body>

<div class="no-print-container no-print">
    <button onclick="window.print()" style="padding: 10px 20px; background-color: #007bff; color: white; border: none; border-radius: 4px; cursor: pointer;">Cetak/Simpan PDF</button>
</div>

<div class="a4-page">
    <div class="letterhead-header">
        <img src="letterhead_header.png" alt="Header Kop Surat GMS">
    </div>

    <div class="letterhead-logo-container">
        <img src="logo.png" alt="Logo PT GMS">
        <span class="company-name-text">PT. GUMILANG<br>MAJU SELARAS</span>
    </div>

    <div class="page-content">
        <div class="kwitansi-header-row">
            <div class="company-info">
                <h1>PT. GUMILANG MAJU SELARAS</h1>
                <p>Jl. Kencana Wangi I No. 10, Komplek Pandan Wangi, Bandung 40287</p>
                <p>HP. 0822 1884 4662 | Email: gumilangmajuselaras@gmail.com</p>
            </div>
            <div class="kwitansi-title-box">
                <h2>KWITANSI</h2>
                <p>No. KW-2026-001</p>
            </div>
        </div>

        <div class="double-separator-line"></div>

        <div class="data-row">
            <div class="label">Telah Diterima Dari</div>
            <div class="colon">:</div>
            <div class="value">Samsuri Sidik</div>
        </div>

        <div class="data-row" style="flex-direction: column;">
            <div style="display: flex;">
                <div class="label">Uang Sejumlah</div>
                <div class="colon">:</div>
                <div class="value" style="border: none;"></div> </div>
            <div class="terbilang-box">
                Tiga Puluh Lima Juta Rupiah
            </div>
        </div>

        <div class="data-row">
            <div class="label">Untuk Pembayaran</div>
            <div class="colon">:</div>
            <div class="value">Material dan consumable pada proyek “Pemasangan Instalasi Pipa Air Compressor Sus-304” Berlokasi di SPIN, Jl. Raya Narogong, Bekasi</div>
        </div>

        <div class="footer-row">
            <div class="amount-box">
                Rp. 35.000.000,-
            </div>
            <div class="signature-box">
                <p class="date-text">Bandung, 7 Juli 2026</p>
                <div class="signature-line"></div>
                <p class="signatory-title">Kasir / Admin</p>
            </div>
        </div>
    </div>

    <div class="letterhead-footer">
        <div class="letterhead-footer-line"></div>
        <p class="letterhead-footer-text">
            PT. Gumilang Maju Selaras<br>
            Kencana Wangi I No. 10, Bandung | Email: <a href="mailto:gumilangmajuselaras@gmail.com">gumilangmajuselaras@gmail.com</a><br>
            Phone: 022-7313361
        </p>
    </div>
</div>

</body>
</html>
