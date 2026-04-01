<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MikroTik Learning Hub | UKK 2025</title>
    <style>
        /* --- Reset & Base Styles --- */
        :root {
            --primary: #3498db; /* Blue */
            --secondary: #2c3e50; /* Dark Navy */
            --accent: #e67e22; /* Orange */
            --bg: #ecf0f1; /* Light Gray */
            --text: #333;
            --code-bg: #2d3436;
            --code-text: #fab1a0;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background-color: var(--bg); color: var(--text); overflow-x: hidden; }
        a { text-decoration: none; color: inherit; }
        ul { list-style: none; }

        /* --- 1. Animasi Layar Loading (Komputer) --- */
        #loader-wrapper {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background-color: var(--secondary);
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            z-index: 1000; transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        #loader-wrapper.hidden { opacity: 0; visibility: hidden; }

        .computer-icon {
            font-size: 70px; margin-bottom: 20px;
            animation: computerPulse 2s infinite ease-in-out;
        }

        .loading-bar-container {
            width: 250px; height: 10px; background: rgba(255,255,255,0.1);
            border-radius: 5px; overflow: hidden; position: relative;
        }

        .loading-bar {
            width: 0; height: 100%; background: var(--primary);
            border-radius: 5px; animation: loadingFill 3s forwards linear;
        }

        .loading-text {
            color: white; font-family: monospace; font-size: 1.2rem; margin-top: 15px;
            letter-spacing: 1px; animation: textPulse 1.5s infinite;
        }

        /* Keyframes Loading */
        @keyframes computerPulse {
            0%, 100% { transform: scale(1); opacity: 0.8; }
            50% { transform: scale(1.1); opacity: 1; }
        }
        @keyframes loadingFill { 0% { width: 0; } 100% { width: 100%; } }
        @keyframes textPulse { 0%, 100% { opacity: 0.5; } 50% { opacity: 1; } }


        /* --- 2. Header & Main Content --- */
        header {
            background: linear-gradient(135deg, var(--secondary) 0%, #1a252f 100%);
            color: white; padding: 60px 20px; text-align: center;
            clip-path: polygon(0 0, 100% 0, 100% 85%, 0% 100%);
            border-bottom: 5px solid var(--primary);
        }

        header h1 { font-size: 2.5rem; margin-bottom: 10px; }
        header p { font-size: 1.1rem; opacity: 0.8; font-weight: 300; }

        main { max-width: 1000px; margin: -40px auto 40px; padding: 0 20px; position: relative; z-index: 10; }

        /* --- 3. Animasi Ikon Alat-Alat --- */
        .tools-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 20px; margin-bottom: 40px;
        }

        .tool-card {
            background: white; padding: 20px; border-radius: 12px;
            text-align: center; box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            opacity: 0; transform: translateY(20px); /* Mulai dari bawah */
        }

        /* Kelas animasi yang dipicu JS */
        .tool-card.animate { opacity: 1; transform: translateY(0); }

        .tool-card:hover { transform: translateY(-5px) scale(1.03); box-shadow: 0 10px 15px rgba(0,0,0,0.1); }

        .tool-icon { font-size: 3.5rem; margin-bottom: 15px; display: block; }
        .tool-card h3 { font-size: 1rem; color: var(--secondary); }

        /* Delay animasi untuk tiap kartu */
        .tool-card:nth-child(1) { transition-delay: 0.1s; }
        .tool-card:nth-child(2) { transition-delay: 0.2s; }
        .tool-card:nth-child(3) { transition-delay: 0.3s; }
        .tool-card:nth-child(4) { transition-delay: 0.4s; }


        /* --- 4. Materi Sections (Fade-in Scroll) --- */
        .materi-section {
            background: white; padding: 30px; border-radius: 15px;
            margin-bottom: 30px; box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            opacity: 0; transform: translateX(-20px); transition: opacity 0.6s ease, transform 0.6s ease;
        }

        /* Kelas animasi yang dipicu JS saat scroll */
        .materi-section.visible { opacity: 1; transform: translateX(0); }

        .materi-section h2 {
            color: var(--primary); border-bottom: 2px solid #eee;
            padding-bottom: 15px; margin-bottom: 20px; display: flex; align-items: center;
        }
        
        .materi-section h2 span.icon { margin-right: 15px; font-size: 1.5rem; }

        .materi-list li {
            padding: 15px; border-bottom: 1px solid #f0f0f0;
            display: flex; align-items: flex-start;
        }
        
        .materi-list li:last-child { border-bottom: none; }
        .materi-list li::before { content: "⚡"; margin-right: 15px; color: var(--accent); font-size: 1.1rem; }

        .materi-list li b { color: var(--secondary); }

        code {
            background-color: var(--code-bg); color: var(--code-text);
            padding: 4px 8px; border-radius: 6px; font-family: monospace;
            font-size: 0.9rem; font-weight: bold; margin-left: 5px;
            display: inline-block; /* Agar padding terlihat bagus */
        }

        /* --- Footer --- */
        footer {
            text-align: center; padding: 30px; background-color: var(--secondary);
            color: rgba(255,255,255,0.6); font-size: 0.9rem; margin-top: auto;
        }

        /* --- Media Queries (Responsive) --- */
        @media (max-width: 600px) {
            header h1 { font-size: 1.8rem; }
            .materi-section { padding: 20px; }
            .tool-icon { font-size: 2.5rem; }
        }
    </style>
</head>
<body>

    <div id="loader-wrapper">
        <div class="computer-icon">💻</div>
        <div class="loading-bar-container">
            <div class="loading-bar"></div>
        </div>
        <div class="loading-text">BOOTING MIKROTIK...</div>
    </div>

    <header>
        <h1>MikroTik Learning Hub</h1>
        <p>Panduan Konfigurasi Praktikum Jaringan | UKK 2025</p>
    </header>

    <main>
        
        <section class="tools-grid" id="tools-section">
            <div class="tool-card">
                <span class="tool-icon">🛠️</span>
                <h3>Tang Crimping</h3>
            </div>
            <div class="tool-card">
                <span class="tool-icon">🔌</span>
                <h3>Kabel & RJ45</h3>
            </div>
            <div class="tool-card">
                <span class="tool-icon">📡</span>
                <h3>RouterBoard</h3>
            </div>
            <div class="tool-card">
                <span class="tool-icon">🎛️</span>
                <h3>Switch</h3>
            </div>
        </section>

        <section class="materi-section">
            <h2><span class="icon">🆔</span>Identitas & Interface</h2>
            <ul class="materi-list">
                <li><b>Identity:</b> Berikan nama router unik. Contoh Kode: <code>/system identity set name=akmal_a</code> (Router A)</li>
                <li><b>Ether1:</b> Jalur masuk Internet (Gateway).</li>
                <li><b>Ether2:</b> Jalur Lokal (LAN).</li>
                <li><b>Wlan1:</b> Jalur Nirkabel (Wireless).</li>
            </ul>
        </section>

        <section class="materi-section">
            <h2><span class="icon">📶</span>Wireless & IP Address</h2>
            <ul class="materi-list">
                <li><b>Mode:</b> <code>ap-bridge</code> | <b>Band:</b> <code>2.4ghz-b/g/n</code></li>
                <li><b>SSID:</b> <code>nama@ukk2025</code></li>
                <li><b>IP Internet A:</b> <code>192.200.[No.Absen].10.2/24</code></li>
                <li><b>IP Wireless B:</b> <code>192.100.[No.Absen].20.2/24</code></li>
            </ul>
        </section>

        <section class="materi-section">
            <h2><span class="icon">🗺️</span>Routing OSPF</h2>
            <p style="margin-bottom: 15px; padding-left: 15px;">Hubungkan Router A dan B dengan mendaftarkan network OSPF:</p>
            <ul class="materi-list">
                <li>Network Inti: <code>192.168.1.0/24</code></li>
                <li>Network Lokal: Daftarkan juga network lokal masing-masing router.</li>
            </ul>
        </section>

        <section class="materi-section">
            <h2><span class="icon">🧱</span>Firewall & Keamanan</h2>
            <ul class="materi-list">
                <li><b>NAT (Masquerade):</b> <code>chain=srcnat</code>, <code>action=masquerade</code></li>
                <li><b>Web Proxy:</b> Redirect port 80 (HTTP) ke port proxy <code>3128</code>.</li>
                <li><b>Access Rules:</b> Gunakan action <code>drop</code> untuk memblokir akses ke situs <code>linux.org</code>.</li>
            </ul>
        </section>

    </main>

    <footer>
        <p>&copy; 2024 Catatan UKK MikroTik. Dibuat untuk persiapan ujian.</p>
    </footer>

    <script>
        // --- JAVASCRIPT UNTUK PEMICU ANIMASI ---

        window.addEventListener('load', () => {
            const loader = document.getElementById('loader-wrapper');
            const toolsSection = document.getElementById('tools-section');
            const toolCards = document.querySelectorAll('.tool-card');
            const materiSections = document.querySelectorAll('.materi-section');

            // 1. Sembunyikan Loading setelah 3 detik (sesuai animasi loading bar)
            setTimeout(() => {
                loader.classList.add('hidden');
                
                // Mulai animasi kartu alat setelah loading hilang
                setTimeout(() => {
                    toolCards.forEach(card => card.classList.add('animate'));
                }, 300);

            }, 3000); 


            // 2. Animasi Fade-in Section saat Scroll (Intersection Observer)
            const sectionObserver = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                        observer.unobserve(entry.target); // Hanya animasikan sekali
                    }
                });
            }, {
                threshold: 0.15 // Picu animasi saat 15% section terlihat
            });

            materiSections.forEach(section => {
                sectionObserver.observe(section);
            });
        });
    </style>
</body>
</html>
