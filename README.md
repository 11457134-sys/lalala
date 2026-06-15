<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>八德生態埤塘觀光與生態資料庫</title>
    <style>
        /* 基礎樣式與淡紫色主題 */
        body {
            font-family: 'Helvetica Neue', Helvetica, Arial, "Microsoft JhengHei", sans-serif;
            background-color: #f4f0fa; /* 極淺淡紫底色 */
            color: #3a2d4a; /* 深紫灰文字 */
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }

        /* 頁首標題 */
        header {
            background-color: #4a3765; /* 濃郁紫 */
            padding: 25px 20px;
            text-align: center;
            border-bottom: 3px solid #6c528d;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        header h1 {
            color: #f3e8ff; /* 亮淡紫 */
            margin: 0;
            font-size: 26px;
            letter-spacing: 1.5px;
            font-weight: bold;
        }
        .author-tag {
            color: #d8b4fe;
            font-size: 14px;
            margin-top: 8px;
        }

        /* 響應式導覽列 */
        nav {
            background-color: #5c457c; /* 中度紫 */
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.08);
        }
        
        /* 第一層選單外層 */
        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            padding: 0;
            list-style: none;
        }

        /* 主選單項目 */
        .nav-item {
            position: relative;
        }

        .nav-item > a {
            color: #f3e8ff;
            text-decoration: none;
            padding: 15px 20px;
            display: block;
            font-size: 15px;
            font-weight: 500;
            transition: all 0.3s ease;
        }

        .nav-item:hover > a {
            color: #ffffff;
            background-color: #745b99;
        }

        /* 第二層下拉選單 (電腦版) */
        .dropdown-menu {
            display: none;
            position: absolute;
            top: 100%;
            left: 0;
            background-color: #ffffff;
            box-shadow: 0 8px 16px rgba(0,0,0,0.1);
            min-width: 200px;
            list-style: none;
            padding: 5px 0;
            margin: 0;
            border-radius: 0 0 6px 6px;
            border: 1px solid #e1d7ec;
        }

        .dropdown-menu li a {
            color: #3a2d4a;
            padding: 10px 20px;
            text-decoration: none;
            display: block;
            font-size: 14px;
            transition: background 0.2s;
        }

        .dropdown-menu li a:hover {
            background-color: #f3e8ff;
            color: #6d28d9;
        }

        /* 滑鼠懸停顯示下拉選單 */
        .nav-item:hover .dropdown-menu {
            display: block;
        }

        /* 主要內容區佈局 */
        main {
            max-width: 1100px;
            margin: 30px auto;
            padding: 0 20px;
        }

        /* 文獻資訊通用卡片 */
        .info-card {
            background-color: #ffffff;
            border-radius: 12px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 6px 15px rgba(74, 55, 101, 0.04);
            border: 1px solid #e1d7ec;
        }

        h2 {
            color: #4a3765;
            font-size: 20px;
            margin-top: 0;
            margin-bottom: 18px;
            border-left: 5px solid #8b5cf6;
            padding-left: 12px;
        }

        h3 {
            color: #6d28d9;
            font-size: 16px;
            margin-top: 20px;
            margin-bottom: 10px;
        }

        hr {
            border: 0;
            height: 1px;
            background: #e1d7ec;
            margin-bottom: 20px;
        }

        p {
            margin: 0 0 15px 0;
            font-size: 15px;
            text-align: justify;
        }

        /* 地圖與互動區塊 */
        .map-wrapper {
            width: 100%;
            max-width: 600px;
            margin: 0 auto 20px auto;
            border-radius: 8px;
            overflow: hidden;
            border: 1px solid #dcd1e8;
        }
        .map-wrapper iframe {
            display: block;
            width: 100%;
        }
        .info-box {
            display: flex;
            align-items: center;
            background-color: #faf5ff;
            padding: 15px 20px;
            border-radius: 8px;
            font-size: 14.5px;
            border: 1px dashed #c084fc;
            max-width: 560px;
            margin: 0 auto;
        }

        /* 鳥類入口網格與卡片頁樣式 */
        .grid-title {
            text-align: center;
            color: #4a3765;
            margin: 40px 0 20px 0;
            font-size: 22px;
        }

        .card-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr); /* 電腦版一行三張 */
            gap: 25px;
            margin-bottom: 40px;
        }

        .bird-card {
            background-color: #ffffff;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 6px 18px rgba(74, 55, 101, 0.06);
            border: 1px solid #e1d7ec;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            display: flex;
            flex-direction: column;
        }

        .bird-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 25px rgba(74, 55, 101, 0.12);
        }

        /* 縮圖容器 */
        .thumbnail-wrapper {
            width: 100%;
            height: 200px;
            overflow: hidden;
            background-color: #eaeaea;
        }

        .thumbnail-wrapper img {
            width: 100%;
            height: 100%;
            object-fit: cover; /* 自動縮放並填滿，保持完美比例 */
            transition: transform 0.5s ease;
        }

        .bird-card:hover .thumbnail-wrapper img {
            transform: scale(1.05); /* 懸停時圖片微放大 */
        }

        /* 卡片文字與按鈕內容區 */
        .card-content {
            padding: 20px;
            display: flex;
            flex-direction: column;
            flex-grow: 1; /* 讓內容自動填滿，使按鈕對齊底部 */
            justify-content: space-between;
        }

        .card-content h4 {
            margin: 0 0 10px 0;
            font-size: 18px;
            color: #4a3765;
        }

        /* 行動呼籲按鈕 (CTA) */
        .cta-btn {
            display: block;
            background-color: #8b5cf6;
            color: #ffffff;
            text-align: center;
            padding: 10px 15px;
            border-radius: 6px;
            text-decoration: none;
            font-size: 14px;
            font-weight: 500;
            transition: background 0.2s ease;
            border: none;
            cursor: pointer;
            width: 100%;
            box-sizing: border-box;
        }

        .cta-btn:hover {
            background-color: #7c3aed;
        }

        /* 頁尾 */
        footer {
            text-align: center;
            padding: 25px;
            color: #867599;
            font-size: 13px;
            margin-top: 50px;
            background-color: #e9e3f0;
            border-top: 1px solid #dcd1e8;
        }

        /* RWD 響應式媒體查詢 */
        @media (max-width: 900px) {
            .card-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (max-width: 600px) {
            .nav-container {
                flex-direction: column;
                align-items: stretch;
            }

            .nav-item {
                text-align: center;
                border-bottom: 1px solid #6c528d;
            }

            .dropdown-menu {
                position: relative;
                box-shadow: none;
                background-color: #4a3765;
                border-radius: 0;
                border: none;
            }

            .dropdown-menu li a {
                color: #d8b4fe;
                padding: 10px;
            }

            .dropdown-menu li a:hover {
                background-color: #745b99;
                color: #ffffff;
            }

            .card-grid {
                grid-template-columns: 1fr;
                gap: 20px;
            }

            .thumbnail-wrapper {
                height: 180px;
            }
        }
    </style>
</head>
<body>

    <header>
        <h1>八德生態埤塘觀光與生態資料庫</h1>
        <div class="author-tag">研究團隊：陳秉詩 ‧ 井上絢香</div>
    </header>

    <nav>
        <ul class="nav-container">
            <li class="nav-item"><a href="#about">關於</a></li>
            <li class="nav-item"><a href="#map">地圖</a></li>
            <li class="nav-item">
                <a href="#history">歷史與文化 ▾</a>
                <ul class="dropdown-menu">
                    <li><a href="#history">起源故事 (陳秉詩)</a></li>
                    <li><a href="#history">周邊生活 (陳秉詩)</a></li>
                </ul>
            </li>
            <li class="nav-item">
                <a href="#ecology">生態調查 ▾</a>
                <ul class="dropdown-menu">
                    <li><a href="#ecology">植物 (陳秉詩)</a></li>
                    <li><a href="#bird-section">動物與鳥類入口</a></li>
                    <li><a href="#bird-section">動物 (陳秉詩)</a></li>
                    <li><a href="#bird-section">鳥類 (陳秉詩)</a></li>
                </ul>
            </li>
            <li class="nav-item">
                <a href="#water">昆蟲與水質 ▾</a>
                <ul class="dropdown-menu">
                    <li><a href="#water">昆蟲 (井上絢香)</a></li>
                    <li><a href="#water text-align: justify;">水質 (井上絢香)</a></li>
                </ul>
            </li>
            <li class="nav-item">
                <a href="#landscape">地景與水利 ▾</a>
                <ul class="dropdown-menu">
                    <li><a href="#landscape">給水系統 (井上絢香)</a></li>
                    <li><a href="#landscape">關鍵構造 (井上絢香)</a></li>
                    <li><a href="#landscape">分水邏輯 (井上絢香)</a></li>
                </ul>
            </li>
            <li class="nav-item">
                <a href="#status">變遷與現狀 ▾</a>
                <ul class="dropdown-menu">
                    <li><a href="#status">土地變化 (井上絢香)</a></li>
                    <li><a href="#status">轉型功能 (井上絢香)</a></li>
                    <li><a href="#status">面臨挑戰 (井上絢香)</a></li>
                </ul>
            </li>
            <li class="nav-item">
                <a href="#mission">互動任務 ▾</a>
                <ul class="dropdown-menu">
                    <li><a href="#mission">選擇題 (井上絢香)</a></li>
                    <li><a href="#mission">填充題 (陳秉詩)</a></li>
                </ul>
            </li>
        </ul>
    </nav>

    <main>
        
        <div class="info-card" id="about">
            <h2>關於八德生態埤塘</h2>
            <hr>
            <p>桃園素有「千塘之鄉」的美譽，而<b>八德生態埤塘自然公園</b>占地約5公頃則是將傳統農業灌溉埤塘成功轉型為都市生態綠洲的指標典範。本站由研究小組建置，旨在全面記錄並保存該埤塘的數位文獻資料。</p>
        </div>

        <div class="info-card" id="map">
            <h2>地理位置與空間軸線</h2>
            <hr>
            <div class="map-wrapper">
                <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3617.718592865783!2d121.30867647482911!3d24.941654742004808!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x34681920e042adb5%3A0xf288e393fa0262bd!2z5qGD5ZyS5YWr5b635Z-k5aGY6Ieq54S255Sf5oWL5YWs5ZyS!5e0!3m2!1szh-TW!2stw!4v1781453790484!5m2!1szh-TW!2stw" width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
            </div>
            <div class="info-box">
                <span class="info-icon">📍</span>
                <div>
                    <strong>核心地標：</strong>桃園市八德區興豐路旁（八德生態埤塘自然公園），鄰近國防大學與八德重劃區。
                </div>
            </div>
        </div>

        <div class="info-card" id="history">
            <h2>歷史與文化變遷</h2>
            <hr>
            <p>這座埤塘原為編號「霄裡分渠5-3號埤塘」早期承載著當地先民農業灌溉與蓄水防洪的重要功能。隨著現代都市發展與水利系統轉型行政院農業委員會與桃園市政府合作將其改建為兼具防災滯洪、生態棲地與環境教育功能的自然公園，於2008年正式啟用。</p>
        </div>

        <div class="info-card" id="ecology">
            <h2>生態調查成果</h2>
            <hr>
            <h3>鳥類與禽類棲地</h3>
            <p>園區內特別規劃了「野鳥之島」，禁止遊客進入，提供鳥類不受干擾的繁衍空間。經長期觀測，此處常年有許多豐富物種出沒。</p>
            <h3>植物相調查</h3>
            <p>池畔周邊種植了大量的高大喬木與水生植物。最著名的莫過於四季皆美、冬季呈現微醺紅褐色的<b>落羽松林</b>；此外，水面上亦培育了台灣萍蓬草、大萍、睡蓮等，建構出多層次的生態環境。</p>
        </div>

        <div id="bird-section">
            <h3 class="grid-title">🦆 園區鳥類觀測入口 (六大核心物種)</h3>
            <div class="card-grid">
                </div>

                <div class="bird-card">
                    <div class="thumbnail-wrapper">
                        <img src="900.jpg" alt="小鷿鷈">
                    </div>
                    <div class="card-content">
                        <h4>小鷿鷈</h4>
                        <button class="cta-btn" onclick="alert('開啟小鷿鷈潛水覓食習性與影音資料！')">探索物種檔案</button>
                    </div>
                </div>

                <div class="bird-card">
                    <div class="thumbnail-wrapper">
                        <img src="1200.jpg" alt="蒼鷺">
                    </div>
                    <div class="card-content">
                        <h4>蒼鷺</h4>
                        <button class="cta-btn" onclick="alert('開啟大水面大型留鳥蒼鷺的站立地標點調查！')">進入地景觀測</button>
                    </div>
                </div>

                <div class="bird-card">
                    <div class="thumbnail-wrapper">
                        <img src="images.jpg" alt="小白鷺">
                    </div>
                    <div class="card-content">
                        <h4>小白鷺</h4>
                        <button class="cta-btn" onclick="alert('深入了解濕地生態指標——小白鷺的繁殖期羽色變化！')">瀏覽棲地報告</button>
                    </div>
                </div>
                </div>

                <div class="bird-card">
                    <div class="thumbnail-wrapper">
                        <img src="鴛鴦攝影：蔡木寬_提供6.jpg" alt="鴛鴦">
                    </div>
                    <div class="card-content">
                        <h4>鴛鴦 (蔡木寬 攝影)</h4>
                        <button class="cta-btn" onclick="alert('查看珍貴過境鳥鴛鴦的季節性遷徙與水質依存度分析！')">觀看珍貴影像</button>
                    </div>
                </div>

            </div>
        </div>

        <div class="info-card" id="water">
            <h2>水質淨化與昆蟲生態</h2>
            <hr>
            <p>八德生態埤塘的一大特色在於其<b>「自然水質淨化系統」</b>。引進的水源會依序經過沉砂池、漫灘濕地、植物淨化池、開放水域等多道關卡。利用水生植物與微藻類的生物代謝作用，自然分解水中雜質與過多養分，使排出的水質達到高標準澄澈度。</p>
            <p>乾淨的水質也孕育了豐富的昆蟲多樣性，包括多種蜻蜓、豆娘以及季節性的螢火蟲，是觀察水生昆蟲的最佳廊道。</p>
            <h3>微氣候與水棲昆蟲指標 (井上絢香 補充)</h3>
            <p>根據研究團隊的實地水質電導度與溶氧量觀測，淨化後的梯田式濕地為特定敏感型昆蟲提供了絕佳的繁衍溫床。此處已被列為桃園重要的蜻蛉目（蜻蜓與豆娘）保育熱點，水質的良窳直接反映在每年春夏季水棲昆蟲稚蟲的羽化存活率上，是極具價值的環境指標生物資料庫。</p>
        </div>

        <div class="info-card" id="landscape">
            <h2>地景與水利工程</h2>
            <hr>
            <ul>
                <li><strong>高架觀景涼亭：</strong> 園區內的制高點綠建築，可俯瞰整個大水面與觀察島上的鳥類動態。</li>
                <li><strong>森之散步道：</strong> 以木棧道與高架方式鋪設，減少對地表土壤與動植物根系的破壞。</li>
                <li><strong>防災滯洪系統：</strong> 在颱風或豪雨期間，能瞬間蓄納周邊地表逕流，保障八德市區的水利安全。</li>
            </ul>
            <h3>分水邏輯與歷史導水網路 (井上絢香 補充)</h3>
            <p>本園區在水利設計上巧妙結合了霄裡分渠的歷史脈絡。古法「分水汴」的邏輯在此處被轉化為現代化的環境工程，透過精密的進水口高程控制與沉砂堰結構，讓埤塘在枯水期能維持基本生態基流量，豐水期則發揮滯洪調節功效，體現了先民治水智慧與現代水利科技的完美交融。</p>
        </div>

        <div class="info-card" id="status">
            <h2>變遷與現狀評估</h2>
            <hr>
            <p>目前八德生態埤塘已通過國家環境教育設施場所認證。然而面對近年重劃區人口移入與遊客量激增，如何平衡「觀光遊憩」與「生態保育」成為當前核心課題。研究小組呼籲減少不當餵食禽鳥行為，維護埤塘的自然平衡。</p>
            <h3>土地利用轉型與都市邊緣效應 (井上絢香 補充)</h3>
            <p>從昔日的純農業灌溉用蓄水池，到今日夾處在都市重劃區與國防大學空間軸線之間的自然公園，八德埤塘正承受著顯著的「都市熱島」邊緣衝擊。如何在快速水泥化的周邊環境中，透過綠帶補償與水域棲地串聯來擴大其生態外溢效果，是延續這片千塘之鄉綠色命脈的關鍵挑戰。</p>
        </div>

        <div class="info-card" id="mission">
            <h2>互動任務與環境教育</h2>
            <hr>
            <p>為了推廣埤塘文化，歡迎加入我們的數位調查挑戰！</p>
            <p>本互動專區由研究團隊共同開發，融入了園區內真實的植物調查數據與水利分水系統知識。透過情境式問答，大眾不僅能化身為一日生態觀察家，更能深刻體會濕地保育的必要性，達成數位典藏與環境普及教育的初衷。</p>
            <button class="cta-btn" style="max-width:200px;" onclick="alert('恭喜解鎖第一關！請填寫井上絢香與陳秉詩設計的埤塘昆蟲與鳥類挑戰賽！')">開始生態解說挑戰</button>
        </div>

    </main>

    <footer>
        研究組員：陳秉詩、井上絢香 | 八德生態埤塘全球資訊庫
    </footer>

</body>
</html>
