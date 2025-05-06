<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>אסטרטגיות מסחר</title>
    <style>
        :root {
            /* Theme Colors */
            --bg-color: #131722;
            --text-color: #d1d4dc;
            --primary-color-text: #2962ff; /* Blue for text accents like H2 */
            --secondary-color: #1e222d;
            --accent-color-reset: #e74c3c;
            --border-color: #434651;
            --checklist-bg: #1e222d;
            --note-bg: #2a2e39;
            --table-header-bg: #363a45;
            --table-row-odd-bg: #2a2e39;
            --completion-color: #26a69a;
            --link-color: #299dcd;
            --button-bg-color: #1f2937; /* Dark Grey-Blue */
            --button-text-color: #d1d4dc; /* Light Grey text for buttons */
            --strikethrough-color: #7a808e; /* Color for completed item text */
            --lightbox-bg: rgba(0, 0, 0, 0.85);
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            padding: 20px;
            font-size: 1.05rem;
        }

        h1 { text-align: center; color: var(--primary-color-text); margin-bottom: 30px; font-size: 2em; font-weight: 600; }

        .strategies-container { max-width: 950px; margin: 0 auto; }

        .strategy { background-color: var(--secondary-color); margin-bottom: 10px; border-radius: 5px; overflow: hidden; border: 1px solid var(--border-color); box-shadow: 0 2px 5px rgba(0,0,0,0.2); }

        /* Strategy Toggle Button Size */
        .strategy-toggle { background-color: var(--button-bg-color); color: var(--button-text-color); border: none; padding: 20px 26px; width: 100%; text-align: center; font-size: 1.6em; font-weight: 600; cursor: pointer; display: flex; justify-content: center; align-items: center; position: relative; transition: background-color 0.3s ease; }
        .strategy-toggle::after { content: '+'; font-size: 1.6em; font-weight: bold; position: absolute; right: 25px; transition: transform 0.3s ease; }
        .strategy-toggle.active::after { content: '−'; transform: rotate(180deg); }
        .strategy-toggle:hover { background-color: #2d3a4f; }

        .checklist { background-color: var(--secondary-color); padding: 25px; display: none; border-top: 1px solid var(--border-color); }
        /* Keep H2, H3, H4 font sizes as they were */
        .checklist h2 { color: var(--primary-color-text); margin-top: 20px; margin-bottom: 15px; padding-bottom: 8px; border-bottom: 1px solid var(--border-color); font-size: 1.5em; font-weight: 600; }
        .checklist h2:first-child { margin-top: 0; }
        .checklist h3 { color: var(--text-color); font-weight: 600; margin-top: 15px; margin-bottom: 10px; font-size: 1.3em; }
        .checklist h4 { color: var(--text-color); font-weight: 500; margin-top: 15px; margin-bottom: 5px; font-size: 1.2em; }

        .checklist-items { margin-bottom: 25px; }

        .checklist-item { display: block; margin-bottom: 15px; padding: 8px 5px; border-radius: 3px; transition: background-color 0.2s; }
        .checklist-item:hover { background-color: rgba(255, 255, 255, 0.05); }
        .checklist-item input[type="checkbox"] { margin-left: 12px; transform: scale(1.3); cursor: pointer; vertical-align: middle; accent-color: var(--primary-color-text); }
        .checklist-item label { cursor: pointer; display: flex; align-items: center; }

        /* Checklist Text Size (Increased in previous step) */
        .checklist-item label span {
            flex-grow: 1;
            font-size: 2.3em;
            line-height: 1.4;
            transition: color 0.3s, text-decoration 0.3s;
        }
        /* Style for Completed Checklist Item Text */
        .checklist-item label.completed-item span {
            text-decoration: line-through;
            text-decoration-thickness: 1.5px;
            color: var(--strikethrough-color);
        }


        /* Table Styling */
        .backtesting-data { background-color: transparent; padding: 0; margin-top: 25px; border: none; font-size: 1.1em; overflow-x: auto; }
        .backtesting-data h3 { margin-bottom: 15px; }
        .backtesting-table { width: 100%; border-collapse: collapse; text-align: right; border: 1px solid var(--border-color); border-radius: 4px; overflow: hidden; margin-bottom: 20px; }
        .backtesting-table th, .backtesting-table td { border: 1px solid var(--border-color); padding: 10px 12px; font-size: 1.2em; vertical-align: middle; }
        .backtesting-table thead th { background-color: var(--table-header-bg); color: var(--text-color); font-weight: 600; text-align: center; }
        .backtesting-table tbody tr { background-color: var(--secondary-color); }
        .backtesting-table tbody tr:nth-child(odd) { background-color: var(--table-row-odd-bg); }
        .backtesting-table tbody tr:hover { background-color: rgba(255, 255, 255, 0.08); }
        .backtesting-table th:nth-child(1), .backtesting-table td:nth-child(1) { width: 15%; }
        .backtesting-table th:nth-child(2), .backtesting-table td:nth-child(2) { width: 45%; }
        .backtesting-table th:nth-child(3), .backtesting-table td:nth-child(3) { width: 20%; text-align: center;}
        .backtesting-table th:nth-child(4), .backtesting-table td:nth-child(4) { width: 20%; text-align: center;}
        .backtesting-table .th-daytrading-asset { width: 20%; }
        .backtesting-table .th-daytrading-settings { width: 45%; }
        .backtesting-table .th-daytrading-success { width: 15%; }
        .backtesting-table .th-daytrading-trades { width: 20%; }


        /* Notes Styling */
        .strategy-notes { background-color: var(--note-bg); padding: 20px; margin-top: 25px; border-radius: 5px; border: 1px solid var(--border-color); font-size: 1.1em; }
        .strategy-notes h3 { margin-top: 0; margin-bottom: 10px; }
        .strategy-notes ul { list-style-position: inside; padding-right: 5px; }
        .strategy-notes li { margin-bottom: 8px; font-size: 1.2em; }

        /* Completion Message */
        .completion-message { margin-top: 0; margin-bottom: 25px; padding: 15px; background-color: var(--completion-color); color: #fff; text-align: center; font-weight: bold; border-radius: 5px; font-size: 1.4em; display: none; }

        /* Reset Button */
        .reset-checklist { background-color: var(--button-bg-color); color: var(--button-text-color); border: none; padding: 10px 18px; border-radius: 4px; cursor: pointer; font-size: 1.1em; font-weight: 500; transition: background-color 0.3s ease; text-align: center; margin-top: 20px; }
        .reset-checklist:hover { background-color: #2d3a4f; }


        /* === Image Reminders & Lightbox Styling (Item 2) === */
        .image-reminders { margin-top: 30px; padding-top: 20px; border-top: 1px solid var(--border-color); }
        .image-reminders h2 { margin-top: 0; margin-bottom: 15px; font-size: 1.5em; }
        .image-reminders h4 { margin-top: 15px; margin-bottom: 10px; font-size: 1.2em; }
        .image-reminders .image-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Base size */
            gap: 15px;
            margin-top: 10px;
        }
        .image-reminders .image-grid a {
            display: block;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            overflow: hidden;
            line-height: 0;
            background-color: var(--note-bg);
            cursor: pointer; /* Indicate clickability for lightbox */
        }
        .image-reminders .image-grid img {
            width: 100%;
            /* Increased height by 40% (150px * 1.4) */
            height: 210px;
            object-fit: cover;
            display: block;
            /* cursor: pointer; (Handled by link) */
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out, opacity 0.2s;
            opacity: 0.9;
        }
         .image-reminders .image-grid img:hover {
            transform: scale(1.05);
             box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
             opacity: 1;
        }

        /* Lightbox Overlay */
        #lightbox-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: var(--lightbox-bg);
            display: none; /* Hidden by default */
            justify-content: center;
            align-items: center;
            z-index: 1000;
            cursor: pointer; /* Click background to close */
            padding: 20px; /* Add padding for smaller screens */
        }
        #lightbox-image {
            max-width: 95%; /* Adjusted max-width */
            max-height: 95%; /* Adjusted max-height */
            object-fit: contain;
            border: 3px solid var(--border-color);
            border-radius: 5px;
            cursor: default; /* Don't close when clicking image itself */
            box-shadow: 0 0 30px rgba(0,0,0,0.5);
        }
        #lightbox-close {
            position: absolute;
            top: 15px;
            right: 30px;
            color: #fff;
            font-size: 45px;
            font-weight: bold;
            line-height: 1;
            cursor: pointer;
            z-index: 1010;
            text-shadow: 0 1px 3px rgba(0,0,0,0.5);
        }
        /* === End Image & Lightbox Styling === */


        /* Responsive adjustments */
        @media (max-width: 768px) {
            body { padding: 15px; font-size: 1rem; }
            .strategy-toggle { padding: 16px 20px; font-size: 1.4em; } .strategy-toggle::after { font-size: 1.4em; right: 20px; }
            .checklist { padding: 20px; } h1 { font-size: 1.8em; }
            /* Adjust checklist text size */
            .checklist-item label span { font-size: 1.9em; }
            .backtesting-table th, .backtesting-table td { font-size: 1.1em; padding: 8px; }
            .strategy-notes li, .reset-checklist { font-size: 1.2em; } .completion-message { font-size: 1.3em; }
            /* Adjust image grid/height */
            .image-reminders .image-grid { grid-template-columns: repeat(auto-fill, minmax(120px, 1fr)); gap: 10px; }
            .image-reminders .image-grid img { height: 168px; /* 120px * 1.4 */ }
        }
        @media (max-width: 480px) {
             body { padding: 10px; } h1 { font-size: 1.6em; }
             .strategy-toggle { padding: 14px 18px; font-size: 1.2em; } .strategy-toggle::after { font-size: 1.2em; right: 18px; }
             /* Adjust checklist text size */
             .checklist-item label span { font-size: 1.7em; }
             .backtesting-table th, .backtesting-table td, .strategy-notes li, .reset-checklist, .completion-message { font-size: 1.1em; }
             /* Adjust image grid/height */
             .image-reminders .image-grid { grid-template-columns: repeat(auto-fill, minmax(100px, 1fr)); gap: 8px; }
             .image-reminders .image-grid img { height: 140px; /* 100px * 1.4 */ }
         }

    </style>
</head>
<body>

    <h1>אסטרטגיות מסחר</h1>

    <div class="strategies-container">

        <div class="strategy">
            <button class="strategy-toggle">Support and Resistance for Stocks and Forex</button>
            <div class="checklist" data-strategy="support-resistance">
                <h2>חוקי כניסה ובדיקות</h2>
                <div class="checklist-items">
                    <label class="checklist-item"><input type="checkbox"><span>האם אנחנו סוחרים בכיוון הטראנד הראשי? EMA 200 ירוק ללונג</span></label>
                    <label class="checklist-item"><input type="checkbox"><span>האם יש לנו אישור של האינדיקטור Patternsmart 10 שאנחנו באיזור תמיכה/התנגדות?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span>האם הנר נסגר באיזור התמיכה/התנגדות שסימנו? נר אדום אחרון בירידות ללונג או נר ירוק בעליות לשורט. (עד החצי לפחות)</span></label>
                    <label class="checklist-item"><input type="checkbox"><span>האם הנר נסגר מחוץ לאיזור תמיכה/התנגדות כלומר פריצה עם כיוון הטראנד?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span>האם המניה נתמכת על הEMA 200? אם כן נסמן את הצאקליסט.</span></label>
                    <label class="checklist-item"><input type="checkbox"><span>להזיז את הסטופלוס לאיזור רחוק ובטוח יותר + לוודא שיש התראה בTradingview</span></label>
                </div>
                 <p class="completion-message" style="display: none;"></p>
                 <div class="backtesting-data">
                    <h3>נתוני Backtesting</h3>
                    <table class="backtesting-table">
                         <thead><tr><th>נכס</th><th>הגדרות מסחר</th><th>% הצלחה</th><th>עסקאות</th></tr></thead>
                         <tbody>
                            <tr><td>GBPUSD</td><td>TP 1:2, EMA 100&200, No Vol</td><td>67.86%</td><td>29</td></tr>
                            <tr><td>USDJPY</td><td>TP 1:2, EMA 100&200, No Vol</td><td>68.42%</td><td>20</td></tr>
                            <tr><td>EUR/USD</td><td>TP 1:2, EMA 50&200, No Vol</td><td>73.68%</td><td>39</td></tr>
                            <tr><td>SPY</td><td>TP 1:2, EMA 50&200, No Vol</td><td>74.07%</td><td>27</td></tr>
                            <tr><td>QQQ</td><td>TP 1:2, EMA 100&200, No Vol</td><td>81.82%</td><td>12</td></tr>
                            <tr><td>Meta</td><td>TP Res/1:2 (First), EMA 50&200, No Vol</td><td>60%</td><td>31</td></tr>
                            <tr><td>Amazon</td><td>TP 1:2, EMA 50&200, No Vol</td><td>66.67%</td><td>13</td></tr>
                            <tr><td>Google</td><td>Res or 1:2 (First), EMA 50&200, No Vol</td><td>80%</td><td>21</td></tr>
                            <tr><td>TSLA</td><td>TP 1:2, EMA 100&200, No Vol</td><td>69.57%</td><td>24</td></tr>
                            <tr><td>NVDA</td><td>TP 1:2/Res (First), EMA 50&200, No Vol</td><td>76%</td><td>26</td></tr>
                            <tr><td>MSFT</td><td>TP 1:2, EMA 50&200, No Vol</td><td>68.97%</td><td>30</td></tr>
                            <tr><td>NFLX</td><td>TP 1:2, EMA 50&200, No Vol</td><td>68.18%</td><td>23</td></tr>
                         </tbody>
                    </table>
                </div>
                <div class="strategy-notes">
                    <h3>💡 הערות חשובות</h3>
                    <ul>
                        <li>בתחילת מגמה, שקול "CrossBoom!" (TP 1:3).</li>
                        <li>באזור קיצון + תמיכת EMA 200, השתמש בסטופ לפי ספירת נרות.</li>
                    </ul>
                </div>
                 <div class="image-reminders">
                    <h2>תמונות לתזכורת</h2>
                    <h4>דוגמאות ללונג:</h4>
                    <div class="image-grid">
                        <a href="https://www.tradingview.com/x/bM0FDnim/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/bM0FDnim/" alt="S&R Long Example 1"></a>
                        <a href="https://www.tradingview.com/x/JohcCkqa/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/JohcCkqa/" alt="S&R Long Example 2"></a>
                        <a href="https://www.tradingview.com/x/PSbc6C3m/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/PSbc6C3m/" alt="S&R Long Example 3"></a>
                    </div>
                    <h4>דוגמאות לשורט:</h4>
                     <div class="image-grid">
                        <a href="https://www.tradingview.com/x/QAp63XED/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/QAp63XED/" alt="S&R Short Example 1"></a>
                        <a href="https://www.tradingview.com/x/Hzb3sH3O/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/Hzb3sH3O/" alt="S&R Short Example 2"></a>
                        <a href="https://www.tradingview.com/x/UgPHw1yU/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/UgPHw1yU/" alt="S&R Short Example 3"></a>
                    </div>
                 </div>
                <button class="reset-checklist">אפס סימונים</button>
            </div>
        </div>

        <div class="strategy">
            <button class="strategy-toggle">RSI Divergences Strategy</button>
            <div class="checklist" data-strategy="rsi-divergence-swing">
                 <h2>חוקי כניסה ובדיקות</h2>
                 <div class="checklist-items">
                    <label class="checklist-item"><input type="checkbox"><span><strong>כיוון טראנד ראשי:</strong> האם סוחרים בכיוון? (EMA 200 ירוק ללונג)</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>התראת Divergence:</strong> האם התקבלה באיזורי קיצון?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>מיקום RSI:</strong> האם מתחת ל-50 (לונג) / מעל 50 (שורט) לאישור קיצון?</span></label>
                 </div>
                 <p class="completion-message" style="display: none;"></p>
                 <div class="backtesting-data">
                     <h3>נתוני Backtesting</h3>
                     <table class="backtesting-table">
                        <thead><tr><th>נכס</th><th>הגדרות מסחר</th><th>% הצלחה</th><th>עסקאות</th></tr></thead>
                        <tbody>
                            <tr><td>NFLX</td><td>Entry 50&200EMA, SL count 3 candles ATR RMA: 2</td><td>80.95%</td><td>29</td></tr>
                            <tr><td>SPY</td><td>Entry 50&200EMA, ATR RMA: 2 (No count)</td><td>66.67%</td><td>34</td></tr>
                            <tr><td>QQQ</td><td>Entry 100&200EMA, SL count 3 candles ATR RMA: 2</td><td>61.06%</td><td>31</td></tr>
                            <tr><td>AAPL</td><td>Entry 50&200EMA, ATR RMA: 2 (No count)</td><td>80.77%</td><td>26</td></tr>
                            <tr><td>GOOGL</td><td>Entry 50&200EMA, ATR RMA: 1.5 (No count)</td><td>86.67%</td><td>30</td></tr>
                            <tr><td>AMZN</td><td>Entry 50&200EMA, SL count 3 candles ATR RMA: 2</td><td>81.25%</td><td>47</td></tr>
                            <tr><td>META</td><td>Entry 50&200EMA, ATR RMA: 1.5/2 (No count)</td><td>48.28%</td><td>31</td></tr>
                            <tr><td>MSFT</td><td>Entry 50&200EMA, ATR RMA: 1.5/2 (No count)</td><td>50%</td><td>26</td></tr>
                            <tr><td>TSLA</td><td>Entry 50&200EMA, ATR RMA: 1.5 (No count)</td><td>48%</td><td>26</td></tr>
                            <tr><td>NVDA</td><td>Entry 50&200EMA, ATR RMA: 1.5/2 (No count)</td><td>76.92%</td><td>10</td></tr>
                            <tr><td>USD/JPY</td><td>Entry 100&200EMA, SL count 3 candles ATR RMA: 2</td><td>71%</td><td>35</td></tr>
                            <tr><td>EUR/USD</td><td>Entry 50&200EMA, SL count 3 candles ATR RMA: 2</td><td>51.61%</td><td>31</td></tr>
                            <tr><td>GBP/USD</td><td>Entry 100&200EMA, SL count 3 candles ATR RMA: 2</td><td>53.85%</td><td>26</td></tr>
                        </tbody>
                     </table>
                 </div>
                  <div class="image-reminders">
                     <h2>תמונות לתזכורת</h2>
                     <h4>דוגמאות לשורט:</h4>
                     <div class="image-grid">
                         <a href="https://www.tradingview.com/x/6doKSOAp/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/6doKSOAp/" alt="RSI Div Swing Short Example 1"></a>
                         <a href="https://www.tradingview.com/x/Z020n6ZO/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/Z020n6ZO/" alt="RSI Div Swing Short Example 2"></a>
                         <a href="https://www.tradingview.com/x/bifOigED/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/bifOigED/" alt="RSI Div Swing Short Example 3"></a>
                     </div>
                     <h4>דוגמאות ללונג:</h4>
                      <div class="image-grid">
                         <a href="https://www.tradingview.com/x/lN96PC0Q/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/lN96PC0Q/" alt="RSI Div Swing Long Example 1"></a>
                         <a href="https://www.tradingview.com/x/3ZFa8Bw3/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/3ZFa8Bw3/" alt="RSI Div Swing Long Example 2"></a>
                         <a href="https://www.tradingview.com/x/BTKuNTpp/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/BTKuNTpp/" alt="RSI Div Swing Long Example 3"></a>
                     </div>
                  </div>
                <button class="reset-checklist">אפס סימונים</button>
            </div>
        </div>

        <div class="strategy">
            <button class="strategy-toggle">RSI Wave Strategy Stocks</button>
             <div class="checklist" data-strategy="rsi-wave">
                 <h2>חוקי כניסה ובדיקות</h2>
                 <div class="checklist-items">
                    <label class="checklist-item"><input type="checkbox"><span><strong>כיוון טראנד ראשי:</strong> האם סוחרים בכיוון? (EMA 200 ירוק ללונג)</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>טראנד חזק:</strong> האם מקפצת מעל EMA 200? + האם הגבוה נשבר?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>התראת RSI:</strong> האם מ-46-54 ללונג? + האם נר נסגר אח"כ?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>תיקון ל-EMA משני:</strong> האם התבצע לפי הרשימה?</span></label>
                 </div>
                 <p class="completion-message" style="display: none;"></p>
                  <div class="backtesting-data">
                     <h3>נתוני Backtesting (RSI Wave)</h3>
                     <table class="backtesting-table">
                        <thead><tr><th>נכס</th><th>הגדרות מסחר</th><th>% הצלחה</th><th>עסקאות</th></tr></thead>
                        <tbody>
                            <tr><td>SPY</td><td>Best TP 1:2, Entry Every RSI > 200EMA</td><td>61.62%</td><td>100</td></tr>
                            <tr><td>QQQ</td><td>Best TP 1:2, Entry on touch EMA100</td><td>61.22%</td><td>98</td></tr>
                            <tr><td>AAPL</td><td>Best TP 1:1.5, Entry RSI > 200EMA, Short TP 1:1.5</td><td>56.03%</td><td>142</td></tr>
                            <tr><td>GOOGL</td><td>Best TP Long 1:1.5, Entry touch EMA100, Short N/A</td><td>53.57%</td><td>85</td></tr>
                            <tr><td>AMZN</td><td>Best TP Long 1:2, Short 1:1, Entry touch EMA50</td><td>65.91%</td><td>88</td></tr>
                            <tr><td>META</td><td>Best TP L/S 1:1, Entry RSI > 200EMA</td><td>50.53%</td><td>95</td></tr>
                            <tr><td>MSFT</td><td>Best TP Long 1:2, Short 1:1, Entry touch EMA80</td><td>68.12%</td><td>70</td></tr>
                            <tr><td>TSLA</td><td>Best TP 1:1.5, Entry RSI > 200EMA</td><td>57.75%</td><td>72</td></tr>
                            <tr><td>NVDA</td><td>Best TP Long 1:1.5, Short 1:1, Entry RSI > 200EMA</td><td>56.41%</td><td>78</td></tr>
                            <tr><td>NFLX</td><td>Best TP 1:1.5, Entry if touch EMA50</td><td>55.32%</td><td>46</td></tr>
                        </tbody>
                     </table>
                 </div>
                 <div class="backtesting-data">
                     <h3>תוצאות Backtesting (CrossBoom Strategy)</h3>
                     <table class="backtesting-table">
                         <thead><tr><th>נכס</th><th>CrossBoom Strategy</th><th>אחוזי הצלחה</th><th>כמות עסקאות שנבדקו</th></tr></thead>
                         <tbody>
                             <tr><td>SPY</td><td>Best take profit is : 1:4</td><td>46.43%</td><td>28</td></tr>
                             <tr><td>QQQ</td><td>Best take profit is : 1:4</td><td>47.06%</td><td>16</td></tr>
                             <tr><td>META</td><td>Best take profit is : Trailing stop</td><td>61.11%</td><td>18</td></tr>
                             <tr><td>TSLA</td><td>לא לעשות טריידים באסטרטגיה זו</td><td>36%</td><td>29</td></tr>
                             <tr><td>NFLX</td><td>Trailing stop Or 1:3</td><td>54.17%</td><td>24</td></tr>
                             <tr><td>Amazon</td><td>Trailing stop Or 1:4</td><td>48.12%</td><td>27</td></tr>
                             <tr><td>NVIDIA</td><td>Trailing stop Only</td><td>59.26%</td><td>27</td></tr>
                             <tr><td>Apple</td><td>Best take profit is : Trailing stop</td><td>46.88%</td><td>30</td></tr>
                             <tr><td>Google</td><td>Best take profit is : 1:4</td><td>63.16%</td><td>26</td></tr>
                        </tbody>
                     </table>
                 </div>
                  <div class="strategy-notes">
                    <h3>💡 הערות חשובות</h3>
                     <ul>
                        <li>לא לסחור שורטים על QQQ.</li>
                        <li>בתחילת מגמה, שקול Crossboom.</li>
                        <li>ניהול סיכונים: עד 50$ לעסקה.</li>
                    </ul>
                 </div>
                  <div class="image-reminders">
                     <h2>תמונות לתזכורת</h2>
                     <h4>ללונג:</h4>
                     <div class="image-grid">
                        <a href="https://www.tradingview.com/x/ud53eXKW/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/ud53eXKW/" alt="RSI Wave Long Example 1"></a>
                        <a href="https://www.tradingview.com/x/AljhrQfj/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/AljhrQfj/" alt="RSI Wave Long Example 2"></a>
                        <a href="https://www.tradingview.com/x/P4QCFZoV/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/P4QCFZoV/" alt="RSI Wave Long Example 3"></a>
                        <a href="https://www.tradingview.com/x/078uX1EQ/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/078uX1EQ/" alt="RSI Wave Long Example 4"></a>
                     </div>
                     <h4>לשורט:</h4>
                      <div class="image-grid">
                        <a href="https://www.tradingview.com/x/2BlHVoEl/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/2BlHVoEl/" alt="RSI Wave Short Example 1"></a>
                        <a href="https://www.tradingview.com/x/wnOBMGJ7/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/wnOBMGJ7/" alt="RSI Wave Short Example 2"></a>
                     </div>
                  </div>
                <button class="reset-checklist">אפס סימונים</button>
            </div>
        </div>

        <div class="strategy">
            <button class="strategy-toggle">FB With RSI Divergences</button>
             <div class="checklist" data-strategy="fb-rsi-divergence">
                 <h2>חוקי כניסה ובדיקות</h2>
                 <div class="checklist-items">
                    <label class="checklist-item"><input type="checkbox"><span><strong>כיוון טראנד ראשי:</strong> האם בכיוון ה-EMA 200?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>התראת FB:</strong> האם התקבלה?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>חזרה לטראנד + Divergence:</strong> האם נר חזר עם RSI Div?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>סגירת נר:</strong> האם נסגר מעל קו S/R?</span></label>
                 </div>
                 <p class="completion-message" style="display: none;"></p>
                  <div class="backtesting-data">
                     <h3>נתוני Backtesting</h3>
                     <table class="backtesting-table">
                        <thead><tr><th>נכס</th><th>הגדרות מסחר</th><th>% הצלחה</th><th>עסקאות</th></tr></thead>
                        <tbody>
                             <tr><td>AMZN</td><td>SL ATR 1, TP 1:2</td><td>76.67%</td><td>30</td></tr>
                             <tr><td>GOOGL</td><td>SL ATR 1, TP 1:2</td><td>81.08%</td><td>37</td></tr>
                             <tr><td>MSFT</td><td>SL ATR 0 (Low), TP 1:2</td><td>78.57%</td><td>28</td></tr>
                             <tr><td>NFLX</td><td>SL ATR 2, TP 1:2</td><td>56%</td><td>26</td></tr>
                             <tr><td>NVDA</td><td>SL ATR 0 (Low), TP 1:2</td><td>76%</td><td>26</td></tr>
                             <tr><td>TSLA</td><td>SL ATR 0 (Low), TP 1:2</td><td>84.21%</td><td>20</td></tr>
                             <tr><td>SPY</td><td>SL ATR 0 (Low), TP 1:2</td><td>70.27%</td><td>38</td></tr>
                             <tr><td>QQQ</td><td>SL ATR 2, TP 1:2</td><td>56.67%</td><td>31</td></tr>
                             <tr><td>EURUSD</td><td>SL ATR 0 (Low), TP 1:2</td><td>69.05%</td><td>42</td></tr>
                             <tr><td>USDJPY</td><td>SL ATR 0 (Low), TP 1:2</td><td>56.41%</td><td>40</td></tr>
                             <tr><td>GBPUSD</td><td>SL ATR 0 (Low), TP 1:2</td><td>66.67%</td><td>39</td></tr>
                        </tbody>
                     </table>
                 </div>
                  <div class="image-reminders">
                     <h2>תמונות לתזכורת</h2>
                     <h4>דוגמאות ללונג:</h4>
                     <div class="image-grid">
                        <a href="https://www.tradingview.com/x/ugJiMJgA/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/ugJiMJgA/" alt="FB RSI Div Long Example 1"></a>
                        <a href="https://www.tradingview.com/x/xsiiFO41/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/xsiiFO41/" alt="FB RSI Div Long Example 2"></a>
                        <a href="https://www.tradingview.com/x/UCbJNWqj/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/UCbJNWqj/" alt="FB RSI Div Long Example 3"></a>
                     </div>
                     <h4>דוגמאות לשורט:</h4>
                      <div class="image-grid">
                        <a href="https://www.tradingview.com/x/PfhWK1M0/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/PfhWK1M0/" alt="FB RSI Div Short Example 1"></a>
                        <a href="https://www.tradingview.com/x/OFQnsnAD/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/OFQnsnAD/" alt="FB RSI Div Short Example 2"></a>
                        <a href="https://www.tradingview.com/x/i6QBGGH8/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/i6QBGGH8/" alt="FB RSI Div Short Example 3"></a>
                     </div>
                  </div>
                <button class="reset-checklist">אפס סימונים</button>
            </div>
        </div>

        <div class="strategy">
            <button class="strategy-toggle">Day trading RSI Divergences Strategy</button>
             <div class="checklist" data-strategy="day-trading-rsi">
                 <h2>חוקי כניסה ובדיקות</h2>
                 <div class="checklist-items">
                    <label class="checklist-item"><input type="checkbox"><span><strong>איזור התנגדות (15ד'):</strong> האם אנחנו סוחרים באיזור התנגדות של 15 דקות?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>סטיה (מחיר-RSI):</strong> האם קיבלנו סטיה בין המחיר ל-RSI עם קו מפיבוט לפיבוט (Patternsmart אינדיקטור 2)?</span></label>
                    <label class="checklist-item"><input type="checkbox"><span><strong>פריצת קו מקווקו:</strong> האם המחיר חזר לאחר הסטיה ופרץ את הקו המקווקו?</span></label>
                 </div>
                 <p class="completion-message" style="display: none;"></p>
                 <div class="strategy-notes">
                    <h3>💡 תזכורות</h3>
                     <ul>
                        <li>במידה וקיבלנו פינבר ניכנס ישירות לעסקה ולא נמתין לנר אישור.</li>
                    </ul>
                 </div>
                 <div class="image-reminders">
                    <h2>תמונות לתזכורת</h2>
                    <h4>דוגמאות לשורט:</h4>
                    <div class="image-grid">
                        <a href="https://www.tradingview.com/x/EABaeTdN/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/EABaeTdN/" alt="Day Trading RSI Short Example 1"></a>
                        <a href="https://www.tradingview.com/x/WVWQut26/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/WVWQut26/" alt="Day Trading RSI Short Example 2"></a>
                        <a href="https://www.tradingview.com/x/ctrWAsDw/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/ctrWAsDw/" alt="Day Trading RSI Short Example 3"></a>
                    </div>
                    <h4>דוגמאות ללונג:</h4>
                    <div class="image-grid">
                        <a href="https://www.tradingview.com/x/xg0jXjzT/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/xg0jXjzT/" alt="Day Trading RSI Long Example 1"></a>
                        <a href="https://www.tradingview.com/x/ZO35VbJM/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/ZO35VbJM/" alt="Day Trading RSI Long Example 2"></a>
                        <a href="https://www.tradingview.com/x/WG1aykzJ/" rel="noopener noreferrer"><img src="https://www.tradingview.com/x/WG1aykzJ/" alt="Day Trading RSI Long Example 4"></a>
                    </div>
                 </div>
                 <div class="backtesting-data">
                     <h3>נתוני Backtesting</h3>
                      <table class="backtesting-table">
                          <thead>
                             <tr>
                                 <th class="th-daytrading-asset">נכס</th>
                                 <th class="th-daytrading-settings">הגדרות מסחר</th>
                                 <th class="th-daytrading-success">% הצלחה</th>
                                 <th class="th-daytrading-trades">עסקאות</th>
                             </tr>
                         </thead>
                         <tbody>
                             <tr>
                                 <td>EUR/USD</td>
                                 <td>Support at 15min</td>
                                 <td>69%</td>
                                 <td>232</td>
                             </tr>
                         </tbody>
                      </table>
                 </div>
                 <button class="reset-checklist">אפס סימונים</button>
            </div>
        </div>
        </div>

    <div id="lightbox-overlay" style="display: none;">
        <span id="lightbox-close">&times;</span>
        <img id="lightbox-image" src="" alt="Enlarged image">
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const strategiesContainer = document.querySelector('.strategies-container');
            const lightboxOverlay = document.getElementById('lightbox-overlay');
            const lightboxImage = document.getElementById('lightbox-image');
            const lightboxClose = document.getElementById('lightbox-close');


            // Function to check completion status for a specific checklist
            function checkCompletion(checklistElement) {
                const checkboxes = checklistElement.querySelectorAll('.checklist-items input[type="checkbox"]');
                const completionMessage = checklistElement.querySelector('.completion-message');
                const strategyType = checklistElement.getAttribute('data-strategy');
                let allChecked = checkboxes.length > 0 && Array.from(checkboxes).every(cb => cb.checked);
                let showMessage = false;
                let messageText = '';

                if (!completionMessage) return;

                switch (strategyType) {
                    case 'support-resistance':
                        const checkedCount = Array.from(checkboxes).filter(cb => cb.checked).length;
                        if (checkedCount === 4) {
                            messageText = 'סיימנו כל הכבוד! 🎉😊🎉';
                            showMessage = true;
                        } else if (checkedCount === 5) {
                            messageText = 'עכשיו ניתן להיכנס לעסקה! אך עדיין לא סיימנו, צריך להזיז סטופים לאחר כניסה ולהציב התראה באיזור הסטופים';
                            showMessage = true;
                        } else if (checkedCount === 6) {
                            messageText = 'סיימנו כל הכבוד! 🎉😊🎉';
                            showMessage = true;
                        } else {
                            showMessage = false;
                        }
                        break;
                    default:
                        if (allChecked) {
                            messageText = 'סיימנו כל הכבוד! 🎉😊🎉';
                            showMessage = true;
                        } else {
                            showMessage = false;
                        }
                        break;
                }

                if (showMessage) {
                    completionMessage.innerHTML = messageText;
                    completionMessage.style.display = 'block';
                } else {
                    completionMessage.style.display = 'none';
                }
            }

             // Function to toggle completed style on checklist item
             function toggleItemCompletionStyle(checkbox) {
                const labelElement = checkbox.closest('label');
                if (labelElement) {
                    if (checkbox.checked) {
                        labelElement.classList.add('completed-item');
                    } else {
                        labelElement.classList.remove('completed-item');
                    }
                }
             }

             // --- Lightbox Functions (Item 2) ---
             function openLightbox(imageUrl, altText) {
                if (!lightboxOverlay || !lightboxImage) return;
                lightboxImage.src = imageUrl;
                lightboxImage.alt = altText;
                lightboxOverlay.style.display = 'flex'; // Show the overlay
             }

             function closeLightbox() {
                 if (!lightboxOverlay) return;
                 lightboxOverlay.style.display = 'none'; // Hide the overlay
                 lightboxImage.src = ''; // Clear image source
                 lightboxImage.alt = '';
             }
             // --- End Lightbox Functions ---


            // Event listener for toggles, reset buttons, image clicks, and checkbox changes
            strategiesContainer.addEventListener('click', function(event) {
                const target = event.target;
                let checklistElement = null;

                // --- Accordion Logic ---
                if (target.classList.contains('strategy-toggle')) {
                    checklistElement = target.nextElementSibling;
                    const isActive = target.classList.contains('active');
                    const allToggles = strategiesContainer.querySelectorAll('.strategy-toggle');

                    allToggles.forEach(otherToggle => {
                        if (otherToggle !== target) {
                            otherToggle.classList.remove('active');
                             if (otherToggle.nextElementSibling) {
                                 otherToggle.nextElementSibling.style.display = 'none';
                             }
                        }
                    });

                    if (isActive) {
                        target.classList.remove('active');
                         if (checklistElement) checklistElement.style.display = 'none';
                    } else {
                        target.classList.add('active');
                         if (checklistElement) {
                             checklistElement.style.display = 'block';
                             checklistElement.querySelectorAll('.checklist-items input[type="checkbox"]').forEach(toggleItemCompletionStyle);
                             checkCompletion(checklistElement);
                         }
                    }
                }

                 // --- Reset Button Logic ---
                if (target.classList.contains('reset-checklist')) {
                    checklistElement = target.closest('.checklist');
                    if (checklistElement) {
                        const checkboxes = checklistElement.querySelectorAll('.checklist-items input[type="checkbox"]');
                        checkboxes.forEach(checkbox => {
                            checkbox.checked = false;
                            toggleItemCompletionStyle(checkbox); // Remove completed style
                        });
                        checkCompletion(checklistElement); // Update completion message
                    }
                }

                // --- Image Click Logic for Lightbox (Item 2) ---
                const imageLink = target.closest('.image-grid a'); // Check if click is on/inside an image link
                if (imageLink && target.tagName === 'IMG') { // Ensure the click was on the image itself
                    event.preventDefault(); // Prevent default link behavior
                    const imageUrl = imageLink.href;
                    const altText = target.alt || 'Enlarged image';
                    openLightbox(imageUrl, altText);
                }
                // --- End Image Click Logic ---
            });

             // --- Checkbox Change Logic ---
             strategiesContainer.addEventListener('change', function(event) {
                 if (event.target.type === 'checkbox') {
                     checklistElement = event.target.closest('.checklist');
                     toggleItemCompletionStyle(event.target); // Toggle strikethrough
                     if (checklistElement) {
                         checkCompletion(checklistElement); // Update completion message
                     }
                 }
             });

             // --- Lightbox Close Logic (Item 2) ---
             if (lightboxOverlay) {
                lightboxOverlay.addEventListener('click', function(event) {
                    // Close if clicked on overlay background or close button
                    if (event.target === lightboxOverlay || event.target === lightboxClose) {
                         closeLightbox();
                    }
                });
             }
             // Optional: Close lightbox with Escape key
             document.addEventListener('keydown', function(event) {
                 if (event.key === 'Escape' && lightboxOverlay && lightboxOverlay.style.display !== 'none') {
                     closeLightbox();
                 }
             });
             // --- End Lightbox Close Logic ---


             // Apply initial styles for potentially pre-opened checklists
             document.querySelectorAll('.checklist').forEach(checklist => {
                 if (checklist.style.display === 'block') {
                      checklist.querySelectorAll('.checklist-items input[type="checkbox"]').forEach(toggleItemCompletionStyle);
                      checkCompletion(checklist);
                 }
             });

        });
    </script>

</body>
</html>
