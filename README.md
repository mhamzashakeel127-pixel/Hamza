<!DOCTYPE html>
<html lang="ur" dir="ltr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>HS Collection</title>
<link href="https://fonts.googleapis.com/css2?family=Noto+Nastaliq+Urdu:wght@400;700&family=Syne:wght@700;800&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
:root {
  --bg: #060a06;
  --bg2: #0a100a;
  --card: #0e160e;
  --card2: #131d13;
  --card3: #192419;
  --border: #1e3020;
  --border2: #254028;
  --accent: #22c55e;
  --accent2: #4ade80;
  --accent3: #86efac;
  --glow: rgba(34,197,94,0.2);
  --red: #f43f5e;
  --orange: #f97316;
  --yellow: #eab308;
  --blue: #3b82f6;
  --purple: #a855f7;
  --text: #f0fdf0;
  --text2: #d1fae5;
  --muted: #4b7a55;
  --muted2: #6aaf78;
  --font: 'DM Sans', sans-serif;
  --font-head: 'Syne', sans-serif;
  --font-ur: 'Noto Nastaliq Urdu', serif;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html{scroll-behavior:smooth;}
body{background:var(--bg);color:var(--text);font-family:var(--font);min-height:100vh;padding-bottom:85px;overflow-x:hidden;}

body::before{content:'';position:fixed;inset:0;background-image:linear-gradient(rgba(34,197,94,0.03) 1px,transparent 1px),linear-gradient(90deg,rgba(34,197,94,0.03) 1px,transparent 1px);background-size:32px 32px;pointer-events:none;z-index:0;}
body::after{content:'';position:fixed;top:-200px;right:-200px;width:500px;height:500px;background:radial-gradient(circle,rgba(34,197,94,0.08) 0%,transparent 70%);pointer-events:none;z-index:0;}

.container{max-width:500px;margin:0 auto;padding:12px;position:relative;z-index:1;}

.header{padding:16px 0 12px;display:flex;align-items:center;justify-content:space-between;}
.brand-wrap{display:flex;align-items:center;gap:10px;}
.brand-dot{width:36px;height:36px;background:var(--accent);border-radius:10px;display:flex;align-items:center;justify-content:center;font-family:var(--font-head);font-size:16px;font-weight:800;color:#060a06;}
.brand-text{font-family:var(--font-head);font-size:20px;font-weight:800;color:var(--text);}
.brand-sub{font-size:10px;color:var(--muted2);font-family:var(--font-ur);}
.header-right{text-align:right;}
.today-badge{background:var(--card2);border:1px solid var(--border2);border-radius:8px;padding:4px 10px;font-size:10px;color:var(--muted2);}

.stock-wrap{background:var(--card);border:1px solid var(--border2);border-radius:16px;padding:14px 16px;margin-bottom:12px;display:flex;align-items:center;justify-content:space-between;position:relative;overflow:hidden;}
.stock-wrap::before{content:'STOCK';position:absolute;right:-8px;top:50%;transform:translateY(-50%);font-family:var(--font-head);font-size:48px;font-weight:800;color:rgba(34,197,94,0.04);pointer-events:none;}
.stock-label{font-size:10px;color:var(--muted2);text-transform:uppercase;letter-spacing:1.5px;}
.stock-num{font-family:var(--font-head);font-size:36px;font-weight:800;line-height:1;color:var(--accent);}
.stock-num.low{color:var(--red);animation:blink 1s infinite;}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:0.5;}}
.stock-actions{display:flex;flex-direction:column;gap:6px;align-items:flex-end;}
.btn-stock-edit{background:var(--card2);border:1px solid var(--border2);color:var(--accent2);padding:7px 14px;border-radius:10px;font-size:11px;cursor:pointer;font-family:var(--font);font-weight:600;}
.stock-alert-tag{background:rgba(244,63,94,0.15);border:1px solid rgba(244,63,94,0.3);color:var(--red);padding:3px 10px;border-radius:20px;font-size:10px;font-weight:600;display:none;}
.stock-alert-tag.show{display:block;}

.page{display:none;animation:fadeIn 0.2s ease;}
.page.active{display:block;}
@keyframes fadeIn{from{opacity:0;transform:translateY(6px);}to{opacity:1;transform:translateY(0);}}

.profit-hero{background:linear-gradient(135deg,#0a1a0e,#0f2415);border:1px solid var(--border2);border-radius:20px;padding:22px;margin-bottom:12px;position:relative;overflow:hidden;}
.profit-hero::before{content:'';position:absolute;top:-30px;right:-30px;width:120px;height:120px;background:radial-gradient(circle,rgba(34,197,94,0.15),transparent 70%);border-radius:50%;}
.profit-label{font-size:11px;color:var(--muted2);text-transform:uppercase;letter-spacing:1.5px;margin-bottom:4px;}
.profit-amount{font-family:var(--font-head);font-size:38px;font-weight:800;color:var(--accent);line-height:1;}
.profit-sub{font-size:11px;color:var(--muted);margin-top:6px;}

.stats-row{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:12px;}
.stat-card{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:12px 14px;}
.stat-card-label{font-size:10px;color:var(--muted2);text-transform:uppercase;letter-spacing:1px;margin-bottom:3px;}
.stat-card-val{font-family:var(--font-head);font-size:20px;font-weight:800;}
.sc-revenue{color:var(--blue);}
.sc-loss{color:var(--red);}
.sc-pending{color:var(--orange);}
.sc-today{color:var(--accent2);}

.counts-row{display:grid;grid-template-columns:repeat(4,1fr);gap:6px;margin-bottom:12px;}
.count-box{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:10px 6px;text-align:center;}
.count-num{font-family:var(--font-head);font-size:18px;font-weight:800;}
.count-lbl{font-size:8px;color:var(--muted);text-transform:uppercase;letter-spacing:0.5px;margin-top:2px;}

.today-orders-box{background:var(--card);border:1px solid var(--border2);border-radius:16px;padding:14px;margin-bottom:12px;}
.section-title{font-family:var(--font-head);font-size:11px;color:var(--muted2);text-transform:uppercase;letter-spacing:1.5px;margin-bottom:10px;display:flex;align-items:center;gap:6px;}
.section-title::after{content:'';flex:1;height:1px;background:var(--border);}

.weekly-wrap{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:14px;margin-bottom:12px;}
.week-chart{display:flex;align-items:flex-end;gap:5px;height:64px;margin-top:8px;}
.wbar-col{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;}
.wbar{width:100%;border-radius:5px 5px 0 0;min-height:3px;transition:height 0.6s cubic-bezier(.34,1.56,.64,1);}
.wbar.has-data{background:linear-gradient(180deg,var(--accent),var(--accent2));}
.wbar.no-data{background:var(--card3);}
.wday{font-size:8px;color:var(--muted);}
.wamt{font-size:7px;color:var(--accent3);}

.city-chart-wrap{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:14px;margin-bottom:12px;}
canvas{display:block;}

.top-city-wrap{background:var(--card);border:1px solid var(--border2);border-radius:14px;padding:12px 16px;margin-bottom:12px;display:flex;justify-content:space-between;align-items:center;}
.top-city-name{font-family:var(--font-head);font-size:20px;font-weight:800;color:var(--accent);}

.dash-btns{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:12px;}
.dash-btn{padding:11px;border-radius:12px;font-size:12px;cursor:pointer;font-family:var(--font);font-weight:600;border:1px solid var(--border2);}
.dash-btn-pdf{background:rgba(244,63,94,0.1);color:var(--red);}
.dash-btn-backup{background:rgba(59,130,246,0.1);color:var(--blue);}
.dash-btn-restore{background:rgba(168,85,247,0.1);color:var(--purple);}
.dash-btn-clear{background:rgba(75,122,85,0.1);color:var(--muted2);}

.form-card{background:var(--card);border:1px solid var(--border);border-radius:18px;padding:16px;margin-bottom:12px;}
.form-section-title{font-family:var(--font-head);font-size:11px;color:var(--accent2);text-transform:uppercase;letter-spacing:1.5px;margin:14px 0 8px;padding-bottom:6px;border-bottom:1px solid var(--border);}
.form-section-title:first-child{margin-top:0;}
.f-label{font-size:10px;color:var(--muted2);text-transform:uppercase;letter-spacing:0.5px;margin-bottom:4px;display:block;}
input,select,textarea{width:100%;background:var(--card2);border:1px solid var(--border);padding:11px 14px;color:var(--text);border-radius:11px;margin-bottom:10px;font-family:var(--font);font-size:14px;outline:none;transition:border-color 0.2s,box-shadow 0.2s;}
input:focus,select:focus,textarea:focus{border-color:var(--accent);box-shadow:0 0 0 3px rgba(34,197,94,0.1);}
textarea{resize:vertical;min-height:55px;}
select option{background:var(--card2);}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.row2 input{margin-bottom:0;}
.emoji-row{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:10px;}
.emoji-btn{background:var(--card2);border:1px solid var(--border);border-radius:8px;padding:5px 10px;font-size:16px;cursor:pointer;}
.emoji-btn:active{background:var(--card3);}
.btn-save{width:100%;padding:15px;border:none;border-radius:13px;font-weight:700;cursor:pointer;background:linear-gradient(135deg,var(--accent),var(--accent2));color:#060a06;font-size:15px;font-family:var(--font-head);letter-spacing:0.5px;margin-top:6px;transition:opacity 0.15s,transform 0.15s;}
.btn-save:active{opacity:0.85;transform:scale(0.98);}

.dup-warn{background:rgba(249,115,22,0.1);border:1px solid rgba(249,115,22,0.3);border-radius:10px;padding:8px 12px;font-size:12px;color:var(--orange);margin-bottom:10px;display:none;}
.dup-warn.show{display:block;}

.search-wrap{background:var(--card);border:1px solid var(--border);border-radius:13px;padding:9px 14px;margin-bottom:8px;display:flex;gap:8px;align-items:center;}
.search-wrap input{margin:0;padding:6px 8px;font-size:13px;border:none;background:transparent;box-shadow:none;}
.search-wrap input:focus{box-shadow:none;border:none;}
.filter-scroll{display:flex;gap:6px;margin-bottom:8px;overflow-x:auto;padding-bottom:4px;scrollbar-width:none;}
.filter-scroll::-webkit-scrollbar{display:none;}
.fbtn{background:var(--card);border:1px solid var(--border);color:var(--muted2);padding:6px 14px;border-radius:20px;font-size:11px;cursor:pointer;white-space:nowrap;transition:all 0.15s;font-family:var(--font);font-weight:500;}
.fbtn.on{background:var(--accent);border-color:var(--accent);color:#060a06;font-weight:700;}
.date-filters{display:flex;gap:6px;margin-bottom:10px;}
.dfbtn{background:var(--card);border:1px solid var(--border);color:var(--muted2);padding:5px 12px;border-radius:20px;font-size:10px;cursor:pointer;white-space:nowrap;font-family:var(--font);}
.dfbtn.on{background:var(--card3);border-color:var(--border2);color:var(--accent2);}

.ocard{background:var(--card);border:1px solid var(--border);border-radius:16px;margin-bottom:10px;overflow:hidden;transition:border-color 0.2s;}
.ocard:active{border-color:var(--border2);}
.ocard-head{padding:13px 14px 10px;cursor:pointer;}
.ocard-row1{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:4px;}
.ocard-num{font-size:10px;color:var(--muted);font-family:var(--font-head);letter-spacing:1px;}
.ocard-name{font-weight:600;font-size:16px;margin-top:1px;}
.ocard-price{font-family:var(--font-head);font-size:17px;font-weight:800;color:var(--accent);}
.ocard-meta{font-size:11px;color:var(--muted2);display:flex;gap:8px;flex-wrap:wrap;margin:4px 0;}
.sbadge{display:inline-flex;align-items:center;padding:3px 10px;border-radius:20px;font-size:9px;font-weight:700;text-transform:uppercase;letter-spacing:0.5px;}
.s-pending{background:rgba(249,115,22,0.12);color:var(--orange);}
.s-dispatched{background:rgba(59,130,246,0.12);color:var(--blue);}
.s-delivered{background:rgba(34,197,94,0.12);color:var(--accent);}
.s-returned{background:rgba(244,63,94,0.12);color:var(--red);}
.s-cancelled{background:rgba(75,85,99,0.2);color:#9ca3af;}
.profit-tag{font-size:10px;font-weight:600;padding:2px 8px;border-radius:10px;}
.profit-pos{background:rgba(34,197,94,0.1);color:var(--accent2);}
.profit-neg{background:rgba(244,63,94,0.1);color:var(--red);}
.ocard-foot{display:flex;gap:5px;padding:9px 12px;border-top:1px solid var(--border);background:var(--card2);}
.abt{flex:1;padding:8px 4px;border-radius:9px;border:1px solid var(--border);background:transparent;color:var(--text2);font-size:10px;cursor:pointer;text-align:center;font-family:var(--font);font-weight:500;transition:all 0.15s;}
.abt:active{opacity:0.7;}
.abt-wa1{color:#25D366;border-color:rgba(37,211,102,0.3);}
.abt-wa2{color:#25D366;border-color:rgba(37,211,102,0.3);}
.abt-wa3{color:#25D366;border-color:rgba(37,211,102,0.3);}
.abt-edit{color:var(--blue);border-color:rgba(59,130,246,0.3);}
.abt-detail{color:var(--accent2);border-color:rgba(74,222,128,0.3);}
.abt-del{color:var(--red);border-color:rgba(244,63,94,0.3);}
.ocard-status-row{padding:8px 12px;border-top:1px solid var(--border);}
.status-sel{width:100%;background:var(--card3);border:1px solid var(--border2);color:var(--text);padding:7px 10px;border-radius:9px;font-size:11px;font-family:var(--font);outline:none;}

.detail-page{display:none;}
.detail-page.active{display:block;}
.back-btn{display:flex;align-items:center;gap:6px;color:var(--accent2);font-size:13px;cursor:pointer;margin-bottom:14px;font-weight:600;}
.detail-card{background:var(--card);border:1px solid var(--border2);border-radius:18px;padding:18px;margin-bottom:12px;}
.detail-title{font-family:var(--font-head);font-size:11px;color:var(--muted2);text-transform:uppercase;letter-spacing:1.5px;margin-bottom:12px;}
.detail-row{display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:1px solid var(--border);}
.detail-row:last-child{border-bottom:none;}
.d-key{font-size:12px;color:var(--muted2);}
.d-val{font-size:13px;font-weight:600;text-align:right;max-width:60%;}
.slip-btn{width:100%;padding:13px;border:none;border-radius:13px;background:linear-gradient(135deg,var(--accent),var(--accent2));color:#060a06;font-family:var(--font-head);font-size:14px;font-weight:800;cursor:pointer;margin-bottom:8px;}
.slip-btn:active{opacity:0.85;}

.cust-card{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:14px;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center;}
.cust-name{font-weight:700;font-size:15px;}
.cust-phone{font-size:11px;color:var(--muted2);margin-top:2px;}
.cust-city{font-size:10px;color:var(--muted);margin-top:2px;}
.cust-stats{text-align:right;}
.cust-orders{font-family:var(--font-head);font-size:18px;font-weight:800;color:var(--accent);}
.cust-amount{font-size:11px;color:var(--muted2);}
.cust-best{border-color:var(--border2);position:relative;}
.cust-best::before{content:'⭐ BEST';position:absolute;top:8px;right:12px;font-size:8px;color:var(--yellow);font-weight:700;letter-spacing:1px;}

.ret-summary{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:12px;}
.ret-box{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:13px;text-align:center;}
.ret-num{font-family:var(--font-head);font-size:26px;font-weight:800;color:var(--red);}
.ret-lbl{font-size:10px;color:var(--muted2);margin-top:2px;}
.reason-tag{background:rgba(244,63,94,0.08);border:1px solid rgba(244,63,94,0.2);border-radius:8px;padding:6px 10px;font-size:11px;color:#fca5a5;margin-top:6px;}

.modal-bg{position:fixed;inset:0;background:rgba(0,0,0,0.88);z-index:500;display:none;align-items:flex-end;justify-content:center;padding:0;}
.modal-bg.show{display:flex;}
.modal-box{background:var(--card);border:1px solid var(--border2);border-radius:22px 22px 0 0;padding:20px;width:100%;max-width:500px;max-height:90vh;overflow-y:auto;}
.modal-handle{width:36px;height:4px;background:var(--border2);border-radius:2px;margin:0 auto 16px;}
.modal-title{font-family:var(--font-head);font-size:14px;color:var(--accent2);margin-bottom:16px;display:flex;justify-content:space-between;align-items:center;}
.modal-close{background:none;border:none;color:var(--muted);font-size:22px;cursor:pointer;line-height:1;}
.btn-modal-save{width:100%;padding:13px;border:none;border-radius:12px;background:linear-gradient(135deg,var(--accent),var(--accent2));color:#060a06;font-family:var(--font-head);font-size:14px;font-weight:800;cursor:pointer;margin-top:4px;}

.toast{position:fixed;top:16px;left:50%;transform:translateX(-50%) translateY(-100px);background:var(--card);border:1px solid var(--border2);border-radius:14px;padding:11px 20px;z-index:1000;transition:transform 0.3s cubic-bezier(.34,1.56,.64,1);font-size:13px;white-space:nowrap;font-weight:600;box-shadow:0 8px 32px rgba(0,0,0,0.5);}
.toast.show{transform:translateX(-50%) translateY(0);}
.toast.ok{border-color:rgba(34,197,94,0.5);color:var(--accent2);}
.toast.err{border-color:rgba(244,63,94,0.5);color:var(--red);}
.toast.warn{border-color:rgba(249,115,22,0.5);color:var(--orange);}

.nav{position:fixed;bottom:0;left:0;right:0;background:rgba(6,10,6,0.96);backdrop-filter:blur(16px);border-top:1px solid var(--border);display:flex;padding:8px 8px 10px;z-index:100;gap:4px;}
.nbtn{flex:1;display:flex;flex-direction:column;align-items:center;gap:2px;color:var(--muted);background:none;border:none;cursor:pointer;padding:6px 4px;border-radius:12px;transition:all 0.2s;font-family:var(--font);}
.nbtn.on{color:var(--accent);background:rgba(34,197,94,0.08);}
.nbtn-icon{font-size:20px;line-height:1;}
.nbtn-label{font-size:8px;text-transform:uppercase;letter-spacing:0.5px;font-weight:600;}

.empty{text-align:center;padding:50px 20px;color:var(--muted);}
.empty-ico{font-size:52px;margin-bottom:10px;opacity:0.5;}

#restoreInput{display:none;}

.slip-preview{background:white;color:#111;border-radius:12px;padding:16px;margin-bottom:12px;font-family:'DM Sans',sans-serif;}
.slip-header{text-align:center;border-bottom:2px solid #111;padding-bottom:10px;margin-bottom:10px;}
.slip-brand{font-family:'Syne',sans-serif;font-size:20px;font-weight:800;}
.slip-row{display:flex;justify-content:space-between;padding:4px 0;font-size:12px;border-bottom:1px dashed #ddd;}
.slip-row:last-child{border-bottom:none;}
.slip-key{color:#666;}
.slip-val{font-weight:700;text-align:right;}
</style>
</head>
<body>

<div class="toast" id="toast"></div>
<input type="file" id="restoreInput" accept=".json" onchange="restoreData(event)">

<!-- STOCK MODAL -->
<div class="modal-bg" id="stockModal">
<div class="modal-box">
  <div class="modal-handle"></div>
  <div class="modal-title">STOCK UPDATE <button class="modal-close" onclick="closeM('stockModal')">✕</button></div>
  <label class="f-label">Nai Stock Darj Karo</label>
  <input type="number" id="newStockVal" placeholder="e.g. 100">
  <button class="btn-modal-save" onclick="doUpdateStock()">✅ UPDATE KARO</button>
</div>
</div>

<!-- EDIT MODAL -->
<div class="modal-bg" id="editModal">
<div class="modal-box">
  <div class="modal-handle"></div>
  <div class="modal-title">ORDER EDIT <button class="modal-close" onclick="closeM('editModal')">✕</button></div>
  <label class="f-label">Customer Name</label><input id="e_name" type="text">
  <label class="f-label">WhatsApp Number</label><input id="e_phone" type="text">
  <label class="f-label">Sale Price</label><input id="e_sell" type="number">
  <label class="f-label">Cost Price</label><input id="e_buy" type="number">
  <label class="f-label">Delivery Charges</label><input id="e_del" type="number">
  <label class="f-label">City</label><input id="e_city" type="text">
  <label class="f-label">Area</label><input id="e_area" type="text">
  <label class="f-label">Address</label><input id="e_addr" type="text">
  <label class="f-label">Tracking No</label><input id="e_track" type="text">
  <label class="f-label">Courier</label>
  <select id="e_courier">
    <option>Postex</option><option>TCS</option><option>Leopards</option><option>BlueEx</option><option>M&amp;P</option><option>Trax</option>
  </select>
  <label class="f-label">ETA Date</label><input id="e_eta" type="date">
  <label class="f-label">Notes</label><textarea id="e_notes"></textarea>
  <label class="f-label">Special Instructions</label><textarea id="e_special"></textarea>
  <label class="f-label">Return Reason</label><input id="e_ret" type="text">
  <button class="btn-modal-save" onclick="doSaveEdit()">💾 SAVE CHANGES</button>
</div>
</div>

<!-- SLIP MODAL -->
<div class="modal-bg" id="slipModal">
<div class="modal-box">
  <div class="modal-handle"></div>
  <div class="modal-title">SHIPPING SLIP <button class="modal-close" onclick="closeM('slipModal')">✕</button></div>
  <div class="slip-preview" id="slipPreview"></div>
  <button class="btn-modal-save" onclick="printSlip()">🖨️ PRINT SLIP</button>
</div>
</div>

<div class="container">

  <!-- HEADER -->
  <div class="header">
    <div class="brand-wrap">
      <div class="brand-dot">HS</div>
      <div>
        <div class="brand-text">HS COLLECTION</div>
        <div class="brand-sub">پرو بزنس مینجمنٹ</div>
      </div>
    </div>
    <div class="header-right">
      <div class="today-badge" id="todayBadge">📅 --</div>
    </div>
  </div>

  <!-- STOCK -->
  <div class="stock-wrap">
    <div class="stock-info">
      <div class="stock-label">Chunri Suit Stock</div>
      <div class="stock-num" id="stockNum">0</div>
    </div>
    <div class="stock-actions">
      <button class="btn-stock-edit" onclick="openM('stockModal')">✏️ Edit Stock</button>
      <div class="stock-alert-tag" id="stockAlertTag">⚠️ Low Stock!</div>
    </div>
  </div>

  <!-- DASHBOARD -->
  <div id="page-dash" class="page active">

    <div class="profit-hero">
      <div class="profit-label">Net Profit — Delivered Orders</div>
      <div class="profit-amount" id="d_profit">₨ 0</div>
      <div class="profit-sub" id="d_profit_sub">0 orders delivered</div>
    </div>

    <div class="stats-row">
      <div class="stat-card">
        <div class="stat-card-label">Revenue</div>
        <div class="stat-card-val sc-revenue" id="d_rev">₨0</div>
      </div>
      <div class="stat-card">
        <div class="stat-card-label">Return Loss</div>
        <div class="stat-card-val sc-loss" id="d_loss">₨0</div>
      </div>
      <div class="stat-card">
        <div class="stat-card-label">Pending Amount</div>
        <div class="stat-card-val sc-pending" id="d_pend">₨0</div>
      </div>
      <div class="stat-card">
        <div class="stat-card-label">Today's Orders</div>
        <div class="stat-card-val sc-today" id="d_today">0</div>
      </div>
    </div>

    <div class="counts-row">
      <div class="count-box"><div class="count-num" style="color:var(--orange)" id="c_pend">0</div><div class="count-lbl">Pending</div></div>
      <div class="count-box"><div class="count-num" style="color:var(--blue)" id="c_disp">0</div><div class="count-lbl">Dispatch</div></div>
      <div class="count-box"><div class="count-num" style="color:var(--accent)" id="c_deliv">0</div><div class="count-lbl">Deliver</div></div>
      <div class="count-box"><div class="count-num" style="color:var(--red)" id="c_ret">0</div><div class="count-lbl">Return</div></div>
    </div>

    <div class="today-orders-box">
      <div class="section-title">⚡ Aaj Ke Orders</div>
      <div id="todayOrdersList"></div>
    </div>

    <div class="weekly-wrap">
      <div class="section-title">📅 Weekly Profit</div>
      <div class="week-chart" id="weekChart"></div>
    </div>

    <div class="city-chart-wrap">
      <div class="section-title">🗺️ City-wise Orders</div>
      <canvas id="cityCanvas" height="170"></canvas>
    </div>

    <div class="top-city-wrap">
      <div>
        <div class="stat-card-label">Top Selling City</div>
        <div class="top-city-name" id="topCity">---</div>
      </div>
      <div style="font-size:28px;">🏆</div>
    </div>

    <div class="dash-btns">
      <button class="dash-btn dash-btn-pdf" onclick="exportPDF()">📄 PDF Export</button>
      <button class="dash-btn dash-btn-backup" onclick="backupData()">💾 Backup</button>
      <button class="dash-btn dash-btn-restore" onclick="document.getElementById('restoreInput').click()">📂 Restore</button>
      <button class="dash-btn dash-btn-clear" onclick="clearAll()">🗑️ Clear All</button>
    </div>
  </div>

  <!-- ADD ORDER -->
  <div id="page-add" class="page">
    <div class="form-card">
      <div class="form-section-title">👤 Customer Info</div>
      <div class="dup-warn" id="dupWarn">⚠️ Ye number pehle bhi use hua hai! Duplicate order ho sakta hai.</div>
      <label class="f-label">Customer Name *</label>
      <input type="text" id="f_name" placeholder="Customer ka poora naam">
      <label class="f-label">WhatsApp Number</label>
      <input type="text" id="f_phone" placeholder="923001234567" oninput="checkDup(this.value)">

      <div class="form-section-title">📦 Order Details</div>
      <label class="f-label">Quantity</label>
      <input type="number" id="f_qty" value="1" min="1">
      <div class="row2">
        <div><label class="f-label">Sale Price (₨)</label><input type="number" id="f_sell" placeholder="Sale"></div>
        <div><label class="f-label">Cost Price (₨)</label><input type="number" id="f_buy" placeholder="Cost"></div>
      </div>
      <label class="f-label">Delivery Charges (₨)</label>
      <input type="number" id="f_del" placeholder="0">

      <div class="form-section-title">📍 Delivery Info</div>
      <label class="f-label">City</label>
      <input type="text" id="f_city" placeholder="Shehar ka naam">
      <label class="f-label">Area</label>
      <input type="text" id="f_area" placeholder="Mohalla / Area">
      <label class="f-label">Full Address</label>
      <input type="text" id="f_addr" placeholder="Ghar ka pata">
      <label class="f-label">Tracking Number</label>
      <input type="text" id="f_track" placeholder="Tracking ID">
      <label class="f-label">Courier Company</label>
      <select id="f_courier">
        <option selected>Postex</option><option>TCS</option><option>Leopards</option><option>BlueEx</option><option>M&amp;P</option><option>Trax</option>
      </select>
      <label class="f-label">Estimated Delivery Date</label>
      <input type="date" id="f_eta">

      <div class="form-section-title">📝 Notes</div>
      <label class="f-label">Notes / Remarks</label>
      <div class="emoji-row" id="emojiRow">
        <button class="emoji-btn" onclick="addEmoji('📦')">📦</button>
        <button class="emoji-btn" onclick="addEmoji('⚡')">⚡</button>
        <button class="emoji-btn" onclick="addEmoji('🔴')">🔴</button>
        <button class="emoji-btn" onclick="addEmoji('✅')">✅</button>
        <button class="emoji-btn" onclick="addEmoji('⚠️')">⚠️</button>
        <button class="emoji-btn" onclick="addEmoji('💎')">💎</button>
      </div>
      <textarea id="f_notes" placeholder="Koi note likho..."></textarea>
      <label class="f-label">Special Instructions</label>
      <textarea id="f_special" placeholder="Customer ki khas hidayat..."></textarea>

      <button class="btn-save" onclick="saveOrder()">💾 ORDER SAVE KARO</button>
    </div>
  </div>

  <!-- HISTORY -->
  <div id="page-history" class="page">
    <div class="search-wrap">
      <span style="color:var(--muted)">🔍</span>
      <input type="text" id="searchQ" placeholder="Name, city ya status..." oninput="renderOrders()">
    </div>
    <div class="filter-scroll">
      <button class="fbtn on" onclick="setFilter('all',this)">Sab</button>
      <button class="fbtn" onclick="setFilter('pending',this)">Pending</button>
      <button class="fbtn" onclick="setFilter('dispatched',this)">Dispatched</button>
      <button class="fbtn" onclick="setFilter('delivered',this)">Delivered</button>
      <button class="fbtn" onclick="setFilter('returned',this)">Returned</button>
      <button class="fbtn" onclick="setFilter('cancelled',this)">Cancelled</button>
    </div>
    <div class="date-filters">
      <button class="dfbtn on" onclick="setDate('all',this)">Sab Din</button>
      <button class="dfbtn" onclick="setDate('today',this)">Aaj</button>
      <button class="dfbtn" onclick="setDate('week',this)">Is Hafte</button>
      <button class="dfbtn" onclick="setDate('month',this)">Is Mahine</button>
    </div>
    <div id="orderList"></div>
  </div>

  <!-- ORDER DETAIL -->
  <div id="page-detail" class="page">
    <div class="back-btn" onclick="goBack()">← Wapas Jao</div>
    <div id="detailContent"></div>
  </div>

  <!-- CUSTOMERS -->
  <div id="page-customers" class="page">
    <div class="section-title" style="margin-bottom:12px;">👥 Customers List</div>
    <div id="customersList"></div>
  </div>

  <!-- RETURNS -->
  <div id="page-returns" class="page">
    <div class="ret-summary">
      <div class="ret-box"><div class="ret-num" id="r_count">0</div><div class="ret-lbl">Total Returns</div></div>
      <div class="ret-box"><div class="ret-num" id="r_loss" style="color:var(--orange)">₨0</div><div class="ret-lbl">Total Loss</div></div>
    </div>
    <div id="returnsList"></div>
  </div>

</div>

<!-- NAV -->
<nav class="nav">
  <button class="nbtn on" onclick="showP('dash',this)"><span class="nbtn-icon">📊</span><span class="nbtn-label">Dash</span></button>
  <button class="nbtn" onclick="showP('add',this)"><span class="nbtn-icon">➕</span><span class="nbtn-label">Add</span></button>
  <button class="nbtn" onclick="showP('history',this)"><span class="nbtn-icon">📜</span><span class="nbtn-label">History</span></button>
  <button class="nbtn" onclick="showP('customers',this)"><span class="nbtn-icon">👥</span><span class="nbtn-label">Customers</span></button>
  <button class="nbtn" onclick="showP('returns',this)"><span class="nbtn-icon">↩️</span><span class="nbtn-label">Returns</span></button>
</nav>

<script>
let orders = JSON.parse(localStorage.getItem('hsc_v2_orders') || '[]');
let stock = parseInt(localStorage.getItem('hsc_v2_stock') || '50');
let orderCounter = parseInt(localStorage.getItem('hsc_v2_counter') || '1000');
let activeFilter = 'all';
let activeDateFilter = 'all';
let editId = null;
let prevPage = 'history';
let slipOrderId = null;

function save() {
  localStorage.setItem('hsc_v2_orders', JSON.stringify(orders));
  localStorage.setItem('hsc_v2_stock', stock.toString());
  localStorage.setItem('hsc_v2_counter', orderCounter.toString());
}

function toast(msg, type='ok') {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = 'toast show ' + type;
  setTimeout(() => t.className = 'toast', 2600);
}

function showP(id, btn) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nbtn').forEach(b => b.classList.remove('on'));
  document.getElementById('page-' + id).classList.add('active');
  if(btn) btn.classList.add('on');
  updateUI();
}

function goBack() {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-' + prevPage).classList.add('active');
}

function openM(id) { document.getElementById(id).classList.add('show'); }
function closeM(id) { document.getElementById(id).classList.remove('show'); }

function doUpdateStock() {
  const v = parseInt(document.getElementById('newStockVal').value);
  if(isNaN(v) || v < 0) { toast('Sahi number likho!', 'err'); return; }
  stock = v;
  save();
  closeM('stockModal');
  updateUI();
  toast('✅ Stock update ho gaya!');
}

function checkStock() {
  const tag = document.getElementById('stockAlertTag');
  const num = document.getElementById('stockNum');
  if(stock < 5) {
    tag.classList.add('show');
    num.classList.add('low');
    toast('⚠️ Stock sirf ' + stock + ' bachi! Jaldi bharain!', 'warn');
  } else {
    tag.classList.remove('show');
    num.classList.remove('low');
  }
}

function checkDup(phone) {
  const clean = phone.replace(/\D/g,'');
  const warn = document.getElementById('dupWarn');
  if(clean.length >= 7 && orders.some(o => o.phone.replace(/\D/g,'') === clean)) {
    warn.classList.add('show');
  } else {
    warn.classList.remove('show');
  }
}

function addEmoji(e) {
  const t = document.getElementById('f_notes');
  t.value += e + ' ';
  t.focus();
}

function saveOrder() {
  const name = document.getElementById('f_name').value.trim();
  if(!name) { toast('❌ Naam zaroor likho!', 'err'); return; }
  const qty = parseInt(document.getElementById('f_qty').value) || 1;
  if(stock === 0) { toast('⚠️ Stock khatam! Phir bhi save ho raha hai.', 'warn'); }
  if(stock > 0 && stock < qty) { toast('❌ Itni stock nahi!', 'err'); return; }

  orderCounter++;
  const order = {
    id: Date.now(),
    orderNo: 'HS-' + orderCounter,
    name,
    phone: document.getElementById('f_phone').value.trim(),
    qty,
    sell: parseFloat(document.getElementById('f_sell').value) || 0,
    buy: parseFloat(document.getElementById('f_buy').value) || 0,
    delivery: parseFloat(document.getElementById('f_del').value) || 0,
    city: document.getElementById('f_city').value.trim() || 'Unknown',
    area: document.getElementById('f_area').value.trim(),
    address: document.getElementById('f_addr').value.trim(),
    tracking: document.getElementById('f_track').value.trim(),
    courier: document.getElementById('f_courier').value,
    eta: document.getElementById('f_eta').value,
    notes: document.getElementById('f_notes').value.trim(),
    special: document.getElementById('f_special').value.trim(),
    returnReason: '',
    status: 'pending',
    date: new Date().toLocaleDateString('en-PK'),
    ts: Date.now()
  };

  if(stock > 0) stock -= qty;
  orders.push(order);
  save();

  ['f_name','f_phone','f_sell','f_buy','f_del','f_city','f_area','f_addr','f_track','f_eta','f_notes','f_special'].forEach(id => {
    const el = document.getElementById(id);
    if(el) el.value = '';
  });
  document.getElementById('f_qty').value = 1;
  document.getElementById('dupWarn').classList.remove('show');

  updateUI();
  toast('✅ Order save! ' + order.orderNo);

  setTimeout(() => {
    if(confirm('WhatsApp pe Confirm message bhejna hai?')) sendWA(order.id, 'confirm');
  }, 400);

  document.querySelectorAll('.nbtn')[2].click();
}

function changeStatus(id, newS) {
  const o = orders.find(x => x.id === id);
  if(!o) return;
  const old = o.status;
  if(newS === 'returned' && old !== 'returned') stock += o.qty;
  if(old === 'returned' && newS !== 'returned') stock -= o.qty;
  if(newS === 'cancelled' && old !== 'cancelled' && old !== 'returned') stock += o.qty;
  if(old === 'cancelled' && newS !== 'cancelled' && newS !== 'returned') stock -= o.qty;
  o.status = newS;
  save();
  updateUI();
  toast('✅ Status: ' + newS);
}

function deleteOrder(id) {
  if(!confirm('Ye order delete karna hai?')) return;
  const o = orders.find(x => x.id === id);
  if(o && o.status !== 'delivered' && o.status !== 'cancelled' && o.status !== 'returned') stock += o.qty;
  orders = orders.filter(x => x.id !== id);
  save();
  updateUI();
  toast('🗑️ Order delete ho gaya!', 'err');
}

function openEdit(id) {
  editId = id;
  const o = orders.find(x => x.id === id);
  if(!o) return;
  document.getElementById('e_name').value = o.name;
  document.getElementById('e_phone').value = o.phone;
  document.getElementById('e_sell').value = o.sell;
  document.getElementById('e_buy').value = o.buy;
  document.getElementById('e_del').value = o.delivery;
  document.getElementById('e_city').value = o.city;
  document.getElementById('e_area').value = o.area || '';
  document.getElementById('e_addr').value = o.address || '';
  document.getElementById('e_track').value = o.tracking;
  document.getElementById('e_courier').value = o.courier || 'Postex';
  document.getElementById('e_eta').value = o.eta || '';
  document.getElementById('e_notes').value = o.notes || '';
  document.getElementById('e_special').value = o.special || '';
  document.getElementById('e_ret').value = o.returnReason || '';
  openM('editModal');
}

function doSaveEdit() {
  const o = orders.find(x => x.id === editId);
  if(!o) return;
  o.name = document.getElementById('e_name').value;
  o.phone = document.getElementById('e_phone').value;
  o.sell = parseFloat(document.getElementById('e_sell').value) || 0;
  o.buy = parseFloat(document.getElementById('e_buy').value) || 0;
  o.delivery = parseFloat(document.getElementById('e_del').value) || 0;
  o.city = document.getElementById('e_city').value;
  o.area = document.getElementById('e_area').value;
  o.address = document.getElementById('e_addr').value;
  o.tracking = document.getElementById('e_track').value;
  o.courier = document.getElementById('e_courier').value;
  o.eta = document.getElementById('e_eta').value;
  o.notes = document.getElementById('e_notes').value;
  o.special = document.getElementById('e_special').value;
  o.returnReason = document.getElementById('e_ret').value;
  save();
  closeM('editModal');
  updateUI();
  toast('✅ Order edit ho gaya!');
}

function openDetail(id) {
  const o = orders.find(x => x.id === id);
  if(!o) return;
  prevPage = 'history';
  slipOrderId = id;
  const profit = o.sell - o.buy - o.delivery;
  document.getElementById('detailContent').innerHTML = `
    <div class="detail-card">
      <div class="detail-title">${o.orderNo} — Order Details</div>
      <div class="detail-row"><span class="d-key">Customer</span><span class="d-val">${o.name}</span></div>
      <div class="detail-row"><span class="d-key">Phone</span><span class="d-val">${o.phone||'---'}</span></div>
      <div class="detail-row"><span class="d-key">Status</span><span class="d-val"><span class="sbadge s-${o.status}">${o.status}</span></span></div>
      <div class="detail-row"><span class="d-key">Sale Price</span><span class="d-val">₨${o.sell.toLocaleString()}</span></div>
      <div class="detail-row"><span class="d-key">Cost Price</span><span class="d-val">₨${o.buy.toLocaleString()}</span></div>
      <div class="detail-row"><span class="d-key">Delivery</span><span class="d-val">₨${o.delivery.toLocaleString()}</span></div>
      <div class="detail-row"><span class="d-key">Profit/Loss</span><span class="d-val" style="color:${profit>=0?'var(--accent)':'var(--red)'}">₨${profit.toLocaleString()}</span></div>
      <div class="detail-row"><span class="d-key">Quantity</span><span class="d-val">${o.qty}</span></div>
      <div class="detail-row"><span class="d-key">City</span><span class="d-val">${o.city}</span></div>
      <div class="detail-row"><span class="d-key">Area</span><span class="d-val">${o.area||'---'}</span></div>
      <div class="detail-row"><span class="d-key">Address</span><span class="d-val">${o.address||'---'}</span></div>
      <div class="detail-row"><span class="d-key">Courier</span><span class="d-val">${o.courier||'Postex'}</span></div>
      <div class="detail-row"><span class="d-key">Tracking</span><span class="d-val">${o.tracking||'---'}</span></div>
      <div class="detail-row"><span class="d-key">ETA</span><span class="d-val">${o.eta||'---'}</span></div>
      <div class="detail-row"><span class="d-key">Order Date</span><span class="d-val">${o.date}</span></div>
      ${o.notes?`<div class="detail-row"><span class="d-key">Notes</span><span class="d-val">${o.notes}</span></div>`:''}
      ${o.special?`<div class="detail-row"><span class="d-key">Special</span><span class="d-val">${o.special}</span></div>`:''}
      ${o.returnReason?`<div class="detail-row"><span class="d-key">Return Reason</span><span class="d-val" style="color:var(--red)">${o.returnReason}</span></div>`:''}
    </div>
    <button class="slip-btn" onclick="openSlip(${o.id})">🖨️ Shipping Slip Print Karo</button>
  `;
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-detail').classList.add('active');
}

function openSlip(id) {
  const o = orders.find(x => x.id === id);
  if(!o) return;
  document.getElementById('slipPreview').innerHTML = `
    <div class="slip-header">
      <div class="slip-brand">HS COLLECTION</div>
      <div style="font-size:10px;color:#666;margin-top:2px;">Shipping Slip</div>
    </div>
    <div class="slip-row"><span class="slip-key">Order No</span><span class="slip-val">${o.orderNo}</span></div>
    <div class="slip-row"><span class="slip-key">Customer</span><span class="slip-val">${o.name}</span></div>
    <div class="slip-row"><span class="slip-key">Phone</span><span class="slip-val">${o.phone||'---'}</span></div>
    <div class="slip-row"><span class="slip-key">City</span><span class="slip-val">${o.city}</span></div>
    <div class="slip-row"><span class="slip-key">Area</span><span class="slip-val">${o.area||'---'}</span></div>
    <div class="slip-row"><span class="slip-key">Address</span><span class="slip-val">${o.address||'---'}</span></div>
    <div class="slip-row"><span class="slip-key">Item</span><span class="slip-val">Chunri Suit x${o.qty}</span></div>
    <div class="slip-row"><span class="slip-key">Amount (COD)</span><span class="slip-val">₨${o.sell.toLocaleString()}</span></div>
    <div class="slip-row"><span class="slip-key">Courier</span><span class="slip-val">${o.courier||'Postex'}</span></div>
    <div class="slip-row"><span class="slip-key">Tracking</span><span class="slip-val">${o.tracking||'---'}</span></div>
    <div class="slip-row"><span class="slip-key">ETA</span><span class="slip-val">${o.eta||'---'}</span></div>
    <div class="slip-row"><span class="slip-key">Date</span><span class="slip-val">${o.date}</span></div>
  `;
  openM('slipModal');
}

function printSlip() {
  const content = document.getElementById('slipPreview').innerHTML;
  const w = window.open('','_blank');
  w.document.write('<html><head><title>Slip</title><link href="https://fonts.googleapis.com/css2?family=Syne:wght@800&family=DM+Sans:wght@400;700&display=swap" rel="stylesheet"><style>body{font-family:\'DM Sans\',sans-serif;padding:20px;max-width:400px;margin:0 auto;}.slip-brand{font-family:\'Syne\',sans-serif;font-size:22px;font-weight:800;}.slip-header{text-align:center;border-bottom:2px solid #111;padding-bottom:10px;margin-bottom:10px;}.slip-row{display:flex;justify-content:space-between;padding:5px 0;font-size:13px;border-bottom:1px dashed #ddd;}.slip-key{color:#666;}.slip-val{font-weight:700;text-align:right;}</style></head><body>'+content+'</body></html>');
  w.document.close();
  w.print();
  closeM('slipModal');
}

function sendWA(id, type) {
  const o = orders.find(x => x.id === id);
  if(!o || !o.phone || o.phone.replace(/\D/g,'').length < 7) { toast('❌ Phone number sahi nahi!', 'err'); return; }
  const ph = o.phone.replace(/\D/g,'');
  let msg = '';
  if(type === 'confirm') {
    msg = 'السلام علیکم *'+o.name+'* صاحب! 🙏\n\n*HS Collection* میں آپ کا خیر مقدم ہے! 🌿\n\nآپ کا آرڈر کنفرم ہو گیا ہے۔\n\n🔢 آرڈر نمبر: *'+o.orderNo+'*\n📦 آئٹم: Chunri Suit × '+o.qty+'\n💰 کل رقم (COD): *₨'+o.sell.toLocaleString()+'*\n📍 شہر: '+o.city+'\n\nجلد ہی آپ کا پارسل روانہ کیا جائے گا۔ شکریہ! 💚';
  } else if(type === 'dispatch') {
    msg = 'السلام علیکم *'+o.name+'* صاحب! 📦\n\n*HS Collection* سے خوشخبری!\n\nآپ کا آرڈر روانہ کر دیا گیا ہے۔ 🚚\n\n🔢 آرڈر: *'+o.orderNo+'*\n🚚 کورئیر: '+(o.courier||'Postex')+'\n🔍 ٹریکنگ: *'+(o.tracking||'جلد ملے گی')+'*\n📅 متوقع تاریخ: '+(o.eta||'2-3 دن')+'\n💰 COD رقم: *₨'+o.sell.toLocaleString()+'*\n📍 '+o.city+(o.area?', '+o.area:'')+'\n\nملنے پر COD ادا فرمائیں۔ شکریہ! 💚';
  } else {
    msg = 'السلام علیکم *'+o.name+'* صاحب! ✅\n\n*HS Collection* — آپ کا آرڈر ڈلیور ہو گیا!\n\n🔢 آرڈر: *'+o.orderNo+'*\n📦 Chunri Suit × '+o.qty+'\n💰 ادا شدہ: *₨'+o.sell.toLocaleString()+'*\n\nہمیں خوشی ہوئی آپ کی خدمت کر کے! 🌿\n⭐ اپنے دوستوں کو بھی بتائیں۔\n\nدوبارہ آرڈر کے لیے ہم حاضر ہیں! شکریہ 🙏';
  }
  window.open('https://api.whatsapp.com/send?phone='+ph+'&text='+encodeURIComponent(msg), '_blank');
}

function setFilter(f, btn) {
  activeFilter = f;
  document.querySelectorAll('.fbtn').forEach(b => b.classList.remove('on'));
  btn.classList.add('on');
  renderOrders();
}
function setDate(d, btn) {
  activeDateFilter = d;
  document.querySelectorAll('.dfbtn').forEach(b => b.classList.remove('on'));
  btn.classList.add('on');
  renderOrders();
}

function matchDate(o) {
  const now = new Date();
  const d = new Date(o.ts);
  if(activeDateFilter === 'all') return true;
  if(activeDateFilter === 'today') return d.toDateString() === now.toDateString();
  if(activeDateFilter === 'week') return (now - d) < 7*24*60*60*1000;
  if(activeDateFilter === 'month') return d.getMonth()===now.getMonth() && d.getFullYear()===now.getFullYear();
  return true;
}

function renderOrders() {
  const q = (document.getElementById('searchQ')?.value||'').toLowerCase();
  const filtered = orders.slice().reverse().filter(o => {
    const ms = !q || o.name.toLowerCase().includes(q) || o.city.toLowerCase().includes(q) || o.status.includes(q) || (o.orderNo||'').toLowerCase().includes(q);
    const mf = activeFilter==='all' || o.status===activeFilter;
    const md = matchDate(o);
    return ms && mf && md;
  });
  const el = document.getElementById('orderList');
  if(!el) return;
  if(!filtered.length) { el.innerHTML='<div class="empty"><div class="empty-ico">📭</div>Koi order nahi mila</div>'; return; }
  el.innerHTML = filtered.map(o => {
    const p = o.sell - o.buy - o.delivery;
    return `<div class="ocard">
      <div class="ocard-head" onclick="openDetail(${o.id})">
        <div class="ocard-row1">
          <div><div class="ocard-num">${o.orderNo||''}</div><div class="ocard-name">${o.name}</div></div>
          <div class="ocard-price">₨${o.sell.toLocaleString()}</div>
        </div>
        <div class="ocard-meta"><span>📍${o.city}</span><span>📅${o.date}</span><span>×${o.qty}</span></div>
        <div style="display:flex;justify-content:space-between;align-items:center;">
          <span class="sbadge s-${o.status}">${o.status}</span>
          ${o.status==='delivered'?`<span class="profit-tag ${p>=0?'profit-pos':'profit-neg'}">P: ₨${p.toLocaleString()}</span>`:''}
        </div>
        ${o.courier||o.tracking?`<div style="font-size:10px;color:var(--muted);margin-top:4px;">🚚 ${o.courier||''} ${o.tracking?'| '+o.tracking:''}</div>`:''}
        ${o.notes?`<div style="font-size:11px;color:var(--muted2);background:var(--card2);border-radius:7px;padding:5px 9px;margin-top:5px;border-left:2px solid var(--accent)">${o.notes}</div>`:''}
      </div>
      <div class="ocard-status-row">
        <select class="status-sel" onchange="changeStatus(${o.id},this.value)">
          <option value="pending" ${o.status==='pending'?'selected':''}>⏳ Pending</option>
          <option value="dispatched" ${o.status==='dispatched'?'selected':''}>🚚 Dispatched</option>
          <option value="delivered" ${o.status==='delivered'?'selected':''}>✅ Delivered</option>
          <option value="returned" ${o.status==='returned'?'selected':''}>↩️ Returned</option>
          <option value="cancelled" ${o.status==='cancelled'?'selected':''}>❌ Cancelled</option>
        </select>
      </div>
      <div class="ocard-foot">
        <button class="abt abt-wa1" onclick="sendWA(${o.id},'confirm')">📩 Confirm</button>
        <button class="abt abt-wa2" onclick="sendWA(${o.id},'dispatch')">📤 Dispatch</button>
        <button class="abt abt-wa3" onclick="sendWA(${o.id},'delivered')">✅ Deliver</button>
        <button class="abt abt-edit" onclick="openEdit(${o.id})">✏️</button>
        <button class="abt abt-del" onclick="deleteOrder(${o.id})">🗑️</button>
      </div>
    </div>`;
  }).join('');
}

function renderTodayOrders() {
  const today = new Date().toDateString();
  const todays = orders.filter(o => new Date(o.ts).toDateString()===today).slice().reverse();
  const el = document.getElementById('todayOrdersList');
  if(!el) return;
  if(!todays.length) { el.innerHTML='<div style="color:var(--muted);font-size:12px;text-align:center;padding:10px;">Aaj koi order nahi</div>'; return; }
  el.innerHTML = todays.map(o=>`
    <div style="display:flex;justify-content:space-between;align-items:center;padding:7px 0;border-bottom:1px solid var(--border);">
      <div><div style="font-size:13px;font-weight:600;">${o.name}</div><div style="font-size:10px;color:var(--muted2);">${o.orderNo} · ${o.city}</div></div>
      <div style="text-align:right;"><div style="font-family:var(--font-head);font-size:14px;color:var(--accent);">₨${o.sell.toLocaleString()}</div><div><span class="sbadge s-${o.status}" style="font-size:8px;">${o.status}</span></div></div>
    </div>
  `).join('');
}

function renderCustomers() {
  const el = document.getElementById('customersList');
  if(!el) return;
  const map = {};
  orders.forEach(o => {
    const key = o.phone||o.name;
    if(!map[key]) map[key]={name:o.name,phone:o.phone,city:o.city,count:0,total:0};
    map[key].count++;
    map[key].total += o.sell;
  });
  const custs = Object.values(map).sort((a,b)=>b.count-a.count);
  if(!custs.length) { el.innerHTML='<div class="empty"><div class="empty-ico">👤</div>Koi customer nahi</div>'; return; }
  const bestCount = custs[0].count;
  el.innerHTML = custs.map((c,i)=>`
    <div class="cust-card ${c.count===bestCount&&i===0?'cust-best':''}">
      <div><div class="cust-name">${c.name}</div><div class="cust-phone">${c.phone||'---'}</div><div class="cust-city">📍${c.city}</div></div>
      <div class="cust-stats"><div class="cust-orders">${c.count}</div><div class="cust-amount">₨${c.total.toLocaleString()}</div><div style="font-size:9px;color:var(--muted);">orders</div></div>
    </div>`).join('');
}

function renderReturns() {
  const rets = orders.filter(o=>o.status==='returned');
  const el = document.getElementById('returnsList');
  const r_c = document.getElementById('r_count');
  const r_l = document.getElementById('r_loss');
  if(r_c) r_c.textContent = rets.length;
  const loss = rets.reduce((s,o)=>s+(o.buy+o.delivery),0);
  if(r_l) r_l.textContent = '₨'+loss.toLocaleString();
  if(!el) return;
  if(!rets.length) { el.innerHTML='<div class="empty"><div class="empty-ico">🎉</div>Koi return nahi! Mubarak!</div>'; return; }
  el.innerHTML = rets.slice().reverse().map(o=>`
    <div class="ocard">
      <div class="ocard-head">
        <div class="ocard-row1"><div><div class="ocard-num">${o.orderNo||''}</div><div class="ocard-name">${o.name}</div></div><div style="color:var(--red);font-family:var(--font-head);font-size:16px;">₨${o.sell}</div></div>
        <div class="ocard-meta"><span>📍${o.city}</span><span>📅${o.date}</span></div>
        ${o.returnReason?`<div class="reason-tag">↩️ Wajah: ${o.returnReason}</div>`:'<div class="reason-tag" style="color:var(--muted)">↩️ Wajah darj nahi</div>'}
        <div style="font-size:11px;color:var(--red);margin-top:6px;">💸 Loss: ₨${(o.buy+o.delivery).toLocaleString()}</div>
      </div>
    </div>`).join('');
}

function renderWeekly() {
  const days=['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];
  const now=new Date();
  const profits=new Array(7).fill(0);
  orders.forEach(o=>{
    if(o.status!=='delivered') return;
    const diff=Math.floor((now-new Date(o.ts))/(86400000));
    if(diff<7) profits[6-diff]+=(o.sell-o.buy-o.delivery);
  });
  const max=Math.max(...profits,1);
  const el=document.getElementById('weekChart');
  if(!el) return;
  el.innerHTML=profits.map((p,i)=>{
    const di=(now.getDay()-(6-i)+7)%7;
    return `<div class="wbar-col">
      <div class="wamt">${p>0?'₨'+Math.round(p/1000)+'k':''}</div>
      <div class="wbar ${p>0?'has-data':'no-data'}" style="height:${Math.max((p/max)*52,3)}px"></div>
      <div class="wday">${days[di]}</div>
    </div>`;
  }).join('');
}

function renderCityPie() {
  const cities={};
  orders.forEach(o=>{cities[o.city]=(cities[o.city]||0)+1;});
  const labels=Object.keys(cities);
  const data=Object.values(cities);
  const canvas=document.getElementById('cityCanvas');
  if(!canvas) return;
  const W=canvas.parentElement.offsetWidth-28||280;
  canvas.width=W; canvas.height=170;
  const ctx=canvas.getContext('2d');
  ctx.clearRect(0,0,W,170);
  if(!labels.length){ctx.fillStyle='#4b7a55';ctx.font='12px DM Sans';ctx.textAlign='center';ctx.fillText('Data nahi',W/2,85);return;}
  const colors=['#22c55e','#3b82f6','#f97316','#a855f7','#f43f5e','#eab308','#06b6d4','#ec4899'];
  const total=data.reduce((a,b)=>a+b,0);
  const cx=W/2,cy=75,r=62;
  let start=-Math.PI/2;
  data.forEach((v,i)=>{
    const sl=(v/total)*2*Math.PI;
    ctx.beginPath();ctx.moveTo(cx,cy);ctx.arc(cx,cy,r,start,start+sl);ctx.closePath();
    ctx.fillStyle=colors[i%colors.length];ctx.fill();
    ctx.strokeStyle='#060a06';ctx.lineWidth=2;ctx.stroke();
    start+=sl;
  });
  ctx.beginPath();ctx.arc(cx,cy,30,0,2*Math.PI);ctx.fillStyle='#060a06';ctx.fill();
  ctx.fillStyle='#22c55e';ctx.font='bold 11px Syne';ctx.textAlign='center';ctx.fillText(orders.length,cx,cy+4);
  const perRow=3,legY=143;
  labels.slice(0,6).forEach((l,i)=>{
    const col=i%perRow,row=Math.floor(i/perRow);
    const x=(W/perRow)*col+8,y=legY+row*16;
    ctx.fillStyle=colors[i%colors.length];ctx.fillRect(x,y-8,9,9);
    ctx.fillStyle='#6aaf78';ctx.font='9px DM Sans';ctx.textAlign='left';
    ctx.fillText(l.substring(0,9)+' ('+data[i]+')',x+12,y);
  });
}

function updateDash() {
  let profit=0,revenue=0,loss=0,pendAmt=0,delivered=0,pending=0,dispatched=0,returned=0,cancelled=0;
  const today=new Date().toDateString();
  let todayCount=0;
  const cities={};
  orders.forEach(o=>{
    if(o.status==='delivered'){profit+=(o.sell-o.buy-o.delivery);revenue+=o.sell;delivered++;}
    if(o.status==='returned'){loss+=(o.buy+o.delivery);returned++;}
    if(o.status==='pending'){pending++;pendAmt+=o.sell;}
    if(o.status==='dispatched'){dispatched++;pendAmt+=o.sell;}
    if(o.status==='cancelled')cancelled++;
    if(new Date(o.ts).toDateString()===today) todayCount++;
    cities[o.city]=(cities[o.city]||0)+1;
  });
  const el=(id,v)=>{const e=document.getElementById(id);if(e)e.textContent=v;};
  el('d_profit','₨ '+profit.toLocaleString());
  el('d_profit_sub',delivered+' orders delivered');
  el('d_rev','₨'+revenue.toLocaleString());
  el('d_loss','₨'+loss.toLocaleString());
  el('d_pend','₨'+pendAmt.toLocaleString());
  el('d_today',todayCount);
  el('c_pend',pending);el('c_disp',dispatched);el('c_deliv',delivered);el('c_ret',returned);
  const top=Object.keys(cities).reduce((a,b)=>cities[a]>cities[b]?a:b,'---');
  el('topCity',top);
  renderTodayOrders();
  renderWeekly();
  setTimeout(renderCityPie,50);
}

function setTodayDate() {
  const opts={weekday:'short',day:'numeric',month:'short'};
  const str=new Date().toLocaleDateString('en-PK',opts);
  const el=document.getElementById('todayBadge');
  if(el) el.textContent='📅 '+str;
}

function exportPDF() {
  try {
    const {jsPDF}=window.jspdf;
    const doc=new jsPDF();
    doc.setFont('helvetica','bold');doc.setFontSize(22);
    doc.setTextColor(34,197,94);doc.text('HS COLLECTION',105,18,{align:'center'});
    doc.setFontSize(10);doc.setTextColor(107,130,184);
    doc.text('Business Report — '+new Date().toLocaleDateString('en-PK'),105,26,{align:'center'});
    doc.line(14,30,196,30);
    let delivered=0,revenue=0,profit=0,returned=0;
    orders.forEach(o=>{if(o.status==='delivered'){delivered++;revenue+=o.sell;profit+=(o.sell-o.buy-o.delivery);}if(o.status==='returned')returned++;});
    doc.setTextColor(0);doc.setFontSize(11);doc.setFont('helvetica','bold');doc.text('SUMMARY',14,40);
    doc.setFont('helvetica','normal');doc.setFontSize(10);
    const rows=[['Total Orders',orders.length],['Delivered',delivered],['Returned',returned],['Revenue','Rs. '+revenue.toLocaleString()],['Net Profit','Rs. '+profit.toLocaleString()],['Stock Left',stock]];
    rows.forEach((r,i)=>doc.text(r[0]+': '+r[1],14,50+i*8));
    doc.setFont('helvetica','bold');doc.text('ORDER LIST',14,106);doc.line(14,109,196,109);
    let y=116;
    orders.slice(-40).forEach((o,i)=>{
      if(y>270){doc.addPage();y=20;}
      doc.setFont('helvetica','normal');doc.setFontSize(8.5);
      doc.text((o.orderNo||('HS-'+(1001+i)))+'  '+o.name+'  |  '+o.city+'  |  '+o.status.toUpperCase()+'  |  Rs.'+o.sell+'  |  '+o.date,14,y);
      y+=7;
    });
    doc.save('HS_Collection_Report.pdf');
    toast('✅ PDF download ho rahi hai!');
  } catch(e){toast('❌ PDF error!','err');}
}

function backupData() {
  const data={orders,stock,orderCounter,date:new Date().toISOString()};
  const blob=new Blob([JSON.stringify(data,null,2)],{type:'application/json'});
  const a=document.createElement('a');
  a.href=URL.createObjectURL(blob);
  a.download='HS_Collection_Backup_'+new Date().toLocaleDateString('en-PK').replace(/\//g,'-')+'.json';
  a.click();
  toast('✅ Backup file download ho gayi!');
}

function restoreData(e) {
  const file=e.target.files[0];
  if(!file) return;
  const reader=new FileReader();
  reader.onload=ev=>{
    try {
      const data=JSON.parse(ev.target.result);
      if(!data.orders) throw new Error('Invalid');
      if(!confirm('Restore karne se purana data replace ho jayega. Jaari rakhein?')) return;
      orders=data.orders;
      stock=data.stock||50;
      orderCounter=data.orderCounter||1000;
      save();
      updateUI();
      toast('✅ Data restore ho gaya!');
    } catch(err){toast('❌ Galat file!','err');}
  };
  reader.readAsText(file);
  e.target.value='';
}

function clearAll() {
  if(!confirm('Sab data delete ho jayega!')) return;
  if(!confirm('Pakka? Ye undo nahi hoga!')) return;
  orders=[];stock=50;orderCounter=1000;
  save();updateUI();
  toast('🗑️ Data clear ho gaya!','err');
}

function updateUI() {
  document.getElementById('stockNum').textContent = stock;
  checkStock();
  updateDash();
  renderOrders();
  renderReturns();
  renderCustomers();
}

setTodayDate();
updateUI();
</script>
</body>
</html>
