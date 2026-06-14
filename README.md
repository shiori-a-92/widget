# widget
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  html, body { height: 100%; }
  body {
    display: flex; justify-content: center; align-items: center;
    font-family: "Hiragino Sans", "Yu Gothic", sans-serif;
    background: linear-gradient(135deg, #fce4ec 0%, #fdeef2 100%);
  }
  .widget { text-align: center; }
  .year { font-size: 16px; color: #d48aa6; letter-spacing: 1px; margin-bottom: 10px; }
  .date { font-size: 46px; font-weight: 700; color: #e58aa8; line-height: 1.1; }
  .weekday {
    margin-top: 14px; display: inline-block; padding: 8px 30px;
    border-radius: 999px; font-size: 18px; font-weight: 600; letter-spacing: 3px;
  }
</style>
</head>
<body>
  <div class="widget">
    <div class="year" id="year"></div>
    <div class="date" id="date"></div>
    <div class="weekday" id="weekday"></div>
  </div>
<script>
  const holidays = [
    "2026-01-01","2026-01-12","2026-02-11","2026-02-23","2026-03-20",
    "2026-04-29","2026-05-03","2026-05-04","2026-05-05","2026-05-06",
    "2026-07-20","2026-08-11","2026-09-21","2026-09-22","2026-09-23",
    "2026-10-12","2026-11-03","2026-11-23"
  ];
  function reiwa(year) { const r = year - 2018; return r === 1 ? "令和元年" : "令和" + r + "年"; }
  function update() {
    const now = new Date();
    const weekdaysEn = ["Sun","Mon","Tue","Wed","Thu","Fri","Sat"];
    const day = now.getDay();
    const dateStr = now.getFullYear() + "-" + String(now.getMonth()+1).padStart(2,"0") + "-" + String(now.getDate()).padStart(2,"0");
    const isHoliday = holidays.includes(dateStr);
    const el = document.getElementById("weekday");
    if (day === 0 || isHoliday) { el.style.background = "#f8d7d7"; el.style.color = "#c97b7b"; }
    else if (day === 6) { el.style.background = "#d7e6f8"; el.style.color = "#7b9bc9"; }
    else { el.style.background = "#f8d7e3"; el.style.color = "#c97b98"; }
    document.getElementById("year").textContent = now.getFullYear() + "年（" + reiwa(now.getFullYear()) + "）";
    document.getElementById("date").textContent = (now.getMonth()+1) + "月" + now.getDate() + "日";
    el.textContent = weekdaysEn[day];
  }
  update();
  setInterval(update, 60000);
</script>
</body>
</html>
