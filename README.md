# <!DOCTYPE html>
<html lang="ar" dir="rtl" id="htmlRoot">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>شركة المستقبل الأفضل للمقاولات</title>
<meta name="description" content="Daily entry form.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;900&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
<style>
  :root{
    --bg:#E8F0F8; --panel:#ffffff; --dark:#16213E; --steel:#3E5875;
    --accent:#7D2438; --gold:#3E6FA6; --red:#C0392B; --amber:#C98A1A; --green:#2F8A58; --line:#CFDFEE;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{background:var(--bg);font-family:'Tajawal',sans-serif;color:var(--dark);min-height:100vh;-webkit-tap-highlight-color:transparent;}
  .mono{font-family:'JetBrains Mono',monospace;}

  header{background:linear-gradient(155deg, var(--dark) 0%, #1C2C50 60%, #223462 100%);color:#fff;padding:22px 20px 26px;position:relative;overflow:hidden;box-shadow:0 4px 20px rgba(0,0,0,.25);}
  header::after{content:"";position:absolute;inset:auto 0 0 0;height:6px;background:repeating-linear-gradient(-45deg, var(--accent) 0 18px, var(--gold) 18px 36px);}
  .head-row{display:flex;justify-content:space-between;align-items:flex-start;gap:10px;}
  header h1{margin:0;font-size:21px;font-weight:900;}
  header p{margin:6px 0 0;color:#B9C2C9;font-size:13px;}
  .lang-btn{background:#1F2E52;border:1px solid #35486B;color:#cfd6db;font-family:'Tajawal',sans-serif;font-weight:700;font-size:13px;border-radius:8px;padding:8px 12px;cursor:pointer;white-space:nowrap;}
  .role-switch{display:flex;gap:8px;margin-top:16px;flex-wrap:wrap;}
  .role-switch button{flex:1;min-width:110px;padding:10px 8px;border-radius:10px;border:1px solid #35486B;background:#1F2E52;color:#cfd6db;font-family:'Tajawal',sans-serif;font-weight:700;font-size:14px;cursor:pointer;}
  .role-switch button.active{background:var(--accent);border-color:var(--accent);color:#fff;}

  main{max-width:640px;margin:0 auto;padding:18px 16px 60px;}
  .hint{font-size:13px;color:var(--steel);margin:2px 4px 16px;}

  .dept-group{margin-bottom:18px;}
  .dept-label{font-size:12px;font-weight:700;color:var(--steel);margin:0 0 8px 4px;letter-spacing:.3px;}
  .name-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
  .name-card{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:14px 12px;text-align:center;cursor:pointer;font-weight:700;font-size:15px;position:relative;transition:transform .08s, box-shadow .15s;box-shadow:0 2px 8px rgba(23,29,38,.06);}
  html[data-theme="dark"] .name-card{box-shadow:0 2px 8px rgba(0,0,0,.3);}
  .name-card:active{transform:scale(.97);}
  .status-dot{position:absolute;top:8px;inset-inline-start:8px;width:10px;height:10px;border-radius:50%;}
  .dot-red{background:var(--red);} .dot-amber{background:var(--amber);} .dot-green{background:var(--green);} .dot-none{background:#c9c2b2;}

  .tag{background:var(--panel);border-radius:14px;padding:16px 16px 14px;margin-bottom:14px;position:relative;border:2px solid var(--line);box-shadow:0 3px 14px rgba(23,29,38,.06);}
  html[data-theme="dark"] .tag{box-shadow:0 3px 14px rgba(0,0,0,.3);}
  .tag::before{content:"";position:absolute;top:-11px;inset-inline-end:22px;width:22px;height:22px;background:var(--panel);border:2px solid var(--line);border-radius:50%;}
  .tag::after{content:"";position:absolute;top:-4px;inset-inline-end:31px;width:4px;height:4px;background:var(--bg);border-radius:50%;box-shadow:0 0 0 1px var(--line);}
  .tag.red{border-color:var(--red);} .tag.amber{border-color:var(--amber);} .tag.green{border-color:var(--green);}
  .tag-top{display:flex;justify-content:space-between;align-items:flex-start;gap:10px;}
  .tag-name{font-size:17px;font-weight:900;}
  .tag-dept{font-size:12px;color:var(--steel);margin-top:2px;}
  .tag-badge{font-size:11px;font-weight:700;padding:4px 9px;border-radius:20px;color:#fff;white-space:nowrap;}
  .badge-red{background:var(--red);} .badge-amber{background:var(--amber);} .badge-green{background:var(--green);} .badge-none{background:#a39c8c;}
  .tag-task{font-size:13.5px;color:#333;margin-top:10px;line-height:1.5;min-height:18px;}
  .tag-task.empty{color:#999;font-style:italic;}
  .bar-wrap{margin-top:10px;background:#EFEBE2;border-radius:20px;height:9px;overflow:hidden;}
  .bar-fill{height:100%;border-radius:20px;transition:width .2s;}
  .tag-foot{display:flex;justify-content:space-between;font-size:11px;color:var(--steel);margin-top:6px;}
  .hist-btn{margin-top:10px;width:100%;background:none;border:1px solid var(--line);border-radius:8px;padding:8px;font-family:'Tajawal',sans-serif;font-weight:700;font-size:12.5px;color:var(--steel);cursor:pointer;}
  .tag-phone{display:inline-flex;align-items:center;gap:4px;font-size:12.5px;font-weight:700;color:var(--accent);text-decoration:none;margin-top:6px;}
  .tag-timer{font-size:11.5px;color:#8a5c0d;font-weight:700;margin-top:6px;display:flex;align-items:center;gap:4px;}
  .sub-task-note{font-size:12.5px;background:rgba(63,143,95,.08);border:1px solid var(--green);border-radius:8px;padding:8px 10px;margin-top:8px;color:var(--dark);}
  select#f-category, select#nt-name-select, select#f-dept-select{width:100%;border:1px solid var(--line);border-radius:10px;padding:11px 12px;font-family:'Tajawal',sans-serif;font-size:14.5px;background:#fff;color:var(--dark);}
  .timer-box{background:var(--panel);border:1px solid var(--line);border-radius:12px;padding:16px;margin-top:14px;text-align:center;}
  .timer-clock{font-family:'JetBrains Mono',monospace;font-size:34px;font-weight:700;letter-spacing:1px;margin-bottom:12px;color:var(--dark);}
  .timer-btns{display:flex;gap:8px;}
  .timer-btns button{flex:1;padding:11px 6px;border-radius:10px;border:none;font-family:'Tajawal',sans-serif;font-weight:700;font-size:13.5px;cursor:pointer;color:#fff;}
  .timer-btns button:disabled{opacity:.35;cursor:default;}
  .tb-start{background:var(--green);}
  .tb-pause{background:var(--amber);}
  .tb-stop{background:var(--red);}
  .active-task-box{background:rgba(63,143,95,.08);border:2px solid var(--green);border-radius:12px;padding:14px;margin-top:10px;position:relative;}
  .active-task-name{font-weight:900;font-size:15px;}
  .active-task-loc{font-size:12px;color:var(--steel);margin-top:2px;}
  .active-task-clock{font-family:'JetBrains Mono',monospace;font-size:30px;font-weight:700;text-align:center;margin:10px 0 12px;}
  .active-task-finish{width:100%;background:var(--red);color:#fff;border:none;border-radius:10px;padding:11px;font-family:'Tajawal',sans-serif;font-weight:700;font-size:13.5px;cursor:pointer;}
  .new-task-btn{display:block;width:100%;padding:13px;border-radius:10px;border:2px dashed var(--accent);background:none;color:var(--accent);font-family:'Tajawal',sans-serif;font-weight:700;font-size:14px;cursor:pointer;margin-top:10px;}
  .new-task-form{background:var(--panel);border:1px solid var(--line);border-radius:12px;padding:14px;margin-top:10px;display:none;}
  .new-task-form.open{display:block;}
  .photo-btn{display:inline-flex;align-items:center;gap:6px;background:var(--bg);border:1px solid var(--line);border-radius:20px;padding:8px 14px;font-family:'Tajawal',sans-serif;font-weight:700;font-size:12.5px;color:var(--dark);cursor:pointer;margin-top:8px;}
  .photo-popup-overlay{position:fixed;inset:0;background:rgba(20,24,27,.55);display:flex;align-items:center;justify-content:center;z-index:60;padding:20px;}
  .photo-popup{background:var(--panel);border-radius:16px;padding:18px;max-width:340px;width:100%;}
  .photo-popup h3{margin:0 0 12px;font-size:15px;font-weight:900;color:var(--dark);}
  .photo-thumbs{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:14px;}
  .photo-thumb{position:relative;width:72px;height:72px;border-radius:8px;overflow:hidden;border:1px solid var(--line);}
  .photo-thumb img{width:100%;height:100%;object-fit:cover;display:block;cursor:pointer;}
  .photo-thumb .pt-del{position:absolute;top:2px;inset-inline-end:2px;background:rgba(0,0,0,.65);color:#fff;border:none;border-radius:50%;width:18px;height:18px;font-size:11px;cursor:pointer;line-height:1;padding:0;}
  .photo-add-btn{width:72px;height:72px;border-radius:8px;border:2px dashed var(--line);background:none;display:flex;align-items:center;justify-content:center;font-size:24px;color:var(--steel);cursor:pointer;}
  .sr-photos{display:flex;gap:4px;margin-top:6px;flex-wrap:wrap;}
  .sr-photos .sr-photo-wrap{position:relative;width:38px;height:38px;}
  .sr-photos .sr-photo-del{position:absolute;top:-6px;inset-inline-end:-6px;background:var(--red);color:#fff;border:none;border-radius:50%;width:17px;height:17px;font-size:10px;cursor:pointer;line-height:1;padding:0;z-index:1;}
  .sr-photos img{width:38px;height:38px;border-radius:6px;object-fit:cover;cursor:pointer;transition:transform .12s;display:block;}
  .sr-photos img:active{transform:scale(0.92);}
  .photo-lightbox-overlay{position:fixed;inset:0;background:rgba(8,10,12,.94);display:flex;align-items:center;justify-content:center;z-index:200;padding:16px;overflow:auto;animation:lightboxFadeIn .18s ease-out;}
  @keyframes lightboxFadeIn{from{opacity:0;}to{opacity:1;}}
  .photo-lightbox-overlay img{max-width:100%;max-height:90vh;border-radius:12px;object-fit:contain;cursor:zoom-in;transition:transform .25s ease;box-shadow:0 8px 40px rgba(0,0,0,.5);touch-action:pinch-zoom;}
  .photo-lightbox-overlay img.zoomed{max-width:none;max-height:none;width:auto;height:auto;transform:scale(2.2);cursor:zoom-out;}
  .photo-lightbox-hint{position:absolute;bottom:22px;left:0;right:0;text-align:center;color:rgba(255,255,255,.65);font-family:'Tajawal',sans-serif;font-size:12px;pointer-events:none;}
  .photo-lightbox-close{position:absolute;top:18px;inset-inline-end:18px;width:44px;height:44px;border-radius:50%;background:rgba(255,255,255,.15);border:none;color:#fff;font-size:24px;cursor:pointer;display:flex;align-items:center;justify-content:center;z-index:2;}
  .session-log{margin-top:12px;}
  .session-row{display:flex;justify-content:space-between;align-items:center;background:var(--panel);border:1px solid var(--line);border-radius:8px;padding:8px 12px;margin-top:6px;font-size:12.5px;gap:8px;}
  .session-row .sr-name{font-weight:700;}
  .session-row .sr-loc{color:var(--steel);font-size:11px;}
  .session-row .sr-dur{font-family:'JetBrains Mono',monospace;color:var(--steel);white-space:nowrap;}
  .session-del-btn{background:none;border:none;color:var(--red);font-size:11.5px;font-weight:700;cursor:pointer;padding:0;white-space:nowrap;}
  .active-task-del{position:absolute;top:10px;inset-inline-end:10px;background:none;border:none;color:var(--red);font-size:16px;cursor:pointer;padding:2px 6px;line-height:1;}
  .day-del-btn{background:none;border:none;color:var(--red);font-size:12px;font-weight:700;cursor:pointer;margin-top:8px;padding:0;font-family:'Tajawal',sans-serif;}

  .sheet-overlay{position:fixed;inset:0;background:rgba(20,24,27,.5);display:flex;align-items:flex-end;z-index:50;}
  .sheet{background:var(--bg);width:100%;max-width:640px;margin:0 auto;border-radius:18px 18px 0 0;padding:20px 18px 26px;max-height:88vh;overflow-y:auto;}
  .sheet h2{margin:0 0 2px;font-size:19px;font-weight:900;}
  .sheet .sub{font-size:13px;color:var(--steel);margin-bottom:16px;}
  label.field-label{display:block;font-size:13px;font-weight:700;margin:14px 0 6px;color:var(--dark);}
  textarea, input[type=text], input[type=password]{width:100%;border:1px solid var(--line);border-radius:10px;padding:11px 12px;font-family:'Tajawal',sans-serif;font-size:14.5px;background:#fff;resize:vertical;}
  input[type=range]{width:100%;accent-color:var(--accent);}
  .pct-row{display:flex;align-items:center;gap:10px;}
  .pct-num{font-family:'JetBrains Mono',monospace;font-weight:700;font-size:18px;min-width:48px;text-align:center;}
  .status-btns{display:flex;gap:8px;margin-top:2px;}
  .status-btns button{flex:1;padding:12px 6px;border-radius:10px;border:2px solid var(--line);background:#fff;font-family:'Tajawal',sans-serif;font-weight:700;font-size:13px;cursor:pointer;color:var(--dark);}
  .status-btns button.sel-red{border-color:var(--red);background:#FCEBE8;color:var(--red);}
  .status-btns button.sel-amber{border-color:var(--amber);background:#FDF3E1;color:#8a5c0d;}
  .status-btns button.sel-green{border-color:var(--green);background:#E9F5EE;color:var(--green);}
  .sheet-actions{display:flex;gap:10px;margin-top:22px;}
  .btn-save{flex:2;background:var(--accent);color:#fff;border:none;border-radius:10px;padding:14px;font-family:'Tajawal',sans-serif;font-weight:900;font-size:15px;cursor:pointer;}
  .btn-cancel{flex:1;background:none;border:1px solid var(--line);border-radius:10px;color:var(--steel);font-family:'Tajawal',sans-serif;font-weight:700;cursor:pointer;}

  .date-nav{display:flex;align-items:center;justify-content:space-between;gap:10px;background:var(--panel);border:1px solid var(--line);border-radius:12px;padding:8px 10px;margin-bottom:12px;}
  .date-nav-btn{width:36px;height:36px;border-radius:50%;border:1px solid var(--line);background:var(--bg);color:var(--dark);font-size:18px;font-weight:900;cursor:pointer;display:flex;align-items:center;justify-content:center;}
  .date-nav-btn:disabled{opacity:.35;cursor:default;}
  .date-nav-label{flex:1;text-align:center;font-weight:700;font-size:14px;}
  .date-nav-today{display:inline-block;margin-inline-start:6px;background:var(--accent);color:#fff;font-size:10.5px;font-weight:700;border-radius:20px;padding:2px 9px;}
  .date-nav-readonly{text-align:center;font-size:12px;color:var(--steel);background:#EFEBE2;border-radius:8px;padding:7px;margin-bottom:14px;}
  html[data-theme="dark"] .date-nav-readonly{background:#1F2E52;}
  .filters{display:flex;gap:8px;overflow-x:auto;padding-bottom:4px;margin-bottom:14px;}
  .filters button{white-space:nowrap;padding:8px 14px;border-radius:20px;border:1px solid var(--line);background:#fff;font-family:'Tajawal',sans-serif;font-size:13px;font-weight:700;color:var(--steel);cursor:pointer;}
  .filters button.active{background:var(--dark);color:#fff;border-color:var(--dark);}

  .summary-strip{display:flex;gap:8px;margin-bottom:16px;}
  .summary-strip div{flex:1;background:var(--panel);border:1px solid var(--line);border-radius:10px;padding:10px 8px;text-align:center;}
  .summary-strip .num{font-family:'JetBrains Mono',monospace;font-weight:700;font-size:19px;display:block;}
  .summary-strip .lbl{font-size:11px;color:var(--steel);}

  .add-worker-btn{display:block;width:100%;padding:13px;border-radius:10px;border:2px dashed var(--line);background:none;color:var(--steel);font-family:'Tajawal',sans-serif;font-weight:700;font-size:14px;cursor:pointer;margin-top:6px;}
  .delete-worker-btn{display:block;width:100%;padding:12px;border-radius:10px;border:1px solid var(--red);background:none;color:var(--red);font-family:'Tajawal',sans-serif;font-weight:700;font-size:13.5px;cursor:pointer;margin-top:18px;}
  .loading{text-align:center;padding:40px 0;color:var(--steel);}

  .pin-wrap{text-align:center;padding:30px 10px;}
  .pin-lock{font-size:38px;margin-bottom:10px;}
  .pin-wrap input{max-width:180px;margin:14px auto;text-align:center;letter-spacing:6px;font-size:20px;font-family:'JetBrains Mono',monospace;}
  .pin-err{color:var(--red);font-size:13px;margin-top:8px;min-height:18px;}
  .pin-submit{background:var(--accent);color:#fff;border:none;border-radius:10px;padding:12px 28px;font-family:'Tajawal',sans-serif;font-weight:900;font-size:15px;cursor:pointer;margin-top:6px;}

  .daily-log-section{margin-bottom:22px;}
  .daily-log-section h2{font-size:16px;font-weight:900;margin:0 0 12px;}
  .log-form{background:var(--panel);border:1px solid var(--line);border-radius:12px;padding:14px;display:flex;flex-direction:column;gap:10px;margin-bottom:14px;}
  .log-form input[type=date]{border:1px solid var(--line);border-radius:10px;padding:11px 12px;font-family:'Tajawal',sans-serif;font-size:14.5px;background:#fff;color:var(--dark);}
  .log-form #add-log-btn{background:var(--accent);color:#fff;border:none;border-radius:10px;padding:12px;font-family:'Tajawal',sans-serif;font-weight:900;font-size:14.5px;cursor:pointer;}
  .logs-grid{display:flex;flex-direction:column;gap:10px;}
  .log-card{background:var(--panel);border:1px solid var(--line);border-inline-start:4px solid var(--accent);border-radius:10px;padding:12px 14px;}
  .log-card .log-top{display:flex;justify-content:space-between;align-items:center;gap:8px;}
  .log-card .log-manager{font-weight:700;font-size:14.5px;}
  .log-card .log-date{font-size:11.5px;color:var(--steel);font-family:'JetBrains Mono',monospace;}
  .log-card .log-details{font-size:13.5px;color:#333;margin-top:6px;line-height:1.5;white-space:pre-wrap;}
  .log-card .log-del{background:none;border:none;color:var(--red);font-size:12px;cursor:pointer;margin-top:8px;padding:0;font-family:'Tajawal',sans-serif;font-weight:700;}
  .logs-empty{color:var(--steel);font-size:13px;text-align:center;padding:14px 0;}

  #toast-container{position:fixed;bottom:18px;left:0;right:0;display:flex;flex-direction:column;align-items:center;gap:8px;z-index:100;pointer-events:none;}
  .toast{background:var(--dark);color:#fff;font-family:'Tajawal',sans-serif;font-size:13.5px;font-weight:700;padding:10px 18px;border-radius:20px;box-shadow:0 4px 14px rgba(0,0,0,.2);opacity:0;transform:translateY(8px);transition:opacity .2s, transform .2s;}
  .toast.show{opacity:1;transform:translateY(0);}

  .theme-btn{background:#1F2E52;border:1px solid #35486B;color:#cfd6db;font-size:16px;border-radius:8px;padding:8px 11px;cursor:pointer;line-height:1;}
  .sync-badge{font-size:12px;font-weight:700;text-align:center;padding:9px 10px;border-radius:10px;margin-bottom:12px;border:1px solid var(--line);}
  .sync-badge.sb-checking{color:var(--steel);background:var(--panel);}
  .sync-badge.sb-connected{color:var(--green);background:rgba(63,143,95,.08);border-color:var(--green);}
  .sync-badge.sb-error{color:var(--red);background:rgba(180,56,44,.08);border-color:var(--red);}
  .sort-row{display:flex;align-items:center;gap:8px;margin-bottom:12px;}
  .sort-row label{font-size:12.5px;color:var(--steel);white-space:nowrap;font-weight:700;}
  select.sort-select{flex:1;border:1px solid var(--line);border-radius:10px;padding:9px 10px;font-family:'Tajawal',sans-serif;font-size:13.5px;background:#fff;color:var(--dark);}
  html[data-theme="dark"] select.sort-select{background:#1F2E52;color:#EDEAE3;border-color:#35486B;}
  .stale-card{background:var(--panel);border:1px solid var(--amber);border-inline-start:4px solid var(--amber);border-radius:10px;padding:10px 12px;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center;gap:8px;}
  .stale-card .st-name{font-weight:700;font-size:14px;}
  .stale-card .st-dept{font-size:11.5px;color:var(--steel);}
  .stale-card .st-days{font-size:11.5px;color:#8a5c0d;font-weight:700;white-space:nowrap;}
  .hours-card{background:var(--panel);border:1px solid var(--line);border-radius:10px;padding:12px 14px;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center;gap:10px;}
  .hours-card .hc-name{font-weight:700;font-size:14px;}
  .hours-card .hc-dept{font-size:11.5px;color:var(--steel);}
  .hours-card .hc-total{font-family:'JetBrains Mono',monospace;font-weight:700;font-size:16px;color:var(--accent);white-space:nowrap;}
  .export-btn{display:block;width:100%;padding:12px;border-radius:10px;border:1px solid var(--line);background:var(--panel);color:var(--dark);font-family:'Tajawal',sans-serif;font-weight:700;font-size:13.5px;cursor:pointer;margin-top:10px;}
  .search-box{width:100%;border:1px solid var(--line);border-radius:10px;padding:11px 12px;font-family:'Tajawal',sans-serif;font-size:14.5px;background:#fff;margin-bottom:12px;}

  /* Report page: period toggle, charts, expenses, notes — polished/premium styling */
  .period-toggle{display:flex;gap:8px;background:var(--panel);border:1px solid var(--line);border-radius:12px;padding:5px;margin-bottom:16px;}
  .period-toggle button{flex:1;padding:9px 8px;border-radius:9px;border:none;background:none;font-family:'Tajawal',sans-serif;font-weight:700;font-size:13.5px;color:var(--steel);cursor:pointer;}
  .period-toggle button.active{background:var(--accent);color:#fff;box-shadow:0 2px 8px rgba(232,89,12,.35);}
  .print-btn{display:block;width:100%;padding:12px;border-radius:10px;border:none;background:var(--dark);color:#fff;font-family:'Tajawal',sans-serif;font-weight:700;font-size:13.5px;cursor:pointer;margin-bottom:16px;}
  .report-card{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:18px;margin-bottom:16px;box-shadow:0 3px 12px rgba(20,24,27,.05);}
  html[data-theme="dark"] .report-card{box-shadow:0 3px 12px rgba(0,0,0,.25);}
  .report-card h3{margin:0 0 4px;font-size:15.5px;font-weight:900;}
  .report-card .hint{margin:0 0 14px;}
  .chart-row{display:flex;align-items:center;gap:10px;margin-bottom:10px;}
  .chart-row:last-child{margin-bottom:0;}
  .chart-label{width:34%;min-width:80px;font-size:12.5px;font-weight:700;color:var(--dark);overflow:hidden;text-overflow:ellipsis;white-space:nowrap;}
  .chart-bar-wrap{flex:1;background:var(--bg);border-radius:20px;height:14px;overflow:hidden;}
  .chart-bar-fill{height:100%;border-radius:20px;background:var(--accent);transition:width .3s;}
  .chart-value{font-family:'JetBrains Mono',monospace;font-weight:700;font-size:12px;color:var(--steel);min-width:38px;text-align:end;white-space:nowrap;}
  .trend-svg-wrap{background:var(--bg);border-radius:10px;padding:10px 6px 4px;}
  .expense-form{display:flex;flex-direction:column;gap:10px;margin-bottom:14px;}
  .expense-row{display:flex;gap:8px;}
  .expense-row > *{flex:1;}
  .expense-card{background:var(--bg);border-radius:10px;padding:10px 12px;margin-bottom:8px;}
  .expense-card .exp-top{display:flex;justify-content:space-between;align-items:center;gap:8px;}
  .expense-card .exp-amount{font-family:'JetBrains Mono',monospace;font-weight:900;font-size:15px;color:var(--red);}
  .expense-card .exp-meta{font-size:11.5px;color:var(--steel);margin-top:2px;}
  .expense-card .exp-note{font-size:12.5px;margin-top:4px;color:var(--dark);}
  .expense-total-strip{display:flex;justify-content:space-between;align-items:center;background:rgba(180,56,44,.08);border:1px solid var(--red);border-radius:10px;padding:12px 14px;margin-bottom:14px;}
  .expense-total-strip .et-label{font-size:12.5px;font-weight:700;color:var(--red);}
  .expense-total-strip .et-num{font-family:'JetBrains Mono',monospace;font-weight:900;font-size:19px;color:var(--red);}
  .notes-list{display:flex;flex-direction:column;gap:8px;margin-top:10px;}
  .note-card{background:var(--bg);border-inline-start:3px solid var(--accent);border-radius:8px;padding:10px 12px;}
  .note-card .note-date{font-size:11px;color:var(--steel);font-family:'JetBrains Mono',monospace;}
  .note-card .note-text{font-size:13px;margin-top:3px;color:var(--dark);}
  select.expense-select, input.expense-input{border:1px solid var(--line);border-radius:10px;padding:10px 11px;font-family:'Tajawal',sans-serif;font-size:13.5px;background:#fff;color:var(--dark);}
  html[data-theme="dark"] select.expense-select, html[data-theme="dark"] input.expense-input{background:#1F2E52;color:#EDEAE3;border-color:#35486B;}

  /* Municipal projects */
  .project-card{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:16px;margin-bottom:14px;box-shadow:0 3px 12px rgba(20,24,27,.05);cursor:pointer;}
  html[data-theme="dark"] .project-card{box-shadow:0 3px 12px rgba(0,0,0,.25);}
  .project-card .pc-name{font-weight:900;font-size:16px;}
  .project-card .pc-meta{font-size:12px;color:var(--steel);margin-top:2px;}
  .project-stage-dots{display:flex;gap:6px;margin-top:12px;flex-wrap:wrap;}
  .project-stage-dot{font-size:11px;font-weight:700;padding:5px 10px;border-radius:20px;display:inline-flex;align-items:center;gap:4px;}
  .psd-done{background:rgba(63,143,95,.12);color:var(--green);}
  .psd-progress{background:rgba(217,140,21,.12);color:#8a5c0d;}
  .psd-none{background:rgba(69,88,107,.1);color:var(--steel);}
  .stage-edit-row{background:var(--bg);border-radius:10px;padding:12px;margin-bottom:10px;}
  .stage-edit-row .se-top{display:flex;gap:8px;align-items:center;margin-bottom:8px;}
  .stage-edit-row input[type=text]{flex:1;}
  .stage-status-btns{display:flex;gap:6px;margin-bottom:8px;}
  .stage-status-btns button{flex:1;padding:8px 4px;border-radius:8px;border:2px solid var(--line);background:#fff;font-family:'Tajawal',sans-serif;font-weight:700;font-size:12px;cursor:pointer;color:var(--dark);}
  html[data-theme="dark"] .stage-status-btns button{background:#1F2E52;color:#EDEAE3;}
  .stage-status-btns button.sel-red{border-color:var(--red);background:#FCEBE8;color:var(--red);}
  .stage-status-btns button.sel-amber{border-color:var(--amber);background:#FDF3E1;color:#8a5c0d;}
  .stage-status-btns button.sel-green{border-color:var(--green);background:#E9F5EE;color:var(--green);}
  .stage-del-btn{background:none;border:none;color:var(--red);font-size:12px;font-weight:700;cursor:pointer;padding:0;}

  /* Inventory */
  .inv-card{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:14px 16px;margin-bottom:10px;box-shadow:0 3px 12px rgba(23,29,38,.06);cursor:pointer;}
  html[data-theme="dark"] .inv-card{box-shadow:0 3px 12px rgba(0,0,0,.3);}
  .inv-card.low-stock{border-color:var(--red);}
  .inv-card .inv-top{display:flex;justify-content:space-between;align-items:center;gap:10px;}
  .inv-card .inv-name{font-weight:900;font-size:15.5px;}
  .inv-card .inv-cat{font-size:11.5px;color:var(--steel);margin-top:2px;}
  .inv-card .inv-qty{font-family:'JetBrains Mono',monospace;font-weight:900;font-size:19px;color:var(--accent);white-space:nowrap;}
  .inv-card .inv-qty.low{color:var(--red);}
  .inv-card .inv-unit{font-size:11px;color:var(--steel);font-weight:700;}
  .movement-row{display:flex;justify-content:space-between;align-items:center;background:var(--bg);border-radius:8px;padding:9px 12px;margin-top:6px;font-size:12.5px;gap:8px;}
  .movement-row .mv-in{color:var(--green);font-weight:900;}
  .movement-row .mv-out{color:var(--red);font-weight:900;}
  .movement-row .mv-meta{color:var(--steel);font-size:11px;}
  .stock-action-btns{display:flex;gap:8px;margin-top:14px;}
  .stock-action-btns button{flex:1;padding:12px 6px;border-radius:10px;border:none;font-family:'Tajawal',sans-serif;font-weight:700;font-size:13.5px;cursor:pointer;color:#fff;}
  .stock-action-btns .btn-receive{background:var(--green);}
  .stock-action-btns .btn-issue{background:var(--red);}
  .live-map-container{width:100%;height:280px;border-radius:14px;overflow:hidden;}
  .live-map-container .leaflet-popup-content{font-family:'Tajawal',sans-serif;font-size:13px;}
  .official-report-print{display:none;}
  @media print{
    header, .role-switch, .period-toggle, .print-btn, .search-box, .filters, .sort-row,
    .add-worker-btn, .export-btn, .new-task-btn, .new-task-form, .hist-btn,
    .expense-form, #toast-container, .date-nav, .sync-badge, .name-grid { display:none !important; }
    body{background:#fff;}
    .report-card{box-shadow:none;border:1px solid #ccc;break-inside:avoid;}
    main{padding:0;}
    body.printing-official-report > *:not(#official-report-print){display:none !important;}
    body.printing-official-report #official-report-print{display:block !important;}
  }
  .or-header{display:flex;justify-content:space-between;align-items:flex-start;border-bottom:3px solid #16213E;padding-bottom:14px;margin-bottom:20px;}
  .or-header h1{font-size:20px;margin:0;}
  .or-header .or-sub{font-size:12px;color:#555;margin-top:4px;}
  .or-title{text-align:center;font-size:17px;font-weight:900;margin:16px 0 20px;text-decoration:underline;}
  .or-field-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px 24px;margin-bottom:20px;font-size:13px;}
  .or-field-grid .or-label{color:#555;font-weight:700;}
  .or-table{width:100%;border-collapse:collapse;margin-bottom:24px;font-size:13px;}
  .or-table th, .or-table td{border:1px solid #999;padding:8px 10px;text-align:start;}
  .or-table th{background:#eee;}
  .or-signatures{display:flex;justify-content:space-between;margin-top:60px;font-size:13px;}
  .or-signatures div{width:45%;text-align:center;border-top:1px solid #333;padding-top:6px;}
  html[data-theme="dark"] body{--bg:#0F1A2E; --panel:#182746; --dark:#E9F1F8; --steel:#8FA6C4; --line:#2C3F63;}
  html[data-theme="dark"] .log-form input[type=date],
  html[data-theme="dark"] textarea,
  html[data-theme="dark"] input[type=text],
  html[data-theme="dark"] input[type=password],
  html[data-theme="dark"] .search-box{background:#1F2E52;color:#EDEAE3;border-color:#35486B;}
  html[data-theme="dark"] .status-btns button{background:#1F2E52;color:#EDEAE3;}
  html[data-theme="dark"] .filters button{background:#1F2E52;}
  html[data-theme="dark"] select#f-category, html[data-theme="dark"] select#nt-name-select, html[data-theme="dark"] select#f-dept-select{background:#1F2E52;color:#EDEAE3;border-color:#35486B;}
</style>
</head>
<body>

<header>
  <div class="head-row">
    <div>
      <h1 id="hTitle">شركة المستقبل الأفضل للمقاولات</h1>
      <p id="hSub">موقع البُطينة — تسجيل المهام اليومية ونسبة الإنجاز</p>
    </div>
    <div style="display:flex;gap:8px;">
      <button id="theme-toggle" class="theme-btn" aria-label="تبديل الوضع">🌙</button>
      <button class="lang-btn" id="btnLang">English</button>
    </div>
  </div>
  <div class="role-switch" id="roleSwitch">
    <button id="btnWorker" class="active">أنا موظف</button>
    <button id="btnAdmin">لوحة المدير</button>
    <button id="btnReport">📊 التقرير الأسبوعي</button>
    <button id="btnAssign">📌 تكليف مهام</button>
    <button id="btnInventory">📦 المخزون</button>
  </div>
</header>

<main id="app">
  <div class="loading">جاري التحميل...</div>
</main>

<section class="managers-corner daily-log-section" id="dailyLogSection" style="display:none; max-width:640px; margin:0 auto; padding:0 16px 40px;">
  <h2>📅 سجل إنجازات المدراء اليومية</h2>
  <div class="log-form">
    <input type="date" id="log-date" required>
    <input type="text" id="manager-name" placeholder="اسم المدير أو المسؤول..." required>
    <textarea id="log-details" placeholder="اكتب الإنجازات والمهام المنجزة هذا اليوم..." rows="2" required></textarea>
    <button id="add-log-btn">حفظ الإنجاز</button>
  </div>
  <div id="logs-container" class="logs-grid"></div>
</section>

<div id="toast-container"></div>
<div id="official-report-print" class="official-report-print"></div>
<!-- Firebase: real shared cloud database so every employee's phone and the
     manager's phone read/write the exact same data, from anywhere, on any
     network — this is what makes password changes (and everything else)
     show up correctly on every device instead of being stuck on just the
     device that made the change. Loaded as an ES module (Firebase's SDK is
     module-only); it publishes a small window.__fb handle + a
     'firebase-ready' event that the app's main script (further below)
     waits on before it ever needs to read/write data. -->
<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/12.18.0/firebase-app.js";
  import { getFirestore, doc, getDoc, setDoc, collection, getDocs, deleteDoc } from "https://www.gstatic.com/firebasejs/12.18.0/firebase-firestore.js";

  const firebaseConfig = {
    apiKey: "AIzaSyCI0qyCy_aLD1A8cgdgskhxrxIFn3XEdgY",
    authDomain: "almustqbal-ccc42.firebaseapp.com",
    projectId: "almustqbal-ccc42",
    storageBucket: "almustqbal-ccc42.firebasestorage.app",
    messagingSenderId: "313062388854",
    appId: "1:313062388854:web:f34e135e9f5a4cad461b57",
    measurementId: "G-99ST84LVM2"
  };

  try{
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    window.__fb = { db, doc, getDoc, setDoc, collection, getDocs, deleteDoc };
    window.__fbReady = true;
  }catch(e){
    console.error('Firebase init failed', e);
    window.__fbReady = true; // still fire the flag so the app doesn't hang forever waiting
  }
  window.dispatchEvent(new Event('firebase-ready'));
</script>

<script>
const PIN = '2580';
const SUB_PIN = '4321'; // separate code for the task-assignment view (e.g. Silvano) — kept apart from the manager PIN
const DEFAULT_PASSWORD = '1234'; // initial password for every employee — the manager can change each one from the manager panel

const DEPTS = {
  driver:{en:"Driver",ar:"سائق"},
  consultant:{en:"Consultant office",ar:"مكتب استشاري"},
  site_engineer:{en:"Site engineer",ar:"مهندس موقع"},
  construction_manager:{en:"Construction manager",ar:"مدير إنشاءات"},
  surveyor:{en:"Surveyor engineer",ar:"مهندس مساحة"},
  safety:{en:"Safety",ar:"سلامة"},
  documents:{en:"Documents",ar:"مستندات"},
  engineer:{en:"Engineer",ar:"مهندس"},
  civil_engineer:{en:"Civil site engineer",ar:"مهندس مدني"},
  store_keeper:{en:"Store keeper",ar:"أمين مستودع"},
  it:{en:"IT professional",ar:"تقنية معلومات"},
  general:{en:"General",ar:"عام"},
  office_boy:{en:"Office boy",ar:"أوف بوي"},
  quantity_surveyor:{en:"Quantity surveyor",ar:"مساحة كميات"},
  procurement_engineer:{en:"Procurement engineer",ar:"مهندس مشتريات"},
  road_civil_engineer:{en:"Civil engineer - roads & infrastructure",ar:"مهندس مدني - طرق وبنية تحتية"},
  accounts:{en:"Accounts",ar:"حسابات"},
};

const OTHER_CATEGORY = {v:'other', ar:'أخرى / حدد بنفسك', en:'Other / specify'};
const TASK_CATEGORIES = {
  driver: [ {v:'transport_materials', ar:'نقل مواد', en:'Transporting materials'}, {v:'transport_staff', ar:'نقل عمال', en:'Transporting staff'}, {v:'vehicle_maintenance', ar:'صيانة المركبة', en:'Vehicle maintenance'} ],
  consultant: [ {v:'review_drawings', ar:'مراجعة مخططات', en:'Reviewing drawings'}, {v:'site_meeting', ar:'اجتماع موقع', en:'Site meeting'}, {v:'technical_report', ar:'تقرير فني', en:'Technical report'} ],
  site_engineer: [ {v:'supervision', ar:'إشراف تنفيذ', en:'Execution supervision'}, {v:'quality_check', ar:'فحص جودة', en:'Quality check'}, {v:'contractor_coordination', ar:'تنسيق مقاولين', en:'Contractor coordination'} ],
  construction_manager: [ {v:'schedule_followup', ar:'متابعة الجدول الزمني', en:'Schedule follow-up'}, {v:'coordination_meeting', ar:'اجتماع تنسيق', en:'Coordination meeting'}, {v:'progress_report', ar:'تقرير تقدم', en:'Progress report'} ],
  surveyor: [ {v:'land_survey', ar:'رفع مساحي', en:'Land survey'}, {v:'marker_installation', ar:'تثبيت علامات', en:'Marker installation'}, {v:'level_check', ar:'فحص مناسيب', en:'Level check'} ],
  safety: [ {v:'inspection_round', ar:'جولة تفتيش', en:'Inspection round'}, {v:'incident_report', ar:'تقرير حادث', en:'Incident report'}, {v:'safety_training', ar:'تدريب سلامة', en:'Safety training'} ],
  documents: [ {v:'archiving', ar:'أرشفة', en:'Archiving'}, {v:'approvals_followup', ar:'متابعة موافقات', en:'Approvals follow-up'}, {v:'printing_drawings', ar:'طباعة مخططات', en:'Printing drawings'} ],
  engineer: [ {v:'design_work', ar:'تصميم', en:'Design work'}, {v:'technical_review', ar:'مراجعة فنية', en:'Technical review'} ],
  civil_engineer: [ {v:'trench_digging', ar:'حفر ترنشات', en:'Trench digging'}, {v:'concrete_pour', ar:'صب خرسانة', en:'Concrete pouring'}, {v:'rebar_install', ar:'تركيب حديد', en:'Rebar installation'}, {v:'soil_test', ar:'فحص تربة', en:'Soil testing'} ],
  store_keeper: [ {v:'receive_materials', ar:'استلام مواد', en:'Receiving materials'}, {v:'issue_materials', ar:'صرف مواد', en:'Issuing materials'}, {v:'inventory_count', ar:'جرد مخزون', en:'Inventory count'} ],
  it: [ {v:'device_maintenance', ar:'صيانة أجهزة', en:'Device maintenance'}, {v:'tech_support', ar:'دعم فني', en:'Tech support'}, {v:'network_work', ar:'شبكات', en:'Networking'} ],
  general: [],
  office_boy: [ {v:'deliveries', ar:'توصيل طلبات', en:'Deliveries'}, {v:'office_cleaning', ar:'تنظيف المكتب', en:'Office cleaning'}, {v:'errands', ar:'مشاوير', en:'Errands'}, {v:'serving_guests', ar:'استقبال وضيافة', en:'Serving guests'} ],
  quantity_surveyor: [ {v:'boq_prep', ar:'إعداد جداول كميات', en:'BOQ preparation'}, {v:'measurement', ar:'قياس كميات منفذة', en:'Measuring executed quantities'}, {v:'variation_orders', ar:'أوامر تغييرية', en:'Variation orders'}, {v:'cost_report', ar:'تقرير تكاليف', en:'Cost report'} ],
  procurement_engineer: [ {v:'rfq', ar:'طلب عروض أسعار', en:'Requesting quotes'}, {v:'price_comparison', ar:'مقارنة أسعار', en:'Price comparison'}, {v:'purchase_order', ar:'إصدار أمر شراء', en:'Issuing a purchase order'}, {v:'supplier_followup', ar:'متابعة موردين', en:'Supplier follow-up'} ],
  road_civil_engineer: [ {v:'site_engineering', ar:'هندسة الموقع', en:'Site engineering'}, {v:'interlock_works', ar:'أعمال انترلوك', en:'Interlock paving works'}, {v:'kerbstone_works', ar:'أعمال كيربستون', en:'Kerbstone works'}, {v:'asphalt_layer_works', ar:'أعمال طبقة الإسفلت', en:'Asphalt layer works'}, {v:'asphalt_layer_prep', ar:'تجهيز طبقة الإسفلت', en:'Preparing asphalt layer'}, {v:'excavation_general', ar:'أعمال حفريات', en:'Excavation works'}, {v:'site_prep', ar:'تجهيز موقع', en:'Site preparation'}, {v:'excavation_lighting', ar:'أعمال الحفر لإنارة الطريق', en:'Excavation for road lighting'}, {v:'excavation_pipes', ar:'أعمال حفر وتنزيل بايبات', en:'Excavation & pipe laying'} ],
  accounts: [ {v:'invoices_issue', ar:'إصدار فواتير', en:'Issuing invoices'}, {v:'invoices_review', ar:'مراجعة فواتير موردين', en:'Reviewing supplier invoices'}, {v:'payroll', ar:'إعداد الرواتب', en:'Payroll processing'}, {v:'expense_report', ar:'تقرير مصروفات', en:'Expense report'}, {v:'bank_reconciliation', ar:'تسوية بنكية', en:'Bank reconciliation'}, {v:'petty_cash', ar:'متابعة العهدة النقدية', en:'Petty cash follow-up'}, {v:'collections', ar:'متابعة تحصيلات', en:'Collections follow-up'}, {v:'financial_report', ar:'تقرير مالي', en:'Financial report'}, {v:'vat_tax', ar:'ضريبة القيمة المضافة / زكاة', en:'VAT / Zakat filing'} ],
};
function getCategoriesForWorker(w){
  const list = (w.deptKey && TASK_CATEGORIES[w.deptKey]) ? TASK_CATEGORIES[w.deptKey] : [];
  return [...list, OTHER_CATEGORY];
}

const DEFAULT_WORKERS = [
  {name:"Mahadi", deptKey:"driver", phone:"0528663325", password:"4821"},
  {name:"Ahmed Othman", deptKey:"consultant", phone:"0541932283", password:"3567"},
  {name:"Sufyan", deptKey:"site_engineer", phone:"055720934", password:"7294"},
  {name:"Silvano", deptKey:"construction_manager", phone:"0561139439", password:"6158"},
  {name:"Saleh", deptKey:"consultant", phone:"0543901974", password:"2983"},
  {name:"Tammam", deptKey:"road_civil_engineer", phone:"0504013405", password:"5471"},
  {name:"Ibrahim", deptKey:"surveyor", phone:"0589927427", password:"8362"},
  {name:"Ayman Mohamed", deptKey:"safety", phone:"0588504500", password:"1749"},
  {name:"Ahmed rabea", deptKey:"road_civil_engineer", phone:"0586378175", password:"9026"},
  {name:"Ahmed salah", deptKey:"documents", phone:"0529060617", password:"3814"},
  {name:"Nadeem", deptKey:"road_civil_engineer", phone:"", password:"6702"},
  {name:"Catalino", deptKey:"civil_engineer", phone:"0521559805", password:"4295"},
  {name:"Osama", deptKey:"store_keeper", phone:"0565551385", password:"7638"},
  {name:"Isaamaldin", deptKey:"road_civil_engineer", phone:"0566215772", password:"2951"},
  {name:"Ahmed Abbad", deptKey:"it", phone:"0501716668", password:"8470"},
  {name:"Kabir", deptKey:"procurement_engineer", phone:"0568297684", password:"5183"},
  {name:"Qasem", deptKey:"procurement_engineer", phone:"0569807726", password:"9647"},
  {name:"ilyn", deptKey:"quantity_surveyor", phone:"0553677146", password:"3092"},
  {name:"DANOSHA", deptKey:"office_boy", phone:"0547673021", password:"6825"},
];
// Generates a random 4-digit code that no current employee already has —
// used whenever a brand-new employee is added, or when an old account still
// has the shared "1234" default and needs its own private code instead.
function generateUniqueCode(){
  const taken = new Set(workers.map(w=>w.password));
  let code;
  let guard = 0;
  do{
    code = String(Math.floor(1000 + Math.random()*9000));
    guard++;
  } while(taken.has(code) && guard < 200);
  return code;
}

const T = {
  ar:{
    dir:'rtl', title:'شركة المستقبل الأفضل للمقاولات', sub:'تسجيل المهام اليومية ونسبة الإنجاز',
    langBtn:'English', roleWorker:'أنا موظف', roleAdmin:'لوحة المدير',
    workerHint:'اختر اسمك من القائمة لتسجيل شغلك اليوم',
    pinTitle:'دخول المدراء', pinSub:'هذه اللوحة مخصّصة للمدراء المصرّح لهم فقط', pinPlaceholder:'أدخل الرمز',
    pinSubmit:'دخول', pinErr:'الرمز غير صحيح، حاول مرة ثانية',
    empPinTitle:'دخول موظف', empPinSub:'أدخل كلمة المرور الخاصة بك للمتابعة', empPinPlaceholder:'كلمة المرور',
    empPinErr:'كلمة المرور غير صحيحة، حاول مرة ثانية',
    passwordLabel:'كلمة مرور الموظف', passwordPlaceholder:'كلمة المرور',
    deleteWorkerBtn:'🗑️ حذف الموظف', deleteWorkerConfirm:'هل تريد حذف {name}؟ سيُحذف سجله بالكامل ولا يمكن التراجع.',
    totalWorkers:'إجمالي الموظفين', doneLbl:'مكتمل', progressLbl:'جاري العمل', blockedLbl:'بدون تحديث/متوقف',
    filterAll:'الكل', filterDone:'مكتمل', filterProgress:'جاري العمل', filterBlocked:'لم يبدأ', filterNone:'بدون تحديث',
    noTask:'لم تُسجَّل مهمة بعد', taskLabel:'مهمة اليوم', taskPlaceholder:'اكتب المهمة الرئيسية اليوم...',
    completionLabel:'نسبة الإنجاز', statusLabel:'الحالة',
    statusNotStarted:'لم يبدأ', statusProgress:'جاري العمل', statusDone:'مكتمل', statusNone:'بدون تحديث',
    nameLabel:'الاسم', deptLabel:'القسم', cancel:'إلغاء', save:'حفظ',
    addWorkerBtn:'+ إضافة موظف جديد', addWorkerTitle:'إضافة موظف جديد',
    namePlaceholder:'اسم الموظف', deptPlaceholder:'مثال: مهندس موقع', add:'إضافة',
    now:'الآن', minAgo:(n)=>`قبل ${n} د`, hourAgo:(n)=>`قبل ${n} س`, noUpdate:'لا يوجد تحديث',
    pctSuffix:'% إنجاز',
    historyBtn:'السجل اليومي', historyTitle:'السجل اليومي', historyEmpty:'لا يوجد سجل بعد',
    reportBtn:'📊 التقرير الأسبوعي', weeklyHint:'ملخص آخر 7 أيام لكل الموظفين', updatesLbl:'تحديث',
    noUpdateWeekLbl:'موظفين بدون أي تحديث هذا الأسبوع', allUpdatedLbl:'كل الموظفين حدّثوا حالتهم هذا الأسبوع 👏',
    rewardsTitle:'تقييم المكافآت', chooseWorkerHint:'اختر موظفًا لعرض تقريره الأسبوعي وتقييم مكافأته',
    weeklyTasksTitle:'ما أنجزه خلال هذا الأسبوع', noWeeklyTasks:'لا توجد مهام مسجّلة هذا الأسبوع',
    rewardLabel:'تقييم المكافأة أو ملاحظات الصرف', rewardPlaceholder:'مثال: يستحق مكافأة إضافية لسرعة الإنجاز',
    approveRewardBtn:'اعتماد المكافأة', rewardHistoryTitle:'سجل المكافآت السابقة', rewardHistoryEmpty:'لا توجد مكافآت مسجّلة بعد',
    assignedTaskLabel:'مهمة يكلّفها المدير', assignedTaskPlaceholder:'اكتب المهمة اللي تريد أن يقوم بها الموظف...',
    assignedTaskDisplayLabel:'المهمة المطلوبة منك اليوم',
    phoneLabel:'رقم الجوال', phonePlaceholder:'مثال: 05xxxxxxxx',
    roleAssign:'📌 تكليف مهام',
    assignPinTitle:'دخول تكليف المهام', assignPinSub:'هذه اللوحة لتكليف المهام فقط، ولا تعرض مهام المدير', assignHint:'اختر الموظف لتكليفه بمهمة',
    subTaskLabel:'مهمة تكليف مهام', subTaskPlaceholder:'اكتب المهمة اللي تريد تكليفه فيها...',
    subTaskDisplayLabel:'مهمة إضافية مكلّف فيها', subTaskAdminNote:'مهمة من تكليف المهام',
    timerLabel:'مؤقت المهمة', tbStart:'▶ بدء', tbPause:'⏸ إيقاف مؤقت', tbStop:'⏹ إنهاء',
    durationLabel:'استغرقت', categoryLabel:'اختر المهمة', categoryPlaceholder:'📌 اختر المهمة',
    categoryOtherPlaceholder:'اكتب المهمة...',
    assignSaved:'تم حفظ التكليف ✅',
    searchPlaceholder:'🔍 ابحث بالاسم...',
    payrollTitle:'💰 ساعات العمل الأسبوعية (لقسم الحسابات)', payrollHint:'إجمالي ساعات العمل المسجّلة لكل موظف خلال آخر 7 أيام — لاستخدام قسم الحسابات في الرواتب',
    payrollEmpty:'لا توجد ساعات مسجّلة هذا الأسبوع', exportBtn:'⬇️ تصدير بيانات الأسبوع (CSV) لقسم الحسابات',
    syncing:'جاري المزامنة مع بيانات الشركة...', syncOk:'✅ البيانات متزامنة مع كل الأجهزة',
    syncChecking:'🔄 جاري التحقق من الاتصال بقاعدة البيانات...', syncConnected:'✅ متصل بقاعدة البيانات — كل الأجهزة متزامنة',
    syncError:'⚠️ تعذر الاتصال بقاعدة البيانات — تحقق من الإنترنت',
    sortLabel:'ترتيب حسب', sortName:'الاسم', sortRecent:'آخر تحديث', sortCompletion:'نسبة الإنجاز',
    exportTodayBtn:'⬇️ تصدير تقرير اليوم (CSV)',
    staleTitle:'⏰ موظفون بدون أي تحديث منذ فترة', staleHint:'ما سجّلوا أي شغل من 3 أيام أو أكثر — يحتاجون متابعة',
    staleEmpty:'كل الموظفين حدّثوا حالتهم مؤخراً 👍', staleDaysAgo:(n)=>`آخر تحديث قبل ${n} يوم`,
    periodWeek:'أسبوعي', periodMonth:'شهري', printBtn:'🖨️ طباعة / حفظ PDF',
    weeklyHintMonth:'ملخص آخر 30 يوم لكل الموظفين',
    trendTitle:'📈 اتجاه الإنجاز', deptCompareTitle:'🏗️ نسبة الإنجاز حسب القسم',
    comparisonTitle:'🏆 مقارنة الأداء بين الموظفين', comparisonHint:'ترتيب حسب متوسط نسبة الإنجاز خلال الفترة',
    expensesTitle:'💵 المصروفات (لقسم الحسابات)', expensesHint:'سجّل أي مصروف مرتبط بمشروع أو موظف',
    expenseAmountLabel:'المبلغ (ريال)', expenseCategoryLabel:'نوع المصروف', expenseWorkerLabel:'مرتبط بموظف (اختياري)',
    expenseNoteLabel:'ملاحظة', expenseNotePlaceholder:'وصف مختصر للمصروف...', addExpenseBtn:'➕ إضافة مصروف',
    expensesEmpty:'ما فيه مصروفات مسجّلة بهالفترة', expensesTotal:'إجمالي المصروفات هالفترة', noneOption:'بدون',
    notesTitle:'📝 ملاحظات الأداء', notesPlaceholder:'اكتب ملاحظة عن أداء الموظف...', addNoteBtn:'إضافة ملاحظة',
    notesEmpty:'ما فيه ملاحظات مسجّلة بعد',
    roleMunicipal:'🏛️ مشاريع البلدية', municipalHint:'تتبّع مراحل مشاريع البلدية وولّد تقرير رسمي جاهز',
    addProjectBtn:'+ إضافة مشروع جديد', projectNameLabel:'اسم المشروع', projectNamePlaceholder:'مثال: مشروع رصف حي البُطينة',
    refNumberLabel:'رقم المعاملة / الترخيص (اختياري)', locationLabel:'الموقع', projectNotesLabel:'ملاحظات عامة عن المشروع',
    stagesLabel:'مراحل المشروع', addStageBtn:'+ إضافة مرحلة', stageNamePlaceholder:'اسم المرحلة',
    stageDateLabel:'التاريخ', stageNoteLabel:'ملاحظة المرحلة', deleteStageBtn:'حذف المرحلة',
    generateReportBtn:'🖨️ توليد تقرير رسمي للبلدية', deleteProjectBtn:'🗑️ حذف المشروع',
    noProjects:'ما فيه مشاريع بلدية مسجّلة بعد', overallProgress:'التقدم العام',
    officialReportTitle:'تقرير حالة مشروع', preparedFor:'مُعد لتقديمه لـ: البلدية', preparedOn:'تاريخ الإعداد',
    projectRef:'رقم المعاملة', projectLoc:'الموقع', stageTableName:'المرحلة', stageTableStatus:'الحالة', stageTableDate:'التاريخ', stageTableNote:'ملاحظات',
    signaturePrepared:'إعداد', signatureApproved:'اعتماد المدير المسؤول',
    roleInventory:'📦 المخزون', inventoryHint:'تابعي كميات المواد والمعدات — مفيد جداً لما أكثر من موظف يشتغلون بنفس الوقت',
    addItemBtn:'+ إضافة صنف جديد', itemNameLabel:'اسم الصنف', itemNamePlaceholder:'مثال: إسمنت، حديد تسليح، أنابيب...',
    itemUnitLabel:'الوحدة', itemUnitPlaceholder:'مثال: كيس، متر، قطعة', itemQtyLabel:'الكمية الحالية',
    itemMinLabel:'الحد الأدنى (للتنبيه)', itemCategoryLabel:'الفئة (اختياري)',
    lowStockTitle:'⚠️ أصناف وصلت الحد الأدنى', lowStockHint:'تحتاج إعادة تعبئة قريباً',
    lowStockEmpty:'كل الأصناف بمستوى آمن 👍', currentStockLabel:'الكمية المتوفرة',
    receiveBtn:'📥 استلام مخزون', issueBtn:'📤 صرف مخزون', movementQtyLabel:'الكمية', movementNoteLabel:'ملاحظة',
    movementWorkerLabel:'صُرف لموظف (اختياري)', movementHistoryTitle:'سجل الحركة', movementHistoryEmpty:'ما فيه حركة مسجّلة بعد',
    deleteItemBtn:'🗑️ حذف الصنف', noItems:'ما فيه أصناف مسجّلة بعد', movementTypeIn:'استلام', movementTypeOut:'صرف',
    stockUnitsSuffix:'', invalidQty:'اكتب كمية صحيحة', insufficientStock:'الكمية المتوفرة أقل من كمية الصرف المطلوبة',
    myStatsTitle:'📌 إحصائياتك هذا الأسبوع', myStatsHours:'ساعة عمل', myStatsDone:'يوم إنجاز', myStatsTasks:'مهمة',
    mapTitle:'🗺️ خريطة مواقع العمل الحية', mapHint:'المهام اللي فيها موقع GPS مسجّل خلال آخر 24 ساعة',
    mapEmpty:'ما فيه مواقع مسجّلة حالياً — تُلتقط تلقائياً وقت بدء أي مهمة'
  },
  en:{
    dir:'ltr', title:'Future Best Contracting Co.', sub:'Daily task logging & completion tracking',
    langBtn:'العربية', roleWorker:"I'm an employee", roleAdmin:'Manager view',
    workerHint:'Select your name to log today\'s work',
    pinTitle:'Manager access', pinSub:'This view is limited to authorized managers only', pinPlaceholder:'Enter code',
    pinSubmit:'Enter', pinErr:'Incorrect code, try again',
    empPinTitle:'Employee login', empPinSub:'Enter your personal password to continue', empPinPlaceholder:'Password',
    empPinErr:'Incorrect password, try again',
    passwordLabel:'Employee password', passwordPlaceholder:'Password',
    deleteWorkerBtn:'🗑️ Delete employee', deleteWorkerConfirm:'Delete {name}? Their full record will be removed and this cannot be undone.',
    totalWorkers:'Total employees', doneLbl:'Done', progressLbl:'In progress', blockedLbl:'Not started/stalled',
    filterAll:'All', filterDone:'Done', filterProgress:'In progress', filterBlocked:'Not started', filterNone:'No update',
    noTask:'No task logged yet', taskLabel:"Today's task", taskPlaceholder:"Write today's main task...",
    completionLabel:'Completion', statusLabel:'Status',
    statusNotStarted:'Not started', statusProgress:'In progress', statusDone:'Done', statusNone:'No update',
    nameLabel:'Name', deptLabel:'Department', cancel:'Cancel', save:'Save',
    addWorkerBtn:'+ Add new employee', addWorkerTitle:'Add new employee',
    namePlaceholder:'Employee name', deptPlaceholder:'e.g. Site engineer', add:'Add',
    now:'just now', minAgo:(n)=>`${n}m ago`, hourAgo:(n)=>`${n}h ago`, noUpdate:'No update yet',
    pctSuffix:'% done',
    historyBtn:'Daily history', historyTitle:'Daily history', historyEmpty:'No history yet',
    reportBtn:'📊 Weekly report', weeklyHint:'Summary of the last 7 days for all employees', updatesLbl:'updates',
    noUpdateWeekLbl:'Employees with no update this week', allUpdatedLbl:'Everyone updated their status this week 👏',
    rewardsTitle:'Reward evaluation', chooseWorkerHint:'Select an employee to view their weekly report and evaluate a reward',
    weeklyTasksTitle:'Completed this week', noWeeklyTasks:'No tasks logged this week',
    rewardLabel:'Reward evaluation / payout notes', rewardPlaceholder:'e.g. Deserves an extra bonus for fast completion',
    approveRewardBtn:'Approve reward', rewardHistoryTitle:'Past rewards', rewardHistoryEmpty:'No rewards recorded yet',
    assignedTaskLabel:'Manager-assigned task', assignedTaskPlaceholder:'Write the task you want the employee to do...',
    assignedTaskDisplayLabel:'Task assigned to you today',
    phoneLabel:'Phone number', phonePlaceholder:'e.g. 05xxxxxxxx',
    roleAssign:'📌 Task assignment',
    assignPinTitle:'Task assignment access', assignPinSub:'This view is only for assigning tasks — manager tasks are not shown here', assignHint:'Select an employee to assign a task',
    subTaskLabel:'Assignment task', subTaskPlaceholder:'Write the task you want to assign...',
    subTaskDisplayLabel:'Additional task assigned to you', subTaskAdminNote:'Task from task assignment',
    timerLabel:'Task timer', tbStart:'▶ Start', tbPause:'⏸ Pause', tbStop:'⏹ Stop',
    durationLabel:'took', categoryLabel:'Select task', categoryPlaceholder:'📌 Select task',
    categoryOtherPlaceholder:'Write the task...',
    assignSaved:'Task assigned ✅',
    searchPlaceholder:'🔍 Search by name...',
    payrollTitle:'💰 Weekly work hours (for Accounts)', payrollHint:'Total logged work hours per employee over the last 7 days — for the Accounts department to use for payroll',
    payrollEmpty:'No hours logged this week', exportBtn:'⬇️ Export this week (CSV) for Accounts',
    syncing:'Syncing with company data...', syncOk:'✅ Data synced across all devices',
    syncChecking:'🔄 Checking database connection...', syncConnected:'✅ Connected to the database — all devices in sync',
    syncError:'⚠️ Could not connect to the database — check your internet',
    sortLabel:'Sort by', sortName:'Name', sortRecent:'Last updated', sortCompletion:'Completion %',
    exportTodayBtn:"⬇️ Export today's report (CSV)",
    staleTitle:'⏰ Employees with no update in a while', staleHint:"Haven't logged any work in 3+ days — may need follow-up",
    staleEmpty:'Everyone has updated recently 👍', staleDaysAgo:(n)=>`Last update ${n} day(s) ago`,
    periodWeek:'Weekly', periodMonth:'Monthly', printBtn:'🖨️ Print / Save PDF',
    weeklyHintMonth:'Summary of the last 30 days for all employees',
    trendTitle:'📈 Completion trend', deptCompareTitle:'🏗️ Completion rate by department',
    comparisonTitle:'🏆 Employee performance comparison', comparisonHint:'Ranked by average completion % over the period',
    expensesTitle:'💵 Expenses (for Accounts)', expensesHint:'Log any expense tied to a project or employee',
    expenseAmountLabel:'Amount (SAR)', expenseCategoryLabel:'Expense type', expenseWorkerLabel:'Linked employee (optional)',
    expenseNoteLabel:'Note', expenseNotePlaceholder:'Short description of the expense...', addExpenseBtn:'➕ Add expense',
    expensesEmpty:'No expenses logged for this period', expensesTotal:'Total expenses this period', noneOption:'None',
    notesTitle:'📝 Performance notes', notesPlaceholder:"Write a note about this employee's performance...", addNoteBtn:'Add note',
    notesEmpty:'No notes yet',
    roleMunicipal:'🏛️ Municipal Projects', municipalHint:'Track municipal project stages and generate a ready official report',
    addProjectBtn:'+ Add new project', projectNameLabel:'Project name', projectNamePlaceholder:'e.g. Al-Buteen district paving project',
    refNumberLabel:'Reference / permit number (optional)', locationLabel:'Location', projectNotesLabel:'General project notes',
    stagesLabel:'Project stages', addStageBtn:'+ Add stage', stageNamePlaceholder:'Stage name',
    stageDateLabel:'Date', stageNoteLabel:'Stage note', deleteStageBtn:'Delete stage',
    generateReportBtn:'🖨️ Generate official municipal report', deleteProjectBtn:'🗑️ Delete project',
    noProjects:'No municipal projects logged yet', overallProgress:'Overall progress',
    officialReportTitle:'Project Status Report', preparedFor:'Prepared for submission to: The Municipality', preparedOn:'Prepared on',
    projectRef:'Reference number', projectLoc:'Location', stageTableName:'Stage', stageTableStatus:'Status', stageTableDate:'Date', stageTableNote:'Notes',
    signaturePrepared:'Prepared by', signatureApproved:'Approved by responsible manager',
    roleInventory:'📦 Inventory', inventoryHint:"Track material and equipment quantities — very useful when multiple employees are working at once",
    addItemBtn:'+ Add new item', itemNameLabel:'Item name', itemNamePlaceholder:'e.g. Cement, rebar, pipes...',
    itemUnitLabel:'Unit', itemUnitPlaceholder:'e.g. bag, meter, piece', itemQtyLabel:'Current quantity',
    itemMinLabel:'Minimum threshold (for alerts)', itemCategoryLabel:'Category (optional)',
    lowStockTitle:'⚠️ Items at minimum threshold', lowStockHint:'Need restocking soon',
    lowStockEmpty:'All items are at a safe level 👍', currentStockLabel:'Current stock',
    receiveBtn:'📥 Receive stock', issueBtn:'📤 Issue stock', movementQtyLabel:'Quantity', movementNoteLabel:'Note',
    movementWorkerLabel:'Issued to employee (optional)', movementHistoryTitle:'Movement history', movementHistoryEmpty:'No movements logged yet',
    deleteItemBtn:'🗑️ Delete item', noItems:'No inventory items logged yet', movementTypeIn:'Received', movementTypeOut:'Issued',
    stockUnitsSuffix:'', invalidQty:'Enter a valid quantity', insufficientStock:'Available stock is less than the requested amount',
    myStatsTitle:'📌 Your stats this week', myStatsHours:'hours worked', myStatsDone:'days completed', myStatsTasks:'tasks',
    mapTitle:'🗺️ Live Work Site Map', mapHint:'Tasks with a GPS location logged in the last 24 hours',
    mapEmpty:'No locations logged yet — captured automatically when a task is started'
  }
};

let lang = 'ar';
let workers = [];
let role = 'worker';
let adminUnlocked = false;
let assignUnlocked = false;
let activeFilter = 'all';
let adminSortBy = 'name';
let selectedReportWorkerId = null;
let adminSearchText = '';
let dbConnectionStatus = 'checking'; // 'checking' | 'connected' | 'error'
let dbEmptyUnconfirmed = false; // true when Firestore's "workers" collection came back genuinely empty and is awaiting explicit manager confirmation before anything gets seeded
let reportPeriod = 'week'; // 'week' | 'month'

/* ---------- Local-date helpers (fixes the "date doesn't update" bug:
   toISOString() uses UTC, which is wrong for local timezones — always
   use the device's local year/month/day instead) ---------- */
function localDateKey(d){
  const y=d.getFullYear(), m=String(d.getMonth()+1).padStart(2,'0'), day=String(d.getDate()).padStart(2,'0');
  return `${y}-${m}-${day}`;
}
function todayKey(){ return localDateKey(new Date()); }
function shiftDateKey(dateStr, delta){
  const d = new Date(dateStr+'T00:00:00');
  d.setDate(d.getDate()+delta);
  return localDateKey(d);
}
function formatNavDate(dateStr){
  const d = new Date(dateStr+'T00:00:00');
  return d.toLocaleDateString(lang==='ar'?'ar-EG':'en-GB', {weekday:'long', day:'numeric', month:'long'});
}

/* The date currently being viewed/edited. Defaults to today on every
   load, and each worker's fields shown are read from their history
   entry for this date — so a new day starts blank automatically. */
let viewDate = todayKey();

function getEntry(w, date){
  return (w.history||[]).find(h=>h.date===date) || null;
}
function entryTask(w,date){ const e=getEntry(w,date); return e ? (e.task||'') : ''; }
function entryCompletion(w,date){ const e=getEntry(w,date); return e ? (e.completion||0) : 0; }
function entryStatus(w,date){ const e=getEntry(w,date); return e ? (e.status||null) : null; }
function entryUpdatedAt(w,date){ const e=getEntry(w,date); return e ? e.ts : null; }
function entryCategoryValue(w,date){ const e=getEntry(w,date); return e ? (e.categoryValue||'') : ''; }

function t(){ return T[lang]; }
function deptLabel(key){ if(!key) return ''; if(DEPTS[key]) return DEPTS[key][lang]; return key; }

function statusColor(status){
  if(status==='done') return 'green';
  if(status==='progress') return 'amber';
  if(status==='blocked') return 'red';
  return 'none';
}
function statusLabel(status){
  const s=t();
  if(status==='done') return s.statusDone;
  if(status==='progress') return s.statusProgress;
  if(status==='blocked') return s.statusNotStarted;
  return s.statusNone;
}
// Reads the EXIF "Orientation" tag straight out of the JPEG header (only
// the first ~64KB is needed) without any external library. Camera photos
// — especially portrait shots from phones — carry this tag to say how the
// raw pixel data should be rotated for correct display. Skipping it (as
// before) is exactly why camera photos were coming out sideways/upside
// down after compression: drawing straight to canvas ignores the tag
// completely, unlike an <img> tag which browsers auto-rotate for display.
function getExifOrientation(file){
  return new Promise((resolve)=>{
    const reader = new FileReader();
    reader.onload = (e)=>{
      try{
        const view = new DataView(e.target.result);
        if(view.getUint16(0,false) !== 0xFFD8){ resolve(1); return; }
        let offset = 2;
        while(offset < view.byteLength - 1){
          const marker = view.getUint16(offset, false);
          offset += 2;
          if(marker === 0xFFE1){
            offset += 2; // skip segment length
            if(view.getUint32(offset,false) !== 0x45786966){ resolve(1); return; } // "Exif"
            const tiffOffset = offset + 6;
            const little = view.getUint16(tiffOffset,false) === 0x4949;
            const firstIFDOffset = view.getUint32(tiffOffset+4, little);
            const dirStart = tiffOffset + firstIFDOffset;
            const entries = view.getUint16(dirStart, little);
            for(let i=0;i<entries;i++){
              const entryOffset = dirStart + 2 + i*12;
              if(entryOffset+10 > view.byteLength) break;
              const tag = view.getUint16(entryOffset, little);
              if(tag === 0x0112){ resolve(view.getUint16(entryOffset+8, little)); return; }
            }
            resolve(1); return;
          } else if((marker & 0xFF00) !== 0xFF00){
            break;
          } else {
            offset += view.getUint16(offset, false);
          }
        }
        resolve(1);
      }catch(err){ resolve(1); }
    };
    reader.onerror = ()=>resolve(1);
    reader.readAsArrayBuffer(file.slice(0, 65536));
  });
}
function compressImageFile(file){
  return new Promise(async (resolve,reject)=>{
    const orientation = await getExifOrientation(file);
    const reader = new FileReader();
    reader.onload = (e)=>{
      const img = new Image();
      img.onload = ()=>{
        const maxDim = 480;
        let w = img.width, h = img.height;
        if(w>h){ if(w>maxDim){ h=Math.round(h*maxDim/w); w=maxDim; } }
        else { if(h>maxDim){ w=Math.round(w*maxDim/h); h=maxDim; } }
        const swap = orientation>=5 && orientation<=8; // these orientations are rotated 90°
        const canvas = document.createElement('canvas');
        canvas.width = swap ? h : w;
        canvas.height = swap ? w : h;
        const ctx = canvas.getContext('2d');
        switch(orientation){
          case 2: ctx.transform(-1,0,0,1,canvas.width,0); break;
          case 3: ctx.transform(-1,0,0,-1,canvas.width,canvas.height); break;
          case 4: ctx.transform(1,0,0,-1,0,canvas.height); break;
          case 5: ctx.transform(0,1,1,0,0,0); break;
          case 6: ctx.transform(0,1,-1,0,canvas.height,0); break;
          case 7: ctx.transform(0,-1,-1,0,canvas.height,canvas.width); break;
          case 8: ctx.transform(0,-1,1,0,0,canvas.width); break;
          default: break; // orientation 1 (or unreadable) needs no correction
        }
        ctx.drawImage(img,0,0,w,h);
        resolve(canvas.toDataURL('image/jpeg', 0.42));
      };
      img.onerror = reject;
      img.src = e.target.result;
    };
    reader.onerror = reject;
    reader.readAsDataURL(file);
  });
}
function formatHMS(ms){
  const totalSec = Math.max(0, Math.floor(ms/1000));
  const h = Math.floor(totalSec/3600);
  const m = Math.floor((totalSec%3600)/60);
  const sec = totalSec%60;
  const pad=(n)=>String(n).padStart(2,'0');
  return `${pad(h)} : ${pad(m)} : ${pad(sec)}`;
}
function formatHoursShort(ms){
  const totalHours = ms/3600000;
  return totalHours.toFixed(1);
}
function timerElapsedMs(w){
  let ms = w.timerAccumulatedMs || 0;
  if(w.timerRunning && w.timerStartedAt) ms += (Date.now() - w.timerStartedAt);
  return ms;
}
function timerStatusLine(w){
  const active = getActiveSessions(w);
  if(!active.length) return '';
  return active.map(sess=>`<div class="tag-timer">⏱ ${sess.name}${sess.location?` (${sess.location})`:''} · ${formatHMS(Date.now()-sess.startedAt)}</div>`).join('');
}
function sessionsSpanningDate(w, date){
  return (w.taskSessions||[]).filter(sess=>{
    const startDate = localDateKey(new Date(sess.startedAt));
    const endDate = sess.endedAt ? localDateKey(new Date(sess.endedAt)) : todayKey();
    return startDate <= date && date <= endDate;
  });
}
function getActiveSessions(w){
  return (w.taskSessions||[]).filter(x=>!x.endedAt);
}
function ensureTodayEntry(w){
  if(!w.history) w.history = [];
  let entry = w.history.find(h=>h.date===todayKey());
  if(!entry){ entry = {date: todayKey(), task:'', completion:0, status:null, ts:Date.now()}; w.history.push(entry); }
  return entry;
}
function syncEntryTaskText(w){
  const entry = ensureTodayEntry(w);
  const active = getActiveSessions(w);
  if(active.length){
    entry.task = active.map(sess=> sess.location ? `${sess.name} (${sess.location})` : sess.name).join(' + ');
    entry.status = 'progress';
  }
  entry.ts = Date.now();
}
function startNewSession(w, name, location, photos, gps){
  // Independent sessions: starting a new task does NOT stop any other task
  // already running — a worker can have several running at once (e.g. one
  // crew digging Zone 1 while another handles Zone 2), each with its own clock.
  const now = Date.now();
  if(!w.taskSessions) w.taskSessions=[];
  const session = {id:'s'+now+Math.random().toString(36).slice(2,6), name, location, startedAt: now, endedAt: null, date: todayKey(), photos: photos||[], gps: gps||null};
  w.taskSessions.push(session);
  syncEntryTaskText(w);
}
// Captures the device's current GPS coordinates when starting a task, so a
// manager can confirm the employee was actually on site. Resolves to null
// (never rejects) if location is unavailable, denied, or too slow — GPS is
// a nice-to-have and must never block someone from logging their work.
function getGpsLocation(){
  return new Promise(resolve=>{
    if(!navigator.geolocation){ resolve(null); return; }
    let done=false;
    const finish=(val)=>{ if(done) return; done=true; resolve(val); };
    navigator.geolocation.getCurrentPosition(
      pos=> finish({ lat: pos.coords.latitude, lng: pos.coords.longitude, accuracy: Math.round(pos.coords.accuracy||0) }),
      ()=> finish(null),
      { enableHighAccuracy:true, timeout:8000, maximumAge:60000 }
    );
    setTimeout(()=>finish(null), 8500);
  });
}
function gpsMapUrl(gps){
  return `https://www.google.com/maps?q=${gps.lat},${gps.lng}`;
}
function gpsLine(gps){
  if(!gps) return '';
  return `<a href="${gpsMapUrl(gps)}" target="_blank" rel="noopener" class="tag-phone" style="display:inline-flex;" onclick="event.stopPropagation()">📍 ${lang==='ar'?'عرض الموقع على الخريطة':'View location on map'}</a>`;
}
// Builds a live map of every GPS-tagged task started in the last 24 hours,
// one pin per task, using Leaflet (loaded from cdnjs — no API key needed,
// unlike Google Maps). Fails silently and just shows the "no locations"
// message if Leaflet couldn't load for any reason — a missing map must
// never break the rest of the admin panel.
function renderLiveMap(container){
  const s = t();
  const cutoff = Date.now() - 24*60*60*1000;
  const points = [];
  workers.forEach(w=>{
    (w.taskSessions||[]).forEach(sess=>{
      if(sess.gps && sess.startedAt >= cutoff){
        points.push({ lat: sess.gps.lat, lng: sess.gps.lng, worker: w.name, task: sess.name, location: sess.location, time: sess.startedAt, active: !sess.endedAt });
      }
    });
  });
  if(!points.length || typeof L === 'undefined'){
    container.insertAdjacentHTML('beforeend', `<div class="logs-empty">${s.mapEmpty}</div>`);
    return;
  }
  const mapId = 'live-map-'+Date.now();
  const mapDiv = document.createElement('div');
  mapDiv.className = 'live-map-container';
  mapDiv.id = mapId;
  container.appendChild(mapDiv);
  setTimeout(()=>{
    try{
      const map = L.map(mapId).setView([points[0].lat, points[0].lng], 12);
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; OpenStreetMap contributors', maxZoom: 19
      }).addTo(map);
      const bounds = [];
      points.forEach(p=>{
        const marker = L.marker([p.lat, p.lng]).addTo(map);
        const timeStr = new Date(p.time).toLocaleTimeString(lang==='ar'?'ar-EG':'en-GB', {hour:'2-digit', minute:'2-digit'});
        marker.bindPopup(`<b>${p.worker}</b><br>${p.task}${p.location?` (${p.location})`:''}${p.active?' 🟢':''}<br><span style="font-size:11px;color:#666;">${timeStr}</span>`);
        bounds.push([p.lat, p.lng]);
      });
      if(bounds.length>1) map.fitBounds(bounds, {padding:[30,30]});
    }catch(e){ console.error('renderLiveMap failed', e); }
  }, 60); // let the container actually paint before Leaflet measures it
}
function finishSession(w, sessionId){
  const sess = (w.taskSessions||[]).find(x=>x.id===sessionId);
  if(!sess || sess.endedAt) return;
  const now = Date.now();
  sess.endedAt = now;
  const entry = ensureTodayEntry(w);
  entry.durationMs = (entry.durationMs||0) + (now - sess.startedAt);
  syncEntryTaskText(w);
}

/* ---- ADMIN-ONLY deletion helpers ----
   These are the only functions in the app that ever remove a session, a
   photo inside a session, or a full day's history entry. They are wired
   up ONLY inside admin-mode UI (openEditSheet with mode==='admin' and
   openHistorySheet, which is only ever opened from the admin list), so
   an employee never sees a delete control for anything they already
   saved — only the manager can remove saved work. */
function adminDeleteSession(w, sessionId){
  const sess = (w.taskSessions||[]).find(x=>x.id===sessionId);
  if(!sess) return;
  // If this session had already been finished and its duration folded into
  // that day's total (see finishSession), subtract it back out so payroll
  // hours stay accurate after the deletion.
  if(sess.endedAt){
    const entry = getEntry(w, sess.date);
    if(entry && entry.durationMs){
      entry.durationMs = Math.max(0, entry.durationMs - (sess.endedAt - sess.startedAt));
    }
  }
  w.taskSessions = (w.taskSessions||[]).filter(x=>x.id!==sessionId);
  // Recompute today's task-text line from whatever sessions remain active.
  if(sess.date===todayKey()){
    const entry = ensureTodayEntry(w);
    const active = getActiveSessions(w);
    entry.task = active.length ? active.map(s=> s.location ? `${s.name} (${s.location})` : s.name).join(' + ') : entry.task;
  }
}
function adminDeletePhoto(w, sessionId, photoIndex){
  const sess = (w.taskSessions||[]).find(x=>x.id===sessionId);
  if(!sess || !sess.photos) return;
  sess.photos.splice(photoIndex,1);
}
function adminDeleteHistoryDay(w, date){
  w.history = (w.history||[]).filter(h=>h.date!==date);
  // Also remove sessions that were started on that exact day, so the day
  // doesn't reappear via sessionsSpanningDate after its entry is gone.
  w.taskSessions = (w.taskSessions||[]).filter(sess=>sess.date!==date);
}

function clearAllWorkData(w){
  w.taskSessions = [];
  w.history = [];
}
function clearTodayData(w){
  const today = todayKey();
  if(w.taskSessions) w.taskSessions = w.taskSessions.filter(s=>s.date!==today);
  if(w.history) w.history = w.history.filter(h=>h.date!==today);
}
function durationText(ms){
  return formatHMS(ms);
}
function timeAgo(ts){
  const s=t();
  if(!ts) return s.noUpdate;
  const diffMin = Math.round((Date.now()-ts)/60000);
  if(diffMin<1) return s.now;
  if(diffMin<60) return s.minAgo(diffMin);
  const h = Math.round(diffMin/60);
  if(h<24) return s.hourAgo(h);
  return new Date(ts).toLocaleDateString(lang==='ar'?'ar-EG':'en-GB');
}

/* ---------- STORAGE ----------
   IMPORTANT FIX: this app used to save everything with the browser's
   localStorage. localStorage lives ONLY on one device/browser — it is
   never shared between devices. That's exactly why a password (or any
   other change) made from the manager's phone would look "wrong" the
   next day on an employee's own phone: the employee's device simply
   never received the update, because there was no shared place to send
   it to.

   Shared company data lives in Firebase Firestore — a real cloud
   database. Every device that opens this page, on any network, reads
   and writes the same data, so a password change (or any other edit)
   is visible everywhere immediately.

   ROOT CAUSE OF THE "STORAGE IS FULL" ERROR: everything used to be
   crammed into ONE Firestore document (all employees + their full
   history + every task photo, all in a single doc). Firestore caps
   every single document at ~1MB — with 19 employees' daily history and
   photos piling up over time, that one shared document eventually hit
   the cap and every save started failing, which is exactly the error
   you were seeing. The real fix is structural: each employee now gets
   their OWN Firestore document (collection "workers", one doc per
   employee id). A single employee's own history+photos are extremely
   unlikely to ever approach 1MB on their own, and even if one does,
   it no longer blocks anyone else's data from saving.

   Smaller shared records (daily manager logs, weekly rewards, the
   seeded-defaults bookkeeping) still use one simple document each
   under collection "appdata" — those stay tiny (just text), so a
   single document is fine for them.

   A couple of purely cosmetic per-device preferences (dark mode, the
   last-used "assigned by" name) are kept in this browser's own
   localStorage — losing those on a different device is harmless, and
   it avoids a network round-trip for something this minor. */
function waitForFirebase(){
  return new Promise(resolve=>{
    if(window.__fbReady) return resolve();
    let done=false;
    const finish=()=>{ if(done) return; done=true; resolve(); };
    window.addEventListener('firebase-ready', finish, {once:true});
    setTimeout(finish, 8000); // never hang forever if Firebase can't load (e.g. no network)
  });
}
async function storageGet(key, shared){
  if(!shared){
    try{ return (typeof localStorage!=='undefined') ? localStorage.getItem('pref_'+key) : null; }
    catch(e){ return null; }
  }
  try{
    await waitForFirebase();
    if(!window.__fb) return null;
    const { db, doc, getDoc } = window.__fb;
    const snap = await getDoc(doc(db, 'appdata', key));
    if(!snap.exists()) return null;
    const data = snap.data();
    return (data && typeof data.value === 'string') ? data.value : null;
  }catch(e){ console.error('storageGet failed', key, e); return null; }
}
async function storageSet(key, value, shared){
  if(!shared){
    try{
      if(typeof localStorage==='undefined') return false;
      localStorage.setItem('pref_'+key, value);
      return true;
    }catch(e){ return false; }
  }
  try{
    await waitForFirebase();
    if(!window.__fb) return false;
    const { db, doc, setDoc } = window.__fb;
    await setDoc(doc(db, 'appdata', key), { value, updatedAt: Date.now() });
    return true;
  }catch(e){ console.error('storageSet failed', key, e); return false; }
}

/* ---- Per-employee documents (collection "workers") — see note above ---- */
async function fsWorkersLoadAll(){
  // IMPORTANT: returns {ok, workers} instead of just an array/null, because
  // "the read failed" and "the database is genuinely empty" must NEVER be
  // treated the same way — confusing them was the bug that made tasks
  // vanish after refresh (see loadWorkers below for the full explanation).
  try{
    await waitForFirebase();
    if(!window.__fb) return {ok:false, workers:null, error:'firebase-not-ready'};
    const { db, collection, getDocs } = window.__fb;
    const snap = await getDocs(collection(db, 'workers'));
    const arr = [];
    snap.forEach(d=>{
      const data = d.data();
      if(data && typeof data.data === 'string'){
        try{ arr.push(JSON.parse(data.data)); }catch(e){}
      }
    });
    return {ok:true, workers:arr};
  }catch(e){
    console.error('fsWorkersLoadAll failed', e);
    return {ok:false, workers:null, error: (e && (e.code || e.message)) ? (e.code || e.message) : String(e)};
  }
}
async function fsWorkerSave(w){
  await waitForFirebase();
  if(!window.__fb) throw new Error('firebase not ready');
  const { db, doc, setDoc } = window.__fb;
  await setDoc(doc(db, 'workers', w.id), { data: JSON.stringify(w), updatedAt: Date.now() });
}
async function fsWorkerDelete(id){
  try{
    await waitForFirebase();
    if(!window.__fb) return false;
    const { db, doc, deleteDoc } = window.__fb;
    await deleteDoc(doc(db, 'workers', id));
    return true;
  }catch(e){ console.error('fsWorkerDelete failed', id, e); return false; }
}
async function fsWorkerGet(id){
  try{
    await waitForFirebase();
    if(!window.__fb) return null;
    const { db, doc, getDoc } = window.__fb;
    const snap = await getDoc(doc(db, 'workers', id));
    if(!snap.exists()) return null;
    const data = snap.data();
    if(data && typeof data.data === 'string'){
      try{ return JSON.parse(data.data); }catch(e){ return null; }
    }
    return null;
  }catch(e){ console.error('fsWorkerGet failed', id, e); return null; }
}

/* ---- Generic one-document-per-item collections ----
   Used for the manager's daily logs, weekly rewards, expenses, and
   employee notes. These used to each live as ONE shared JSON-array
   document (via storageGet/storageSet on the "appdata" collection),
   meaning every single add/delete rewrote the ENTIRE list from whatever
   this device had loaded — the exact same overwrite risk the
   per-employee "workers" collection was split apart to avoid. Two
   managers adding/deleting entries around the same time could silently
   clobber each other. Mirroring the workers pattern (one Firestore
   document per item, keyed by its own id) removes that risk here too:
   every add/delete now only ever touches the single item involved. */
async function fsCollectionLoadAll(collectionName){
  try{
    await waitForFirebase();
    if(!window.__fb) return {ok:false, items:null};
    const { db, collection, getDocs } = window.__fb;
    const snap = await getDocs(collection(db, collectionName));
    const arr = [];
    snap.forEach(d=>{
      const data = d.data();
      if(data && typeof data.data === 'string'){
        try{ arr.push(JSON.parse(data.data)); }catch(e){}
      }
    });
    return {ok:true, items:arr};
  }catch(e){
    console.error('fsCollectionLoadAll failed', collectionName, e);
    return {ok:false, items:null};
  }
}
async function fsItemSave(collectionName, item){
  await waitForFirebase();
  if(!window.__fb) throw new Error('firebase not ready');
  const { db, doc, setDoc } = window.__fb;
  await setDoc(doc(db, collectionName, item.id), { data: JSON.stringify(item), updatedAt: Date.now() });
}
async function fsItemDelete(collectionName, id){
  try{
    await waitForFirebase();
    if(!window.__fb) return false;
    const { db, doc, deleteDoc } = window.__fb;
    await deleteDoc(doc(db, collectionName, id));
    return true;
  }catch(e){ console.error('fsItemDelete failed', collectionName, id, e); return false; }
}

async function loadWorkers(){
  try{
    const result = await fsWorkersLoadAll();
    if(result.ok && result.workers.length>0){
      workers = result.workers;
      // Track exactly WHICH worker objects get touched by the migrations
      // below, and only ever save those specific ones — never the whole
      // `workers` array. Saving everything here used to re-write every
      // employee's document from this device's in-memory snapshot on any
      // load that needed even one small migration, which could silently
      // overwrite a fresher save another employee's device made in the
      // meantime (the same class of bug saveOneWorker() exists to avoid
      // everywhere else). A Set of object references naturally dedupes a
      // worker touched by more than one migration step below.
      const touched = new Set();
      workers.forEach(w=>{
        let changed = false;
        if(!w.password){ w.password = DEFAULT_PASSWORD; changed = true; }
        if(!('phone' in w)){ w.phone=''; changed = true; }
        if(!('subAssignedTask' in w)){ w.subAssignedTask=''; w.subAssignedBy=''; changed = true; }
        if(!('timerRunning' in w)){ w.timerRunning=false; w.timerStartedAt=null; w.timerAccumulatedMs=0; changed = true; }
        if(!('taskSessions' in w)){ w.taskSessions=[]; w.activeSessionId=null; changed = true; }
        if(changed) touched.add(w);
      });
      // One-time specific migration: IMad -> Nadeem, and re-specialize the
      // four road/civil engineers into their own category set, but only
      // when the record still has its old un-customized default value
      // (so a manual admin edit is never silently overwritten).
      const imad = workers.find(w=> w.name.trim().toLowerCase()==='imad');
      if(imad && imad.deptKey==='engineer'){
        imad.name = 'Nadeem';
        imad.deptKey = 'road_civil_engineer';
        touched.add(imad);
      }
      ['tammam','ahmed rabea'].forEach(nm=>{
        const wk = workers.find(w=> w.name.trim().toLowerCase()===nm);
        if(wk && wk.deptKey==='site_engineer'){ wk.deptKey='road_civil_engineer'; touched.add(wk); }
      });
      const isaam = workers.find(w=> w.name.trim().toLowerCase()==='isaamaldin');
      if(isaam && isaam.deptKey==='civil_engineer'){ isaam.deptKey='road_civil_engineer'; touched.add(isaam); }

      // Backfill known phone numbers / specialties into an already-used browser,
      // matched by name, without ever overwriting something already set. This
      // only ever patches an EXISTING record — it never re-adds a worker, so
      // an admin's deletion is always respected on every future load.
      DEFAULT_WORKERS.forEach(dw=>{
        const existing = workers.find(w=> w.name.trim().toLowerCase() === dw.name.trim().toLowerCase());
        if(existing){
          let changed = false;
          if(!existing.phone && dw.phone){ existing.phone = dw.phone; changed = true; }
          if((!existing.deptKey || existing.deptKey==='general') && dw.deptKey && dw.deptKey!=='general'){ existing.deptKey = dw.deptKey; existing.deptCustom=''; changed = true; }
          if(changed) touched.add(existing);
        }
      });

      // Seed any brand-new default employees (e.g. ones added to this app
      // after you'd already started using it) — but ONLY the very first
      // time this company data ever sees them, tracked in a separate
      // seeded-list (shared, so this "first time" is company-wide,
      // not per-device). After that, deleting one of them is permanent,
      // exactly like any other employee — reloading will never bring a
      // deleted person back.
      let seeded = [];
      try{ const rawSeed = await storageGet('seeded-defaults', true); seeded = rawSeed ? JSON.parse(rawSeed) : []; }catch(e){ seeded = []; }
      DEFAULT_WORKERS.forEach(dw=>{
        const key = dw.name.trim().toLowerCase();
        const existing = workers.find(w=> w.name.trim().toLowerCase() === key);
        if(!existing && !seeded.includes(key)){
          const newWorker = {id:'w'+Date.now()+Math.random().toString(36).slice(2,6), name: dw.name, deptKey: dw.deptKey, deptCustom:'', task:'', completion:0, status:null, updatedAt:null, assignedTask:'', password: dw.password || DEFAULT_PASSWORD, uniqueCodeAssigned:true, phone: dw.phone||'', subAssignedTask:'', subAssignedBy:'', timerRunning:false, timerStartedAt:null, timerAccumulatedMs:0, taskSessions:[], activeSessionId:null, history:[]};
          workers.push(newWorker);
          touched.add(newWorker);
        }
        if(!seeded.includes(key)) seeded.push(key);
      });
      await storageSet('seeded-defaults', JSON.stringify(seeded), true);

      // One-time privacy upgrade: any employee still holding the old
      // shared "1234" default gets their own private code instead — no
      // two employees should ever be able to log into each other's
      // record with the same code. Uses this person's assigned code from
      // the list above when there's a match, otherwise generates a fresh
      // random one. Flagged with uniqueCodeAssigned so it only ever runs
      // once per employee and never overwrites a code an admin set later.
      workers.forEach(w=>{
        if(!w.uniqueCodeAssigned && (!w.password || w.password === DEFAULT_PASSWORD)){
          const dw = DEFAULT_WORKERS.find(d=> d.name.trim().toLowerCase() === w.name.trim().toLowerCase());
          w.password = (dw && dw.password) ? dw.password : generateUniqueCode();
          w.uniqueCodeAssigned = true;
          touched.add(w);
        }
      });

      if(touched.size) await saveAllWorkers(Array.from(touched));
    } else if(result.ok && result.workers.length===0){
      // Genuinely empty database (confirmed, not a failed read). This
      // should essentially only ever happen on the very first run ever.
      // IMPORTANT: this used to auto-seed a blank default roster right
      // here, silently — which is exactly what would let a real data
      // wipe (the whole "workers" collection somehow emptied) go totally
      // unnoticed: the app would just reseed blank employees and
      // everything would *look* normal again, while the real history was
      // already gone. Now we STOP instead of seeding automatically — the
      // manager has to explicitly confirm (with the manager PIN) that
      // this is really a first-time setup before anything gets created.
      workers = [];
      dbEmptyUnconfirmed = true;
    } else {
      // The read FAILED (network / permissions / Firestore not reachable) —
      // this is NOT the same as "empty". Show the roster locally so the
      // screen isn't blank, but deliberately do NOT save anything here:
      // saving now would overwrite whatever real data is already sitting
      // in Firestore with these blank placeholders. This is exactly the
      // bug that made saved tasks disappear after a refresh — a failed
      // read was being treated as "no data yet" and silently wiping the
      // real records. Leave Firestore untouched and let the next
      // successful load pull the real data back in.
      workers = DEFAULT_WORKERS.map((w,i)=>({id:'w'+i, name:w.name, deptKey:w.deptKey, deptCustom:'', task:'', completion:0, status:null, updatedAt:null, assignedTask:'', password: w.password || DEFAULT_PASSWORD, uniqueCodeAssigned:true, phone:w.phone||'', subAssignedTask:'', subAssignedBy:'', timerRunning:false, timerStartedAt:null, timerAccumulatedMs:0, taskSessions:[], activeSessionId:null}));
      dbConnectionStatus = 'error';
      const errDetail = result.error ? ` [${result.error}]` : '';
      showToast((lang==='ar' ? '⚠️ تعذر تحميل بيانات الموظفين من قاعدة البيانات — تحقق من الاتصال. البيانات المحفوظة سابقاً لم تُمسح.' : "⚠️ Couldn't load employee data from the database — check your connection. Previously saved data was NOT erased.") + errDetail, 10000);
    }
  }catch(e){
    console.error('loadWorkers unexpected error', e);
    workers = DEFAULT_WORKERS.map((w,i)=>({id:'w'+i, name:w.name, deptKey:w.deptKey, deptCustom:'', task:'', completion:0, status:null, updatedAt:null, assignedTask:'', password: w.password || DEFAULT_PASSWORD, uniqueCodeAssigned:true, phone:w.phone||'', subAssignedTask:'', subAssignedBy:'', timerRunning:false, timerStartedAt:null, timerAccumulatedMs:0, taskSessions:[], activeSessionId:null}));
    dbConnectionStatus = 'error';
  }
  applyLangChrome();
  render();
}
// Keeps each employee's document from growing without bound even at high
// volume (e.g. one worker logging 20 tasks a day, every day). Old photos
// are the single biggest space cost, so they're dropped first and soonest;
// full session records are kept much longer since they're tiny without
// photos, but are eventually retired too — that day's total hours, task
// text, and completion % are permanently preserved in `history`, so daily
// reports and payroll exports for old dates are unaffected either way.
const PHOTO_RETENTION_DAYS = 14;
const SESSION_RETENTION_DAYS = 120;
function pruneOldSessionData(w){
  if(!w.taskSessions || !w.taskSessions.length) return;
  const photoCutoff = shiftDateKey(todayKey(), -PHOTO_RETENTION_DAYS);
  const sessionCutoff = shiftDateKey(todayKey(), -SESSION_RETENTION_DAYS);
  w.taskSessions.forEach(sess=>{
    if(sess.date < photoCutoff && sess.photos && sess.photos.length) sess.photos = [];
  });
  w.taskSessions = w.taskSessions.filter(sess => !sess.endedAt || sess.date >= sessionCutoff);
}
// Only ever called right after a fresh load from Firestore (migrations /
// first-time seeding) — never during normal use — so there is no risk of
// clobbering a concurrent edit from another device the way saving the
// whole roster on every action used to.
async function saveAllWorkers(list){
  const arr = list || workers;
  arr.forEach(pruneOldSessionData);
  try{
    await Promise.all(arr.map(w=>fsWorkerSave(w)));
    return true;
  }catch(e){
    // A save failed — almost certainly because ONE employee's own record
    // (their history + task photos) got too large. Try to recover
    // automatically by dropping that employee's older photos, then retry.
    console.error('saveAllWorkers failed, attempting photo cleanup', e);
    try{
      const today = todayKey();
      arr.forEach(w=>{
        (w.taskSessions||[]).forEach(sess=>{
          if(sess.date !== today && sess.photos && sess.photos.length) sess.photos = [];
        });
      });
      await Promise.all(arr.map(w=>fsWorkerSave(w)));
      showToast(lang==='ar' ? '⚠️ سجل أحد الموظفين كان كبير جداً — حذفنا صور الأيام القديمة تلقائياً عشان التغيير ينحفظ' : "⚠️ One employee's record was too large — cleared their old photos automatically so this change could save");
      return true;
    }catch(e2){
      // Last resort: drop every photo (even today's) so the far more
      // important data — status, completion %, task names — still saves.
      try{
        arr.forEach(w=>{ (w.taskSessions||[]).forEach(sess=>{ if(sess.photos) sess.photos=[]; }); });
        await Promise.all(arr.map(w=>fsWorkerSave(w)));
        showToast(lang==='ar' ? '⚠️ تم حذف كل الصور المرفقة عشان البيانات الأساسية تنحفظ' : '⚠️ Cleared all attached photos so the core data could save');
        return true;
      }catch(e3){
        console.error('saveAllWorkers final fallback failed', e3);
        showToast(lang==='ar' ? '❌ فشل الحفظ — تأكد من الاتصال بالإنترنت وقواعد Firestore' : '❌ Save failed — check your internet connection and Firestore rules');
        return false;
      }
    }
  }
}
// CRITICAL FIX — the actual cause of "an employee's saved work disappears":
// saveWorkers() above re-writes EVERY employee's document at once, using
// THIS device's in-memory copy of ALL of them. If employee A's phone has
// been open for a while and employee B saves a new task in the meantime,
// the moment A saves anything, it silently overwrites B's brand-new task
// with A's older, stale copy of B's record — even though A never touched
// B's data. With many employees active at once (exactly this company's
// case) this collision is common, and it's why the disappearance always
// looked random and unrelated to whoever last saved.
//
// The fix: every action that only changes ONE employee must only write
// THAT employee's own document — never anyone else's — so two people
// saving around the same time can never step on each other's data.
async function saveOneWorker(w){
  pruneOldSessionData(w);
  try{
    await fsWorkerSave(w);
    return true;
  }catch(e){
    console.error('saveOneWorker failed, attempting photo cleanup', e);
    try{
      const today = todayKey();
      (w.taskSessions||[]).forEach(sess=>{
        if(sess.date !== today && sess.photos && sess.photos.length) sess.photos = [];
      });
      await fsWorkerSave(w);
      showToast(lang==='ar' ? '⚠️ السجل كان كبير جداً — حذفنا الصور القديمة تلقائياً عشان التغيير ينحفظ' : "⚠️ The record was too large — cleared old photos automatically so this change could save");
      return true;
    }catch(e2){
      try{
        (w.taskSessions||[]).forEach(sess=>{ if(sess.photos) sess.photos=[]; });
        await fsWorkerSave(w);
        showToast(lang==='ar' ? '⚠️ تم حذف كل الصور المرفقة عشان البيانات الأساسية تنحفظ' : '⚠️ Cleared all attached photos so the core data could save');
        return true;
      }catch(e3){
        console.error('saveOneWorker final fallback failed', e3);
        return false;
      }
    }
  }
}
async function saveOneWorkerOrWarn(w){
  const ok = await saveOneWorker(w);
  if(!ok){
    window.alert(lang==='ar'
‎      ? '⚠️ تنبيه مهم: اللي سويته الحين ما انحفظ بسبب مشكلة اتصال! لو تعمل رفرش الحين بيضيع. تأكد من اتصالك بالإنترنت وحاول نفس الخطوة مرة ثانية.'
      : "⚠️ Important: what you just did did NOT save due to a connection problem! If you refresh now it will be lost. Check your internet connection and try the same step again."
    );
  }
  return ok;
}
async function saveUserData(key, data, shared){
  return await storageSet(key, JSON.stringify(data), shared);
}
async function getUserData(key, shared){
  const raw = await storageGet(key, shared);
  return raw ? JSON.parse(raw) : null;
}
/* -------------------------------------------------------------------------- */

function openPhotoLightbox(src){
  const overlay = document.createElement('div');
  overlay.className = 'photo-lightbox-overlay';
  overlay.innerHTML = `
    <button type="button" class="photo-lightbox-close" aria-label="close">×</button>
    <img src="${src}">
    <div class="photo-lightbox-hint">${lang==='ar'?'اضغط على الصورة للتكبير':'Tap the photo to zoom in'}</div>
  `;
  const imgEl = overlay.querySelector('img');
  // Tap the photo itself to zoom in further for a closer look (e.g. reading
  // a label, checking work quality) — tap again to zoom back out. Doesn't
  // close the lightbox, only the ✕ button or tapping the dark backdrop does.
  imgEl.onclick = (e)=>{ e.stopPropagation(); imgEl.classList.toggle('zoomed'); };
  overlay.onclick = (e)=>{ if(e.target===overlay || e.target.classList.contains('photo-lightbox-close')) overlay.remove(); };
  document.body.appendChild(overlay);
}
// Delegated on document so any task photo — in an active task, today's
// session log, or a past day's history — becomes tappable-to-enlarge
// without needing to re-bind handlers every time a sheet re-renders.
document.addEventListener('click', (e)=>{
  const img = e.target.closest('.sr-photos img, .photo-thumb img');
  if(img) openPhotoLightbox(img.src);
});

function showToast(msg, durationMs){
  const container = document.getElementById('toast-container');
  const toast = document.createElement('div');
  toast.className = 'toast';
  toast.textContent = msg;
  container.appendChild(toast);
  requestAnimationFrame(()=> toast.classList.add('show'));
  setTimeout(()=>{
    toast.classList.remove('show');
    setTimeout(()=> toast.remove(), 250);
  }, durationMs || 2200);
}

const LOGS_KEY = 'daily-logs';
let dailyLogs = [];

async function loadLogs(){
  const result = await fsCollectionLoadAll(LOGS_KEY);
  dailyLogs = result.ok ? result.items : [];
  if(result.ok && dailyLogs.length===0){
    // One-time migration: this list used to live as ONE shared JSON-array
    // document under "appdata" instead of one document per entry. If that
    // legacy document still has entries and the new per-item collection is
    // empty, pull them over so nothing looks like it disappeared because
    // of this change.
    try{
      const legacy = await getUserData(LOGS_KEY, true);
      if(legacy && legacy.length){
        dailyLogs = legacy;
        await Promise.all(dailyLogs.map(item=>fsItemSave(LOGS_KEY, item)));
      }
    }catch(e){}
  }
  renderLogs();
}

function renderLogs(){
  const container = document.getElementById('logs-container');
  if(!container) return;
  container.innerHTML = '';
  if(dailyLogs.length === 0){
    container.innerHTML = '<div class="logs-empty">لا توجد إنجازات مسجّلة بعد</div>';
    return;
  }
  const sorted = [...dailyLogs].sort((a,b)=> b.createdAt - a.createdAt);
  sorted.forEach(log=>{
    const card = document.createElement('div');
    card.className = 'log-card';
    card.innerHTML = `
      <div class="log-top">
        <span class="log-manager">${log.manager}</span>
        <span class="log-date mono">${log.date}</span>
      </div>
      <div class="log-details">${log.details}</div>
      <button class="log-del" data-id="${log.id}">حذف</button>
    `;
    card.querySelector('.log-del').onclick = ()=> deleteLog(log.id);
    container.appendChild(card);
  });
}

async function addLog(){
  const dateInput = document.getElementById('log-date');
  const nameInput = document.getElementById('manager-name');
  const detailsInput = document.getElementById('log-details');
  const date = dateInput.value;
  const manager = nameInput.value.trim();
  const details = detailsInput.value.trim();
  if(!date || !manager || !details){ showToast('الرجاء تعبئة جميع الحقول'); return; }
  const newLog = { id:'log'+Date.now(), date, manager, details, createdAt:Date.now() };
  dailyLogs.push(newLog);
  renderLogs();
  showToast('تم حفظ الإنجاز بنجاح ✅');
  nameInput.value = '';
  detailsInput.value = '';
  await fsItemSave(LOGS_KEY, newLog);
}

async function deleteLog(id){
  dailyLogs = dailyLogs.filter(l=> l.id !== id);
  renderLogs();
  showToast('تم حذف الإنجاز');
  await fsItemDelete(LOGS_KEY, id);
}

document.getElementById('add-log-btn').addEventListener('click', addLog);

function updateLogSectionVisibility(){
  const section = document.getElementById('dailyLogSection');
  if(!section) return;
  section.style.display = (role==='admin' && adminUnlocked) ? 'block' : 'none';
}

async function loadTheme(){
  const saved = await getUserData('theme-pref', false);
  applyTheme(saved === 'dark' ? 'dark' : 'light');
}
function applyTheme(theme){
  document.documentElement.setAttribute('data-theme', theme);
  document.getElementById('theme-toggle').textContent = theme==='dark' ? '☀️' : '🌙';
}
document.getElementById('theme-toggle').addEventListener('click', async ()=>{
  const current = document.documentElement.getAttribute('data-theme') === 'dark' ? 'dark' : 'light';
  const next = current === 'dark' ? 'light' : 'dark';
  applyTheme(next);
  await saveUserData('theme-pref', next, false);
});

function getDeptDisplay(w){ if(w.deptCustom) return w.deptCustom; return deptLabel(w.deptKey); }
function groupByDept(list){
  const groups = {};
  list.forEach(w=>{
    const d = getDeptDisplay(w) || (lang==='ar'?'أخرى':'Other');
    if(!groups[d]) groups[d]=[];
    groups[d].push(w);
  });
  return groups;
}

function applyLangChrome(){
  const s=t();
  document.getElementById('htmlRoot').setAttribute('dir', s.dir);
  document.getElementById('htmlRoot').setAttribute('lang', lang);
  document.getElementById('hTitle').textContent = s.title;
  document.getElementById('hSub').textContent = s.sub;
  document.getElementById('btnLang').textContent = s.langBtn;
  document.getElementById('btnWorker').textContent = s.roleWorker;
  document.getElementById('btnAdmin').textContent = s.roleAdmin;
  document.getElementById('btnReport').textContent = s.reportBtn;
  document.getElementById('btnAssign').textContent = s.roleAssign;
}

function renderDateNav(app){
  const isToday = viewDate === todayKey();
  const bar = document.createElement('div');
  bar.className = 'date-nav';
  bar.innerHTML = `
    <button class="date-nav-btn" id="date-prev" aria-label="prev">‹</button>
    <div class="date-nav-label">${formatNavDate(viewDate)}${isToday ? `<span class="date-nav-today">${lang==='ar'?'اليوم':'Today'}</span>` : ''}</div>
    <button class="date-nav-btn" id="date-next" aria-label="next" ${isToday?'disabled':''}>›</button>
  `;
  app.appendChild(bar);
  bar.querySelector('#date-prev').onclick = ()=>{ viewDate = shiftDateKey(viewDate, -1); render(); };
  const nextBtn = bar.querySelector('#date-next');
  if(!isToday) nextBtn.onclick = ()=>{ viewDate = shiftDateKey(viewDate, 1); render(); };
  if(!isToday){
    const note = document.createElement('div');
    note.className = 'date-nav-readonly';
    note.textContent = lang==='ar' ? 'عرض سجل يوم سابق — للعرض فقط' : 'Viewing a past day — read only';
    app.appendChild(note);
  }
}

function render(){
  const app = document.getElementById('app');
  app.innerHTML = '';
  if(dbEmptyUnconfirmed){ renderEmptyDbWarning(app); updateLogSectionVisibility(); return; }
  if(role==='worker'){ renderDateNav(app); renderWorkerPicker(app); }
  else if(role==='assign'){
    if(!assignUnlocked){ renderAssignGate(app); }
    else { renderAssignPanel(app); }
  }
  else if(!adminUnlocked){ renderPinGate(app); }
  else if(role==='admin'){ renderDateNav(app); renderAdmin(app); }
  else if(role==='report'){ renderWeeklyReport(app); }
  else if(role==='municipal'){ renderMunicipalProjects(app); }
  else if(role==='inventory'){ renderInventory(app); }
  updateLogSectionVisibility();
}

// Blocking screen shown when Firestore's "workers" collection comes back
// genuinely empty. Requires the manager PIN before creating anything, so
// an unexpected database wipe is always visible and never silently
// "fixed" by reseeding blank employees over real (already-lost) data.
function renderEmptyDbWarning(app){
  app.innerHTML = `
    <div class="pin-wrap">
      <div class="pin-lock">⚠️</div>
      <h2 style="margin:0 0 8px;color:var(--red);">${lang==='ar' ? 'قاعدة البيانات فاضية بشكل غير متوقع' : 'Database is unexpectedly empty'}</h2>
      <p class="hint" style="margin:0 0 4px;">${lang==='ar'
‎        ? 'ما لقينا أي بيانات موظفين محفوظة في قاعدة البيانات. هذا ممكن يعني إن البيانات انمسحت بالغلط، أو إن هذا فعلاً أول تشغيل للبرنامج. عشان نحمي أي بيانات موجودة، ما راح نضيف قائمة موظفين جديدة تلقائيًا إلا بتأكيد صريح منك.'
        : "We couldn't find any saved employee data in the database. This could mean data was accidentally wiped, or this is genuinely the very first run. To protect any existing data, we won't create a fresh employee list without your explicit confirmation."}</p>
      <p class="hint" style="margin:8px 0 0;font-weight:700;color:var(--red);">${lang==='ar'
‎        ? 'لا تضغط "متأكد" إلا إذا كنت متيقن 100% إن هذا أول استخدام وما فيه بيانات سابقة تستاهل نحافظ عليها.'
        : "Don't press \"I'm sure\" unless you're 100% certain this is a first-time setup with no prior data worth preserving."}</p>
      <div><input type="password" id="emptyDbPin" inputmode="numeric" maxlength="8" placeholder="${t().pinPlaceholder}"></div>
      <button class="pin-submit" id="emptyDbSeedBtn" style="background:var(--red);">${lang==='ar' ? '⚠️ متأكد — ابدأ بقائمة موظفين افتراضية جديدة' : "⚠️ I'm sure — start with a fresh default employee list"}</button>
      <div class="pin-err" id="emptyDbErr"></div>
    </div>
  `;
  const input = document.getElementById('emptyDbPin');
  const trySeed = async ()=>{
    if(input.value !== PIN){
      document.getElementById('emptyDbErr').textContent = t().pinErr;
      input.value=''; input.focus();
      return;
    }
    const btn = document.getElementById('emptyDbSeedBtn');
    btn.disabled = true;
    await confirmSeedDefaults();
  };
  document.getElementById('emptyDbSeedBtn').onclick = trySeed;
  input.onkeydown = (e)=>{ if(e.key==='Enter') trySeed(); };
}
async function confirmSeedDefaults(){
  workers = DEFAULT_WORKERS.map((w,i)=>({id:'w'+i, name:w.name, deptKey:w.deptKey, deptCustom:'', task:'', completion:0, status:null, updatedAt:null, assignedTask:'', password: w.password || DEFAULT_PASSWORD, uniqueCodeAssigned:true, phone:w.phone||'', subAssignedTask:'', subAssignedBy:'', timerRunning:false, timerStartedAt:null, timerAccumulatedMs:0, taskSessions:[], activeSessionId:null}));
  await storageSet('seeded-defaults', JSON.stringify(DEFAULT_WORKERS.map(dw=>dw.name.trim().toLowerCase())), true);
  await saveAllWorkers();
  dbEmptyUnconfirmed = false;
  render();
}

function renderPinGate(app){
  const s=t();
  app.innerHTML = `
    <div class="pin-wrap">
      <div class="pin-lock">🔒</div>
      <h2 style="margin:0 0 4px;">${s.pinTitle}</h2>
      <p class="hint" style="margin:0;">${s.pinSub}</p>
      <div><input type="password" id="pinInput" inputmode="numeric" maxlength="8" placeholder="${s.pinPlaceholder}"></div>
      <button class="pin-submit" id="pinSubmit">${s.pinSubmit}</button>
      <div class="pin-err" id="pinErr"></div>
    </div>
  `;
  const input = document.getElementById('pinInput');
  const tryUnlock = ()=>{
    if(input.value === PIN){ adminUnlocked = true; render(); }
    else { document.getElementById('pinErr').textContent = s.pinErr; input.value=''; input.focus(); }
  };
  document.getElementById('pinSubmit').onclick = tryUnlock;
  input.onkeydown = (e)=>{ if(e.key==='Enter') tryUnlock(); };
}

function openEmployeeGate(id){
  const s=t();
  const w = workers.find(x=>x.id===id);
  if(!w) return;
  const overlay=document.createElement('div'); overlay.className='sheet-overlay';
  const sheet=document.createElement('div'); sheet.className='sheet';
  sheet.innerHTML = `
    <div class="pin-wrap">
      <div class="pin-lock">🔒</div>
      <h2 style="margin:0 0 4px;">${w.name}</h2>
      <p class="hint" style="margin:0;">${s.empPinSub}</p>
      <div><input type="password" id="empPinInput" inputmode="numeric" maxlength="12" placeholder="${s.empPinPlaceholder}"></div>
      <button class="pin-submit" id="empPinSubmit">${s.pinSubmit}</button>
      <div class="pin-err" id="empPinErr"></div>
      <div class="sheet-actions" style="margin-top:16px;">
        <button class="btn-cancel" id="empPinCancel" style="flex:1;">${s.cancel}</button>
      </div>
    </div>
  `;
  overlay.appendChild(sheet);
  document.body.appendChild(overlay);
  const input = sheet.querySelector('#empPinInput');
  input.focus();
  const tryUnlock = async ()=>{
    // Re-fetch this employee's own document before checking the password,
    // so someone opening the app days after a manager changed their code
    // is always checked against the current code, not a stale copy this
    // device happened to load earlier in the session.
    const fresh = await fsWorkerGet(w.id);
    if(fresh && fresh.password) w.password = fresh.password;
    if(input.value === (w.password || DEFAULT_PASSWORD)){
      overlay.remove();
      openEditSheet(w.id, 'worker');
    } else {
      sheet.querySelector('#empPinErr').textContent = s.empPinErr;
      input.value=''; input.focus();
    }
  };
  sheet.querySelector('#empPinSubmit').onclick = tryUnlock;
  input.onkeydown = (e)=>{ if(e.key==='Enter') tryUnlock(); };
  sheet.querySelector('#empPinCancel').onclick = ()=> overlay.remove();
  overlay.onclick=(e)=>{ if(e.target===overlay) overlay.remove(); };
}

function renderWorkerPicker(app){
  const s=t();
  const isToday = viewDate === todayKey();
  const hint=document.createElement('p'); hint.className='hint'; hint.textContent=s.workerHint;
  app.appendChild(hint);
  const groups = groupByDept(workers);
  Object.keys(groups).forEach(dept=>{
    const section=document.createElement('div'); section.className='dept-group';
    const label=document.createElement('div'); label.className='dept-label'; label.textContent=dept;
    section.appendChild(label);
    const grid=document.createElement('div'); grid.className='name-grid';
    groups[dept].forEach(w=>{
      const card=document.createElement('div'); card.className='name-card';
      const dayStatus = entryStatus(w, viewDate);
      const showPin = isToday && w.assignedTask;
      card.innerHTML = `<span class="status-dot dot-${statusColor(dayStatus)}"></span>${showPin?'📌 ':''}${w.name}`;
      card.onclick=()=>openEmployeeGate(w.id);
      grid.appendChild(card);
    });
    section.appendChild(grid);
    app.appendChild(section);
  });
}

function lastActivityTs(w){
  const hist = w.history||[];
  if(!hist.length) return null;
  return hist.reduce((max,h)=> (h.ts && h.ts>max) ? h.ts : max, 0) || null;
}
function getFilteredSortedWorkers(){
  let list = workers;
  if(activeFilter==='none') list = list.filter(w=>!entryStatus(w,viewDate));
  else if(activeFilter!=='all') list = list.filter(w=>entryStatus(w,viewDate)===activeFilter);
  if(adminSearchText.trim()){
    const q = adminSearchText.trim().toLowerCase();
    list = list.filter(w=> w.name.toLowerCase().includes(q));
  }
  list = list.slice();
  if(adminSortBy==='recent'){
    list.sort((a,b)=> (entryUpdatedAt(b,viewDate)||0) - (entryUpdatedAt(a,viewDate)||0));
  } else if(adminSortBy==='completion'){
    list.sort((a,b)=> entryCompletion(b,viewDate) - entryCompletion(a,viewDate));
  } else {
    list.sort((a,b)=> a.name.localeCompare(b.name, lang==='ar'?'ar':'en'));
  }
  return list;
}
function exportTodayCsv(){
  const list = getFilteredSortedWorkers();
  const rows = [['Name','Department','Status','Completion %','Task','Last update']];
  list.forEach(w=>{
    const dayStatus = entryStatus(w, viewDate);
    rows.push([w.name, getDeptDisplay(w), statusLabel(dayStatus), entryCompletion(w,viewDate), entryTask(w,viewDate), entryUpdatedAt(w,viewDate) ? new Date(entryUpdatedAt(w,viewDate)).toLocaleString(lang==='ar'?'ar-EG':'en-GB') : '']);
  });
  const csv = rows.map(r=>r.map(csvEscape).join(',')).join('\n');
  const blob = new Blob(['\uFEFF'+csv], {type:'text/csv;charset=utf-8;'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = `daily-report-${viewDate}.csv`;
  document.body.appendChild(a);
  a.click();
  a.remove();
  URL.revokeObjectURL(url);
}

let dbConnectionErrorDetail = '';
async function checkDbConnection(){
  dbConnectionStatus = 'checking';
  dbConnectionErrorDetail = '';
  try{
    await waitForFirebase();
    if(!window.__fb){ dbConnectionStatus = 'error'; dbConnectionErrorDetail = 'firebase-not-ready'; if(role==='admin') render(); return; }
    const { db, doc, getDoc } = window.__fb;
    await getDoc(doc(db, 'appdata', 'seeded-defaults'));
    dbConnectionStatus = 'connected';
  }catch(e){
    console.error('checkDbConnection failed', e);
    dbConnectionStatus = 'error';
    dbConnectionErrorDetail = (e && (e.code || e.message)) ? (e.code || e.message) : String(e);
  }
  if(role==='admin') render();
}

function renderAdmin(app){
  const s=t();
  const isToday = viewDate === todayKey();
  const total=workers.length;
  const done=workers.filter(w=>entryStatus(w,viewDate)==='done').length;
  const progress=workers.filter(w=>entryStatus(w,viewDate)==='progress').length;
  const blocked=workers.filter(w=>{ const st=entryStatus(w,viewDate); return st==='blocked'||!st; }).length;

  const badge=document.createElement('div');
  badge.className = `sync-badge sb-${dbConnectionStatus==='connected'?'connected':(dbConnectionStatus==='error'?'error':'checking')}`;
  const badgeMsg = dbConnectionStatus==='connected' ? s.syncConnected : (dbConnectionStatus==='error' ? s.syncError : s.syncChecking);
  badge.textContent = badgeMsg + (dbConnectionStatus==='error' && dbConnectionErrorDetail ? ` [${dbConnectionErrorDetail}]` : '');
  app.appendChild(badge);

  const strip=document.createElement('div'); strip.className='summary-strip';
  strip.innerHTML = `
    <div><span class="num mono">${total}</span><span class="lbl">${s.totalWorkers}</span></div>
    <div><span class="num mono" style="color:var(--green)">${done}</span><span class="lbl">${s.doneLbl}</span></div>
    <div><span class="num mono" style="color:#8a5c0d">${progress}</span><span class="lbl">${s.progressLbl}</span></div>
    <div><span class="num mono" style="color:var(--red)">${blocked}</span><span class="lbl">${s.blockedLbl}</span></div>
  `;
  app.appendChild(strip);

  // Live workforce map — the kind of dashboard bigger contracting
  // companies use to see where their crews actually are right now,
  // built from the GPS points already captured when a task starts.
  if(isToday){
    const mapCard=document.createElement('div'); mapCard.className='report-card';
    mapCard.innerHTML = `<h3>${s.mapTitle}</h3><p class="hint">${s.mapHint}</p>`;
    app.appendChild(mapCard);
    renderLiveMap(mapCard);
  }

  // Stale-employee alert: anyone with no logged activity at all in the
  // last 3 days, so a manager can spot who needs following up without
  // having to click into every single employee.
  const staleCutoff = Date.now() - 3*24*60*60*1000;
  const staleWorkers = workers.filter(w=>{
    const last = lastActivityTs(w);
    return !last || last < staleCutoff;
  });
  if(staleWorkers.length){
    const staleSection=document.createElement('div'); staleSection.className='dept-group';
    const staleLabel=document.createElement('div'); staleLabel.className='dept-label'; staleLabel.textContent=s.staleTitle;
    staleSection.appendChild(staleLabel);
    const staleHintEl=document.createElement('p'); staleHintEl.className='hint'; staleHintEl.style.margin='0 4px 8px'; staleHintEl.textContent=s.staleHint;
    staleSection.appendChild(staleHintEl);
    staleWorkers.forEach(w=>{
      const last = lastActivityTs(w);
      const daysAgo = last ? Math.floor((Date.now()-last)/(24*60*60*1000)) : null;
      const card=document.createElement('div'); card.className='stale-card';
      card.innerHTML = `
        <div><div class="st-name">${w.name}</div><div class="st-dept">${getDeptDisplay(w)}</div></div>
        <div class="st-days">${daysAgo===null ? s.noUpdate : s.staleDaysAgo(daysAgo)}</div>
      `;
      card.onclick=()=>openEditSheet(w.id,'admin');
      staleSection.appendChild(card);
    });
    app.appendChild(staleSection);
  }

  const searchBox=document.createElement('input');
  searchBox.type='text'; searchBox.className='search-box'; searchBox.placeholder=s.searchPlaceholder; searchBox.value=adminSearchText;
  searchBox.oninput=()=>{ adminSearchText = searchBox.value; renderAdminList(); };
  app.appendChild(searchBox);

  const sortRow=document.createElement('div'); sortRow.className='sort-row';
  const sortLabelEl=document.createElement('label'); sortLabelEl.textContent=s.sortLabel;
  const sortSelect=document.createElement('select'); sortSelect.className='sort-select';
  sortSelect.innerHTML = `
    <option value="name" ${adminSortBy==='name'?'selected':''}>${s.sortName}</option>
    <option value="recent" ${adminSortBy==='recent'?'selected':''}>${s.sortRecent}</option>
    <option value="completion" ${adminSortBy==='completion'?'selected':''}>${s.sortCompletion}</option>
  `;
  sortSelect.onchange = ()=>{ adminSortBy = sortSelect.value; renderAdminList(); };
  sortRow.appendChild(sortLabelEl);
  sortRow.appendChild(sortSelect);
  app.appendChild(sortRow);

  const filters=document.createElement('div'); filters.className='filters';
  const filterDefs=[['all',s.filterAll],['done',s.filterDone],['progress',s.filterProgress],['blocked',s.filterBlocked],['none',s.filterNone]];
  filterDefs.forEach(([key,label])=>{
    const btn=document.createElement('button'); btn.textContent=label;
    if(activeFilter===key) btn.classList.add('active');
    btn.onclick=()=>{ activeFilter=key; render(); };
    filters.appendChild(btn);
  });
  app.appendChild(filters);

  const listWrap = document.createElement('div');
  listWrap.id = 'admin-list-wrap';
  app.appendChild(listWrap);
  renderAdminList();

  const exportBtn=document.createElement('button'); exportBtn.className='export-btn'; exportBtn.textContent=s.exportTodayBtn;
  exportBtn.onclick=exportTodayCsv;
  app.appendChild(exportBtn);

  if(isToday){
    const addBtn=document.createElement('button'); addBtn.className='add-worker-btn'; addBtn.textContent=s.addWorkerBtn;
    addBtn.onclick=openAddWorker;
    app.appendChild(addBtn);
  }
}

function renderAdminList(){
  const s=t();
  const listWrap = document.getElementById('admin-list-wrap');
  if(!listWrap) return;
  listWrap.innerHTML = '';
  const isToday = viewDate === todayKey();

  const list = getFilteredSortedWorkers();

  list.forEach(w=>{
    const dayStatus = entryStatus(w, viewDate);
    const dayTask = entryTask(w, viewDate);
    const dayCompletion = entryCompletion(w, viewDate);
    const dayUpdatedAt = entryUpdatedAt(w, viewDate);
    const color=statusColor(dayStatus);
    const tag=document.createElement('div'); tag.className=`tag ${color==='none'?'':color}`;
    const timerLine = isToday ? timerStatusLine(w) : '';
    const spanNote = !isToday ? sessionsSpanningDate(w, viewDate).map(sess=>{
      const stillRunning = !sess.endedAt;
      const startDate = formatNavDate(localDateKey(new Date(sess.startedAt)));
      return `<div class="tag-timer" style="color:var(--steel);">🕐 ${sess.name}${sess.location?` (${sess.location})`:''} — ${stillRunning ? (lang==='ar'?'مستمرة، بدأت':'ongoing since') : (lang==='ar'?'كانت مستمرة، بدأت':'was ongoing, started')} ${startDate}</div>`;
    }).join('') : '';
    const subTaskLine = (isToday && w.subAssignedTask) ? `<div class="sub-task-note">📌 ${w.subAssignedBy ? (lang==='ar'?`مهمة من ${w.subAssignedBy}`:`Task from ${w.subAssignedBy}`) : s.subTaskAdminNote}: ${w.subAssignedTask}</div>` : '';
    tag.innerHTML = `
      <div class="tag-top">
        <div><div class="tag-name">${w.name}</div><div class="tag-dept">${getDeptDisplay(w)}</div>${w.phone?`<a class="tag-phone" href="tel:${w.phone}" onclick="event.stopPropagation()">📞 ${w.phone}</a>`:''}${(isToday && w.assignedTask)?`<div class="tag-dept" style="color:var(--accent);margin-top:4px;">📌 ${w.assignedTask}</div>`:''}</div>
        <div class="tag-badge badge-${color}">${statusLabel(dayStatus)}</div>
      </div>
      <div class="tag-task ${dayTask?'':'empty'}">${dayTask?dayTask:s.noTask}</div>
      <div class="bar-wrap"><div class="bar-fill" style="width:${dayCompletion}%; background:var(--${color==='none'?'steel':color})"></div></div>
      <div class="tag-foot"><span>${dayCompletion}${s.pctSuffix}</span><span>${timeAgo(dayUpdatedAt)}</span></div>
      ${timerLine}
      ${spanNote}
      ${subTaskLine}
      <button class="hist-btn" data-id="${w.id}">📅 ${s.historyBtn}</button>
    `;
    tag.onclick=()=>openEditSheet(w.id,'admin');
    tag.querySelector('.hist-btn').onclick=(e)=>{ e.stopPropagation(); openHistorySheet(w.id); };
    listWrap.appendChild(tag);
  });
}

const REWARDS_KEY = 'weekly-rewards';
let weeklyRewards = [];

async function loadRewards(){
  const result = await fsCollectionLoadAll(REWARDS_KEY);
  weeklyRewards = result.ok ? result.items : [];
  if(result.ok && weeklyRewards.length===0){
    try{
      const legacy = await getUserData(REWARDS_KEY, true);
      if(legacy && legacy.length){
        weeklyRewards = legacy;
        await Promise.all(weeklyRewards.map(item=>fsItemSave(REWARDS_KEY, item)));
      }
    }catch(e){}
  }
}
async function saveReward(workerId, workerName, note){
  const item = { id:'rw'+Date.now(), workerId, workerName, note, createdAt:Date.now() };
  weeklyRewards.push(item);
  await fsItemSave(REWARDS_KEY, item);
}
async function deleteReward(id){
  weeklyRewards = weeklyRewards.filter(r=> r.id !== id);
  await fsItemDelete(REWARDS_KEY, id);
}

/* ---- Expenses (for the Accounts department) ---- */
const EXPENSES_KEY = 'expenses';
let expenses = [];
const EXPENSE_CATEGORIES = [
  {v:'materials', ar:'مواد وخامات', en:'Materials'},
  {v:'transport', ar:'نقل ومواصلات', en:'Transport'},
  {v:'maintenance', ar:'صيانة', en:'Maintenance'},
  {v:'labor', ar:'أجور عمالة إضافية', en:'Extra labor'},
  {v:'permits', ar:'رسوم ومستندات', en:'Permits/fees'},
  {v:'other', ar:'أخرى', en:'Other'},
];
async function loadExpenses(){
  const result = await fsCollectionLoadAll(EXPENSES_KEY);
  expenses = result.ok ? result.items : [];
  if(result.ok && expenses.length===0){
    try{
      const legacy = await getUserData(EXPENSES_KEY, true);
      if(legacy && legacy.length){
        expenses = legacy;
        await Promise.all(expenses.map(item=>fsItemSave(EXPENSES_KEY, item)));
      }
    }catch(e){}
  }
}
async function addExpense(entry){
  const item = { id:'ex'+Date.now(), ...entry, createdAt:Date.now() };
  expenses.push(item);
  await fsItemSave(EXPENSES_KEY, item);
}
async function deleteExpense(id){
  expenses = expenses.filter(x=> x.id !== id);
  await fsItemDelete(EXPENSES_KEY, id);
}

/* ---- Employee performance notes (separate from reward log) ---- */
const NOTES_KEY = 'employee-notes';
let employeeNotes = [];
async function loadEmployeeNotes(){
  const result = await fsCollectionLoadAll(NOTES_KEY);
  employeeNotes = result.ok ? result.items : [];
  if(result.ok && employeeNotes.length===0){
    try{
      const legacy = await getUserData(NOTES_KEY, true);
      if(legacy && legacy.length){
        employeeNotes = legacy;
        await Promise.all(employeeNotes.map(item=>fsItemSave(NOTES_KEY, item)));
      }
    }catch(e){}
  }
}
async function addEmployeeNote(workerId, workerName, note){
  const item = { id:'nt'+Date.now(), workerId, workerName, note, createdAt:Date.now() };
  employeeNotes.push(item);
  await fsItemSave(NOTES_KEY, item);
}
async function deleteEmployeeNote(id){
  employeeNotes = employeeNotes.filter(n=> n.id !== id);
  await fsItemDelete(NOTES_KEY, id);
}

/* ---- Municipal projects (stage tracking + official report generation) ---- */
const PROJECTS_KEY = 'municipal-projects';
let municipalProjects = [];
function defaultProjectStages(){
  const names = lang==='ar' ? ['ترخيص','فحص','تسليم'] : ['Permit/License','Inspection','Handover'];
  return names.map((n,i)=>({id:'stg'+Date.now()+i, name:n, status:null, date:'', note:''}));
}
async function loadMunicipalProjects(){
  const saved = await getUserData(PROJECTS_KEY, true);
  municipalProjects = saved || [];
}
async function saveMunicipalProjects(){
  await saveUserData(PROJECTS_KEY, municipalProjects, true);
}
function projectProgress(p){
  const stages = p.stages||[];
  if(!stages.length) return 0;
  const doneCount = stages.filter(st=>st.status==='done').length;
  const progCount = stages.filter(st=>st.status==='progress').length;
  return Math.round(((doneCount + progCount*0.5) / stages.length) * 100);
}

/* ---- Inventory (materials & equipment stock tracking) ----
   Requested specifically because many employees can be working — and
   drawing on the same shared materials — at the same time, so knowing
   what's actually left in stock matters. Two small shared records: the
   item list itself, and a running movement log (receipts/issues) kept
   separate so the item list stays tiny and fast to load. */
const INVENTORY_ITEMS_KEY = 'inventory-items';
const INVENTORY_LOG_KEY = 'inventory-log';
let inventoryItems = [];
let inventoryLog = [];
async function loadInventory(){
  const itemsResult = await fsCollectionLoadAll(INVENTORY_ITEMS_KEY);
  inventoryItems = itemsResult.ok ? itemsResult.items : [];
  if(itemsResult.ok && inventoryItems.length===0){
    try{
      const legacy = await getUserData(INVENTORY_ITEMS_KEY, true);
      if(legacy && legacy.length){
        inventoryItems = legacy;
        await Promise.all(inventoryItems.map(item=>fsItemSave(INVENTORY_ITEMS_KEY, item)));
      }
    }catch(e){}
  }
  const logResult = await fsCollectionLoadAll(INVENTORY_LOG_KEY);
  inventoryLog = logResult.ok ? logResult.items : [];
  if(logResult.ok && inventoryLog.length===0){
    try{
      const legacy = await getUserData(INVENTORY_LOG_KEY, true);
      if(legacy && legacy.length){
        inventoryLog = legacy;
        await Promise.all(inventoryLog.map(item=>fsItemSave(INVENTORY_LOG_KEY, item)));
      }
    }catch(e){}
  }
}
function isLowStock(item){
  return (item.minThreshold||0) > 0 && item.quantity <= item.minThreshold;
}
async function recordStockMovement(item, type, qty, note, workerId, workerName){
  item.quantity = type==='in' ? (item.quantity + qty) : (item.quantity - qty);
  item.updatedAt = Date.now();
  const logEntry = { id:'mv'+Date.now(), itemId:item.id, itemName:item.name, type, qty, note, workerId, workerName, createdAt: Date.now() };
  inventoryLog.push(logEntry);
  await fsItemSave(INVENTORY_ITEMS_KEY, item);
  await fsItemSave(INVENTORY_LOG_KEY, logEntry);
}

function getLastNDates(n){
  const arr=[];
  for(let i=n-1;i>=0;i--){
    const d=new Date();
    d.setDate(d.getDate()-i);
    arr.push(localDateKey(d));
  }
  return arr;
}

function workerWeeklyMs(w, days){
  let total = 0;
  (w.taskSessions||[]).forEach(sess=>{
    const start = sess.startedAt;
    const end = sess.endedAt || Date.now();
    // Only count the portion of the session that falls within the reporting window
    const windowStart = new Date(days[0]+'T00:00:00').getTime();
    const windowEnd = new Date(days[days.length-1]+'T23:59:59').getTime();
    const overlapStart = Math.max(start, windowStart);
    const overlapEnd = Math.min(end, windowEnd);
    if(overlapEnd > overlapStart) total += (overlapEnd - overlapStart);
  });
  return total;
}

function csvEscape(val){
  const str = String(val==null?'':val);
  if(/[",\n]/.test(str)) return '"' + str.replace(/"/g,'""') + '"';
  return str;
}
function exportWeeklyCsv(){
  const days = reportPeriod==='month' ? getLastNDates(30) : getLastNDates(7);
  const rows = [['Name','Department','Hours this period','Days done','Days in progress','Days no update']];
  workers.forEach(w=>{
    const ms = workerWeeklyMs(w, days);
    const doneDays = days.filter(d=>entryStatus(w,d)==='done').length;
    const progDays = days.filter(d=>entryStatus(w,d)==='progress').length;
    const noneDays = days.filter(d=>!entryStatus(w,d)).length;
    rows.push([w.name, getDeptDisplay(w), formatHoursShort(ms), doneDays, progDays, noneDays]);
  });
  rows.push([]);
  rows.push(['Expenses']);
  rows.push(['Date','Category','Amount','Employee','Note']);
  expenses.filter(x=>days.includes(localDateKey(new Date(x.createdAt)))).forEach(x=>{
    rows.push([localDateKey(new Date(x.createdAt)), x.category, x.amount, x.workerName||'', x.note||'']);
  });
  const csv = rows.map(r=>r.map(csvEscape).join(',')).join('\n');
  const blob = new Blob(['\uFEFF'+csv], {type:'text/csv;charset=utf-8;'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = `${reportPeriod}-report-${todayKey()}.csv`;
  document.body.appendChild(a);
  a.click();
  a.remove();
  URL.revokeObjectURL(url);
}
function renderBarChartHTML(items){
  const max = Math.max(1, ...items.map(i=>i.value));
  return items.map(i=>`
    <div class="chart-row">
      <div class="chart-label">${i.label}</div>
      <div class="chart-bar-wrap"><div class="chart-bar-fill" style="width:${Math.max(3,Math.round((i.value/max)*100))}%;${i.color?`background:${i.color};`:''}"></div></div>
      <div class="chart-value">${i.valueLabel!==undefined?i.valueLabel:i.value}</div>
    </div>
  `).join('');
}
function renderTrendSvg(days){
  const counts = days.map(d=> workers.filter(w=>entryStatus(w,d)==='done').length);
  const max = Math.max(1, ...counts);
  const w = 600, h = 70, pad = 8;
  const stepX = (w-pad*2)/Math.max(1,days.length-1);
  const points = counts.map((c,i)=>{
    const x = pad + i*stepX;
    const y = h - pad - (c/max)*(h-pad*2);
    return `${x.toFixed(1)},${y.toFixed(1)}`;
  }).join(' ');
  const areaPoints = `${pad},${h-pad} ${points} ${w-pad},${h-pad}`;
  return `<div class="trend-svg-wrap"><svg viewBox="0 0 ${w} ${h}" style="width:100%;height:64px;display:block;" preserveAspectRatio="none">
    <polygon points="${areaPoints}" fill="var(--accent)" opacity="0.12"/>
    <polyline points="${points}" fill="none" stroke="var(--accent)" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/>
  </svg></div>`;
}

function renderWeeklyReport(app){
  const s=t();
  app.innerHTML='';

  const periodToggle=document.createElement('div'); periodToggle.className='period-toggle';
  periodToggle.innerHTML = `
    <button data-p="week" class="${reportPeriod==='week'?'active':''}">${s.periodWeek}</button>
    <button data-p="month" class="${reportPeriod==='month'?'active':''}">${s.periodMonth}</button>
  `;
  periodToggle.querySelectorAll('button').forEach(btn=>{
    btn.onclick=()=>{ reportPeriod = btn.dataset.p; selectedReportWorkerId=null; render(); };
  });
  app.appendChild(periodToggle);

  const printBtn=document.createElement('button'); printBtn.className='print-btn'; printBtn.textContent=s.printBtn;
  printBtn.onclick=()=>window.print();
  app.appendChild(printBtn);

  const hint=document.createElement('p'); hint.className='hint'; hint.textContent = reportPeriod==='month' ? s.weeklyHintMonth : s.weeklyHint;
  app.appendChild(hint);

  const days = reportPeriod==='month' ? getLastNDates(30) : getLastNDates(7);

  if(reportPeriod==='week'){
    days.forEach(day=>{
      const dayEntries = [];
      workers.forEach(w=>{
        const h = (w.history||[]).find(x=>x.date===day);
        if(h) dayEntries.push(h);
      });
      const done = dayEntries.filter(e=>e.status==='done').length;
      const progress = dayEntries.filter(e=>e.status==='progress').length;
      const blocked = dayEntries.filter(e=>e.status==='blocked').length;
      const dateDisplay = new Date(day+'T00:00:00').toLocaleDateString(lang==='ar'?'ar-EG':'en-GB', {weekday:'short', month:'short', day:'numeric'});
      const card=document.createElement('div'); card.className='tag';
      card.innerHTML = `
        <div class="tag-top">
          <div class="tag-name mono">${dateDisplay}</div>
          <div class="tag-dept">${dayEntries.length} ${s.updatesLbl}</div>
        </div>
        <div class="summary-strip" style="margin-top:10px;margin-bottom:0;">
          <div><span class="num mono" style="color:var(--green)">${done}</span><span class="lbl">${s.doneLbl}</span></div>
          <div><span class="num mono" style="color:#8a5c0d">${progress}</span><span class="lbl">${s.progressLbl}</span></div>
          <div><span class="num mono" style="color:var(--red)">${blocked}</span><span class="lbl">${s.blockedLbl}</span></div>
        </div>
      `;
      app.appendChild(card);
    });
  } else {
    const trendCard=document.createElement('div'); trendCard.className='report-card';
    trendCard.innerHTML = `<h3>${s.trendTitle}</h3><p class="hint">${s.weeklyHintMonth}</p>`;
    trendCard.insertAdjacentHTML('beforeend', renderTrendSvg(days));
    app.appendChild(trendCard);
  }

  const noUpdateWorkers = workers.filter(w=>{
    const h = w.history||[];
    return !h.some(x=> days.includes(x.date));
  });

  const section=document.createElement('div'); section.className='dept-group';
  const label=document.createElement('div'); label.className='dept-label'; label.textContent=s.noUpdateWeekLbl;
  section.appendChild(label);
  if(noUpdateWorkers.length===0){
    const p=document.createElement('div'); p.className='logs-empty'; p.textContent=s.allUpdatedLbl;
    section.appendChild(p);
  } else {
    const grid=document.createElement('div'); grid.className='name-grid';
    noUpdateWorkers.forEach(w=>{
      const card=document.createElement('div'); card.className='name-card';
      card.innerHTML = `<span class="status-dot dot-none"></span>${w.name}`;
      grid.appendChild(card);
    });
    section.appendChild(grid);
  }
  app.appendChild(section);

  // ---- Department completion-rate comparison chart ----
  const deptGroups = {};
  workers.forEach(w=>{
    const d = getDeptDisplay(w) || (lang==='ar'?'أخرى':'Other');
    if(!deptGroups[d]) deptGroups[d] = [];
    deptGroups[d].push(w);
  });
  const deptChartItems = Object.keys(deptGroups).map(d=>{
    const list = deptGroups[d];
    let sum=0, count=0;
    list.forEach(w=>{ days.forEach(day=>{ const e=getEntry(w,day); if(e){ sum+=(e.completion||0); count++; } }); });
    const avg = count ? Math.round(sum/count) : 0;
    return {label:d, value:avg, valueLabel:avg+'%'};
  }).sort((a,b)=>b.value-a.value);
  if(deptChartItems.length){
    const deptCard=document.createElement('div'); deptCard.className='report-card';
    deptCard.innerHTML = `<h3>${s.deptCompareTitle}</h3><p class="hint">${s.comparisonHint}</p>` + renderBarChartHTML(deptChartItems);
    app.appendChild(deptCard);
  }

  // ---- Employee performance comparison (ranked) ----
  const empChartItems = workers.map(w=>{
    let sum=0, count=0;
    days.forEach(day=>{ const e=getEntry(w,day); if(e){ sum+=(e.completion||0); count++; } });
    const avg = count ? Math.round(sum/count) : 0;
    return {label:w.name, value:avg, valueLabel:avg+'%'};
  }).filter(x=>x.value>0).sort((a,b)=>b.value-a.value).slice(0,10);
  const compCard=document.createElement('div'); compCard.className='report-card';
  compCard.innerHTML = `<h3>${s.comparisonTitle}</h3><p class="hint">${s.comparisonHint}</p>` + (empChartItems.length ? renderBarChartHTML(empChartItems) : `<div class="logs-empty">${s.noWeeklyTasks}</div>`);
  app.appendChild(compCard);

  // ---- Accounts / payroll helper section ----
  // Requested by the Accounts department: a ready-made hours total per
  // employee (computed from their logged task timers), plus a CSV export
  // button so Accounts can pull it straight into payroll without
  // re-typing anything.
  const payrollCard=document.createElement('div'); payrollCard.className='report-card';
  payrollCard.innerHTML = `<h3>${s.payrollTitle}</h3><p class="hint">${s.payrollHint}</p>`;
  const withHours = workers
    .map(w=>({w, ms: workerWeeklyMs(w, days)}))
    .filter(x=>x.ms>0)
    .sort((a,b)=> b.ms - a.ms);
  if(withHours.length===0){
    payrollCard.insertAdjacentHTML('beforeend', `<div class="logs-empty">${s.payrollEmpty}</div>`);
  } else {
    withHours.forEach(({w,ms})=>{
      payrollCard.insertAdjacentHTML('beforeend', `
        <div class="hours-card">
          <div><div class="hc-name">${w.name}</div><div class="hc-dept">${getDeptDisplay(w)}</div></div>
          <div class="hc-total">${formatHoursShort(ms)} ${lang==='ar'?'س':'h'}</div>
        </div>
      `);
    });
  }
  const exportBtn=document.createElement('button'); exportBtn.className='export-btn'; exportBtn.textContent=s.exportBtn;
  exportBtn.onclick=exportWeeklyCsv;
  payrollCard.appendChild(exportBtn);
  app.appendChild(payrollCard);

  // ---- Expenses section (Accounts) ----
  const expCard=document.createElement('div'); expCard.className='report-card';
  const periodExpenses = expenses.filter(x=> days.includes(localDateKey(new Date(x.createdAt)))).sort((a,b)=>b.createdAt-a.createdAt);
  const expTotal = periodExpenses.reduce((sum,x)=> sum + (parseFloat(x.amount)||0), 0);
  expCard.innerHTML = `
    <h3>${s.expensesTitle}</h3><p class="hint">${s.expensesHint}</p>
    <div class="expense-form">
      <div class="expense-row">
        <input type="text" inputmode="decimal" id="exp-amount" class="expense-input" placeholder="${s.expenseAmountLabel}">
        <select id="exp-category" class="expense-select">
          ${EXPENSE_CATEGORIES.map(c=>`<option value="${c.v}">${c[lang]}</option>`).join('')}
        </select>
      </div>
      <select id="exp-worker" class="expense-select">
        <option value="">${s.expenseWorkerLabel}</option>
        ${workers.map(w=>`<option value="${w.id}">${w.name}</option>`).join('')}
      </select>
      <input type="text" id="exp-note" class="expense-input" placeholder="${s.expenseNotePlaceholder}">
      <button type="button" id="exp-add-btn" class="btn-save">${s.addExpenseBtn}</button>
    </div>
    <div class="expense-total-strip"><span class="et-label">${s.expensesTotal}</span><span class="et-num mono">${expTotal.toLocaleString()} ${lang==='ar'?'ريال':'SAR'}</span></div>
    <div id="expenses-list"></div>
  `;
  app.appendChild(expCard);
  const expListEl = expCard.querySelector('#expenses-list');
  if(periodExpenses.length===0){
    expListEl.innerHTML = `<div class="logs-empty">${s.expensesEmpty}</div>`;
  } else {
    periodExpenses.forEach(x=>{
      const catObj = EXPENSE_CATEGORIES.find(c=>c.v===x.category);
      const catLabel = catObj ? catObj[lang] : x.category;
      const dateDisplay = new Date(x.createdAt).toLocaleDateString(lang==='ar'?'ar-EG':'en-GB');
      const card=document.createElement('div'); card.className='expense-card';
      card.innerHTML = `
        <div class="exp-top">
          <span class="exp-amount">${(parseFloat(x.amount)||0).toLocaleString()} ${lang==='ar'?'ريال':'SAR'}</span>
          <span class="exp-meta mono">${dateDisplay}</span>
        </div>
        <div class="exp-meta">${catLabel}${x.workerName?` · ${x.workerName}`:''}</div>
        ${x.note?`<div class="exp-note">${x.note}</div>`:''}
        <button class="log-del" data-id="${x.id}">${lang==='ar'?'حذف':'Delete'}</button>
      `;
      card.querySelector('.log-del').onclick = async ()=>{ await deleteExpense(x.id); render(); };
      expListEl.appendChild(card);
    });
  }
  expCard.querySelector('#exp-add-btn').onclick = async ()=>{
    const amountInput = expCard.querySelector('#exp-amount');
    const amount = parseFloat(amountInput.value);
    if(!amount || amount<=0){ showToast(lang==='ar'?'اكتب مبلغ صحيح':'Enter a valid amount'); return; }
    const category = expCard.querySelector('#exp-category').value;
    const workerId = expCard.querySelector('#exp-worker').value;
    const workerName = workerId ? (workers.find(w=>w.id===workerId)||{}).name || '' : '';
    const note = expCard.querySelector('#exp-note').value.trim();
    await addExpense({amount, category, workerId, workerName, note});
    showToast(lang==='ar'?'تم إضافة المصروف ✅':'Expense added ✅');
    render();
  };

  const rewardsLabel=document.createElement('div'); rewardsLabel.className='dept-label'; rewardsLabel.style.marginTop='22px'; rewardsLabel.textContent=s.rewardsTitle;
  app.appendChild(rewardsLabel);
  const chooseHint=document.createElement('p'); chooseHint.className='hint'; chooseHint.textContent=s.chooseWorkerHint;
  app.appendChild(chooseHint);

  const pickGrid=document.createElement('div'); pickGrid.className='name-grid';
  workers.forEach(w=>{
    const card=document.createElement('div'); card.className='name-card';
    if(selectedReportWorkerId===w.id){ card.style.background='var(--accent)'; card.style.color='#fff'; card.style.borderColor='var(--accent)'; }
    card.innerHTML = `<span class="status-dot dot-${statusColor(w.status)}"></span>${w.name}`;
    card.onclick=()=>{ selectedReportWorkerId = (selectedReportWorkerId===w.id) ? null : w.id; render(); };
    pickGrid.appendChild(card);
  });
  app.appendChild(pickGrid);

  if(selectedReportWorkerId){
    const w = workers.find(x=>x.id===selectedReportWorkerId);
    if(w){
      const weekTasks = (w.history||[])
        .filter(h=> days.includes(h.date) && h.task)
        .slice().sort((a,b)=> b.date.localeCompare(a.date));
      const tasksHtml = weekTasks.length
        ? `<ul style="margin:8px 0 0;padding-inline-start:18px;">${weekTasks.map(h=>`<li style="margin-bottom:4px;">${h.task} <span class="mono" style="color:var(--steel);font-size:11px;">(${h.date})</span></li>`).join('')}</ul>`
        : `<div class="tag-task empty">${s.noWeeklyTasks}</div>`;

      const workerRewards = weeklyRewards.filter(r=>r.workerId===w.id).sort((a,b)=>b.createdAt-a.createdAt);
      const rewardsHtml = workerRewards.length
        ? workerRewards.map(r=>`
            <div class="log-card" style="margin-top:8px;">
              <div class="log-top"><span class="log-manager mono">${new Date(r.createdAt).toLocaleDateString(lang==='ar'?'ar-EG':'en-GB')}</span></div>
              <div class="log-details">${r.note}</div>
              <button class="log-del" data-id="${r.id}">${lang==='ar'?'حذف':'Delete'}</button>
            </div>
          `).join('')
        : `<div class="logs-empty">${s.rewardHistoryEmpty}</div>`;

      const workerNotes = employeeNotes.filter(n=>n.workerId===w.id).sort((a,b)=>b.createdAt-a.createdAt);
      const notesHtml = workerNotes.length
        ? `<div class="notes-list">${workerNotes.map(n=>`
            <div class="note-card">
              <div class="note-date mono">${new Date(n.createdAt).toLocaleDateString(lang==='ar'?'ar-EG':'en-GB')}</div>
              <div class="note-text">${n.note}</div>
              <button class="log-del" data-id="${n.id}" style="margin-top:6px;">${lang==='ar'?'حذف':'Delete'}</button>
            </div>
          `).join('')}</div>`
        : `<div class="logs-empty">${s.notesEmpty}</div>`;

      const detail=document.createElement('div'); detail.className='tag'; detail.style.marginTop='14px';
      detail.innerHTML = `
        <div class="tag-name">${w.name}</div>
        <div class="tag-dept">${getDeptDisplay(w)}</div>
        <div class="dept-label" style="margin-top:14px;">${s.weeklyTasksTitle}</div>
        ${tasksHtml}
        <div class="dept-label" style="margin-top:16px;">${s.notesTitle}</div>
        <textarea id="note-input" rows="2" placeholder="${s.notesPlaceholder}"></textarea>
        <button id="note-add-btn" class="btn-save" style="width:100%;margin-top:10px;">${s.addNoteBtn}</button>
        ${notesHtml}
        <div class="dept-label" style="margin-top:18px;">${s.rewardLabel}</div>
        <input type="text" id="reward-input" placeholder="${s.rewardPlaceholder}">
        <button id="reward-approve-btn" class="btn-save" style="width:100%;margin-top:10px;">${s.approveRewardBtn}</button>
        <div class="dept-label" style="margin-top:18px;">${s.rewardHistoryTitle}</div>
        ${rewardsHtml}
      `;
      app.appendChild(detail);

      detail.querySelector('#reward-approve-btn').onclick = async ()=>{
        const input = detail.querySelector('#reward-input');
        const note = input.value.trim();
        if(!note){ showToast(lang==='ar' ? 'الرجاء كتابة ملاحظة' : 'Please write a note'); return; }
        await saveReward(w.id, w.name, note);
        showToast(lang==='ar' ? 'تم اعتماد المكافأة ✅' : 'Reward approved ✅');
        render();
      };
      detail.querySelector('#note-add-btn').onclick = async ()=>{
        const input = detail.querySelector('#note-input');
        const note = input.value.trim();
        if(!note){ showToast(lang==='ar' ? 'الرجاء كتابة ملاحظة' : 'Please write a note'); return; }
        await addEmployeeNote(w.id, w.name, note);
        render();
      };
      detail.querySelectorAll('.log-del').forEach(btn=>{
        btn.onclick = async ()=>{
          if(employeeNotes.some(n=>n.id===btn.dataset.id)) await deleteEmployeeNote(btn.dataset.id);
          else await deleteReward(btn.dataset.id);
          render();
        };
      });
    }
  }
}

function renderMunicipalProjects(app){
  const s=t();
  const hint=document.createElement('p'); hint.className='hint'; hint.textContent=s.municipalHint;
  app.appendChild(hint);

  if(municipalProjects.length===0){
    const empty=document.createElement('div'); empty.className='logs-empty'; empty.textContent=s.noProjects;
    app.appendChild(empty);
  } else {
    municipalProjects.forEach(p=>{
      const progress = projectProgress(p);
      const card=document.createElement('div'); card.className='project-card';
      card.innerHTML = `
        <div class="pc-name">${p.name}</div>
        <div class="pc-meta">${p.refNumber?`${s.refNumberLabel.replace(' (اختياري)','').replace(' (optional)','')}: ${p.refNumber}`:''}${p.location?` ${p.refNumber?'· ':''}${p.location}`:''}</div>
        <div class="bar-wrap" style="margin-top:10px;"><div class="bar-fill" style="width:${progress}%;background:var(--accent);"></div></div>
        <div class="tag-foot" style="margin-top:4px;"><span>${s.overallProgress}</span><span>${progress}%</span></div>
        <div class="project-stage-dots">
          ${(p.stages||[]).map(st=>{
            const cls = st.status==='done'?'psd-done':(st.status==='progress'?'psd-progress':'psd-none');
            const icon = st.status==='done'?'✅':(st.status==='progress'?'🔶':'⚪');
            return `<span class="project-stage-dot ${cls}">${icon} ${st.name}</span>`;
          }).join('')}
        </div>
      `;
      card.onclick = ()=> openProjectEditSheet(p.id);
      app.appendChild(card);
    });
  }

  const addBtn=document.createElement('button'); addBtn.className='add-worker-btn'; addBtn.textContent=s.addProjectBtn;
  addBtn.onclick = openAddProject;
  app.appendChild(addBtn);
}

function openAddProject(){
  const s=t();
  const overlay=document.createElement('div'); overlay.className='sheet-overlay';
  const sheet=document.createElement('div'); sheet.className='sheet';
  sheet.innerHTML = `
    <h2>${s.addProjectBtn.replace('+ ','')}</h2>
    <label class="field-label">${s.projectNameLabel}</label>
    <input type="text" id="p-name" placeholder="${s.projectNamePlaceholder}">
    <label class="field-label">${s.refNumberLabel}</label>
    <input type="text" id="p-ref">
    <label class="field-label">${s.locationLabel}</label>
    <input type="text" id="p-loc">
    <div class="sheet-actions">
      <button class="btn-cancel" id="p-cancel">${s.cancel}</button>
      <button class="btn-save" id="p-save">${s.add}</button>
    </div>
  `;
  overlay.appendChild(sheet);
  document.body.appendChild(overlay);
  overlay.onclick=(e)=>{ if(e.target===overlay) overlay.remove(); };
  sheet.querySelector('#p-cancel').onclick=()=>overlay.remove();
  sheet.querySelector('#p-save').onclick=async ()=>{
    const name = sheet.querySelector('#p-name').value.trim();
    if(!name) return;
    const refNumber = sheet.querySelector('#p-ref').value.trim();
    const location = sheet.querySelector('#p-loc').value.trim();
    municipalProjects.push({id:'proj'+Date.now(), name, refNumber, location, notes:'', stages: defaultProjectStages(), createdAt:Date.now()});
    await saveMunicipalProjects();
    overlay.remove();
    render();
  };
}

function openProjectEditSheet(id){
  const s=t();
  const p = municipalProjects.find(x=>x.id===id);
  if(!p) return;
  const overlay=document.createElement('div'); overlay.className='sheet-overlay';
  const sheet=document.createElement('div'); sheet.className='sheet';

  function stagesHtml(){
    return (p.stages||[]).map(st=>`
      <div class="stage-edit-row" data-stage-id="${st.id}">
        <div class="se-top">
          <input type="text" class="st-name-input" value="${st.name}" placeholder="${s.stageNamePlaceholder}">
          <button type="button" class="stage-del-btn" data-stage-id="${st.id}">${s.deleteStageBtn}</button>
        </div>
        <div class="stage-status-btns">
          <button data-v="blocked" class="${st.status==='blocked'||!st.status?'sel-red':''}">${s.statusNotStarted}</button>
          <button data-v="progress" class="${st.status==='progress'?'sel-amber':''}">${s.statusProgress}</button>
          <button data-v="done" class="${st.status==='done'?'sel-green':''}">${s.statusDone}</button>
        </div>
        <input type="text" class="st-date-input" value="${st.date||''}" placeholder="${s.stageDateLabel}" style="margin-bottom:6px;">
        <input type="text" class="st-note-input" value="${st.note||''}" placeholder="${s.stageNoteLabel}">
      </div>
    `).join('');
  }

  sheet.innerHTML = `
    <h2>${p.name}</h2>
    <label class="field-label">${s.projectNameLabel}</label>
    <input type="text" id="p-name" value="${p.name}">
    <label class="field-label">${s.refNumberLabel}</label>
    <input type="text" id="p-ref" value="${p.refNumber||''}">
    <label class="field-label">${s.locationLabel}</label>
    <input type="text" id="p-loc" value="${p.location||''}">
    <label class="field-label">${s.projectNotesLabel}</label>
    <textarea id="p-notes" rows="2">${p.notes||''}</textarea>
    <label class="field-label">${s.stagesLabel}</label>
    <div id="stages-list">${stagesHtml()}</div>
    <button type="button" id="add-stage-btn" class="new-task-btn">${s.addStageBtn}</button>
    <button type="button" id="gen-report-btn" class="btn-save" style="width:100%;margin-top:16px;">${s.generateReportBtn}</button>
    <button type="button" id="p-delete" class="delete-worker-btn">${s.deleteProjectBtn}</button>
    <div class="sheet-actions">
      <button class="btn-cancel" id="p-cancel">${s.cancel}</button>
      <button class="btn-save" id="p-save">${s.save}</button>
    </div>
  `;
  overlay.appendChild(sheet);
  document.body.appendChild(overlay);

  function wireStageHandlers(){
    sheet.querySelectorAll('.stage-status-btns').forEach(wrap=>{
      const row = wrap.closest('.stage-edit-row');
      const stageId = row.dataset.stageId;
      wrap.querySelectorAll('button').forEach(btn=>{
        btn.onclick = ()=>{
          const st = p.stages.find(x=>x.id===stageId);
          st.status = btn.dataset.v==='blocked' ? null : btn.dataset.v;
          wrap.querySelectorAll('button').forEach(b=>b.className='');
          if(!st.status) btn.className='sel-red'; else if(st.status==='progress') btn.className='sel-amber'; else btn.className='sel-green';
        };
      });
    });
    sheet.querySelectorAll('.stage-del-btn').forEach(btn=>{
      btn.onclick = ()=>{
        p.stages = p.stages.filter(x=>x.id!==btn.dataset.stageId);
        sheet.querySelector('#stages-list').innerHTML = stagesHtml();
        wireStageHandlers();
      };
    });
  }
  wireStageHandlers();

  sheet.querySelector('#add-stage-btn').onclick = ()=>{
    p.stages.push({id:'stg'+Date.now()+Math.random().toString(36).slice(2,4), name:'', status:null, date:'', note:''});
    sheet.querySelector('#stages-list').innerHTML = stagesHtml();
    wireStageHandlers();
  };

  overlay.onclick=(e)=>{ if(e.target===overlay) overlay.remove(); };
  sheet.querySelector('#p-cancel').onclick=()=>overlay.remove();

  sheet.querySelector('#gen-report-btn').onclick = ()=>{
    // Sync any unsaved edits in the sheet into the in-memory stage objects
    // before generating the report, so what prints matches what's on screen.
    sheet.querySelectorAll('.stage-edit-row').forEach(row=>{
      const st = p.stages.find(x=>x.id===row.dataset.stageId);
      if(!st) return;
      st.name = row.querySelector('.st-name-input').value.trim() || st.name;
      st.date = row.querySelector('.st-date-input').value.trim();
      st.note = row.querySelector('.st-note-input').value.trim();
    });
    p.name = sheet.querySelector('#p-name').value.trim() || p.name;
    p.refNumber = sheet.querySelector('#p-ref').value.trim();
    p.location = sheet.querySelector('#p-loc').value.trim();
    printOfficialReport(p);
  };

  sheet.querySelector('#p-save').onclick = async ()=>{
    sheet.querySelectorAll('.stage-edit-row').forEach(row=>{
      const st = p.stages.find(x=>x.id===row.dataset.stageId);
      if(!st) return;
      st.name = row.querySelector('.st-name-input').value.trim() || st.name;
      st.date = row.querySelector('.st-date-input').value.trim();
      st.note = row.querySelector('.st-note-input').value.trim();
    });
    p.name = sheet.querySelector('#p-name').value.trim() || p.name;
    p.refNumber = sheet.querySelector('#p-ref').value.trim();
    p.location = sheet.querySelector('#p-loc').value.trim();
    p.notes = sheet.querySelector('#p-notes').value.trim();
    await saveMunicipalProjects();
    overlay.remove();
    render();
  };

  sheet.querySelector('#p-delete').onclick = async ()=>{
    const ok = window.confirm(lang==='ar' ? `حذف مشروع "${p.name}"؟ ما ينرجع بعد الحذف.` : `Delete project "${p.name}"? This cannot be undone.`);
    if(!ok) return;
    municipalProjects = municipalProjects.filter(x=>x.id!==p.id);
    await saveMunicipalProjects();
    overlay.remove();
    render();
  };
}

function printOfficialReport(p){
  const s=t();
  const progress = projectProgress(p);
  const todayDisplay = new Date().toLocaleDateString(lang==='ar'?'ar-EG':'en-GB', {year:'numeric', month:'long', day:'numeric'});
  const rows = (p.stages||[]).map(st=>`
    <tr>
      <td>${st.name}</td>
      <td>${statusLabel(st.status)}</td>
      <td>${st.date||'—'}</td>
      <td>${st.note||'—'}</td>
    </tr>
  `).join('');
  const container = document.getElementById('official-report-print');
  container.innerHTML = `
    <div class="or-header">
      <div>
        <h1>${T[lang].title}</h1>
        <div class="or-sub">${T[lang].sub}</div>
      </div>
      <div class="or-sub">${todayDisplay}</div>
    </div>
    <div class="or-title">${s.officialReportTitle}</div>
    <div class="or-field-grid">
      <div><span class="or-label">${s.projectNameLabel}: </span>${p.name}</div>
      <div><span class="or-label">${s.projectRef}: </span>${p.refNumber||'—'}</div>
      <div><span class="or-label">${s.projectLoc}: </span>${p.location||'—'}</div>
      <div><span class="or-label">${s.overallProgress}: </span>${progress}%</div>
      <div style="grid-column:1/-1;"><span class="or-label">${s.preparedFor}</span></div>
      <div style="grid-column:1/-1;"><span class="or-label">${s.preparedOn}: </span>${todayDisplay}</div>
    </div>
    <table class="or-table">
      <thead><tr><th>${s.stageTableName}</th><th>${s.stageTableStatus}</th><th>${s.stageTableDate}</th><th>${s.stageTableNote}</th></tr></thead>
      <tbody>${rows}</tbody>
    </table>
    ${p.notes ? `<div style="font-size:13px;margin-bottom:20px;"><strong>${s.projectNotesLabel}:</strong> ${p.notes}</div>` : ''}
    <div class="or-signatures">
      <div>${s.signaturePrepared}</div>
      <div>${s.signatureApproved}</div>
    </div>
  `;
  document.body.classList.add('printing-official-report');
  const cleanup = ()=>{ document.body.classList.remove('printing-official-report'); window.removeEventListener('afterprint', cleanup); };
  window.addEventListener('afterprint', cleanup);
  setTimeout(()=>window.print(), 50);
}

function renderInventory(app){
  const s=t();
  const hint=document.createElement('p'); hint.className='hint'; hint.textContent=s.inventoryHint;
  app.appendChild(hint);

  const lowStockItems = inventoryItems.filter(isLowStock);
  if(lowStockItems.length){
    const section=document.createElement('div'); section.className='dept-group';
    const label=document.createElement('div'); label.className='dept-label'; label.textContent=s.lowStockTitle;
    section.appendChild(label);
    const hintEl=document.createElement('p'); hintEl.className='hint'; hintEl.style.margin='0 4px 8px'; hintEl.textContent=s.lowStockHint;
    section.appendChild(hintEl);
    lowStockItems.forEach(item=>{
      const card=document.createElement('div'); card.className='stale-card';
      card.innerHTML = `
        <div><div class="st-name">${item.name}</div><div class="st-dept">${item.category||''}</div></div>
        <div class="st-days" style="color:var(--red);">${item.quantity} ${item.unit}</div>
      `;
      card.onclick=()=>openInventoryItemSheet(item.id);
      section.appendChild(card);
    });
    app.appendChild(section);
  }

  if(inventoryItems.length===0){
    const empty=document.createElement('div'); empty.className='logs-empty'; empty.textContent=s.noItems;
    app.appendChild(empty);
  } else {
    inventoryItems.slice().sort((a,b)=>a.name.localeCompare(b.name, lang==='ar'?'ar':'en')).forEach(item=>{
      const low = isLowStock(item);
      const card=document.createElement('div'); card.className='inv-card'+(low?' low-stock':'');
      card.innerHTML = `
        <div class="inv-top">
          <div><div class="inv-name">${item.name}</div>${item.category?`<div class="inv-cat">${item.category}</div>`:''}</div>
          <div style="text-align:end;"><div class="inv-qty${low?' low':''}">${item.quantity}</div><div class="inv-unit">${item.unit}</div></div>
        </div>
      `;
      card.onclick=()=>openInventoryItemSheet(item.id);
      app.appendChild(card);
    });
  }

  const addBtn=document.createElement('button'); addBtn.className='add-worker-btn'; addBtn.textContent=s.addItemBtn;
  addBtn.onclick = openAddInventoryItem;
  app.appendChild(addBtn);
}

function openAddInventoryItem(){
  const s=t();
  const overlay=document.createElement('div'); overlay.className='sheet-overlay';
  const sheet=document.createElement('div'); sheet.className='sheet';
  sheet.innerHTML = `
    <h2>${s.addItemBtn.replace('+ ','')}</h2>
    <label class="field-label">${s.itemNameLabel}</label>
    <input type="text" id="i-name" placeholder="${s.itemNamePlaceholder}">
    <label class="field-label">${s.itemUnitLabel}</label>
    <input type="text" id="i-unit" placeholder="${s.itemUnitPlaceholder}">
    <label class="field-label">${s.itemQtyLabel}</label>
    <input type="text" id="i-qty" inputmode="decimal" value="0">
    <label class="field-label">${s.itemMinLabel}</label>
    <input type="text" id="i-min" inputmode="decimal" value="0">
    <label class="field-label">${s.itemCategoryLabel}</label>
    <input type="text" id="i-cat">
    <div class="sheet-actions">
      <button class="btn-cancel" id="i-cancel">${s.cancel}</button>
      <button class="btn-save" id="i-save">${s.add}</button>
    </div>
  `;
  overlay.appendChild(sheet);
  document.body.appendChild(overlay);
  overlay.onclick=(e)=>{ if(e.target===overlay) overlay.remove(); };
  sheet.querySelector('#i-cancel').onclick=()=>overlay.remove();
  sheet.querySelector('#i-save').onclick=async ()=>{
    const name = sheet.querySelector('#i-name').value.trim();
    const unit = sheet.querySelector('#i-unit').value.trim();
    if(!name || !unit) return;
    const quantity = parseFloat(sheet.querySelector('#i-qty').value) || 0;
    const minThreshold = parseFloat(sheet.querySelector('#i-min').value) || 0;
    const category = sheet.querySelector('#i-cat').value.trim();
    const newItem = {id:'inv'+Date.now(), name, unit, quantity, minThreshold, category, updatedAt:Date.now()};
    inventoryItems.push(newItem);
    await fsItemSave(INVENTORY_ITEMS_KEY, newItem);
    overlay.remove();
    render();
  };
}

function openInventoryItemSheet(id){
  const s=t();
  const item = inventoryItems.find(x=>x.id===id);
  if(!item) return;
  const overlay=document.createElement('div'); overlay.className='sheet-overlay';
  const sheet=document.createElement('div'); sheet.className='sheet';
  const itemLog = inventoryLog.filter(l=>l.itemId===id).sort((a,b)=>b.createdAt-a.createdAt).slice(0,25);
  const logHtml = itemLog.length
    ? itemLog.map(l=>`
        <div class="movement-row">
          <div><span class="${l.type==='in'?'mv-in':'mv-out'}">${l.type==='in'?'+':'-'}${l.qty} ${item.unit}</span> ${l.type==='in'?s.movementTypeIn:s.movementTypeOut}${l.workerName?` · ${l.workerName}`:''}${l.note?` · ${l.note}`:''}</div>
          <div class="mv-meta mono">${new Date(l.createdAt).toLocaleDateString(lang==='ar'?'ar-EG':'en-GB')}</div>
        </div>
      `).join('')
    : `<div class="logs-empty">${s.movementHistoryEmpty}</div>`;

  sheet.innerHTML = `
    <h2>${item.name}</h2>
    <div class="sub">${item.category||''}</div>
    <div class="tag-foot" style="margin-top:6px;"><span>${s.currentStockLabel}</span><span class="mono" style="font-weight:900;font-size:16px;color:${isLowStock(item)?'var(--red)':'var(--accent)'};">${item.quantity} ${item.unit}</span></div>
    <div class="stock-action-btns">
      <button type="button" id="btn-receive" class="btn-receive">${s.receiveBtn}</button>
      <button type="button" id="btn-issue" class="btn-issue">${s.issueBtn}</button>
    </div>
    <div class="dept-label" style="margin-top:18px;">${s.movementHistoryTitle}</div>
    ${logHtml}
    <button type="button" id="i-delete" class="delete-worker-btn">${s.deleteItemBtn}</button>
    <div class="sheet-actions">
      <button class="btn-cancel" id="i-close" style="flex:1;">${s.cancel}</button>
    </div>
  `;
  overlay.appendChild(sheet);
  document.body.appendChild(overlay);
  overlay.onclick=(e)=>{ if(e.target===overlay) overlay.remove(); };
  sheet.querySelector('#i-close').onclick=()=>overlay.remove();

  function openMovementForm(type){
    const formOverlay=document.createElement('div'); formOverlay.className='sheet-overlay';
    const formSheet=document.createElement('div'); formSheet.className='sheet';
    formSheet.innerHTML = `
      <h2>${type==='in'?s.receiveBtn:s.issueBtn}</h2>
      <div class="sub">${item.name} — ${s.currentStockLabel}: ${item.quantity} ${item.unit}</div>
      <label class="field-label">${s.movementQtyLabel}</label>
      <input type="text" id="mv-qty" inputmode="decimal">
      ${type==='out' ? `
      <label class="field-label">${s.movementWorkerLabel}</label>
      <select id="mv-worker" class="expense-select" style="width:100%;">
        <option value="">${s.noneOption}</option>
        ${workers.map(w=>`<option value="${w.id}">${w.name}</option>`).join('')}
      </select>
      ` : ''}
      <label class="field-label">${s.movementNoteLabel}</label>
      <input type="text" id="mv-note">
      <div class="sheet-actions">
        <button class="btn-cancel" id="mv-cancel">${s.cancel}</button>
        <button class="btn-save" id="mv-save">${s.save}</button>
      </div>
    `;
    formOverlay.appendChild(formSheet);
    document.body.appendChild(formOverlay);
    formOverlay.onclick=(e)=>{ if(e.target===formOverlay) formOverlay.remove(); };
    formSheet.querySelector('#mv-cancel').onclick=()=>formOverlay.remove();
    formSheet.querySelector('#mv-save').onclick=async ()=>{
      const qty = parseFloat(formSheet.querySelector('#mv-qty').value);
      if(!qty || qty<=0){ showToast(s.invalidQty); return; }
      if(type==='out' && qty>item.quantity){ showToast(s.insufficientStock); return; }
      const note = formSheet.querySelector('#mv-note').value.trim();
      const workerSelect = formSheet.querySelector('#mv-worker');
      const workerId = workerSelect ? workerSelect.value : '';
      const workerName = workerId ? (workers.find(w=>w.id===workerId)||{}).name || '' : '';
      await recordStockMovement(item, type, qty, note, workerId, workerName);
      formOverlay.remove();
      overlay.remove();
      showToast('✅');
      render();
    };
  }
  sheet.querySelector('#btn-receive').onclick = ()=>openMovementForm('in');
  sheet.querySelector('#btn-issue').onclick = ()=>openMovementForm('out');

  sheet.querySelector('#i-delete').onclick = async ()=>{
    const ok = window.confirm(lang==='ar' ? `حذف "${item.name}" من المخزون؟ سجل الحركة الخاص فيه بيضل محفوظ.` : `Delete "${item.name}" from inventory? Its movement history stays recorded.`);
    if(!ok) return;
    inventoryItems = inventoryItems.filter(x=>x.id!==item.id);
    await fsItemDelete(INVENTORY_ITEMS_KEY, item.id);
    overlay.remove();
    render();
  };
}

function openEditSheet(id, mode){
  const s=t();
  const w = workers.find(x=>x.id===id);
  if(!w) return;
  const editDate = viewDate;
  const isToday = editDate === todayKey();
  const dayTask = entryTask(w, editDate);
  const dayCompletion = entryCompletion(w, editDate);
  const dayStatus = entryStatus(w, editDate);

  const overlay=document.createElement('div'); overlay.className='sheet-overlay';
  const sheet=document.createElement('div'); sheet.className='sheet';

  if(!isToday){
    // Read-only view of a past day
    const spanningNote = sessionsSpanningDate(w, editDate).map(sess=>{
      const stillRunning = !sess.endedAt;
      const startDate = formatNavDate(localDateKey(new Date(sess.startedAt)));
      return `<div class="tag-timer" style="color:var(--steel);margin-top:8px;">🕐 ${sess.name}${sess.location?` (${sess.location})`:''} — ${stillRunning ? (lang==='ar'?'مستمرة، بدأت':'ongoing since') : (lang==='ar'?'كانت مستمرة، بدأت':'was ongoing, started')} ${startDate}</div>`;
    }).join('');
    sheet.innerHTML = `
      <h2>${w.name}</h2>
      <div class="sub">${getDeptDisplay(w)} — ${formatNavDate(editDate)} · ${lang==='ar'?'للعرض فقط':'Read only'}</div>
      <label class="field-label">${s.taskLabel}</label>
      <div class="tag-task ${dayTask?'':'empty'}" style="background:var(--bg);border-radius:8px;padding:10px 12px;">${dayTask?dayTask:s.noTask}</div>
      ${spanningNote}
      <label class="field-label" style="margin-top:14px;">${s.completionLabel}</label>
      <div class="bar-wrap"><div class="bar-fill" style="width:${dayCompletion}%; background:var(--${statusColor(dayStatus)==='none'?'steel':statusColor(dayStatus)})"></div></div>
      <div class="tag-foot" style="margin-top:6px;"><span>${dayCompletion}${s.pctSuffix}</span></div>
      <label class="field-label" style="margin-top:14px;">${s.statusLabel}</label>
      <div class="tag-badge badge-${statusColor(dayStatus)}" style="display:inline-block;">${statusLabel(dayStatus)}</div>
      ${mode==='admin' ? `<button type="button" id="admin-del-day-btn" class="day-del-btn">${lang==='ar'?'🗑️ حذف سجل هذا اليوم بالكامل':"🗑️ Delete this whole day's record"}</button>` : ''}
      <div class="sheet-actions">
        <button class="btn-cancel" id="f-cancel" style="flex:1;">${s.cancel}</button>
      </div>
    `;
    overlay.appendChild(sheet);
    document.body.appendChild(overlay);
    sheet.querySelector('#f-cancel').onclick=()=>overlay.remove();
    overlay.onclick=(e)=>{ if(e.target===overlay) overlay.remove(); };
    if(mode==='admin'){
      const delDayBtn = sheet.querySelector('#admin-del-day-btn');
      if(delDayBtn){
        delDayBtn.onclick = async ()=>{
          const msg = lang==='ar'
‎            ? `حذف سجل ${w.name} ليوم ${formatNavDate(editDate)} بالكامل؟ ما ينرجع بعد الحذف.`
            : `Delete ${w.name}'s entire record for ${formatNavDate(editDate)}? This cannot be undone.`;
          const ok = window.confirm(msg);
          if(!ok) return;
          adminDeleteHistoryDay(w, editDate);
          await saveOneWorkerOrWarn(w);
          overlay.remove();
          render();
          showToast(lang==='ar' ? 'تم حذف سجل اليوم ✅' : "Day's record deleted ✅");
        };
      }
    }
    return;
  }

  const activeSessions = getActiveSessions(w);
  const todaySessions = (w.taskSessions||[]).filter(x=>x.date===todayKey());

  // Personal workspace: a compact "your week" summary shown only to the
  // employee themselves — purely additive, doesn't touch or change any
  // existing admin/report behavior. Gives workers their own visibility
  // into their week without needing to ask the manager.
  const myWeekDays = getLastNDates(7);
  const myWeekMs = workerWeeklyMs(w, myWeekDays);
  const myDoneDays = myWeekDays.filter(d=>entryStatus(w,d)==='done').length;
  const myTaskCount = (w.taskSessions||[]).filter(sess=> myWeekDays.includes(sess.date)).length;

  sheet.innerHTML = `
    <h2>${w.name}</h2>
    <div class="sub">${getDeptDisplay(w)}</div>
    ${mode==='worker' ? `
    <div class="report-card" style="padding:14px 16px;margin-top:12px;margin-bottom:0;">
      <h3 style="font-size:13.5px;">${s.myStatsTitle}</h3>
      <div class="summary-strip" style="margin-top:10px;margin-bottom:0;">
        <div><span class="num mono" style="color:var(--accent)">${formatHoursShort(myWeekMs)}</span><span class="lbl">${s.myStatsHours}</span></div>
        <div><span class="num mono" style="color:var(--green)">${myDoneDays}</span><span class="lbl">${s.myStatsDone}</span></div>
        <div><span class="num mono" style="color:var(--steel)">${myTaskCount}</span><span class="lbl">${s.myStatsTasks}</span></div>
      </div>
    </div>
    ` : ''}
    ${mode==='admin' && w.subAssignedTask ? `
    <div class="sub-task-note" style="margin-top:14px;">📌 ${w.subAssignedBy ? (lang==='ar'?`مهمة من ${w.subAssignedBy}`:`Task from ${w.subAssignedBy}`) : s.subTaskAdminNote}: ${w.subAssignedTask}</div>
    ` : ''}
    ${mode==='admin' ? `
    <label class="field-label">${s.assignedTaskLabel}</label>
    <textarea id="f-assigned" rows="2" placeholder="${s.assignedTaskPlaceholder}">${w.assignedTask||''}</textarea>
    ` : (w.assignedTask ? `
    <label class="field-label">${s.assignedTaskDisplayLabel}</label>
    <div class="tag-task" style="background:rgba(232,89,12,0.08);border:1px solid var(--accent);border-radius:8px;padding:10px 12px;">${w.assignedTask}</div>
    ` : '')}
    ${mode==='worker' && w.subAssignedTask ? `
    <label class="field-label">${w.subAssignedBy ? (lang==='ar'?`مهمة من ${w.subAssignedBy}`:`Task from ${w.subAssignedBy}`) : s.subTaskDisplayLabel}</label>
    <div class="tag-task" style="background:rgba(63,143,95,.08);border:1px solid var(--green);border-radius:8px;padding:10px 12px;">${w.subAssignedTask}</div>
    ` : ''}
    <label class="field-label">${lang==='ar'?`المهام الشغالة الآن${activeSessions.length?` (${activeSessions.length})`:''}`:`Running now${activeSessions.length?` (${activeSessions.length})`:''}`}</label>
    ${activeSessions.length ? activeSessions.map(sess=>`
    <div class="active-task-box" data-session-id="${sess.id}">
      ${mode==='admin' ? `<button type="button" class="active-task-del admin-del-session-btn" data-session-id="${sess.id}" title="${lang==='ar'?'حذف هذي المهمة':'Delete this task'}">🗑️</button>` : ''}
      <div class="active-task-name">${sess.name}</div>
      ${sess.location?`<div class="active-task-loc">📍 ${sess.location}</div>`:''}
      ${sess.photos && sess.photos.length ? `<div class="sr-photos" style="justify-content:center;">${sess.photos.map((p,pi)=>`<div class="sr-photo-wrap"><img src="${p}">${mode==='admin'?`<button type="button" class="sr-photo-del admin-del-photo-btn" data-session-id="${sess.id}" data-photo-i="${pi}">×</button>`:''}</div>`).join('')}</div>` : ''}
      ${sess.gps ? `<div style="text-align:center;margin-top:6px;">${gpsLine(sess.gps)}</div>` : ''}
      <div class="active-task-clock mono active-clock" data-session-id="${sess.id}">${formatHMS(Date.now()-sess.startedAt)}</div>
      <button type="button" class="active-task-finish finish-active-btn" data-session-id="${sess.id}">${lang==='ar'?'⏹ إنهاء هذي المهمة':'⏹ Finish this task'}</button>
    </div>
    `).join('') : `<div class="tag-task empty">${lang==='ar'?'لا توجد مهمة شغالة حالياً':'No task running right now'}</div>`}
    <button type="button" id="new-task-toggle" class="new-task-btn">${lang==='ar'?'+ بدء مهمة جديدة':'+ Start new task'}</button>
    <div class="new-task-form" id="new-task-form">
      <div style="font-size:12px;color:var(--steel);margin-bottom:8px;">${lang==='ar'?'ما توقف باقي المهام الشغالة':"Won't stop other running tasks"}</div>
      <label class="field-label" style="margin-top:0;">${lang==='ar'?'اسم المهمة':'Task name'}</label>
      <select id="nt-name-select">
        <option value="">${s.categoryPlaceholder}</option>
        ${getCategoriesForWorker(w).map(c=>`<option value="${c.v}">${c[lang]}</option>`).join('')}
      </select>
      <input type="text" id="nt-name-other" placeholder="${s.categoryOtherPlaceholder}" style="margin-top:8px;display:none;">
      <label class="field-label">${lang==='ar'?'الموقع أو رقم الغرفة (اختياري)':'Location / room number (optional)'}</label>
      <input type="text" id="nt-loc" placeholder="${lang==='ar'?'مثال: Zone 1':'e.g. Zone 1'}">
      <div style="font-size:11.5px;color:var(--steel);margin-top:6px;">${lang==='ar'?'📍 راح ناخذ موقعك الجغرافي تلقائياً عند الضغط على "بدء" (لازم توافق على إذن الموقع من المتصفح)':'📍 Your GPS location is captured automatically when you tap "Start" (browser will ask for location permission)'}</div>
      <button type="button" id="photo-btn" class="photo-btn">📷 <span id="photo-count">0/3</span></button>
      <input type="file" id="photo-input" accept="image/*" multiple capture="environment" style="display:none;">
      <button type="button" id="nt-start-btn" class="btn-save" style="width:100%;margin-top:12px;">${s.tbStart}</button>
    </div>
    ${todaySessions.length ? `
    <div class="session-log">
      ${todaySessions.slice().reverse().map(sess=>`
        <div class="session-row" style="flex-direction:column;align-items:stretch;">
          <div style="display:flex;justify-content:space-between;align-items:center;">
            <div><div class="sr-name">${sess.name}</div>${sess.location?`<div class="sr-loc">📍 ${sess.location}</div>`:''}</div>
            <div style="display:flex;align-items:center;gap:8px;">
              <div class="sr-dur">${formatHMS(sess.endedAt ? (sess.endedAt-sess.startedAt) : (Date.now()-sess.startedAt))}</div>
              ${mode==='admin' ? `<button type="button" class="session-del-btn admin-del-session-btn" data-session-id="${sess.id}">${lang==='ar'?'حذف':'Delete'}</button>` : ''}
            </div>
          </div>
          ${sess.photos && sess.photos.length ? `<div class="sr-photos">${sess.photos.map((p,pi)=>`<div class="sr-photo-wrap"><img src="${p}">${mode==='admin'?`<button type="button" class="sr-photo-del admin-del-photo-btn" data-session-id="${sess.id}" data-photo-i="${pi}">×</button>`:''}</div>`).join('')}</div>` : ''}
          ${sess.gps ? `<div style="margin-top:4px;">${gpsLine(sess.gps)}</div>` : ''}
        </div>
      `).join('')}
    </div>
    ` : ''}
    <label class="field-label">${s.completionLabel}</label>
    <div class="pct-row">
      <input type="range" id="f-pct" min="0" max="100" step="5" value="${dayCompletion}">
      <div class="pct-num mono" id="f-pct-val">${dayCompletion}%</div>
    </div>
    <label class="field-label">${s.statusLabel}</label>
    <div class="status-btns" id="f-status">
      <button data-v="blocked" class="${dayStatus==='blocked'?'sel-red':''}">${s.statusNotStarted}</button>
      <button data-v="progress" class="${dayStatus==='progress'?'sel-amber':''}">${s.statusProgress}</button>
      <button data-v="done" class="${dayStatus==='done'?'sel-green':''}">${s.statusDone}</button>
    </div>
    ${mode==='admin' ? `
    <label class="field-label">${s.nameLabel}</label>
    <input type="text" id="f-name" value="${w.name}">
    <label class="field-label">${s.deptLabel}</label>
    <select id="f-dept-select">
      ${Object.keys(DEPTS).map(k=>`<option value="${k}" ${w.deptKey===k?'selected':''}>${DEPTS[k][lang]}</option>`).join('')}
      <option value="__other__" ${!w.deptKey?'selected':''}>${lang==='ar'?'أخرى / حدد بنفسك':'Other / specify'}</option>
    </select>
    <input type="text" id="f-dept-other" value="${!w.deptKey?(w.deptCustom||''):''}" placeholder="${lang==='ar'?'اكتب المسمى الوظيفي':'Write the job title'}" style="margin-top:8px;display:${!w.deptKey?'block':'none'};">
    <label class="field-label">${s.phoneLabel}</label>
    <input type="text" id="f-phone" value="${w.phone||''}" placeholder="${s.phonePlaceholder}" inputmode="tel">
    <label class="field-label">${s.passwordLabel}</label>
    <div class="pct-row">
      <input type="text" id="f-password" value="${w.password || DEFAULT_PASSWORD}" placeholder="${s.passwordPlaceholder}" style="flex:1;">
      <button type="button" id="f-regen" class="photo-btn" style="margin-top:0;">🔄 ${lang==='ar'?'رمز جديد':'New code'}</button>
    </div>
    <button type="button" id="admin-del-day-btn" class="day-del-btn">${lang==='ar'?'🗑️ حذف سجل اليوم لهذا الموظف':"🗑️ Delete today's record for this employee"}</button>
    <button type="button" id="f-delete" class="delete-worker-btn">${s.deleteWorkerBtn}</button>
    <button type="button" id="f-clear-data" class="delete-worker-btn" style="border-color:var(--amber);color:#8a5c0d;margin-top:10px;">${lang==='ar'?'🧹 مسح كل سجل شغل هذا الموظف':"🧹 Clear all this employee's work log"}</button>
    ` : ''}
    <div class="sheet-actions">
      <button class="btn-cancel" id="f-cancel">${s.cancel}</button>
      <button class="btn-save" id="f-save">${s.save}</button>
    </div>
  `;
  overlay.appendChild(sheet);
  document.body.appendChild(overlay);

  // Live-ticking clocks for every active session while the sheet is open
  const clockInterval = setInterval(()=>{
    sheet.querySelectorAll('.active-clock').forEach(el=>{
      const sess = (w.taskSessions||[]).find(x=>x.id===el.dataset.sessionId);
      if(sess && !sess.endedAt) el.textContent = formatHMS(Date.now()-sess.startedAt);
    });
  }, 1000);
  const stopTicking = ()=> clearInterval(clockInterval);

  const newTaskToggle = sheet.querySelector('#new-task-toggle');
  const newTaskForm = sheet.querySelector('#new-task-form');
  newTaskToggle.onclick = ()=> newTaskForm.classList.toggle('open');

  const deptSelect = sheet.querySelector('#f-dept-select');
  if(deptSelect){
    const deptOther = sheet.querySelector('#f-dept-other');
    deptSelect.onchange = ()=>{ deptOther.style.display = (deptSelect.value==='__other__') ? 'block' : 'none'; };
  }
  const regenBtn = sheet.querySelector('#f-regen');
  if(regenBtn){
    regenBtn.onclick = ()=>{ sheet.querySelector('#f-password').value = generateUniqueCode(); };
  }

  // Admin-only: delete an individual task/session (works for both a still-
  // running session and one already finished today).
  if(mode==='admin'){
    sheet.querySelectorAll('.admin-del-session-btn').forEach(btn=>{
      btn.onclick = async (e)=>{
        e.stopPropagation();
        const sessionId = btn.dataset.sessionId;
        const sess = (w.taskSessions||[]).find(x=>x.id===sessionId);
        const label = sess ? sess.name : '';
        const ok = window.confirm(lang==='ar' ? `حذف مهمة "${label}"؟ ما ينرجع بعد الحذف.` : `Delete task "${label}"? This cannot be undone.`);
        if(!ok) return;
        adminDeleteSession(w, sessionId);
        const saved = await saveOneWorkerOrWarn(w);
        if(!saved) return;
        stopTicking();
        overlay.remove();
        openEditSheet(id, mode);
        render();
        showToast(lang==='ar' ? 'تم حذف المهمة ✅' : 'Task deleted ✅');
      };
    });
    // Admin-only: delete a single photo out of a session's photo list.
    sheet.querySelectorAll('.admin-del-photo-btn').forEach(btn=>{
      btn.onclick = async (e)=>{
        e.stopPropagation();
        const sessionId = btn.dataset.sessionId;
        const photoI = parseInt(btn.dataset.photoI,10);
        adminDeletePhoto(w, sessionId, photoI);
        const saved = await saveOneWorkerOrWarn(w);
        if(!saved) return;
        stopTicking();
        overlay.remove();
        openEditSheet(id, mode);
        render();
      };
    });
    // Admin-only: delete this employee's ENTIRE record for today (all of
    // today's sessions + today's history entry), separate from the
    // "clear all history / all days" button further down.
    const delTodayBtn = sheet.querySelector('#admin-del-day-btn');
    if(delTodayBtn){
      delTodayBtn.onclick = async ()=>{
        const msg = lang==='ar'
‎          ? `حذف سجل ${w.name} لهذا اليوم بالكامل (كل المهام والصور)؟ ما ينرجع بعد الحذف.`
          : `Delete ${w.name}'s entire record for today (all tasks and photos)? This cannot be undone.`;
        const ok = window.confirm(msg);
        if(!ok) return;
        adminDeleteHistoryDay(w, todayKey());
        const saved = await saveOneWorkerOrWarn(w);
        if(!saved) return;
        stopTicking();
        overlay.remove();
        render();
        showToast(lang==='ar' ? "تم حذف سجل اليوم ✅" : "Today's record deleted ✅");
      };
    }
  }

  const ntSelect = sheet.querySelector('#nt-name-select');
  const ntOther = sheet.querySelector('#nt-name-other');
  const ntCategories = getCategoriesForWorker(w);
  ntSelect.onchange = ()=>{ ntOther.style.display = (ntSelect.value==='other') ? 'block' : 'none'; };

  let pendingPhotos = [];
  const photoBtn = sheet.querySelector('#photo-btn');
  const photoInput = sheet.querySelector('#photo-input');
  const photoCountEl = sheet.querySelector('#photo-count');
  const updatePhotoCount = ()=>{ photoCountEl.textContent = `${pendingPhotos.length}/3`; };
  photoInput.onchange = async ()=>{
    const files = Array.from(photoInput.files||[]).slice(0, 3-pendingPhotos.length);
    for(const f of files){
      try{ pendingPhotos.push(await compressImageFile(f)); }catch(e){}
    }
    photoInput.value='';
    updatePhotoCount();
    renderPhotoPopup();
  };
  let photoPopupOverlay = null;
  function renderPhotoPopup(){
    if(!photoPopupOverlay) return;
    const popup = photoPopupOverlay.querySelector('.photo-popup');
    popup.innerHTML = `
      <h3>${lang==='ar'?'صور المهمة (حتى 3)':'Task photos (up to 3)'}</h3>
      <div class="photo-thumbs">
        ${pendingPhotos.map((p,i)=>`<div class="photo-thumb"><img src="${p}"><button type="button" class="pt-del" data-i="${i}">×</button></div>`).join('')}
        ${pendingPhotos.length<3 ? `<button type="button" class="photo-add-btn" id="pp-add">+</button>` : ''}
      </div>
      <button type="button" class="btn-cancel" id="pp-close" style="width:100%;">${lang==='ar'?'إغلاق':'Close'}</button>
    `;
    popup.querySelectorAll('.pt-del').forEach(btn=>{
      btn.onclick=()=>{ pendingPhotos.splice(parseInt(btn.dataset.i,10),1); updatePhotoCount(); renderPhotoPopup(); };
    });
    const addBtn = popup.querySelector('#pp-add');
    if(addBtn) addBtn.onclick = ()=> photoInput.click();
    popup.querySelector('#pp-close').onclick = ()=>{ photoPopupOverlay.remove(); photoPopupOverlay=null; };
  }
  photoBtn.onclick = ()=>{
    photoPopupOverlay = document.createElement('div');
    photoPopupOverlay.className = 'photo-popup-overlay';
    const popup = document.createElement('div'); popup.className='photo-popup';
    photoPopupOverlay.appendChild(popup);
    document.body.appendChild(photoPopupOverlay);
    photoPopupOverlay.onclick=(e)=>{ if(e.target===photoPopupOverlay){ photoPopupOverlay.remove(); photoPopupOverlay=null; } };
    renderPhotoPopup();
  };

  sheet.querySelectorAll('.finish-active-btn').forEach(btn=>{
    btn.onclick = async ()=>{
      finishSession(w, btn.dataset.sessionId);
      const ok = await saveOneWorkerOrWarn(w);
      if(!ok) return; // keep the sheet open so nothing already typed is lost
      stopTicking();
      overlay.remove();
      openEditSheet(id, mode);
      render();
    };
  });

  sheet.querySelector('#nt-start-btn').onclick = async ()=>{
    const catValue = ntSelect.value;
    if(!catValue){ showToast(lang==='ar'?'اختر المهمة':'Select a task'); return; }
    const catObj = ntCategories.find(c=>c.v===catValue);
    const name = catValue==='other' ? ntOther.value.trim() : (catObj ? catObj[lang] : '');
    if(!name){ showToast(lang==='ar'?'اكتب اسم المهمة':'Enter a task name'); return; }
    const loc = sheet.querySelector('#nt-loc').value.trim();
    const startBtn = sheet.querySelector('#nt-start-btn');
    const originalLabel = startBtn.textContent;
    startBtn.disabled = true;
    startBtn.textContent = lang==='ar' ? '📍 جاري تحديد الموقع...' : '📍 Getting location...';
    const gps = await getGpsLocation();
    startBtn.disabled = false;
    startBtn.textContent = originalLabel;
    startNewSession(w, name, loc, pendingPhotos, gps);
    const ok = await saveOneWorkerOrWarn(w);
    if(!ok) return; // keep the sheet open so the employee can retry immediately
    stopTicking();
    overlay.remove();
    openEditSheet(id, mode);
    render();
  };

  let chosenStatus=dayStatus;
  const statusWrap=sheet.querySelector('#f-status');
  statusWrap.querySelectorAll('button').forEach(btn=>{
    btn.onclick=()=>{
      chosenStatus=btn.dataset.v;
      statusWrap.querySelectorAll('button').forEach(b=>b.className='');
      if(chosenStatus==='blocked') btn.className='sel-red';
      if(chosenStatus==='progress') btn.className='sel-amber';
      if(chosenStatus==='done') btn.className='sel-green';
    };
  });
  const pctInput=sheet.querySelector('#f-pct');
  const pctVal=sheet.querySelector('#f-pct-val');
  pctInput.oninput=()=>{ pctVal.textContent=pctInput.value+'%'; };
  sheet.querySelector('#f-cancel').onclick=()=>{ stopTicking(); overlay.remove(); };
  overlay.onclick=(e)=>{ if(e.target===overlay){ stopTicking(); overlay.remove(); } };
  sheet.querySelector('#f-save').onclick=async ()=>{
    const newCompletion=parseInt(pctInput.value,10);
    const newStatus=chosenStatus;
    const now=Date.now();
    if(mode==='admin'){
      w.name=sheet.querySelector('#f-name').value.trim()||w.name;
      const deptChoice = sheet.querySelector('#f-dept-select').value;
      if(deptChoice==='__other__'){
        w.deptKey = null;
        w.deptCustom = sheet.querySelector('#f-dept-other').value.trim();
      } else {
        w.deptKey = deptChoice;
        w.deptCustom = '';
      }
      w.phone=sheet.querySelector('#f-phone').value.trim();
      w.assignedTask=sheet.querySelector('#f-assigned').value.trim();
      const newPass = sheet.querySelector('#f-password').value.trim();
      w.password = newPass || generateUniqueCode();
      w.uniqueCodeAssigned = true;
    }

    // Task name/duration are managed by the +/Finish session buttons above —
    // Save here only records completion % and status, leaving the task text as-is.
    const entry = ensureTodayEntry(w);
    entry.completion = newCompletion;
    entry.status = newStatus;
    entry.ts = now;
    const ok = await saveOneWorkerOrWarn(w);
    if(!ok) return; // keep the sheet open so the entered values aren't lost
    stopTicking();
    overlay.remove();
    render();
    if(mode==='admin') showToast(lang==='ar' ? `✅ تم الحفظ — التغييرات (وأي كلمة مرور جديدة) وصلت لكل الأجهزة الآن` : `✅ Saved — changes (including any new password) are now on every device`);
  };
  if(mode==='admin'){
    sheet.querySelector('#f-delete').onclick=async ()=>{
      const ok = window.confirm(s.deleteWorkerConfirm.replace('{name}', w.name));
      if(!ok) return;
      const deletedId = w.id;
      const deletedName = w.name;
      workers = workers.filter(x=>x.id!==deletedId);
      try{
        const rawSeed = await storageGet('seeded-defaults', true);
        let seeded = rawSeed ? JSON.parse(rawSeed) : [];
        const key = deletedName.trim().toLowerCase();
        if(!seeded.includes(key)) seeded.push(key);
        await storageSet('seeded-defaults', JSON.stringify(seeded), true);
      }catch(e){}

      // The employee's Firestore document must be explicitly deleted — it
      // lives in its own document (collection "workers"), so this only
      // ever touches that one document and never re-writes anyone else's
      // (re-writing every remaining employee here used to risk overwriting
      // another device's more recent changes with this device's stale
      // copy — the same class of bug explained above). Delete it directly,
      // then verify by re-reading that exact document rather than
      // trusting the in-memory array.
      await fsWorkerDelete(deletedId);

      let verified = false;
      try{ verified = !(await fsWorkerGet(deletedId)); }catch(e){ verified = false; }

      if(!verified){
        // Retry once more before giving up
        await fsWorkerDelete(deletedId);
        try{ verified = !(await fsWorkerGet(deletedId)); }catch(e){ verified = false; }
      }

      if(!verified){
        window.alert(lang==='ar'
‎          ? `⚠️ تنبيه: حذف ${deletedName} ما انحفظ فعلياً رغم إنه اختفى من الشاشة! جرب مرة ثانية بعد شوي — لو استمرت المشكلة قد يكون في اتصال بالإنترنت.`
          : `⚠️ Warning: deleting ${deletedName} did NOT actually save even though it disappeared from screen! Try again shortly — if this keeps happening it may be a connectivity issue.`
        );
      }

      stopTicking();
      overlay.remove();
      render();
    };
    sheet.querySelector('#f-clear-data').onclick=async ()=>{
      const msg = lang==='ar'
‎        ? `مسح كل سجل الشغل والمهام والوقت لـ ${w.name} (كل الأيام)؟ الاسم ورقمه وكلمة مروره ما راح تتأثر. ما ينرجع بعد ما تمسحه.`
        : `Clear ALL work log, tasks, and time for ${w.name} (every day)? Name, phone, and password stay untouched. This can't be undone.`;
      const ok = window.confirm(msg);
      if(!ok) return;
      clearAllWorkData(w);
      const saved = await saveOneWorkerOrWarn(w);
      if(!saved) return;
      stopTicking();
      overlay.remove();
      openEditSheet(id, mode);
      render();
      showToast(lang==='ar' ? `تم مسح سجل ${w.name} ✅` : `Cleared ${w.name}'s log ✅`);
    };
  }
}

function openHistorySheet(id){
  const s=t();
  const w = workers.find(x=>x.id===id);
  if(!w) return;
  const overlay=document.createElement('div'); overlay.className='sheet-overlay';
  const sheet=document.createElement('div'); sheet.className='sheet';

  function historyRows(){
    const history = (w.history||[]).slice().sort((a,b)=> b.date.localeCompare(a.date));
    if(!history.length) return `<div class="logs-empty">${s.historyEmpty}</div>`;
    return history.map(h=>{
      const color = statusColor(h.status);
      const dateDisplay = new Date(h.date+'T00:00:00').toLocaleDateString(lang==='ar'?'ar-EG':'en-GB', {weekday:'short', year:'numeric', month:'short', day:'numeric'});
      const daySessions = sessionsSpanningDate(w, h.date).filter(sess=>sess.gps);
      const gpsRows = daySessions.length ? `<div style="margin-top:6px;display:flex;flex-direction:column;gap:4px;">${daySessions.map(sess=>gpsLine(sess.gps)).join('')}</div>` : '';
      return `
        <div class="log-card" data-day="${h.date}">
          <div class="log-top">
            <span class="log-manager mono">${dateDisplay}</span>
            <span class="tag-badge badge-${color}">${statusLabel(h.status)}</span>
          </div>
          <div class="log-details">${h.task ? h.task : s.noTask}</div>
          <div class="tag-foot" style="margin-top:8px;"><span>${h.completion}${s.pctSuffix}</span></div>
          ${h.durationMs ? `<div class="tag-foot" style="margin-top:2px;"><span>${s.durationLabel}: ${durationText(h.durationMs)}</span></div>` : ''}
          ${gpsRows}
          <button type="button" class="day-del-btn admin-del-day-btn" data-day="${h.date}">${lang==='ar'?'🗑️ حذف سجل هذا اليوم':"🗑️ Delete this day's record"}</button>
        </div>
      `;
    }).join('');
  }

  sheet.innerHTML = `
    <h2>${s.historyTitle} — ${w.name}</h2>
    <div class="sub">${getDeptDisplay(w)}</div>
    <div class="logs-grid" id="history-rows" style="margin-top:12px;">${historyRows()}</div>
    <div class="sheet-actions">
      <button class="btn-cancel" id="h-close" style="flex:1;">${s.cancel}</button>
    </div>
  `;
  overlay.appendChild(sheet);
  document.body.appendChild(overlay);
  overlay.onclick=(e)=>{ if(e.target===overlay) overlay.remove(); };
  sheet.querySelector('#h-close').onclick=()=>overlay.remove();

  function wireDeleteButtons(){
    sheet.querySelectorAll('.admin-del-day-btn').forEach(btn=>{
      btn.onclick = async ()=>{
        const day = btn.dataset.day;
        const dateDisplay = new Date(day+'T00:00:00').toLocaleDateString(lang==='ar'?'ar-EG':'en-GB', {weekday:'short', year:'numeric', month:'short', day:'numeric'});
        const ok = window.confirm(lang==='ar' ? `حذف سجل ${w.name} ليوم ${dateDisplay}؟ ما ينرجع بعد الحذف.` : `Delete ${w.name}'s record for ${dateDisplay}? This cannot be undone.`);
        if(!ok) return;
        adminDeleteHistoryDay(w, day);
        const saved = await saveOneWorkerOrWarn(w);
        if(!saved) return;
        sheet.querySelector('#history-rows').innerHTML = historyRows();
        wireDeleteButtons();
        render();
        showToast(lang==='ar' ? 'تم حذف سجل اليوم ✅' : "Day's record deleted ✅");
      };
    });
  }
  wireDeleteButtons();
}

function renderAssignGate(app){
  const s=t();
  app.innerHTML = `
    <div class="pin-wrap">
      <div class="pin-lock">📌</div>
      <h2 style="margin:0 0 4px;">${s.assignPinTitle}</h2>
      <p class="hint" style="margin:0;">${s.assignPinSub}</p>
      <div><input type="password" id="assignPinInput" inputmode="numeric" maxlength="8" placeholder="${s.pinPlaceholder}"></div>
      <button class="pin-submit" id="assignPinSubmit">${s.pinSubmit}</button>
      <div class="pin-err" id="assignPinErr"></div>
    </div>
  `;
  const input = document.getElementById('assignPinInput');
  const tryUnlock = ()=>{
    if(input.value === SUB_PIN){ assignUnlocked = true; render(); }
    else { document.getElementById('assignPinErr').textContent = s.pinErr; input.value=''; input.focus(); }
  };
  document.getElementById('assignPinSubmit').onclick = tryUnlock;
  input.onkeydown = (e)=>{ if(e.key==='Enter') tryUnlock(); };
}

function renderAssignPanel(app){
  const s=t();
  const hint=document.createElement('p'); hint.className='hint'; hint.textContent=s.assignHint;
  app.appendChild(hint);
  const groups = groupByDept(workers);
  Object.keys(groups).forEach(dept=>{
    const section=document.createElement('div'); section.className='dept-group';
    const label=document.createElement('div'); label.className='dept-label'; label.textContent=dept;
    section.appendChild(label);
    const grid=document.createElement('div'); grid.className='name-grid';
    groups[dept].forEach(w=>{
      const card=document.createElement('div'); card.className='name-card';
      card.innerHTML = `${w.subAssignedTask?'📌 ':''}${w.name}`;
      card.onclick=()=>openAssignEditSheet(w.id);
      grid.appendChild(card);
    });
    section.appendChild(grid);
    app.appendChild(section);
  });
}

function openAssignEditSheet(id){
  const s=t();
  const w = workers.find(x=>x.id===id);
  if(!w) return;
  const overlay=document.createElement('div'); overlay.className='sheet-overlay';
  const sheet=document.createElement('div'); sheet.className='sheet';
  const initialBy = w.subAssignedBy || 'Silvano';
  // Deliberately minimal: this panel only ever reads/writes subAssignedTask/subAssignedBy —
  // it never touches or displays assignedTask (the manager's own assignments),
  // status, completion, or history, so this role can't see what managers give.
  sheet.innerHTML = `
    <h2>${w.name}</h2>
    <div class="sub">${getDeptDisplay(w)}</div>
    <label class="field-label">${lang==='ar'?'اسمك (سيظهر مع المهمة)':'Your name (shown with the task)'}</label>
    <input type="text" id="a-by" value="${initialBy}" placeholder="Silvano">
    <label class="field-label">${s.subTaskLabel}</label>
    <textarea id="a-task" rows="3" placeholder="${s.subTaskPlaceholder}">${w.subAssignedTask||''}</textarea>
    <div class="sheet-actions">
      <button class="btn-cancel" id="a-cancel">${s.cancel}</button>
      <button class="btn-save" id="a-save">${s.save}</button>
    </div>
  `;
  overlay.appendChild(sheet);
  document.body.appendChild(overlay);
  // Personal per-device convenience: prefill "your name" from what this
  // device used last time, without blocking the sheet from opening.
  getUserData('assign-default-name', false).then(saved=>{
    if(saved && !w.subAssignedBy){ const inp = sheet.querySelector('#a-by'); if(inp) inp.value = saved; }
  });
  sheet.querySelector('#a-cancel').onclick=()=>overlay.remove();
  overlay.onclick=(e)=>{ if(e.target===overlay) overlay.remove(); };
  sheet.querySelector('#a-save').onclick=async ()=>{
    const byName = sheet.querySelector('#a-by').value.trim() || 'Silvano';
    w.subAssignedTask = sheet.querySelector('#a-task').value.trim();
    w.subAssignedBy = w.subAssignedTask ? byName : '';
    await saveUserData('assign-default-name', byName, false);
    const ok = await saveOneWorkerOrWarn(w);
    if(!ok) return;
    overlay.remove();
    showToast(s.assignSaved);
    render();
  };
}

function openAddWorker(){
  const s=t();
  const overlay=document.createElement('div'); overlay.className='sheet-overlay';
  const sheet=document.createElement('div'); sheet.className='sheet';
  sheet.innerHTML = `
    <h2>${s.addWorkerTitle}</h2>
    <label class="field-label">${s.nameLabel}</label>
    <input type="text" id="n-name" placeholder="${s.namePlaceholder}">
    <label class="field-label">${s.deptLabel}</label>
    <select id="n-dept-select">
      ${Object.keys(DEPTS).map(k=>`<option value="${k}">${DEPTS[k][lang]}</option>`).join('')}
      <option value="__other__">${lang==='ar'?'أخرى / حدد بنفسك':'Other / specify'}</option>
    </select>
    <input type="text" id="n-dept-other" placeholder="${s.deptPlaceholder}" style="margin-top:8px;display:none;">
    <label class="field-label">${s.phoneLabel}</label>
    <input type="text" id="n-phone" placeholder="${s.phonePlaceholder}" inputmode="tel">
    <label class="field-label">${s.passwordLabel}</label>
    <div class="pct-row">
      <input type="text" id="n-password" value="${generateUniqueCode()}" placeholder="${s.passwordPlaceholder}" style="flex:1;">
      <button type="button" id="n-regen" class="photo-btn" style="margin-top:0;">🔄 ${lang==='ar'?'رمز جديد':'New code'}</button>
    </div>
    <div class="sheet-actions">
      <button class="btn-cancel" id="n-cancel">${s.cancel}</button>
      <button class="btn-save" id="n-save">${s.add}</button>
    </div>
  `;
  overlay.appendChild(sheet);
  document.body.appendChild(overlay);
  const deptSelect = sheet.querySelector('#n-dept-select');
  const deptOther = sheet.querySelector('#n-dept-other');
  deptSelect.onchange = ()=>{ deptOther.style.display = (deptSelect.value==='__other__') ? 'block' : 'none'; };
  sheet.querySelector('#n-regen').onclick = ()=>{ sheet.querySelector('#n-password').value = generateUniqueCode(); };
  overlay.onclick=(e)=>{ if(e.target===overlay) overlay.remove(); };
  sheet.querySelector('#n-cancel').onclick=()=>overlay.remove();
  sheet.querySelector('#n-save').onclick=async ()=>{
    const name=sheet.querySelector('#n-name').value.trim();
    if(!name) return;
    const deptChoice = deptSelect.value;
    const deptKey = deptChoice==='__other__' ? null : deptChoice;
    const deptCustom = deptChoice==='__other__' ? deptOther.value.trim() : '';
    const phone = sheet.querySelector('#n-phone').value.trim();
    const password=sheet.querySelector('#n-password').value.trim() || generateUniqueCode();
    const newWorker = {id:'w'+Date.now(), name, deptKey, deptCustom, task:'', completion:0, status:null, updatedAt:null, assignedTask:'', password, uniqueCodeAssigned:true, phone, subAssignedTask:'', subAssignedBy:'', timerRunning:false, timerStartedAt:null, timerAccumulatedMs:0, taskSessions:[], activeSessionId:null};
    workers.push(newWorker);
    const ok = await saveOneWorkerOrWarn(newWorker);
    if(!ok) return;
    overlay.remove();
    render();
  };
}

function setActiveRoleBtn(activeId){
  ['btnWorker','btnAdmin','btnReport','btnAssign','btnInventory'].forEach(id=>{
    document.getElementById(id).classList.toggle('active', id===activeId);
  });
}

document.getElementById('btnWorker').onclick=()=>{ role='worker'; setActiveRoleBtn('btnWorker'); render(); };
document.getElementById('btnAdmin').onclick=()=>{ role='admin'; setActiveRoleBtn('btnAdmin'); render(); };
document.getElementById('btnReport').onclick=()=>{ role='report'; setActiveRoleBtn('btnReport'); render(); };
document.getElementById('btnAssign').onclick=()=>{ role='assign'; setActiveRoleBtn('btnAssign'); render(); };
document.getElementById('btnInventory').onclick=()=>{ role='inventory'; setActiveRoleBtn('btnInventory'); render(); };
document.getElementById('btnLang').onclick=()=>{ lang = lang==='ar' ? 'en' : 'ar'; applyLangChrome(); render(); };

loadWorkers();
loadTheme();
loadLogs();
loadRewards();
loadExpenses();
loadEmployeeNotes();
loadMunicipalProjects();
loadInventory();
checkDbConnection();
</script>

</body>
</html>
