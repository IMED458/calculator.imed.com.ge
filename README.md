<html lang="ka">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=5, user-scalable=yes" />
    <title>IMEDCalc - სამედიცინო კალკულატორები</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Fira+Sans:wght@400;600;700&display=swap" rel="stylesheet">
    <meta name="theme-color" content="#0f172a">
    <style>
        :root {
            --bg: #0f172a;
            --card: #1e293b;
            --surface: #334155;
            --muted: #94a3b8;
            --text: #e2e8f0;
            --brand: #22d3ee;
            --brand-2: #818cf8;
            --ok: #22c55e;
            --warn: #f59e0b;
            --err: #ef4444;
            --ring: rgba(34, 211, 238, 0.35);
            --shadow-3: 0 10px 30px rgba(0,0,0,.45), 0 2px 8px rgba(0,0,0,.35);
            --radius-2xl: 1.25rem;
            --transition: all 0.3s ease;
        }

        [data-theme="light"] {
            --bg: #f8fafc;
            --card: #ffffff;
            --surface: #f1f5f9;
            --muted: #64748b;
            --text: #0f172a;
            --brand: #0ea5e9;
            --brand-2: #6366f1;
            --ok: #10b981;
            --warn: #f59e0b;
            --err: #ef4444;
            --ring: rgba(14, 165, 233, 0.25);
            --shadow-3: 0 10px 30px rgba(0,0,0,.08), 0 2px 8px rgba(0,0,0,.04);
        }

        * { 
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }
        
        html, body { 
            height: 100%; 
            margin: 0;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }
        
        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background: var(--bg);
            color: var(--text);
            transition: var(--transition);
            line-height: 1.6;
            font-size: 16px;
            overscroll-behavior: none;
        }
        
        [data-theme="dark"] body {
            background: radial-gradient(80rem 40rem at 10% -10%, rgba(129,140,248,.08), transparent 60%),
                        radial-gradient(70rem 30rem at 110% 10%, rgba(34,211,238,.08), transparent 60%),
                        var(--bg);
        }

        .container { 
            max-width: 1100px; 
            margin: 0 auto; 
            padding: 1rem 1rem 3rem;
        }
        
        header {
            background: var(--card);
            padding: 1.25rem;
            border-radius: var(--radius-2xl);
            box-shadow: var(--shadow-3);
            display: flex;
            align-items: center;
            gap: 1rem;
            justify-content: space-between;
            flex-wrap: wrap;
            border: 1px solid var(--surface);
            transition: var(--transition);
            margin-bottom: 1rem;
        }
        
        .brand { 
            display: flex; 
            align-items: center; 
            gap: 1rem;
            flex: 1;
            min-width: 0;
        }
        
        .logo {
            width: 48px;
            height: 48px;
            min-width: 48px;
            border-radius: 14px;
            background: linear-gradient(135deg, var(--brand), var(--brand-2));
            box-shadow: 0 8px 25px rgba(34,211,238,.3);
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            transition: var(--transition);
        }
        
        [data-theme="light"] .logo {
            box-shadow: 0 8px 25px rgba(14, 165, 233, .25);
        }
        
        .logo svg {
            width: 85%;
            height: 85%;
            color: white;
        }
        
        .brand-text {
            flex: 1;
            min-width: 0;
        }
        
        .brand h1 { 
            margin: 0; 
            font-weight: 800; 
            font-size: 1.5rem; 
            letter-spacing: -0.5px;
            background: linear-gradient(135deg, var(--brand), var(--brand-2));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .brand p { 
            margin: 0.25rem 0 0; 
            color: var(--muted); 
            font-size: 0.9rem;
        }
        
        .disclaimer { 
            color: var(--muted); 
            font-size: 0.9rem; 
            margin: 0 0 1rem;
            padding: 0.75rem 1rem;
            background: var(--surface);
            border-radius: 0.75rem;
            border-left: 4px solid var(--brand);
        }
        
        .theme-toggle {
            background: var(--surface);
            color: var(--text);
            border: 1px solid var(--muted);
            border-radius: 50%;
            padding: 0.65rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: var(--transition);
            touch-action: manipulation;
            width: 44px;
            height: 44px;
            min-width: 44px;
        }
        
        .theme-toggle:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0,0,0,.15);
            border-color: var(--brand);
        }
        
        .theme-toggle svg {
            width: 20px;
            height: 20px;
        }
        
        .theme-text {
            display: none;
        }

        .nav-menu {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 0.75rem;
            margin-bottom: 1.5rem;
        }
        
        .nav-btn {
            background: linear-gradient(135deg, var(--brand), var(--brand-2));
            color: white;
            padding: 1rem 1.25rem;
            border-radius: 1rem;
            font-weight: 700;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: 0 8px 20px rgba(34,211,238,.25);
            border: none;
            font-size: 0.95rem;
            touch-action: manipulation;
            text-align: center;
        }
        
        .nav-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 28px rgba(34,211,238,.35);
        }
        
        .nav-btn:active {
            transform: translateY(-1px);
        }

        .grid { 
            display: none; 
            gap: 1.25rem;
            grid-template-columns: 1fr;
        }
        
        .grid.active { 
            display: grid; 
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn { 
            from { 
                opacity: 0; 
                transform: translateY(20px); 
            } 
            to { 
                opacity: 1; 
                transform: translateY(0); 
            } 
        }

        .card {
            background: var(--card);
            border: 1px solid var(--surface);
            border-radius: var(--radius-2xl);
            padding: 1.5rem;
            box-shadow: var(--shadow-3);
            transition: var(--transition);
        }
        
        .card:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.5), 0 5px 15px rgba(0,0,0,0.4);
        }
        
        [data-theme="light"] .card:hover {
            box-shadow: 0 15px 40px rgba(0,0,0,.12), 0 5px 15px rgba(0,0,0,.08);
        }

        .card h2 { 
            margin: 0 0 1rem; 
            font-size: 1.3rem; 
            font-weight: 800;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            flex-wrap: wrap;
        }
        
        .formula {
            font-family: 'Fira Sans', 'Courier New', monospace;
            font-size: 0.95rem;
            color: var(--brand);
            padding: 0.75rem 1rem;
            border: 1px dashed var(--brand);
            background: rgba(34, 211, 238, 0.05);
            border-radius: 0.75rem;
            margin-bottom: 1rem;
            word-wrap: break-word;
        }
        
        [data-theme="light"] .formula {
            background: rgba(14, 165, 233, 0.08);
        }
        
        .muted { 
            color: var(--muted); 
            font-size: 0.9rem;
            margin-bottom: 1rem;
        }
        
        .row { 
            display: grid; 
            gap: 1rem;
            grid-template-columns: 1fr;
            margin-bottom: 1rem;
        }
        
        label { 
            display: block; 
            font-size: 0.9rem; 
            margin-bottom: 0.4rem; 
            color: var(--text);
            font-weight: 600;
        }
        
        input, select {
            width: 100%;
            padding: 0.875rem 1rem;
            background: var(--surface);
            color: var(--text);
            border: 2px solid transparent;
            border-radius: 0.875rem;
            outline: none;
            transition: var(--transition);
            font-size: 1rem;
            min-height: 48px;
            font-family: inherit;
        }
        
        input:focus, select:focus { 
            border-color: var(--brand); 
            box-shadow: 0 0 0 4px var(--ring);
            background: var(--card);
        }
        
        .btns { 
            display: flex; 
            gap: 0.75rem;
            margin-top: 1.25rem;
            flex-wrap: wrap;
        }
        
        button {
            padding: 0.875rem 1.5rem;
            border: none;
            border-radius: 0.875rem;
            font-weight: 700;
            cursor: pointer;
            transition: var(--transition);
            background: linear-gradient(135deg, var(--brand), var(--brand-2));
            color: white;
            box-shadow: 0 8px 20px rgba(34,211,238,.25);
            font-size: 1rem;
            min-height: 48px;
            touch-action: manipulation;
            flex: 1;
            min-width: 120px;
        }
        
        button:hover { 
            transform: translateY(-2px); 
            box-shadow: 0 12px 28px rgba(34,211,238,.35);
        }
        
        button:active {
            transform: translateY(-1px);
        }
        
        .ghost {
            background: var(--surface);
            color: var(--text);
            border: 2px solid var(--muted);
            box-shadow: none;
        }
        
        .ghost:hover {
            background: var(--card);
            border-color: var(--brand);
        }
        
        .result {
            margin-top: 1.25rem;
            padding: 1rem 1.25rem;
            border-radius: 1rem;
            background: var(--surface);
            border: 2px solid var(--brand-2);
            font-weight: 700;
            letter-spacing: 0.3px;
            transition: var(--transition);
            font-size: 1.05rem;
            text-align: center;
        }
        
        .note { 
            margin-top: 1rem;
            padding: 1rem;
            border-left: 4px solid var(--warn);
            background: rgba(245, 158, 11, .12);
            border-radius: 0.75rem;
            font-size: 0.9rem;
        }
        
        [data-theme="light"] .note {
            background: rgba(245, 158, 11, .15);
        }
        
        .success { 
            border-left-color: var(--ok); 
            background: rgba(34, 197, 94, .12);
        }
        
        [data-theme="light"] .success {
            background: rgba(16, 185, 129, .15);
        }
        
        .danger { 
            border-left-color: var(--err); 
            background: rgba(239, 68, 68, .12);
        }
        
        [data-theme="light"] .danger {
            background: rgba(239, 68, 68, .15);
        }
        
        .foot { 
            margin-top: 2rem;
            color: var(--muted); 
            font-size: 0.85rem;
            text-align: center;
            padding: 1rem;
        }
        
        .tag, .chip {
            display: inline-block;
            font-size: 0.8rem;
            padding: 0.35rem 0.75rem;
            border-radius: 999px;
            background: var(--surface);
            border: 1px solid var(--muted);
            color: var(--text);
            font-weight: 600;
        }
        
        .chip { 
            background: rgba(34,211,238,.15); 
            border-color: rgba(34,211,238,.3); 
            color: var(--brand);
        }
        
        [data-theme="light"] .chip { 
            background: rgba(14, 165, 233, .15); 
            border-color: rgba(14, 165, 233, .3); 
            color: var(--brand);
        }

        .recommendations {
            margin-top: 1.5rem;
            padding: 1.25rem;
            background: var(--surface);
            border-radius: 1rem;
            border: 2px solid var(--brand-2);
        }
        
        .recommendations h3 {
            margin: 0 0 1rem;
            font-size: 1.1rem;
            color: var(--text);
        }
        
        .recommendations table {
            width: 100%;
            border-collapse: collapse;
            background: var(--card);
            border-radius: 0.75rem;
            overflow: hidden;
        }
        
        .recommendations th, .recommendations td {
            padding: 0.875rem;
            text-align: left;
            font-size: 0.9rem;
            border-bottom: 1px solid var(--surface);
        }
        
        .recommendations th {
            background: linear-gradient(135deg, var(--brand), var(--brand-2));
            color: white;
            font-weight: 700;
            text-transform: uppercase;
            font-size: 0.8rem;
            letter-spacing: 0.5px;
        }
        
        .recommendations tr:last-child td {
            border-bottom: none;
        }
        
        .recommendations tr:hover {
            background: var(--surface);
        }
        
        [data-theme="light"] .recommendations table {
            border: 1px solid #e2e8f0;
        }
        
        [data-theme="light"] .recommendations th {
            background: linear-gradient(135deg, #0ea5e9, #6366f1);
        }
        
        [data-theme="light"] .recommendations td {
            color: var(--text);
            border-bottom-color: #e2e8f0;
        }
        
        [data-theme="light"] .recommendations tr:hover {
            background: #f8fafc;
        }

        /* Mobile optimizations */
        @media (max-width: 768px) {
            body { 
                font-size: 15px;
            }
            
            .container { 
                padding: 0.75rem 0.75rem 2.5rem;
            }
            
            header { 
                padding: 1rem;
                gap: 0.75rem;
            }
            
            .brand {
                flex: 1 1 100%;
            }
            
            .logo { 
                width: 42px; 
                height: 42px;
                min-width: 42px;
            }
            
            .brand h1 { 
                font-size: 1.3rem;
            }
            
            .brand p { 
                font-size: 0.85rem;
            }
            
            .theme-toggle { 
                width: 42px;
                height: 42px;
                min-width: 42px;
                padding: 0.6rem;
            }
            
            .nav-menu { 
                grid-template-columns: 1fr;
                gap: 0.75rem;
            }
            
            .nav-btn { 
                padding: 0.875rem 1rem;
                font-size: 0.95rem;
            }
            
            .grid { 
                gap: 1rem;
            }
            
            .card { 
                padding: 1.25rem;
            }
            
            .card h2 { 
                font-size: 1.15rem;
            }
            
            .formula { 
                font-size: 0.85rem;
                padding: 0.75rem;
            }
            
            .btns {
                flex-direction: column;
            }
            
            .btns button { 
                width: 100%;
                min-width: unset;
            }
            
            .result { 
                font-size: 1rem;
            }
            
            /* Mobile table styles */
            .recommendations table,
            .recommendations thead,
            .recommendations tbody,
            .recommendations th,
            .recommendations td,
            .recommendations tr {
                display: block;
            }
            
            .recommendations thead {
                display: none;
            }
            
            .recommendations tr {
                margin-bottom: 1rem;
                border: 2px solid var(--surface);
                border-radius: 0.75rem;
                overflow: hidden;
            }
            
            [data-theme="light"] .recommendations tr {
                border-color: #e2e8f0;
            }
            
            .recommendations td {
                display: flex;
                justify-content: space-between;
                padding: 0.75rem 1rem;
                border-bottom: 1px solid var(--surface);
                position: relative;
            }
            
            [data-theme="light"] .recommendations td {
                border-bottom-color: #e2e8f0;
            }
            
            .recommendations td:last-child {
                border-bottom: none;
            }
            
            .recommendations td:before {
                content: attr(data-label);
                font-weight: 700;
                color: var(--brand);
                flex-shrink: 0;
                margin-right: 1rem;
            }
            
            .recommendations td:after {
                content: attr(data-value);
                text-align: right;
                flex: 1;
                color: var(--text);
            }
        }
        
        @media (max-width: 480px) {
            .card h2 {
                font-size: 1.05rem;
            }
            
            .disclaimer {
                font-size: 0.85rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="brand">
                <div class="logo">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M9 2v6h6V2M9 22v-6h6v6M2 9h6v6H2M16 9h6v6h-6M12 2v20M2 12h20"/>
                    </svg>
                </div>
                <div class="brand-text">
                    <h1>IMEDCalc</h1>
                    <p>სამედიცინო კალკულატორები</p>
                </div>
            </div>
            <button class="theme-toggle" onclick="toggleTheme()" title="თემის შეცვლა">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" id="theme-icon">
                    <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>
                </svg>
            </button>
        </header>
        
        <p class="disclaimer">📋 დამხმარე ხელსაწყო. სავალდებულოა შედეგების გადამოწმება კლინიკურ პროტოკოლებთან.</p>
        
        <div class="nav-menu">
            <button class="nav-btn" onclick="showCalculator('bicarb-card')">სოდა ბუფერი</button>
            <button class="nav-btn" onclick="showCalculator('potassium-card')">კალიუმის გადასხმა</button>
            <button class="nav-btn" onclick="showCalculator('kcoef-card')">K კოეფიციენტი</button>
            <button class="nav-btn" onclick="showCalculator('solu-card')">სოლუმედროლი</button>
            <button class="nav-btn" onclick="showCalculator('crcl-card')">კრეატინინის კლირენსი</button>
        </div>
        
        <div class="grid" id="grid">
            <section class="card" id="bicarb-card">
                <h2>სოდა ბუფერი — გადასხმის გამოთვლა <span class="tag">ფორმულა</span></h2>
                <div class="formula">წონა × BE(act) × 2 × 0.3</div>
                <p class="muted">შეიყვანეთ პაციენტის მონაცემები. შედეგი გამოისახება ქვემოთ.</p>
                <div class="row">
                    <div>
                        <label for="bicarb-weight">პაციენტის წონა (კგ)</label>
                        <input id="bicarb-weight" type="number" min="0" step="0.1" placeholder="მაგ. 70" />
                    </div>
                    <div>
                        <label for="bicarb-be">BE(act)</label>
                        <input id="bicarb-be" type="number" step="0.1" placeholder="მაგ. -8" />
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcBicarb()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('bicarb-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('bicarb-result')">კოპირება</button>
                </div>
                <div id="bicarb-result" class="result" aria-live="polite">შედეგი: —</div>
                <div class="note">💡 შენიშვნა: ერთეულების ინტერპრეტაცია შეადარეთ თქვენს პროტოკოლს/ხსნარის კონცენტრაციას.</div>
            </section>
            
            <section class="card" id="potassium-card">
                <h2>კალიუმის გადასხმა <span class="chip">ნელა გადასხმა</span></h2>
                <div class="formula">წონა × 1.74 ÷ კალიუმის მაჩვენებელი</div>
                <p class="muted">ფორმულა ითვლის საჭირო ოდენობას მითითებული დონის შესაბამისად.</p>
                <div class="row">
                    <div>
                        <label for="k-weight">პაციენტის წონა (კგ)</label>
                        <input id="k-weight" type="number" min="0" step="0.1" placeholder="მაგ. 70" />
                    </div>
                    <div>
                        <label for="k-level">კალიუმის მაჩვენებელი (mmol/L)</label>
                        <input id="k-level" type="number" min="0.1" step="0.1" placeholder="მაგ. 3.0" />
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcPotassium()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('potassium-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('potassium-result')">კოპირება</button>
                </div>
                <div id="potassium-result" class="result" aria-live="polite">შედეგი: —</div>
                <div class="note success">✅ აუცილებლად <strong>ნელა</strong> გადაისხას ინსტიტუციური წესების შესაბამისად.</div>
            </section>
            
            <section class="card" id="kcoef-card">
                <h2>K კოეფიციენტი</h2>
                <div class="formula">მედიკამენტის მილიგრამი × 1000 ÷ ხსნარის რაოდენობა</div>
                <p class="muted">შედეგი პრაქტიკულად უდრის კონცენტრაციას <em>(მკგ/მლ)</em>, თუ მოცულობა შეყვანილია მლ-ში.</p>
                <div class="row">
                    <div>
                        <label for="kcoef-mg">მედიკამენტის რაოდენობა (mg)</label>
                        <input id="kcoef-mg" type="number" min="0" step="0.1" placeholder="მაგ. 500" />
                    </div>
                    <div>
                        <label for="kcoef-vol">ხსნარის რაოდენობა (მლ)</label>
                        <input id="kcoef-vol" type="number" min="0.1" step="0.1" placeholder="მაგ. 100" />
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcKcoef()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('kcoef-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('kcoef-result')">კოპირება</button>
                </div>
                <div id="kcoef-result" class="result" aria-live="polite">შედეგი: —</div>
            </section>
            
            <section class="card" id="solu-card">
                <h2>სოლუმედროლი — დამრტყმელი დოზა</h2>
                <div class="formula">30 mg/kg — გადასხმა 15 წუთში</div>
                <p class="muted">შეიყვანეთ მხოლოდ პაციენტის წონა. სისტემა გამოთვლის დოზას.</p>
                <div class="row">
                    <div>
                        <label for="solu-weight">პაციენტის წონა (კგ)</label>
                        <input id="solu-weight" type="number" min="0" step="0.1" placeholder="მაგ. 70" />
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcSolu()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('solu-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('solu-result')">კოპირება</button>
                </div>
                <div id="solu-result" class="result" aria-live="polite">შედეგი: —</div>
                <div class="note success">⚡ რეკომენდაცია: პამპი დააყენეთ <strong>200 მლ/სთ</strong>-ზე. გადასხმა უნდა დასრულდეს ~15 წუთში.</div>
            </section>
            
            <section class="card" id="crcl-card">
                <h2>კრეატინინის კლირენსი (CrCl)</h2>
                <div class="formula">[140 − ასაკი] × წონა × (0.85 თუ ქალი) ÷ (72 × სერუმის კრეატინინი)</div>
                <p class="muted">შეიყვანეთ პაციენტის მონაცემები. შედეგი გამოისახება ქვემოთ, ანტიბიოტიკების დოზირების რეკომენდაციებით.</p>
                <div class="row">
                    <div>
                        <label for="crcl-age">ასაკი (წელი)</label>
                        <input id="crcl-age" type="number" min="0" step="1" placeholder="მაგ. 60" />
                    </div>
                    <div>
                        <label for="crcl-weight">წონა (კგ)</label>
                        <input id="crcl-weight" type="number" min="0" step="0.1" placeholder="მაგ. 70" />
                    </div>
                    <div>
                        <label for="crcl-gender">სქესი</label>
                        <select id="crcl-gender">
                            <option value="male">მამრობითი</option>
                            <option value="female">მდედრობითი</option>
                        </select>
                    </div>
                    <div>
                        <label for="crcl-creatinine">სერუმის კრეატინინი</label>
                        <input id="crcl-creatinine" type="number" min="0.1" step="0.01" placeholder="მაგ. 1.2 (mg/dL) ან 106 (µmol/L)" />
                    </div>
                    <div>
                        <label for="crcl-unit">ერთეული</label>
                        <select id="crcl-unit">
                            <option value="mg/dL">mg/dL</option>
                            <option value="µmol/L">µmol/L</option>
                        </select>
                    </div>
                </div>
                <div class="btns">
                    <button onclick="calcCrCl()">გამოთვლა</button>
                    <button class="ghost" onclick="resetCard('crcl-card')">გასუფთავება</button>
                    <button class="ghost" onclick="copyResult('crcl-result')">კოპირება</button>
                </div>
                <div id="crcl-result" class="result" aria-live="polite">შედეგი: —</div>
                <div id="crcl-recommendations" class="recommendations" style="display: none;">
                    <h3>💊 ანტიბიოტიკების დოზირების რეკომენდაციები</h3>
                    <table>
                        <thead>
                            <tr>
                                <th>ანტიბიოტიკი</th>
                                <th>CrCl (მლ/წთ)</th>
                                <th>დოზა</th>
                                <th>სიხშირე</th>
                            </tr>
                        </thead>
                        <tbody id="crcl-rec-table-body"></tbody>
                    </table>
                    <p class="muted" style="margin-top: 1rem;">💡 შენიშვნა: ეს არის ზოგადი რეკომენდაციები. გადაამოწმეთ კლინიკურ პროტოკოლებთან და პაციენტის მდგომარეობასთან.</p>
                </div>
            </section>
        </div>
        
        <p class="foot">© 2025 IMEDCalc • შექმნილია სამედიცინო პერსონალისთვის 💙</p>
    </div>

    <script>
        // Theme management
        function toggleTheme() {
            const body = document.body;
            const themeIcon = document.getElementById('theme-icon');
            const currentTheme = body.getAttribute('data-theme');
            let newTheme = currentTheme === 'dark' ? 'light' : 'dark';
            body.setAttribute('data-theme', newTheme);
            
            // Update icon
            if (newTheme === 'dark') {
                // Moon icon for dark theme
                themeIcon.innerHTML = '<path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>';
            } else {
                // Sun icon for light theme
                themeIcon.innerHTML = '<circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/>';
            }
            
            localStorage.setItem('theme', newTheme);
        }

        function applyTheme() {
            const savedTheme = localStorage.getItem('theme') || 'dark';
            const body = document.body;
            const themeIcon = document.getElementById('theme-icon');
            body.setAttribute('data-theme', savedTheme);
            
            // Update icon based on saved theme
            if (themeIcon) {
                if (savedTheme === 'dark') {
                    themeIcon.innerHTML = '<path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/>';
                } else {
                    themeIcon.innerHTML = '<circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/>';
                }
            }
        }
        document.addEventListener('DOMContentLoaded', applyTheme);

        // Show specific calculator
        function showCalculator(cardId) {
            const cards = document.querySelectorAll('.card');
            cards.forEach(card => {
                card.style.display = 'none';
            });
            const selectedCard = document.getElementById(cardId);
            if (selectedCard) {
                selectedCard.style.display = 'block';
            }
            const grid = document.getElementById('grid');
            grid.classList.add('active');
        }

        // Core calculator functions
        const fmt = (n) => {
            if (isNaN(n) || !isFinite(n)) return "—";
            const abs = Math.abs(n);
            if (abs >= 1000) return n.toLocaleString('ka-GE', { maximumFractionDigits: 0 });
            if (abs >= 100) return n.toLocaleString('ka-GE', { maximumFractionDigits: 1 });
            return n.toLocaleString('ka-GE', { maximumFractionDigits: 2 });
        };
        
        function setResult(id, value, unitHint = '') {
            const el = document.getElementById(id);
            el.textContent = `შედეგი: ${fmt(value)} ${unitHint}`.trim();
        }
        
        function requireValidNumber(...vals) {
            return vals.every(v => typeof v === 'number' && isFinite(v));
        }

        function calcBicarb() {
            const w = parseFloat(document.getElementById('bicarb-weight').value);
            const be = parseFloat(document.getElementById('bicarb-be').value);
            if (!requireValidNumber(w, be)) { setResult('bicarb-result', NaN); return; }
            const dose = w * Math.abs(be) * 2 * 0.3;
            setResult('bicarb-result', dose, 'მლ');
        }

        function calcPotassium() {
            const w = parseFloat(document.getElementById('k-weight').value);
            const lvl = parseFloat(document.getElementById('k-level').value);
            if (!requireValidNumber(w, lvl) || lvl <= 0) { setResult('potassium-result', NaN); return; }
            const amount = (w * 1.74) / lvl;
            setResult('potassium-result', amount, 'მლ');
        }

        function calcKcoef() {
            const mg = parseFloat(document.getElementById('kcoef-mg').value);
            const vol = parseFloat(document.getElementById('kcoef-vol').value);
            if (!requireValidNumber(mg, vol) || vol <= 0) { setResult('kcoef-result', NaN); return; }
            const k = (mg * 1000) / vol;
            setResult('kcoef-result', k, 'მკგ/მლ');
        }

        function calcSolu() {
            const w = parseFloat(document.getElementById('solu-weight').value);
            if (!requireValidNumber(w)) { setResult('solu-result', NaN); return; }
            const doseMg = 30 * w;
            setResult('solu-result', doseMg, 'mg');
        }

        function calcCrCl() {
            const age = parseFloat(document.getElementById('crcl-age').value);
            const weight = parseFloat(document.getElementById('crcl-weight').value);
            const gender = document.getElementById('crcl-gender').value;
            let creatinine = parseFloat(document.getElementById('crcl-creatinine').value);
            const unit = document.getElementById('crcl-unit').value;
            
            if (!requireValidNumber(age, weight, creatinine) || creatinine <= 0) { 
                setResult('crcl-result', NaN); 
                document.getElementById('crcl-recommendations').style.display = 'none';
                return; 
            }
            
            // Convert µmol/L to mg/dL if necessary (1 mg/dL = 88.4 µmol/L)
            if (unit === 'µmol/L') {
                creatinine = creatinine / 88.4;
            }
            
            const genderFactor = gender === 'female' ? 0.85 : 1;
            const crcl = ((140 - age) * weight * genderFactor) / (72 * creatinine);
            setResult('crcl-result', crcl, 'მლ/წთ');
            
            // Show recommendations
            const recDiv = document.getElementById('crcl-recommendations');
            const tableBody = document.getElementById('crcl-rec-table-body');
            tableBody.innerHTML = '';
            
            let category;
            if (crcl > 50) category = '>50';
            else if (crcl >= 30 && crcl <= 50) category = '30-50';
            else if (crcl >= 10 && crcl < 30) category = '10-30';
            else category = '<10';

            const recs = [
                { antibiotic: 'ამოქსიცილინი', ...getAmoxicillinRec(category) },
                { antibiotic: 'ციპროფლოქსაცინი', ...getCiprofloxacinRec(category) },
                { antibiotic: 'გენტამიცინი', ...getGentamicinRec(category) },
                { antibiotic: 'მეროპენემი', ...getMeropenemRec(category) },
                { antibiotic: 'ვანკომიცინი', ...getVancomycinRec(category) },
                { antibiotic: 'ცეფტრიაქსონი', ...getCeftriaxoneRec(category) },
                { antibiotic: 'მეტრონიდაზოლი', ...getMetronidazoleRec(category) },
                { antibiotic: 'ამპიცილინი', ...getAmpicillinRec(category) },
                { antibiotic: 'ლევოფლოქსაცინი', ...getLevofloxacinRec(category) }
            ];

            recs.forEach(rec => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td data-label="ანტიბიოტიკი" data-value="${rec.antibiotic}">${rec.antibiotic}</td>
                    <td data-label="CrCl (მლ/წთ)" data-value="${rec.range}">${rec.range}</td>
                    <td data-label="დოზა" data-value="${rec.dose}">${rec.dose}</td>
                    <td data-label="სიხშირე" data-value="${rec.frequency}">${rec.frequency}</td>
                `;
                tableBody.appendChild(row);
            });

            recDiv.style.display = 'block';
        }

        function getAmoxicillinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '875 მგ ან 500 მგ', frequency: 'ყოველ 12 სთ ან 8 სთ' };
                case '30-50': return { range: '30-50', dose: '875 მგ ან 500 მგ', frequency: 'ყოველ 12 სთ ან 8 სთ' };
                case '10-30': return { range: '10-30', dose: '500 მგ', frequency: 'ყოველ 12 სთ' };
                case '<10': return { range: '<10', dose: '500 მგ', frequency: 'ყოველ 24 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getCiprofloxacinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '250-750 მგ (PO) / 400 მგ (IV)', frequency: 'ყოველ 12 სთ' };
                case '30-50': return { range: '30-50', dose: '250-750 მგ (PO) / 400 მგ (IV)', frequency: 'ყოველ 12 სთ' };
                case '10-30': return { range: '10-30', dose: '250-750 მგ (PO) / 400 მგ (IV)', frequency: 'ყოველ 12 სთ' };
                case '<10': return { range: '<10', dose: '250-750 მგ (PO) / 400 მგ (IV)', frequency: 'ყოველ 24 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getGentamicinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '7 მგ/კგ ან 1.5-2.5 მგ/კგ', frequency: 'ყოველ 24 სთ / 8 სთ' };
                case '30-50': return { range: '30-50', dose: '1.5-2.5 მგ/კგ', frequency: 'ყოველ 12 სთ' };
                case '10-30': return { range: '10-30', dose: '1.5-2.5 მგ/კგ', frequency: 'ყოველ 24 სთ' };
                case '<10': return { range: '<10', dose: '1.5-2.5 მგ/კგ', frequency: 'ყოველ 48-72 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getMeropenemRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '500 მგ / 2000 მგ (მენინგიტი)', frequency: 'ყოველ 6-8 სთ' };
                case '30-50': return { range: '30-50', dose: '500 მგ / 2000 მგ', frequency: 'ყოველ 6-8 სთ' };
                case '10-30': return { range: '10-30', dose: '500 მგ / 2000 მგ', frequency: 'ყოველ 6-8 სთ' };
                case '<10': return { range: '<10', dose: '500 მგ / 1000 მგ', frequency: 'ყოველ 12 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getVancomycinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '15-20 მგ/კგ / 25 მგ/კგ (ლოუდ)', frequency: 'ყოველ 12 სთ' };
                case '30-50': return { range: '30-50', dose: '15-20 მგ/კგ', frequency: 'ყოველ 12-24 სთ' };
                case '10-30': return { range: '10-30', dose: '15-20 მგ/კგ', frequency: 'ყოველ 24-48 სთ' };
                case '<10': return { range: '<10', dose: 'გაზომეთ დონე', frequency: 'გადაამოწმეთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getCeftriaxoneRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '1000-2000 მგ', frequency: 'ყოველ 24 სთ / 12 სთ' };
                case '30-50': return { range: '30-50', dose: '1000-2000 მგ', frequency: 'ყოველ 24 სთ / 12 სთ' };
                case '10-30': return { range: '10-30', dose: '1000-2000 მგ', frequency: 'ყოველ 24 სთ / 12 სთ' };
                case '<10': return { range: '<10', dose: '1000-2000 მგ', frequency: 'ყოველ 24 სთ / 12 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getMetronidazoleRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '500 მგ', frequency: 'ყოველ 8 სთ' };
                case '30-50': return { range: '30-50', dose: '500 მგ', frequency: 'ყოველ 8 სთ' };
                case '10-30': return { range: '10-30', dose: '500 მგ', frequency: 'ყოველ 8 სთ' };
                case '<10': return { range: '<10', dose: '500 მგ', frequency: 'ყოველ 8 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getAmpicillinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '1000-2000 მგ', frequency: 'ყოველ 4-6 სთ' };
                case '30-50': return { range: '30-50', dose: '1000-2000 მგ', frequency: 'ყოველ 6 სთ' };
                case '10-30': return { range: '10-30', dose: '1000-2000 მგ', frequency: 'ყოველ 8 სთ' };
                case '<10': return { range: '<10', dose: '1000-2000 მგ', frequency: 'ყოველ 12 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function getLevofloxacinRec(category) {
            switch (category) {
                case '>50': return { range: '>50', dose: '500-750 მგ', frequency: 'ყოველ 24 სთ' };
                case '30-50': return { range: '30-50', dose: '250-500 მგ', frequency: 'ყოველ 24 სთ' };
                case '10-30': return { range: '10-30', dose: '250-500 მგ', frequency: 'ყოველ 48 სთ' };
                case '<10': return { range: '<10', dose: '250 მგ', frequency: 'ყოველ 48 სთ' };
                default: return { range: 'უცნობი', dose: 'გადაამოწმეთ', frequency: 'გადაამოწმეთ' };
            }
        }

        function resetCard(cardId) {
            const card = document.getElementById(cardId);
            const inputs = card.querySelectorAll('input, select');
            inputs.forEach(i => {
                if (i.tagName === 'SELECT') i.value = i.options[0].value;
                else i.value = '';
            });
            const res = card.querySelector('.result');
            if (res) res.textContent = 'შედეგი: —';
            const recDiv = card.querySelector('.recommendations');
            if (recDiv) recDiv.style.display = 'none';
        }

        async function copyResult(resultId) {
            const text = document.getElementById(resultId).textContent;
            try {
                await navigator.clipboard.writeText(text);
                toast('✅ შედეგი დაკოპირდა!');
            } catch (err) {
                toast('❌ კოპირება ვერ მოხერხდა.');
            }
        }

        function toast(msg) {
            const t = document.createElement('div');
            t.textContent = msg;
            t.style.cssText = `
                position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%);
                padding: 12px 20px; background: var(--card); border: 2px solid var(--brand);
                border-radius: 999px; box-shadow: var(--shadow-3); z-index: 1000;
                color: var(--text); font-size: 0.9rem; font-weight: 600;
                transition: opacity .3s ease-in-out;
            `;
            document.body.appendChild(t);
            setTimeout(() => { t.style.opacity = '0'; }, 2500);
            setTimeout(() => t.remove(), 2800);
        }
    </script>
</body>
</html>
