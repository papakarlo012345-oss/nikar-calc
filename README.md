<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>НикАрин · Калькулятор снабжения</title>
<style>
:root{
  --bg:#f0f2f6;--s:#fff;--s2:#f5f7fa;--s3:#eaecf1;
  --bd:#dce0e8;--bd2:#bcc2ce;
  --t:#1b1e26;--t2:#4e566a;--t3:#8890a2;
  --blue:#1a3a6b;--blue2:#2356a6;--bl:#e4ecf7;
  --green:#155f30;--gl:#e2f3eb;
  --ora:#b85500;--ol:#fff2e5;
  --red:#9e2222;--rl:#fdf0f0;
  --r:10px;--r2:6px;
  --sh:0 1px 3px rgba(0,0,0,.06),0 3px 12px rgba(0,0,0,.04);
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',system-ui,sans-serif;background:var(--bg);color:var(--t);font-size:14px;line-height:1.55}
.hdr{background:var(--blue);height:52px;display:flex;align-items:center;padding:0 20px;gap:11px;position:sticky;top:0;z-index:200;box-shadow:0 2px 10px rgba(0,0,0,.22)}
.hdr-ico{width:30px;height:30px;border-radius:7px;background:rgba(255,255,255,.14);display:flex;align-items:center;justify-content:center}
.hdr-ico svg{width:16px;height:16px}
.hdr-name{color:#fff;font-weight:600;font-size:14px}
.hdr-sub{color:rgba(255,255,255,.55);font-size:11px}
.hdr-ver{margin-left:auto;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.18);color:rgba(255,255,255,.75);font-size:11px;padding:2px 9px;border-radius:20px}
.nav{background:var(--blue);border-top:1px solid rgba(255,255,255,.12);display:flex;padding:0 20px;gap:2px;overflow-x:auto}
.nav-item{padding:8px 14px;font-size:12px;font-weight:500;color:rgba(255,255,255,.65);cursor:pointer;border-bottom:2px solid transparent;transition:all .14s;white-space:nowrap;user-select:none}
.nav-item:hover{color:#fff}
.nav-item.on{color:#fff;border-bottom-color:#fff}
.page{display:none}.page.on{display:block}
.wrap{max-width:960px;margin:0 auto;padding:20px 16px 60px}
.card{background:var(--s);border:1px solid var(--bd);border-radius:var(--r);padding:18px 20px;box-shadow:var(--sh);margin-bottom:14px}
.slbl{font-size:11px;font-weight:700;letter-spacing:.07em;text-transform:uppercase;color:var(--t3);margin-bottom:10px}
.tabs{display:flex;gap:5px;flex-wrap:wrap}
.tab{padding:6px 14px;border:1.5px solid var(--bd2);border-radius:20px;font-size:13px;font-weight:500;color:var(--t2);cursor:pointer;background:var(--s2);transition:all .14s;user-select:none;white-space:nowrap}
.tab:hover{border-color:var(--blue);color:var(--blue)}
.tab.on{background:var(--blue);border-color:var(--blue);color:#fff}
.fg{display:grid;grid-template-columns:repeat(auto-fill,minmax(165px,1fr));gap:11px;margin-top:14px}
.fl label{display:block;font-size:11px;font-weight:600;color:var(--t3);letter-spacing:.04em;text-transform:uppercase;margin-bottom:4px}
.fl small{display:block;font-size:10px;color:var(--t3);margin-top:2px;line-height:1.4}
select,input[type=number],input[type=text],textarea{font-family:inherit;outline:none;appearance:none}
select,input[type=number],input[type=text]{width:100%;padding:8px 10px;border:1.5px solid var(--bd2);border-radius:var(--r2);font-size:14px;color:var(--t);background:var(--s2);transition:border-color .14s}
select{background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='11' height='7'%3E%3Cpath d='M1 1l4.5 4.5L10 1' stroke='%23888' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 9px center;padding-right:26px}
select:focus,input:focus{border-color:var(--blue);box-shadow:0 0 0 3px rgba(26,58,107,.1);background:#fff}
.go-btn{width:100%;margin-top:14px;padding:12px;background:var(--blue);color:#fff;border:none;border-radius:var(--r2);font-size:15px;font-weight:700;cursor:pointer;font-family:inherit;transition:background .14s,transform .1s}
.go-btn:hover{background:var(--blue2)}.go-btn:active{transform:scale(.99)}
.drum-items{margin-top:14px;border:1px solid var(--bd);border-radius:var(--r2);overflow:hidden}
.drum-head{padding:8px 12px;background:var(--s2);color:var(--t2);font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.05em;border-bottom:1px solid var(--bd);display:flex;justify-content:space-between;align-items:center}
.drum-row{display:grid;grid-template-columns:1fr 70px 130px 36px;border-bottom:1px solid var(--bd);align-items:stretch}
.drum-row:last-child{border-bottom:none}
.drum-row input{border:none;border-right:1px solid var(--bd);border-radius:0;padding:7px 10px;background:transparent;font-size:13px;color:var(--t);width:100%;font-family:inherit}
.drum-row input:last-of-type{border-right:none;text-align:right}
.drum-row input:focus{background:var(--bl);outline:none}
.drum-del{padding:0 8px;border:none;background:transparent;color:var(--red);cursor:pointer;font-size:18px;display:flex;align-items:center;justify-content:center}
.drum-add{border:none;background:transparent;color:var(--blue);cursor:pointer;font-size:12px;font-weight:600;padding:4px 8px;font-family:inherit}
.drum-add:hover{background:var(--bl);border-radius:3px}
.rtitle{font-size:17px;font-weight:700;margin-bottom:14px;display:flex;align-items:center;gap:9px}
.rtitle-bar{flex-shrink:0;width:4px;height:20px;background:var(--blue);border-radius:2px}
.mcards{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-bottom:12px}
.mc{background:var(--s2);border-radius:var(--r2);padding:12px 14px;border:1px solid var(--bd)}
.mc-lbl{font-size:11px;color:var(--t3);font-weight:600;text-transform:uppercase;letter-spacing:.04em;margin-bottom:3px}
.mc-val{font-size:20px;font-weight:700}
.mc-val.blue{color:var(--blue)}.mc-val.ora{color:var(--ora)}.mc-val.green{color:var(--green)}.mc-val.red{color:var(--red)}
.mc-sub{font-size:11px;color:var(--t3);margin-top:2px}
.min-strip{display:flex;align-items:center;gap:10px;padding:10px 14px;background:var(--rl);border:1px solid #f0b8b8;border-radius:var(--r2);margin-bottom:11px;font-size:13px}
.min-strip b{color:var(--red)}
.bd-card{background:var(--s);border:1px solid var(--bd);border-radius:var(--r);overflow:hidden;box-shadow:var(--sh);margin-bottom:11px}
.bd-head{padding:8px 14px;background:var(--blue);color:#fff;font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.06em}
.brow{display:flex;justify-content:space-between;align-items:center;padding:8px 14px;border-bottom:1px solid var(--bd);font-size:13px}
.brow:last-child{border-bottom:none}
.brow-n{color:var(--t2)}.brow-v{font-weight:600}
.brow-v.blue{color:var(--blue)}.brow-v.green{color:var(--green)}.brow-v.ora{color:var(--ora)}.brow-v.red{color:var(--red)}
.drow{display:flex;justify-content:space-between;align-items:center;padding:9px 14px;background:var(--s2);border-top:2px solid var(--blue);font-size:14px;font-weight:700}
.drow-sub{font-size:11px;color:var(--t3);font-weight:400;margin-left:6px}
.warn-strip{padding:9px 14px;background:var(--rl);color:var(--red);font-size:12.5px;font-weight:600;border-top:1px solid #f0b8b8}
.ok-strip{padding:9px 14px;background:var(--gl);color:var(--green);font-size:12.5px;font-weight:600;border-top:1px solid #a8d9be}
.ibox{border-radius:var(--r2);padding:11px 14px;margin-bottom:11px;font-size:12.5px;line-height:1.7}
.ibox.green{background:var(--gl);border:1px solid #a8d9be;color:#0f4a25}
.ibox.orange{background:var(--ol);border:1px solid #f5c57a;color:var(--ora)}
.ibox.grey{background:var(--s3);border:1px solid var(--bd);color:var(--t3)}
.ibox b{display:block;margin-bottom:3px;font-size:13px}
.sp-card{background:var(--s);border:1px solid var(--bd);border-radius:var(--r);overflow:hidden;box-shadow:var(--sh);margin-bottom:11px}
.sp-head{padding:8px 14px;background:var(--s2);color:var(--t2);font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.06em;border-bottom:1px solid var(--bd)}
table{width:100%;border-collapse:collapse;font-size:13px}
th{text-align:left;padding:6px 12px;color:var(--t3);font-weight:600;font-size:11px;text-transform:uppercase;border-bottom:1px solid var(--bd);background:var(--s2)}
td{padding:6px 12px;border-bottom:1px solid var(--bd);color:var(--t)}
tr:last-child td{border-bottom:none}
tr:hover td{background:#fafbfd}
.tr,.th{text-align:right}
tfoot td{background:var(--s2)!important;font-weight:700;border-top:1.5px solid var(--bd2)}
.note{background:var(--bl);border-left:3px solid var(--blue);border-radius:0 var(--r2) var(--r2) 0;padding:10px 13px;font-size:12.5px;color:#2a4880;margin-bottom:13px;line-height:1.6}
.acts{display:flex;gap:8px;flex-wrap:wrap}
.abtn{padding:8px 16px;border-radius:var(--r2);font-size:13px;font-weight:600;cursor:pointer;font-family:inherit;border:1.5px solid;transition:all .14s}
.abtn.pri{background:var(--blue);color:#fff;border-color:var(--blue)}.abtn.pri:hover{background:var(--blue2)}
.abtn.grn{background:var(--green);color:#fff;border-color:var(--green)}
.abtn.sec{background:transparent;color:var(--t2);border-color:var(--bd2)}.abtn.sec:hover{border-color:var(--blue);color:var(--blue)}
.weight-box{display:none;margin-top:12px;padding:10px 14px;background:var(--gl);border:1px solid #a8d9be;border-radius:var(--r2)}
.weight-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;font-size:13px}
.weight-grid span{display:block;font-size:11px;color:var(--t3);margin-bottom:2px}
.batch-area{width:100%;min-height:120px;padding:10px 12px;border:1.5px solid var(--bd2);border-radius:var(--r2);font-size:13px;color:var(--t);background:var(--s2);resize:vertical;font-family:monospace}
.batch-area:focus{border-color:var(--blue);background:#fff}
.file-drop{margin-bottom:14px;padding:12px 14px;background:var(--s2);border:1.5px dashed var(--bd2);border-radius:var(--r2);display:flex;align-items:center;gap:12px;flex-wrap:wrap}
.file-lbl{padding:7px 14px;background:var(--blue);color:#fff;border-radius:var(--r2);font-size:12px;font-weight:600;cursor:pointer;white-space:nowrap}
.hist-filters{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px;align-items:center}
.hist-filters select,.hist-filters input[type=text]{max-width:180px;padding:6px 10px;font-size:13px}
.hitem{background:var(--s);border:1px solid var(--bd);border-radius:var(--r2);padding:9px 13px;display:flex;justify-content:space-between;align-items:center;cursor:pointer;margin-bottom:6px;transition:border-color .14s}
.hitem:hover{border-color:var(--blue)}
.hitem-n{font-size:13px;font-weight:500}.hitem-m{font-size:11px;color:var(--t3)}
.hitem-p{font-size:14px;font-weight:700;color:var(--blue);white-space:nowrap;margin-left:12px}
.load-bar-wrap{background:var(--s3);border-radius:4px;height:10px;overflow:hidden;margin:5px 0 12px}
.load-bar{height:100%;border-radius:4px;transition:width .4s;background:var(--green)}
.load-bar.warn{background:var(--ora)}.load-bar.full{background:var(--red)}
.price-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr));gap:10px}
.price-item{background:var(--s2);border:1px solid var(--bd);border-radius:var(--r2);padding:10px 12px}
.price-item label{font-size:11px;font-weight:600;color:var(--t3);text-transform:uppercase;letter-spacing:.04em;display:block;margin-bottom:5px}
.price-item input{width:100%;padding:7px 10px;border:1.5px solid var(--bd2);border-radius:var(--r2);font-size:14px;font-weight:600;color:var(--t);background:#fff;text-align:right;font-family:inherit}
.price-item input:focus{border-color:var(--blue);outline:none}
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:500;align-items:center;justify-content:center}
.modal-bg.on{display:flex}
#mkt-overlay.on{display:flex}
.modal{background:var(--s);border-radius:var(--r);padding:24px;max-width:520px;width:90%;box-shadow:0 8px 40px rgba(0,0,0,.2)}
.modal h3{font-size:16px;font-weight:700;margin-bottom:14px;display:flex;justify-content:space-between;align-items:center}
.modal-x{border:none;background:transparent;font-size:22px;cursor:pointer;color:var(--t3);line-height:1;padding:0}
@media print{.hdr,.nav,.form-wrap,.acts,.hist-wrap,.page-batch,.page-load,.page-prices,.page-history,.modal-bg{display:none!important}.res-wrap{display:block!important}body{background:#fff}}
@media(max-width:600px){.mcards{grid-template-columns:1fr 1fr}.mcards .mc:last-child{grid-column:1/-1}.fg{grid-template-columns:1fr 1fr}.hist-filters{flex-direction:column;align-items:stretch}}
</style>
</head>
<body>

<div class="hdr">
  <div class="hdr-ico"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2L2 7l10 5 10-5-10-5M2 17l10 5 10-5M2 12l10 5 10-5"/></svg></div>
  <div><div class="hdr-name">Калькулятор снабжения · НикАрин</div><div class="hdr-sub">ПартнёрПромСнаб · Челябинск</div></div>
  <div class="hdr-ver">v10</div>
</div>

<div class="nav">
  <div class="nav-item on" onclick="showPage('calc')">⚙ Расчёт</div>
  <div class="nav-item" onclick="showPage('batch')">📋 Пакетный расчёт</div>
  <div class="nav-item" onclick="showPage('load')">🏭 Загрузка</div>
  <div class="nav-item" onclick="showPage('prices')">💰 Цены</div>
  <div class="nav-item" onclick="showPage('history')">🕒 История</div>
</div>

<!-- СТРАНИЦА: РАСЧЁТ -->
<div class="page on" id="page-calc">
<div class="wrap">

  <div id="price-age-warn" class="ibox orange" style="display:none;margin-bottom:14px">
    <span>⚠ <b id="price-age-txt"></b> — проверьте актуальность в разделе «Цены»</span>
    <button onclick="showPage('prices')" style="margin-left:10px;padding:3px 10px;background:var(--ora);color:#fff;border:none;border-radius:3px;cursor:pointer;font-size:12px">Обновить</button>
  </div>

  <div class="form-wrap">
    <div class="card">
      <div class="slbl">Выберите продукт</div>
      <div class="tabs">
        <div class="tab on"  onclick="setP('roliki')">Ролики конвейерные</div>
        <div class="tab"     onclick="setP('barabany')">Барабаны</div>
        <div class="tab"     onclick="setP('buksy')">Буксы</div>
        <div class="tab"     onclick="setP('rolikoopory')">Роликоопоры</div>
        <div class="tab"     onclick="setP('konveyery')">Конвейеры (КЛ)</div>
      </div>

      <!-- РОЛИКИ -->
      <div id="f-roliki" class="fg">
        <div class="fl"><label>Диаметр трубы (мм)</label>
          <select id="r-d" onchange="fillLens();updWeight()">
            <option value="76">Ф 76</option><option value="89">Ф 89</option>
            <option value="102">Ф 102</option><option value="108">Ф 108</option>
            <option value="127" selected>Ф 127</option><option value="133">Ф 133</option>
            <option value="159">Ф 159</option>
          </select>
        </div>
        <div class="fl"><label>Длина (мм)</label>
          <select id="r-l" onchange="updWeight()"></select>
          <small>До 2000 мм включительно</small>
        </div>
        <div class="fl"><label>Толщина стенки (мм)</label>
          <select id="r-wall" onchange="updWeight()">
            <option value="2.5">2,5 мм</option>
            <option value="3.0">3,0 мм</option>
            <option value="3.5">3,5 мм</option>
            <option value="4.0" selected>4,0 мм</option>
            <option value="4.5">4,5 мм</option>
            <option value="5.0">5,0 мм</option>
          </select>
          <small>Прайс_на_ролики.xlsx</small>
        </div>
        <div class="fl"><label>Диаметр вала (мм)</label>
          <select id="r-shaft" onchange="updWeight()">
            <option value="22" selected>Ф 22 мм</option>
            <option value="27">Ф 27 мм</option>
            <option value="32">Ф 32 мм</option>
            <option value="37">Ф 37 мм</option>
            <option value="42">Ф 42 мм</option>
            <option value="47">Ф 47 мм</option>
          </select>
          <small>Прайс_на_ролики.xlsx</small>
        </div>
        <div class="fl"><label>Выбор подшипника</label>
          <select id="r-brg" onchange="updWeight()">
            <optgroup label="Серия 200 (лёгкая)">
              <option value="204|26">204 — 26 ₽/шт</option>
              <option value="205|75">205 — 75 ₽/шт</option>
              <option value="206|75">206 — 75 ₽/шт</option>
            </optgroup>
            <optgroup label="Серия 300 (тяжёлая)">
              <option value="304|75">304 — 75 ₽/шт</option>
              <option value="305|74">305 — 74 ₽/шт</option>
              <option value="306|160">306 — 160 ₽/шт</option>
              <option value="307|150">307 — 150 ₽/шт</option>
              <option value="308|198">308 — 198 ₽/шт</option>
            </optgroup>
          </select>
          <small>Калькуляции НикАрин 2024–2026</small>
        </div>
        <div class="fl"><label>Количество (шт)</label>
          <input type="number" id="r-q" value="200" min="1" oninput="onQtyChange()">
        </div>
        <div class="fl"><label>Целевая наценка (%)</label>
          <input type="number" id="r-m" value="70" min="1" max="500">
          <small>Авто по кол-ву, можно изменить</small>
        </div>
      </div>
      <div id="markup-info" style="display:none;margin-top:9px;padding:9px 13px;background:var(--bl);border-left:3px solid var(--blue);border-radius:0 var(--r2) var(--r2) 0;font-size:12.5px;color:#2a4880"></div>

      <!-- АВТО-ВЕС РОЛИКА -->
      <div class="weight-box" id="weight-box">
        <div style="font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.06em;color:var(--green);margin-bottom:8px">⚖ Расчётный вес изделия (обновляется автоматически)</div>
        <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:10px;font-size:13px">
          <div style="background:#fff;padding:8px 12px;border-radius:var(--r2);border:1px solid #a8d9be">
            <div style="font-size:10px;color:var(--t3);text-transform:uppercase;letter-spacing:.04em;margin-bottom:3px">Труба (обечайка)</div>
            <b id="w-tube" style="font-size:15px">—</b>
          </div>
          <div style="background:#fff;padding:8px 12px;border-radius:var(--r2);border:1px solid #a8d9be">
            <div style="font-size:10px;color:var(--t3);text-transform:uppercase;letter-spacing:.04em;margin-bottom:3px">Вал</div>
            <b id="w-shaft" style="font-size:15px">—</b>
          </div>
          <div style="background:var(--green);padding:8px 12px;border-radius:var(--r2)">
            <div style="font-size:10px;color:rgba(255,255,255,.75);text-transform:uppercase;letter-spacing:.04em;margin-bottom:3px">Итого 1 ролик</div>
            <b id="w-total" style="font-size:18px;color:#fff">—</b>
          </div>
          <div style="background:#fff;padding:8px 12px;border-radius:var(--r2);border:1px solid #a8d9be" id="w-batch-box">
            <div style="font-size:10px;color:var(--t3);text-transform:uppercase;letter-spacing:.04em;margin-bottom:3px">Вес партии</div>
            <b id="w-batch" style="font-size:15px;color:var(--blue)">—</b>
          </div>
        </div>
      </div>

      <!-- БАРАБАНЫ -->
      <div id="f-barabany" style="display:none">
        <div class="fg" style="margin-top:0">
          <div class="fl"><label>Тип</label>
            <select id="b-t" onchange="initDrumRows()">
              <option value="drive">Приводной</option><option value="tail">Не приводной</option>
            </select>
          </div>
          <div class="fl"><label>Диаметр обечайки (мм)</label><input type="number" id="b-d" value="630"><small>Произвольный ввод</small></div>
          <div class="fl"><label>Толщина стенки (мм)</label><input type="number" id="b-wall" value="8"><small>Произвольный ввод</small></div>
          <div class="fl"><label>Диаметр вала (мм)</label><input type="number" id="b-vd" value="80"><small>Произвольный ввод</small></div>
          <div class="fl"><label>Длина вала (мм)</label><input type="number" id="b-vl" value="500"><small>Влияет на стоимость</small></div>
          <div class="fl"><label>Ширина обечайки (мм)</label><input type="number" id="b-b" value="1000"><small>Произвольный ввод</small></div>
          <div class="fl"><label>Количество (шт)</label><input type="number" id="b-q" value="1" min="1"></div>
          <div class="fl"><label>Целевая наценка (%)</label><input type="number" id="b-m" value="40" min="1"></div>
        </div>
        <div class="drum-items">
          <div class="drum-head">
            <span>Позиции материалов — по счетам поставщиков</span>
            <button class="drum-add" onclick="addDrumRow('','1','0')">+ Добавить позицию</button>
          </div>
          <div id="drum-rows"></div>
        </div>
      </div>

      <!-- БУКСЫ -->
      <div id="f-buksy" class="fg" style="display:none">
        <div class="fl"><label>Модель / тип</label>
          <select id="bk-m" onchange="onBuksyChange()">
            <optgroup label="Буксы НикАрин">
              <option value="3610">Букса 3610 · Ф140</option>
              <option value="3612">Букса 3612 · Ф160</option>
              <option value="3614" selected>Букса 3614 · Ф180</option>
              <option value="3616">Букса 3616 · Ф210</option>
              <option value="3618">Букса 3618 · Ф250</option>
              <option value="3620">Букса 3620 · Ф265</option>
              <option value="3622">Букса 3622 · Ф290</option>
              <option value="3624">Букса 3624 · Ф320</option>
              <option value="3626">Букса 3626 · Ф360</option>
            </optgroup>
            <optgroup label="UCP корпусные (покупные)">
              <option value="ucp306">UCP 306 · d=30</option><option value="ucp307">UCP 307 · d=35</option>
              <option value="ucp308">UCP 308 · d=40</option><option value="ucp309">UCP 309 · d=45</option>
              <option value="ucp310">UCP 310 · d=50</option><option value="ucp311">UCP 311 · d=55</option>
              <option value="ucp312">UCP 312 · d=60</option><option value="ucp313">UCP 313 · d=65</option>
              <option value="ucp314">UCP 314 · d=70</option><option value="ucp315">UCP 315 · d=75</option>
              <option value="ucp316">UCP 316 · d=80</option><option value="ucp317">UCP 317 · d=85</option>
              <option value="ucp318">UCP 318 · d=90</option><option value="ucp320">UCP 320 · d=100</option>
              <option value="ucp322">UCP 322 · d=110</option>
            </optgroup>
          </select>
        </div>
        <div class="fl"><label>Цена закупки (₽/шт)</label>
          <input type="number" id="bk-buy" value="0" min="0">
          <small>НикАрин — авто. UCP — вручную</small>
        </div>
        <div class="fl"><label>Количество (шт)</label><input type="number" id="bk-q" value="1" min="1"></div>
        <div class="fl"><label>Целевая наценка (%)</label><input type="number" id="bk-mk" value="30" min="1"></div>
      </div>

      <!-- РОЛИКООПОРЫ -->
      <div id="f-rolikoopory" class="fg" style="display:none">
        <div class="fl"><label>Тип</label>
          <select id="ro-t">
            <option value="3r">3-роликовая рядовая</option>
            <option value="1r">1-роликовая нижняя</option>
            <option value="center">Центрирующая</option>
            <option value="amort">Амортизирующая</option>
          </select>
        </div>
        <div class="fl"><label>Диаметр ролика (мм)</label>
          <select id="ro-d">
            <option value="76">Ф 76</option><option value="89" selected>Ф 89</option>
            <option value="102">Ф 102</option><option value="108">Ф 108</option>
            <option value="127">Ф 127</option><option value="133">Ф 133</option><option value="159">Ф 159</option>
          </select>
        </div>
        <div class="fl"><label>Ширина ленты (мм)</label>
          <select id="ro-b">
            <option value="500">500</option><option value="650">650</option>
            <option value="800" selected>800</option><option value="1000">1000</option>
            <option value="1200">1200</option><option value="1400">1400</option>
          </select>
        </div>
        <div class="fl"><label>Количество (шт)</label><input type="number" id="ro-q" value="50" min="1"></div>
        <div class="fl"><label>Целевая наценка (%)</label><input type="number" id="ro-m" value="35" min="1"></div>
      </div>

      <!-- КОНВЕЙЕРЫ -->
      <div id="f-konveyery" class="fg" style="display:none">
        <div class="fl"><label>Ширина ленты (мм)</label>
          <select id="kl-b">
            <option value="400" selected>400</option><option value="500">500</option>
            <option value="650">650</option><option value="800">800</option>
            <option value="1000">1000</option><option value="1200">1200</option>
          </select>
        </div>
        <div class="fl"><label>Длина (м)</label><input type="number" id="kl-l" value="5" min="1" max="200"></div>
        <div class="fl"><label>Тип ленты</label>
          <select id="kl-belt">
            <option value="1.00">Гладкая EP200 — база</option>
            <option value="1.10">Гладкая EP300 (+10%)</option>
            <option value="1.20">Шевронная стандарт (+20%)</option>
            <option value="1.35">Шевронная высокая (+35%)</option>
            <option value="1.25">Рифлёная (+25%)</option>
            <option value="1.40">Огнестойкая (+40%)</option>
          </select>
        </div>
        <div class="fl"><label>Привод (кВт)</label>
          <select id="kl-drive">
            <option value="0">Без привода</option>
            <option value="15000">1,1 кВт — +15 000 ₽</option>
            <option value="22000">2,2 кВт — +22 000 ₽</option>
            <option value="35000">4 кВт — +35 000 ₽</option>
            <option value="45000">5,5 кВт — +45 000 ₽</option>
            <option value="58000">7,5 кВт — +58 000 ₽</option>
            <option value="75000">11 кВт — +75 000 ₽</option>
            <option value="95000">15 кВт — +95 000 ₽</option>
            <option value="115000">18,5 кВт — +115 000 ₽</option>
            <option value="140000">22 кВт — +140 000 ₽</option>
            <option value="175000">30 кВт — +175 000 ₽</option>
            <option value="220000">45 кВт — +220 000 ₽</option>
          </select>
        </div>
        <div class="fl"><label>Шкаф управления</label>
          <select id="kl-panel">
            <option value="0">Без шкафа</option>
            <option value="45000">Шкаф простой — +45 000 ₽</option>
            <option value="95000">С частотником — +95 000 ₽</option>
            <option value="130000">С частотником + аварийка — +130 000 ₽</option>
          </select>
        </div>
        <div class="fl"><label>Количество (шт)</label><input type="number" id="kl-q" value="1" min="1"></div>
        <div class="fl"><label>Целевая наценка (%)</label><input type="number" id="kl-m" value="50" min="1"></div>
      </div>

      <button class="go-btn" onclick="doCalc()">⚙ Рассчитать</button>
    </div>
  </div>

  <!-- РЕЗУЛЬТАТ -->
  <div id="res-wrap" style="display:none">
    <div class="rtitle"><div class="rtitle-bar"></div><span id="res-title"></span></div>
    <div class="mcards">
      <div class="mc"><div class="mc-lbl">Себестоимость материалов</div><div class="mc-val blue" id="mc-mat"></div><div class="mc-sub" id="mc-mat-s"></div></div>
      <div class="mc"><div class="mc-lbl">Цена реализации</div><div class="mc-val ora" id="mc-price"></div><div class="mc-sub" id="mc-price-s"></div></div>
      <div class="mc"><div class="mc-val" id="mc-profit"></div><div class="mc-lbl">Прибыль / Маржа</div><div class="mc-sub" id="mc-profit-s"></div></div>
    </div>
    <div id="mc-extra" style="display:none;margin-bottom:12px">
      <div class="mc" style="background:var(--bl);border-color:#b8ccee;display:inline-block;min-width:200px">
        <div class="mc-lbl" id="mc-extra-lbl"></div>
        <div class="mc-val blue" id="mc-extra-val"></div>
        <div class="mc-sub" id="mc-extra-sub"></div>
      </div>
    </div>
    <div class="min-strip">⛔ &nbsp;Минимальная цена (маржа 10%): <b id="min-u"></b>/шт &nbsp;·&nbsp; <b id="min-t"></b> за партию</div>
    <div class="bd-card"><div class="bd-head">Сводка расчёта</div><div id="bd-body"></div></div>
    <div id="shift-info"></div>
    <div id="spec-wrap"></div>
    <div id="src-wrap"></div>
    <div class="note" id="res-note"></div>
    <div class="acts">
      <button class="abtn pri" onclick="printResult()">⎙ Распечатать</button>
      <button class="abtn" style="background:var(--green);color:#fff;border-color:var(--green);border-width:1.5px" onclick="if(lastResult)openMkt(lastResult)">📊 Анализ рынка</button>
      <button class="abtn grn" onclick="openKP()">📄 Сформировать КП</button>
      <button class="abtn sec" onclick="resetCalc()">← Новый расчёт</button>
    </div>
  </div>
</div>
</div>

<!-- СТРАНИЦА: ПАКЕТНЫЙ РАСЧЁТ -->
<div class="page" id="page-batch">
<div class="wrap">
  <div class="card">
    <div class="slbl">Пакетный расчёт роликов</div>
    <p style="font-size:13px;color:var(--t2);margin-bottom:8px">Введите список позиций <b>или загрузите файл CSV/TXT</b></p>
    <p style="font-size:12px;color:var(--t3);margin-bottom:14px">Формат строки: <code style="background:var(--s3);padding:2px 6px;border-radius:3px">127x310, 50, 30</code> &nbsp;(диаметр x длина, кол-во, наценка%)</p>
    <div class="file-drop">
      <div>
        <div style="font-size:12px;font-weight:600;color:var(--t2);margin-bottom:3px">📎 Загрузить CSV или TXT</div>
        <div style="font-size:11px;color:var(--t3)">Колонки: Диаметр, Длина, Количество, Наценка%</div>
      </div>
      <label class="file-lbl">📂 Выбрать файл<input type="file" id="batch-file" accept=".csv,.txt" style="display:none" onchange="loadFile(this)"></label>
      <span id="batch-fname" style="font-size:12px;color:var(--t3)">не выбран</span>
    </div>
    <textarea class="batch-area" id="batch-ta" rows="6" placeholder="127x310, 50, 30&#10;89x500, 100, 25&#10;159x950, 200, 35&#10;76x400, 300, 30"></textarea>
    <div style="display:flex;gap:8px;margin-top:10px">
      <button class="go-btn" style="flex:1;margin-top:0" onclick="runBatch()">⚙ Рассчитать всё</button>
      <button class="abtn sec" onclick="document.getElementById('batch-ta').value='';document.getElementById('batch-result').innerHTML='';document.getElementById('batch-fname').textContent='не выбран'">Очистить</button>
    </div>
  </div>
  <div id="batch-result"></div>
</div>
</div>

<!-- СТРАНИЦА: ЗАГРУЗКА -->
<div class="page" id="page-load">
<div class="wrap">
  <div class="card">
    <div class="slbl">Загрузка производства на неделе</div>
    <p style="font-size:13px;color:var(--t2);margin-bottom:16px">Укажите сколько смен уже занято (5 рабочих дней = 5 смен максимум)</p>
    <div class="fg" style="margin-top:0;margin-bottom:16px">
      <div class="fl"><label>Ролики — занято смен</label><input type="number" id="ld-r" value="2" min="0" max="5" oninput="renderLoad()"></div>
      <div class="fl"><label>Барабаны — занято смен</label><input type="number" id="ld-b" value="1" min="0" max="5" oninput="renderLoad()"></div>
      <div class="fl"><label>Роликоопоры — занято</label><input type="number" id="ld-ro" value="1" min="0" max="5" oninput="renderLoad()"></div>
      <div class="fl"><label>Конвейеры — занято</label><input type="number" id="ld-kl" value="0" min="0" max="5" oninput="renderLoad()"></div>
    </div>
    <div id="load-bars"></div>
    <div style="border-top:1px solid var(--bd);padding-top:14px;margin-top:4px">
      <div class="slbl">Проверить — влезет ли заказ?</div>
      <div class="fg" style="margin-top:0">
        <div class="fl"><label>Продукт</label>
          <select id="ld-chk-type">
            <option value="roliki">Ролики (200/смена)</option>
            <option value="barabany">Барабаны (5/смена)</option>
            <option value="rolikoopory">Роликоопоры (50/смена)</option>
            <option value="konveyery">Конвейеры (1/смена)</option>
          </select>
        </div>
        <div class="fl"><label>Количество (шт)</label><input type="number" id="ld-chk-qty" value="200" min="1"></div>
      </div>
      <button class="go-btn" style="margin-top:10px" onclick="checkLoad()">Проверить</button>
      <div id="load-result" style="margin-top:12px"></div>
    </div>
  </div>
</div>
</div>

<!-- СТРАНИЦА: ЦЕНЫ -->
<div class="page" id="page-prices">
<div class="wrap">
  <div class="card">
    <div class="slbl">Редактор цен на материалы</div>
    <p style="font-size:13px;color:var(--t2);margin-bottom:4px">Измените цены — все расчёты автоматически пересчитываются</p>
    <p style="font-size:12px;color:var(--t3);margin-bottom:16px">Последнее обновление: <b id="prices-date">—</b></p>
    <div class="price-grid" id="price-grid"></div>
    <div style="display:flex;gap:8px;margin-top:16px;flex-wrap:wrap">
      <button class="abtn pri" onclick="savePrices()">💾 Сохранить цены</button>
      <button class="abtn sec" onclick="resetPrices()">↺ Сбросить к исходным</button>
    </div>
    <div id="prices-msg" style="display:none;margin-top:10px;padding:8px 12px;background:var(--gl);border-radius:var(--r2);font-size:13px;color:var(--green)">✓ Цены сохранены</div>
  </div>
</div>
</div>

<!-- СТРАНИЦА: ИСТОРИЯ -->
<div class="page" id="page-history">
<div class="wrap">
  <div class="card">
    <div class="slbl">История расчётов</div>
    <div class="hist-filters">
      <select id="hf-type" onchange="renderHist()">
        <option value="">Все продукты</option>
        <option value="roliki">Ролики</option>
        <option value="barabany">Барабаны</option>
        <option value="buksy">Буксы</option>
        <option value="rolikoopory">Роликоопоры</option>
        <option value="konveyery">Конвейеры</option>
      </select>
      <select id="hf-mg" onchange="renderHist()">
        <option value="0">Любая маржа</option>
        <option value="10">≥ 10%</option>
        <option value="20">≥ 20%</option>
        <option value="30">≥ 30%</option>
        <option value="40">≥ 40%</option>
      </select>
      <input type="text" id="hf-q" placeholder="Поиск..." oninput="renderHist()">
      <button class="abtn sec" style="padding:6px 12px;font-size:12px" onclick="clearHist()">Очистить</button>
    </div>
    <div id="hist-list"></div>
  </div>
</div>
</div>

<!-- КП МОДАЛ -->
<div class="modal-bg" id="kp-modal">
  <div class="modal">
    <h3>Коммерческое предложение <button class="modal-x" onclick="document.getElementById('kp-modal').classList.remove('on')">×</button></h3>
    <div class="fg" style="margin-top:0;margin-bottom:16px">
      <div class="fl"><label>Клиент</label><input type="text" id="kp-client" placeholder="ООО Название"></div>
      <div class="fl"><label>Контактное лицо</label><input type="text" id="kp-contact" placeholder="Иванов И.И."></div>
      <div class="fl"><label>Срок поставки (дней)</label><input type="number" id="kp-days" value="14" min="1"></div>
      <div class="fl"><label>Условия оплаты</label><input type="text" id="kp-payment" value="100% предоплата"></div>
    </div>
    <button class="abtn grn" style="width:100%" onclick="printKP()">⎙ Открыть для печати / PDF</button>
  </div>
</div>

<script>
// ================================================================
//  ДАННЫЕ
// ================================================================

var RP = {
  76:{195:1028,200:1028,250:1065,300:1092,350:1118,400:1132,450:1171,500:1198,550:1225,600:1251,650:1278,700:1304,750:1341,800:1378,850:1394,900:1410,950:1447,1000:1474,1050:1511,1100:1537,1150:1564,1200:1591},
  89:{200:1050,250:1079,300:1106,310:1110,350:1138,400:1167,450:1197,500:1226,550:1256,600:1295,650:1325,700:1354,750:1384,800:1424,850:1442,900:1461,950:1491,1000:1520,1050:1571,1100:1600,1150:1609,1200:1659},
  102:{195:1122,200:1133,245:1162,250:1170,300:1206,310:1211,350:1245,380:1262,400:1270,450:1320,500:1432,550:1396,600:1444,650:1481,700:1518,750:1556,800:1604,850:1631,900:1658,950:1696,1000:1744,1050:1792,1100:1829,1150:1867,1200:1904},
  108:{200:1120,245:1154,250:1154,300:1187,350:1224,400:1258,450:1293,500:1327,550:1362,600:1407,650:1441,700:1476,750:1510,800:1555,850:1579,900:1603,950:1638,1000:1683,1050:1728,1100:1762,1150:1797,1200:1832},
  127:{200:1155,250:1198,300:1240,310:1246,350:1285,400:1328,450:1371,460:1380,500:1415,550:1458,600:1511,650:1555,700:1598,750:1641,800:1696,850:1728,900:1760,950:1804,1000:1857,1050:1911,1100:1954,1150:1997,1200:2041},
  133:{200:1386,250:1438,300:1488,310:1495,350:1542,400:1594,450:1646,460:1656,500:1697,550:1749,600:1814,650:1866,700:1917,750:1969,800:2035,850:2073,900:2113,950:2164,1000:2229,1050:2293,1100:2345,1150:2397,1200:2449},
  159:{200:1408,250:1466,300:1535,350:1612,400:1685,450:1758,500:1831,550:1904,600:1997,650:2070,700:2142,750:2215,800:2308,850:2361,900:2415,950:2488,1000:2580,1050:2671,1100:2746,1150:2819,1200:2892}
};
var TKG = {76:0.00710208,89:0.0083844,102:0.00966672,108:0.01025856,127:0.01213272,133:0.01272456,159:0.0152892};
var LKM_KGM2 = 0.4854;
var FREZ = 2.565, LENTA_T = 1.70, SOZ = 0.278;
var BK = {
  3610:{dia:140,mat:7800,brg:800,price:17668},
  3612:{dia:160,mat:9400,brg:1200,price:20000},
  3614:{dia:180,mat:11960,brg:1563,price:23310},
  3616:{dia:210,mat:15950,brg:2000,price:30000},
  3618:{dia:250,mat:24560,brg:2465,price:42869},
  3620:{dia:265,mat:29550,brg:3500,price:50092},
  3622:{dia:290,mat:33800,brg:5000,price:60000},
  3624:{dia:320,mat:37600,brg:7000,price:70000},
  3626:{dia:360,mat:44200,brg:10000,price:85000}
};
var UCP_BUY = {ucp306:650,ucp307:720,ucp308:800,ucp309:890,ucp310:980,ucp311:1100,ucp312:1250,ucp313:1400,ucp314:1550,ucp315:1700,ucp316:1900,ucp317:2100,ucp318:2350,ucp320:2800,ucp322:3300};
var UCP_D = {ucp306:30,ucp307:35,ucp308:40,ucp309:45,ucp310:50,ucp311:55,ucp312:60,ucp313:65,ucp314:70,ucp315:75,ucp316:80,ucp317:85,ucp318:90,ucp320:100,ucp322:110};
var KL_M = {400:46078,500:55000,650:68000,800:86000,1000:111000,1200:141000};
var OVH = 35000;
var OVH_SH = {roliki:0.55,barabany:0.45,rolikoopory:0.45,konveyery:0.45};
var SHIFT = {roliki:200,barabany:5,rolikoopory:50,konveyery:1};
var SHAFT_KG_MM = {22:0.002944,26:0.004133,30:0.005497,32:0.006257,35:0.007494,40:0.009793,45:0.01240,50:0.01532};
// ── РАСШИРЕННЫЕ ДАННЫЕ (добавлены в v12) ─────────────────────

// Коэффициенты веса трубы по диаметру И толщине стенки (кг/мм)
// Источник: Прайс_на_ролики.xlsx — таблица весов
var TKG_WALL = {
  76: {2.5:0.00448,3.0:0.00540054,3.5:0.006257475,4.0:0.00710208,4.5:0.00795,5.0:0.00880},
  89: {2.5:0.00528,3.0:0.00636228,3.5:0.007379505,4.0:0.0083844, 4.5:0.00940,5.0:0.01040},
  102:{2.5:0.00608,3.0:0.00732402,3.5:0.008501535,4.0:0.00966672,4.5:0.01083,5.0:0.01200},
  108:{2.5:0.00645,3.0:0.0077679, 3.5:0.009019395,4.0:0.01025856,4.5:0.01150,5.0:0.01273},
  127:{2.5:0.00762,3.0:0.00917352,3.5:0.010659285,4.0:0.01213272,4.5:0.01360,5.0:0.01506},
  133:{2.5:0.00800,3.0:0.0096174, 3.5:0.011177145,4.0:0.01272456,4.5:0.01427,5.0:0.01581},
  159:{2.5:0.00960,3.0:0.01154088,3.5:0.013421205,4.0:0.0152892, 4.5:0.01714,5.0:0.01898}
};
function getTKGw(dia, wall) {
  var tbl = TKG_WALL[dia]; if(!tbl) return 0.007;
  var w = parseFloat(wall);
  if(tbl[w] !== undefined) return tbl[w];
  return tbl[4.0] || 0.007;
}

// Весовые коэффициенты вала (кг/мм) — Прайс_на_ролики.xlsx
var SHAFT_KGM_EX = {22:0.002944,27:0.003880,32:0.004768,37:0.006050,42:0.007800,47:0.009750};

// Подшипники — калькуляции НикАрин 2024-2026
function parseBrg(val) {
  var p = (val||'204|26').split('|');
  return {num:p[0]||'204', price:+(p[1]||26)};
}
var KPU_PRICE = {76:45,89:46,102:54,108:58,127:72,133:77,159:87};

// Авто-наценка для роликов
var MK_TIERS = [
  {max:50,   mk:100,lbl:'до 50 шт'},
  {max:100,  mk:85, lbl:'51-100 шт'},
  {max:200,  mk:70, lbl:'101-200 шт'},
  {max:400,  mk:55, lbl:'201-400 шт'},
  {max:600,  mk:45, lbl:'401-600 шт'},
  {max:800,  mk:38, lbl:'601-800 шт'},
  {max:1000, mk:32, lbl:'801-1000 шт'},
  {max:9e9,  mk:28, lbl:'свыше 1000 шт'}
];
function getAutoMkup(qty) {
  for(var i=0;i<MK_TIERS.length;i++) if(qty<=MK_TIERS[i].max) return MK_TIERS[i];
  return MK_TIERS[MK_TIERS.length-1];
}

// Типы ленты — название по коэффициенту
var BELT_NAME = {
  '1':   'Гладкая EP200 (база)',
  '1.1': 'Гладкая EP300',
  '1.2': 'Шевронная стандарт',
  '1.35':'Шевронная высокая',
  '1.25':'Рифлёная',
  '1.4': 'Огнестойкая'
};
function getBeltName(mult) {
  var k = String(parseFloat(mult));
  return BELT_NAME[k] || ('Тип ×'+mult);
}

var DEFAULT_P = {
  t76:61.9,t89:63.1,t102:64.0,t108:64.5,t127:63.09,t133:64.0,t159:65.0,
  s22:53.6,s26:55.0,s30:56.5,s32:57.0,s35:58.0,s40:59.5,s45:61.0,s50:63.0,
  kpu76:45,kpu89:46,kpu102:54,kpu108:58,kpu127:72,kpu133:77,kpu159:87,
  bearing:26,lkm:320
};

var PRICE_FIELDS = [
  {k:'t76',lbl:'Труба Ф76 (₽/кг)'},{k:'t89',lbl:'Труба Ф89 (₽/кг)'},{k:'t102',lbl:'Труба Ф102 (₽/кг)'},
  {k:'t108',lbl:'Труба Ф108 (₽/кг)'},{k:'t127',lbl:'Труба Ф127 (₽/кг)'},{k:'t133',lbl:'Труба Ф133 (₽/кг)'},
  {k:'t159',lbl:'Труба Ф159 (₽/кг)'},{k:'s22',lbl:'Круг Ф22 (₽/кг)'},{k:'s26',lbl:'Круг Ф26 (₽/кг)'},
  {k:'s30',lbl:'Круг Ф30 (₽/кг)'},{k:'s32',lbl:'Круг Ф32 (₽/кг)'},{k:'s35',lbl:'Круг Ф35 (₽/кг)'},
  {k:'s40',lbl:'Круг Ф40 (₽/кг)'},{k:'s45',lbl:'Круг Ф45 (₽/кг)'},{k:'s50',lbl:'Круг Ф50 (₽/кг)'},
  {k:'kpu76',lbl:'КПУ-76 (₽/шт)'},{k:'kpu89',lbl:'КПУ-89 (₽/шт)'},{k:'kpu102',lbl:'КПУ-102 (₽/шт)'},
  {k:'kpu108',lbl:'КПУ-108 (₽/шт)'},{k:'kpu127',lbl:'КПУ-127 (₽/шт)'},{k:'kpu133',lbl:'КПУ-133 (₽/шт)'},
  {k:'kpu159',lbl:'КПУ-159 (₽/шт)'},{k:'bearing',lbl:'Подшипник (₽/шт)'},{k:'lkm',lbl:'ЛКМ RAL7024 (₽/кг)'}
];

// ================================================================
//  ВСПОМОГАТЕЛЬНЫЕ
// ================================================================
function f(n){ return Math.round(n).toLocaleString('ru-RU') + ' ₽'; }
function fn(n){ return Math.round(n).toLocaleString('ru-RU'); }

function getP(){
  var stored = localStorage.getItem('nik_p');
  if(!stored) return Object.assign({}, DEFAULT_P);
  return Object.assign({}, DEFAULT_P, JSON.parse(stored));
}

function matRoller(d, l, shaftDia){
  var p = getP();
  var tpr = p['t'+d] || 63;
  var shKgMm = SHAFT_KG_MM[shaftDia] || 0.002944;
  var shPr = p['s'+shaftDia] || 53.6;
  var tubeKg = TKG[d] * l;
  var shaftKg = shKgMm * (l + 30);
  var lkmKg = Math.PI * (d/1000) * (l/1000) * LKM_KGM2;
  var kpuP = p['kpu'+d] || 60;
  return {
    tubeKg: tubeKg, shaftKg: shaftKg,
    tube: tubeKg * tpr,
    shaft: shaftKg * shPr,
    kpu: kpuP * 2,
    bearing: p.bearing * 2,
    lkm: lkmKg * p.lkm,
    tool: FREZ + LENTA_T + SOZ,
    lkmKg: lkmKg
  };
}

// ================================================================
//  НАВИГАЦИЯ
// ================================================================
var PAGES = ['calc','batch','load','prices','history'];

function showPage(id){
  PAGES.forEach(function(p){
    document.getElementById('page-'+p).classList.remove('on');
  });
  document.querySelectorAll('.nav-item').forEach(function(n){ n.classList.remove('on'); });
  document.getElementById('page-'+id).classList.add('on');
  var idx = PAGES.indexOf(id);
  if(idx >= 0) document.querySelectorAll('.nav-item')[idx].classList.add('on');
  if(id==='history') renderHist();
  if(id==='prices') renderPriceEditor();
  if(id==='load') renderLoad();
}

// ================================================================
//  ФОРМА
// ================================================================
var curP = 'roliki';
var lastResult = null;
var drumRowId = 0;

function setP(p){
  curP = p;
  var products = ['roliki','barabany','buksy','rolikoopory','konveyery'];
  document.querySelectorAll('.tab').forEach(function(t, i){
    t.classList.toggle('on', products[i] === p);
  });
  products.forEach(function(n){
    var el = document.getElementById('f-'+n);
    if(el) el.style.display = (n===p) ? (n==='barabany'?'block':'grid') : 'none';
  });
  document.getElementById('weight-box').style.display = 'none';
  if(p==='barabany') initDrumRows();
  document.getElementById('res-wrap').style.display = 'none';
}

function fillLens(){
  var d = +document.getElementById('r-d').value;
  var sel = document.getElementById('r-l');
  var lens = Object.keys(RP[d]||{}).map(Number).sort(function(a,b){return a-b;});
  for(var xl=1250;xl<=2000;xl+=50){ if(lens.indexOf(xl)<0) lens.push(xl); }
  lens.sort(function(a,b){return a-b;});
  sel.innerHTML = lens.map(function(l){
    return '<option value="'+l+'"'+(l===310?' selected':'')+'>'+l+'</option>';
  }).join('');
  updWeight();
}

function onQtyChange(){
  var q = +document.getElementById('r-q').value || 1;
  var row = getAutoMkup(q);
  document.getElementById('r-m').value = row.mk;
  var info = document.getElementById('markup-info');
  if(info){ info.style.display='block'; info.innerHTML='Авто-наценка: <b>'+row.mk+'%</b> ('+row.lbl+') — можно изменить вручную'; }
  updWeight();
}

function updWeight(){
  var d = +document.getElementById('r-d').value;
  var lEl = document.getElementById('r-l');
  var l = lEl ? +lEl.value : 0;
  var q = +document.getElementById('r-q').value || 1;
  var sd = +document.getElementById('r-shaft').value || 22;
  var wallEl = document.getElementById('r-wall');
  var wall = wallEl ? parseFloat(wallEl.value) : 4.0;
  var box = document.getElementById('weight-box');
  if(!d || !l){ if(box) box.style.display='none'; return; }
  var shKgMm = SHAFT_KGM_EX[sd] || 0.002944;
  var tubeKg = getTKGw(d, wall) * l;
  var shaftKg = shKgMm * (l + 30);
  var totalKg = tubeKg + shaftKg + 0.15*2 + 0.05*2;
  if(box) box.style.display = 'block';
  var wt=document.getElementById('w-tube'); if(wt) wt.textContent=tubeKg.toFixed(3)+' кг';
  var ws=document.getElementById('w-shaft'); if(ws) ws.textContent=shaftKg.toFixed(3)+' кг (Ф'+sd+')';
  var wo=document.getElementById('w-total'); if(wo) wo.textContent=totalKg.toFixed(3)+' кг';
  var batchEl=document.getElementById('w-batch');
  var batchBox=document.getElementById('w-batch-box');
  if(q>1){
    if(batchEl) batchEl.textContent=fn(q)+' шт = '+(totalKg*q).toFixed(1)+' кг / '+(totalKg*q/1000).toFixed(3)+' т';
    if(batchBox) batchBox.style.display='block';
  } else { if(batchBox) batchBox.style.display='none'; }
}

// Drum rows
function getDrumTpl(tp){
  if(tp==='drive') return [
    ['Труба (обечайка)',1,10875],['Вал к подшипнику',1,3700],
    ['Боковые вставки',2,764],['Подшипник',2,1580],
    ['Корпус подшипника',2,6800],['Крышка глухая',1,1000],
    ['Крышка сквозная',1,1000],['Футеровка резиновая',1,5865],
    ['Клей двухкомпонентный',1,2820],['Метизы, болты',1,500]
  ];
  return [
    ['Труба (обечайка)',1,10875],['Вал к подшипнику',1,5000],
    ['Боковые вставки',2,764],['Подшипник',2,1580],
    ['Корпус подшипника',2,6800],['Крышка глухая',2,1000],
    ['Метизы, болты',1,500]
  ];
}
function initDrumRows(){
  var tp = document.getElementById('b-t').value;
  document.getElementById('drum-rows').innerHTML = '';
  drumRowId = 0;
  getDrumTpl(tp).forEach(function(r){ addDrumRow(r[0], r[1], r[2]); });
}
function addDrumRow(name, qty, price){
  var id = ++drumRowId;
  var cont = document.getElementById('drum-rows');
  var div = document.createElement('div');
  div.className = 'drum-row';
  div.id = 'dr-'+id;
  div.innerHTML = '<input type="text" value="'+name+'" placeholder="Наименование"><input type="number" value="'+qty+'" min="1" style="width:70px"><input type="number" value="'+price+'" min="0" step="0.01" placeholder="Цена ₽"><button class="drum-del" onclick="document.getElementById(\'dr-'+id+'\').remove()">×</button>';
  cont.appendChild(div);
}
function getDrumRows(){
  var rows = [];
  document.querySelectorAll('#drum-rows .drum-row').forEach(function(row){
    var inp = row.querySelectorAll('input');
    var qty = +inp[1].value || 1;
    var price = +inp[2].value || 0;
    rows.push({n:inp[0].value||'Позиция', qty:qty, price:price, total:qty*price});
  });
  return rows;
}

function onBuksyChange(){
  var m = document.getElementById('bk-m').value;
  var inp = document.getElementById('bk-buy');
  if(BK[m]){
    inp.value = BK[m].mat + BK[m].brg;
    inp.disabled = true;
    inp.style.opacity = '0.6';
  } else {
    inp.value = UCP_BUY[m] || 0;
    inp.disabled = false;
    inp.style.opacity = '1';
  }
}

// ================================================================
//  РАСЧЁТЫ
// ================================================================
function doCalc(){
  var r = null;
  if(curP==='roliki') r = calcRoliki();
  else if(curP==='barabany') r = calcBarabany();
  else if(curP==='buksy') r = calcBuksy();
  else if(curP==='rolikoopory') r = calcRoliko();
  else if(curP==='konveyery') r = calcKonv();
  if(!r) return;
  lastResult = r;
  renderResult(r);
  pushHist(r);
}

function calcRoliki(){
  var d=+document.getElementById('r-d').value;
  var l=+document.getElementById('r-l').value;
  var wallEl=document.getElementById('r-wall');
  var wall=wallEl?parseFloat(wallEl.value):4.0;
  var q=+document.getElementById('r-q').value||1;
  var mk=+document.getElementById('r-m').value||70;
  var sd=+document.getElementById('r-shaft').value||22;
  var brgEl=document.getElementById('r-brg');
  var brg=parseBrg(brgEl?brgEl.value:'204|26');
  var p=getP();
  var tpr=p['t'+d]||63;
  var shPr=p['s'+sd]||53.6;
  var shKgMm=SHAFT_KGM_EX[sd]||0.002944;
  var kpuPr=KPU_PRICE[d]||60;
  var lkmKg=Math.PI*(d/1000)*(l/1000)*LKM_KGM2;
  var tubeKg=getTKGw(d,wall)*l;
  var shaftKg=shKgMm*(l+30);
  var mTube=tubeKg*tpr, mShaft=shaftKg*shPr;
  var mKpu=kpuPr*2, mBrg=brg.price*2;
  var mLkm=lkmKg*p.lkm, mTool=FREZ+LENTA_T+SOZ;
  var matU=mTube+mShaft+mKpu+mBrg+mLkm+mTool;
  var matT=matU*q;
  var priceU=Math.round(matU*(1+mk/100));
  var priceT=priceU*q;
  var pricePL=RP[d]?RP[d][l]:null;
  var profit=priceT-matT;
  var mg=(profit/priceT)*100;
  var shifts=Math.ceil(q/SHIFT.roliki);
  var ovhOrder=OVH*OVH_SH.roliki*shifts;
  var minU=Math.ceil(matU/0.9);
  var autoRow=getAutoMkup(q);
  return {
    type:'roliki',qty:q,
    title:'Ролики Ф'+d+'/ст.'+wall+'мм, вал Ф'+sd+', подш.'+brg.num+' — '+fn(q)+' шт',
    matT:matT,matU:matU,priceT:priceT,priceU:priceU,pricePL:pricePL,
    profit:profit,mg:mg,profitNet:profit-ovhOrder,
    ovhOrder:ovhOrder,shifts:shifts,shiftPlan:SHIFT.roliki,area:'Токарный участок',
    minU:minU,minT:minU*q,
    mats:[
      {n:'Труба Ф'+d+'×'+wall+' мм',qty:fn(q)+' шт',mass:(tubeKg*q).toFixed(2)+' кг',up:tpr,u1:mTube,tot:mTube*q},
      {n:'Круг Ф'+sd+' (вал), L='+(l+30)+' мм',qty:fn(q)+' шт',mass:(shaftKg*q).toFixed(2)+' кг',up:shPr,u1:mShaft,tot:mShaft*q},
      {n:'КПУ-'+d+'/'+brg.num+' · 2 шт',qty:fn(q*2)+' шт',mass:'—',up:kpuPr,u1:mKpu,tot:mKpu*q},
      {n:'Подшипник '+brg.num+' · 2 шт',qty:fn(q*2)+' шт',mass:'—',up:brg.price,u1:mBrg,tot:mBrg*q},
      {n:'ЛКМ RAL7024 · '+lkmKg.toFixed(4)+' кг/шт',qty:(lkmKg*q).toFixed(2)+' кг',mass:'—',up:p.lkm,u1:mLkm,tot:mLkm*q},
      {n:'Инструмент (фреза+лента+СОЖ)',qty:fn(q)+' шт',mass:'—',up:mTool,u1:mTool,tot:mTool*q}
    ],
    srcLines:[
      'Прайс_на_ролики.xlsx — TKG трубы Ф'+d+'/'+wall+'мм = '+getTKGw(d,wall).toFixed(7)+' кг/мм',
      'Прайс_на_ролики.xlsx — вал Ф'+sd+' = '+shKgMm.toFixed(6)+' кг/мм',
      'Калькуляции НикАрин 2024–2026 — КПУ-'+d+'/'+brg.num+'='+kpuPr+'₽, подш.'+brg.num+'='+brg.price+'₽',
      'Калькуляция сч.4170 (янв.2026) — ЛКМ 0.4854 кг/м², '+p.lkm+'₽/кг',
      'Авто-наценка: '+autoRow.mk+'% ('+autoRow.lbl+')'+(pricePL?' | Прайс НикАрин: '+f(pricePL)+'/шт':'')
    ],
    note:'Смен: '+shifts+'. Накладные токарного: '+f(ovhOrder)+'.'
  };
}

function calcBarabany(){
  var tp = document.getElementById('b-t').value;
  var D = +document.getElementById('b-d').value || 630;
  var wall = +document.getElementById('b-wall').value || 8;
  var Vd = +document.getElementById('b-vd').value || 80;
  var B = +document.getElementById('b-b').value || 1000;
  var q = +document.getElementById('b-q').value || 1;
  var mk = +document.getElementById('b-m').value || 40;
  var rows = getDrumRows();
  if(!rows.length){ alert('Добавьте позиции материалов!'); return null; }
  var matU = rows.reduce(function(s,r){ return s+r.total; }, 0);
  var matT = matU * q;
  var priceU = Math.round(matU * (1 + mk/100));
  var priceT = priceU * q;
  var profit = priceT - matT;
  var mg = (profit/priceT)*100;
  var shifts = Math.ceil(q / SHIFT.barabany);
  var ovhOrder = OVH * OVH_SH.barabany * shifts;
  var minU = Math.ceil(matU / 0.9);
  var tn = tp==='drive' ? 'приводной' : 'не приводной';
  return {
    type:'barabany', qty:q,
    title:'Барабан '+tn+' Ф'+D+'×'+B+' мм / стенка '+wall+' / вал Ф'+Vd+' — '+fn(q)+' шт',
    matT:matT, matU:matU, priceT:priceT, priceU:priceU, pricePL:null,
    profit:profit, mg:mg, profitNet:profit-ovhOrder,
    ovhOrder:ovhOrder, shifts:shifts, shiftPlan:SHIFT.barabany, area:'Сварочный пост',
    minU:minU, minT:minU*q,
    mats:rows.map(function(r){ return {n:r.n, qty:r.qty+' шт', mass:'—', up:r.price, u1:r.total, tot:r.total*q}; }),
    note:'Сменный план '+SHIFT.barabany+' шт/смена. Партия '+fn(q)+' шт = '+shifts+' смен. Накладные: '+f(ovhOrder)+'.'
  };
}

function calcBuksy(){
  var m = document.getElementById('bk-m').value;
  var q = +document.getElementById('bk-q').value || 1;
  var mk = +document.getElementById('bk-mk').value || 30;
  if(BK[m]){
    var b = BK[m];
    var matU = b.mat + b.brg;
    var matT = matU * q;
    var priceU = Math.round(matU * (1 + mk/100));
    var priceT = priceU * q;
    var profit = priceT - matT;
    var mg = (profit/priceT)*100;
    var minU = Math.ceil(matU / 0.9);
    return {
      type:'buksy', qty:q,
      title:'Букса '+m+' (Ф'+b.dia+' мм) — '+fn(q)+' шт',
      matT:matT, matU:matU, priceT:priceT, priceU:priceU, pricePL:b.price,
      profit:profit, mg:mg, profitNet:profit,
      ovhOrder:0, shifts:0, shiftPlan:0, area:'',
      minU:minU, minT:minU*q,
      mats:[
        {n:'Корпус '+m+' (с мех. обработкой)', qty:fn(q)+' шт', mass:'—', up:null, u1:b.mat-b.brg-200, tot:(b.mat-b.brg-200)*q},
        {n:'Подшипник (1 шт/букса)', qty:fn(q)+' шт', mass:'—', up:b.brg, u1:b.brg, tot:b.brg*q},
        {n:'Метизы, болты, манжеты, масленки', qty:fn(q)+' шт', mass:'—', up:200, u1:200, tot:200*q}
      ],
      note:'Цена рассчитана от наценки '+mk+'%. Справочная цена прайса НикАрин: '+f(b.price)+'/шт.'
    };
  } else {
    var buyU = +document.getElementById('bk-buy').value || UCP_BUY[m] || 0;
    var priceU2 = Math.round(buyU * (1 + mk/100));
    var priceT2 = priceU2 * q;
    var matT2 = buyU * q;
    var profit2 = priceT2 - matT2;
    var mg2 = (profit2/priceT2)*100;
    var nm = m.replace('ucp','UCP ');
    return {
      type:'buksy', qty:q,
      title:nm+' (d='+UCP_D[m]+' мм) — '+fn(q)+' шт',
      matT:matT2, matU:buyU, priceT:priceT2, priceU:priceU2, pricePL:null,
      profit:profit2, mg:mg2, profitNet:profit2,
      ovhOrder:0, shifts:0, shiftPlan:0, area:'',
      minU:Math.ceil(buyU/0.9), minT:Math.ceil(buyU/0.9)*q,
      mats:[{n:nm+' корпусной подшипниковый узел', qty:fn(q)+' шт', mass:'—', up:buyU, u1:buyU, tot:buyU*q}],
      note:'Покупное изделие, перепродажа. Наценка '+mk+'%.'
    };
  }
}

function calcRoliko(){
  var tp = document.getElementById('ro-t').value;
  var d = +document.getElementById('ro-d').value;
  var b = +document.getElementById('ro-b').value;
  var q = +document.getElementById('ro-q').value || 1;
  var mk = +document.getElementById('ro-m').value || 35;
  var nR = {r3:3,'3r':3,'1r':1,center:3,amort:3}[tp] || 3;
  var rl = Math.max(200, Math.min(Math.round(b/nR*0.9/50)*50, 1200));
  var sd = 22;
  var rm = matRoller(d, rl, sd);
  var rollerMat = rm.tube + rm.shaft + rm.kpu + rm.bearing + rm.lkm + rm.tool;
  var frameMat = 1800 * ({500:1.0,650:1.18,800:1.35,1000:1.6,1200:1.85,1400:2.1}[b]||1.35) * q;
  var matT = rollerMat * nR * q + frameMat;
  var matU = matT / q;
  var priceU = Math.round(matU * (1 + mk/100));
  var priceT = priceU * q;
  var profit = priceT - matT;
  var mg = (profit/priceT)*100;
  var shifts = Math.ceil(q / SHIFT.rolikoopory);
  var ovhOrder = OVH * OVH_SH.rolikoopory * shifts;
  var minU = Math.ceil(matU / 0.9);
  var tns = {'3r':'3-роликовая рядовая','1r':'1-роликовая нижняя',center:'Центрирующая',amort:'Амортизирующая'};
  return {
    type:'rolikoopory', qty:q,
    title:'Роликоопора '+tns[tp]+' Ф'+d+', лента '+b+' мм — '+fn(q)+' шт',
    matT:matT, matU:matU, priceT:priceT, priceU:priceU, pricePL:null,
    profit:profit, mg:mg, profitNet:profit-ovhOrder,
    ovhOrder:ovhOrder, shifts:shifts, shiftPlan:SHIFT.rolikoopory, area:'Сварочный пост',
    minU:minU, minT:minU*q,
    mats:[
      {n:'Ролики Ф'+d+'×'+rl+' мм ('+nR+' шт/рама)', qty:fn(nR*q)+' шт', mass:'—', up:Math.round(rollerMat), u1:rollerMat*nR, tot:rollerMat*nR*q},
      {n:'Рама металлоконструкция', qty:fn(q)+' шт', mass:'—', up:null, u1:frameMat/q, tot:frameMat}
    ],
    note:'Длина ролика ~'+rl+' мм. Сменный план '+SHIFT.rolikoopory+' шт/смена. Смен: '+shifts+'. Накладные: '+f(ovhOrder)+'.'
  };
}

function calcKonv(){
  var b=+document.getElementById('kl-b').value;
  var l=+document.getElementById('kl-l').value||5;
  var q=+document.getElementById('kl-q').value||1;
  var mk=+document.getElementById('kl-m').value||50;
  var beltEl=document.getElementById('kl-belt');
  var driveEl=document.getElementById('kl-drive');
  var panelEl=document.getElementById('kl-panel');
  var beltMult=beltEl?parseFloat(beltEl.value):1.0;
  var beltName=getBeltName(beltMult);
  var driveAdd=driveEl?(+driveEl.value||0):0;
  var panelAdd=panelEl?(+panelEl.value||0):0;
  var driveText=driveEl&&driveAdd>0?driveEl.options[driveEl.selectedIndex].text.split(' — ')[0]:'';
  var panelText=panelEl&&panelAdd>0?panelEl.options[panelEl.selectedIndex].text.split(' — ')[0]:'';
  var basePerM=KL_M[b]||70000;
  var baseMat=basePerM*l;
  var beltShare=baseMat*0.25;
  var adjustedMat=beltShare*beltMult+baseMat*0.75;
  var unitMat=adjustedMat+driveAdd+panelAdd;
  var matT=unitMat*q, matU=unitMat;
  var priceU=Math.round(matU*(1+mk/100));
  var priceT=priceU*q;
  var profit=priceT-matT, mg=(profit/priceT)*100;
  var shifts=Math.max(1,Math.ceil(q*3));
  var ovhOrder=OVH*OVH_SH.konveyery*shifts;
  var pricePerM=Math.round(priceU/l);
  var minU=Math.ceil(matU/0.9);
  var mats=[
    {n:'Лента '+b+' мм ('+beltName+')',qty:'~'+fn(l*1.08)+' м/шт',mass:'—',up:null,u1:beltShare*beltMult,tot:beltShare*beltMult*q},
    {n:'Барабаны (привод+натяжка)',qty:'2 шт',mass:'—',up:null,u1:baseMat*0.20,tot:baseMat*0.20*q},
    {n:'Ролики+роликоопоры',qty:'—',mass:'—',up:null,u1:baseMat*0.18,tot:baseMat*0.18*q},
    {n:'Металлоконструкция рамы',qty:'—',mass:'—',up:null,u1:baseMat*0.22,tot:baseMat*0.22*q},
    {n:'Натяжное устройство, очистители',qty:'—',mass:'—',up:null,u1:baseMat*0.10,tot:baseMat*0.10*q}
  ];
  if(driveAdd>0) mats.push({n:'Привод '+driveText,qty:'1 шт',mass:'—',up:driveAdd,u1:driveAdd,tot:driveAdd*q});
  if(panelAdd>0) mats.push({n:'Шкаф: '+panelText,qty:'1 шт',mass:'—',up:panelAdd,u1:panelAdd,tot:panelAdd*q});
  return {
    type:'konveyery',qty:q,
    title:'КЛ-'+b+', '+l+'м, '+beltName+(driveText?' '+driveText:'')+' — '+fn(q)+' шт',
    matT:matT,matU:matU,priceT:priceT,priceU:priceU,pricePL:null,pricePerM:pricePerM,
    profit:profit,mg:mg,profitNet:profit-ovhOrder,
    ovhOrder:ovhOrder,shifts:shifts,shiftPlan:SHIFT.konveyery,area:'Сварочный пост',
    minU:minU,minT:minU*q,mats:mats,
    srcLines:[
      'База: сч.1677 (янв.2026) — КЛ-400/5м=230388₽. Ставка '+fn(basePerM)+'₽/м для КЛ-'+b,
      'Лента: '+beltName+' (коэф.×'+beltMult+' к доле ленты 25% от себестоимости)',
      driveAdd>0?'Привод '+driveText+': +'+fn(driveAdd)+'₽':'Привод: не включён',
      panelAdd>0?'Шкаф управления '+panelText+': +'+fn(panelAdd)+'₽':'Шкаф управления: не включён'
    ],
    note:'Цена за 1 м.п.: '+f(pricePerM)+'. Накладные: '+f(ovhOrder)+'. Для КП нужны чертежи.'
  };
}

function renderResult(d){
  document.getElementById('res-title').textContent = d.title;
  document.getElementById('mc-mat').textContent = f(d.matT);
  document.getElementById('mc-mat-s').textContent = d.qty>1 ? f(d.matU)+' / шт' : '';
  document.getElementById('mc-price').textContent = f(d.priceT);
  document.getElementById('mc-price-s').textContent = f(d.priceU)+' / шт';
  var mg = Math.round(d.mg);
  var pe = document.getElementById('mc-profit');
  pe.textContent = f(d.profit);
  pe.className = 'mc-val ' + (mg>=30?'green':mg>=10?'ora':'red');
  document.getElementById('mc-profit-s').textContent = 'Маржа '+mg+'%';
  document.getElementById('min-u').textContent = f(d.minU);
  document.getElementById('min-t').textContent = f(d.minT);

  // Extra card
  var ec = document.getElementById('mc-extra');
  if(d.pricePL){
    ec.style.display='block';
    document.getElementById('mc-extra-lbl').textContent='Цена по прайсу НикАрин';
    document.getElementById('mc-extra-val').textContent=f(d.pricePL)+'/шт';
    document.getElementById('mc-extra-sub').textContent=f(d.pricePL*d.qty)+' за партию';
  } else if(d.pricePerM){
    ec.style.display='block';
    document.getElementById('mc-extra-lbl').textContent='Цена за 1 м.п.';
    document.getElementById('mc-extra-val').textContent=f(d.pricePerM);
    document.getElementById('mc-extra-sub').textContent='';
  } else {
    ec.style.display='none';
  }

  // Summary
  var bd = document.getElementById('bd-body');
  var rows = '';
  rows += brow('Себестоимость материалов', d.matT, 'blue');
  if(d.qty>1) rows += brow('Себестоимость 1 шт', d.matU, '');
  rows += drow('Цена реализации партии', d.priceT, d.qty>1 ? f(d.priceU)+'/шт' : '');
  rows += brow('Прибыль с заказа (маржа '+mg+'%)', d.profit, mg>=10?'green':'red');
  if(d.ovhOrder>0){
    rows += brow('Накладные · '+d.area+' ('+d.shifts+' смен)', d.ovhOrder, 'ora');
    rows += brow('Чистая прибыль с заказа', d.profitNet, d.profitNet>=0?'green':'red');
  }
  bd.innerHTML = rows;
  if(mg<10) bd.innerHTML += '<div class="warn-strip">⚠ Маржа '+mg+'% ниже 10%! Мин. цена: '+f(d.minU)+'/шт</div>';
  else if(mg>=25) bd.innerHTML += '<div class="ok-strip">✓ Хорошая маржа — '+mg+'%</div>';

  // Shift info
  var si = document.getElementById('shift-info');
  if(d.shifts>0 && d.shiftPlan>0){
    si.innerHTML = '<div class="ibox green"><b>📊 Производственный план · '+d.area+'</b>Сменный план: '+d.shiftPlan+' шт/смена. Партия '+fn(d.qty)+' шт = '+d.shifts+' смен. Накладные за '+d.shifts+' смен: '+f(d.ovhOrder)+'.</div>';
  } else si.innerHTML = '';

  // Spec table
  if(d.mats && d.mats.length){
    var trows = d.mats.map(function(m){
      return '<tr><td>'+m.n+'</td><td>'+m.qty+'</td><td class="tr">'+(m.mass&&m.mass!='—'?m.mass:'—')+'</td><td class="tr">'+(m.up?f(m.up):'—')+'</td><td class="tr" style="font-weight:700">'+f(m.u1)+'</td><td class="tr" style="font-weight:700">'+f(m.tot)+'</td></tr>';
    }).join('');
    var tot = d.mats.reduce(function(s,m){ return s+m.tot; }, 0);
    document.getElementById('spec-wrap').innerHTML =
      '<div class="sp-card"><div class="sp-head">Полная спецификация материалов</div>'+
      '<table><thead><tr><th>Наименование</th><th>Кол-во</th><th class="tr">Масса</th><th class="tr">Цена ед.</th><th class="tr">На 1 шт</th><th class="tr">Итого</th></tr></thead>'+
      '<tbody>'+trows+'</tbody>'+
      '<tfoot><tr><td colspan="4">Итого материалы</td><td class="tr">'+f(d.matU)+'</td><td class="tr">'+f(tot)+'</td></tr></tfoot>'+
      '</table></div>';
  } else document.getElementById('spec-wrap').innerHTML = '';

  // Источники данных
  var srcW=document.getElementById('src-wrap');
  if(srcW){
    if(d.srcLines&&d.srcLines.length){
      var sh='<div style="background:var(--s3);border:1px solid var(--bd);border-radius:var(--r2);padding:10px 14px;margin-bottom:11px;font-size:12px;line-height:1.7">';
      sh+='<div style="font-weight:700;color:var(--t2);margin-bottom:5px">📎 Источники данных расчёта</div>';
      d.srcLines.forEach(function(s){sh+='<div style="color:var(--t3)">· '+s+'</div>';});
      sh+='</div>';
      srcW.innerHTML=sh;
    } else srcW.innerHTML='';
  }
  document.getElementById('res-note').textContent = d.note || '';
  document.getElementById('res-wrap').style.display = 'block';
  document.getElementById('res-wrap').scrollIntoView({behavior:'smooth',block:'start'});
}

function brow(n,v,cls){
  return '<div class="brow"><span class="brow-n">'+n+'</span><span class="brow-v '+(cls||'')+'">'+f(v)+'</span></div>';
}
function drow(n,v,sub){
  return '<div class="drow"><span>'+n+(sub?'<span class="drow-sub"> · '+sub+'</span>':'')+'</span><span>'+f(v)+'</span></div>';
}

function resetCalc(){
  document.getElementById('res-wrap').style.display = 'none';
  window.scrollTo({top:0,behavior:'smooth'});
}

// ================================================================
//  КП — формирование через Blob URL
// ================================================================
function printResult(){
  if(!lastResult) return;
  var d = lastResult;
  var mats = d.mats.map(function(m){
    return '<tr><td style="padding:6px 10px;border-bottom:1px solid #e8eaed">'+m.n+'</td><td style="padding:6px 10px;border-bottom:1px solid #e8eaed;text-align:center">'+m.qty+'</td><td style="padding:6px 10px;border-bottom:1px solid #e8eaed;text-align:right">'+(m.up?f(m.up):'—')+'</td><td style="padding:6px 10px;border-bottom:1px solid #e8eaed;text-align:right;font-weight:700">'+f(m.tot)+'</td></tr>';
  }).join('');
  var mg = Math.round(d.mg);
  var parts = [
    '<!DOCTYPE html><html lang="ru"><head><meta charset="UTF-8"><title>'+d.title+'</title>',
    '<style>body{font-family:Arial,sans-serif;padding:20px;max-width:800px;margin:0 auto;color:#222}',
    'h1{color:#1a3a6b;font-size:18px;margin-bottom:12px}',
    '.grid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin-bottom:16px}',
    '.card{border:1px solid #dce0e8;border-radius:6px;padding:10px 12px}',
    '.card-lbl{font-size:10px;color:#888;text-transform:uppercase;margin-bottom:3px}',
    '.card-val{font-size:18px;font-weight:700;color:#1a3a6b}',
    'table{width:100%;border-collapse:collapse;font-size:13px}',
    'th{background:#1a3a6b;color:#fff;padding:7px 10px;text-align:left;font-size:11px}',
    '@media print{body{padding:8px}}',
    '</style></head><body>',
    '<h1>'+d.title+'</h1>',
    '<div class="grid">',
    '<div class="card"><div class="card-lbl">Себестоимость</div><div class="card-val">'+f(d.matT)+'</div><div style="font-size:11px;color:#888">'+f(d.matU)+'/шт</div></div>',
    '<div class="card"><div class="card-lbl">Цена реализации</div><div class="card-val">'+f(d.priceT)+'</div><div style="font-size:11px;color:#888">'+f(d.priceU)+'/шт</div></div>',
    '<div class="card"><div class="card-lbl">Прибыль (маржа '+mg+'%)</div><div class="card-val" style="color:'+(mg>=25?'#155f30':mg>=10?'#b85500':'#9e2222')+'">'+f(d.profit)+'</div></div>',
    '</div>',
    '<h3 style="font-size:14px;margin-bottom:8px">Спецификация материалов</h3>',
    '<table><thead><tr><th>Наименование</th><th>Кол-во</th><th style="text-align:right">Цена ед.</th><th style="text-align:right">Сумма</th></tr></thead>',
    '<tbody>'+mats+'</tbody></table>',
    '<p style="margin-top:14px;font-size:12px;color:#888">'+d.note+'</p>',
    '<p style="font-size:10px;color:#aaa;margin-top:20px">НикАрин · ПартнёрПромСнаб · г. Челябинск · '+new Date().toLocaleDateString('ru-RU')+'</p>',
    '</body></html>'
  ];
  var html = parts.join('');
  var blob = new Blob([html], {type: 'text/html;charset=utf-8'});
  var url = URL.createObjectURL(blob);
  var w = window.open(url, '_blank', 'width=860,height=700,scrollbars=yes');
  if(!w) alert('Разрешите всплывающие окна в браузере для печати.');
}

function openKP(){
  if(!lastResult){ alert('Сначала выполните расчёт!'); return; }
  document.getElementById('kp-modal').classList.add('on');
}

function printKP(){
  if(!lastResult) return;
  var d = lastResult;
  var client = document.getElementById('kp-client').value || '—';
  var contact = document.getElementById('kp-contact').value || '—';
  var days = document.getElementById('kp-days').value || 14;
  var payment = document.getElementById('kp-payment').value || '100% предоплата';
  var dateStr = new Date().toLocaleDateString('ru-RU');

  var trows = d.mats.map(function(m){
    return '<tr><td style="padding:7px 10px;border-bottom:1px solid #e0e4ea">'+m.n+'</td>'+
      '<td style="padding:7px 10px;border-bottom:1px solid #e0e4ea">'+m.qty+'</td>'+
      '<td style="padding:7px 10px;border-bottom:1px solid #e0e4ea;text-align:right">'+(m.up?f(m.up):'—')+'</td>'+
      '<td style="padding:7px 10px;border-bottom:1px solid #e0e4ea;text-align:right;font-weight:700">'+f(m.tot)+'</td></tr>';
  }).join('');

  var parts = [
    '<!DOCTYPE html><html lang="ru"><head><meta charset="UTF-8"><title>КП</title>',
    '<style>body{font-family:Arial,sans-serif;padding:30px;max-width:820px;margin:0 auto;color:#222}',
    'h1{color:#1a3a6b;font-size:20px}',
    '.meta{background:#f5f7fa;padding:12px;border-radius:6px;margin:14px 0;font-size:13px}',
    'table{width:100%;border-collapse:collapse}',
    'th{background:#1a3a6b;color:#fff;padding:8px 10px;text-align:left;font-size:12px}',
    '.tot{font-size:16px;font-weight:700;color:#1a3a6b}',
    '.cond{margin-top:20px;padding:12px;background:#f5f7fa;border-radius:6px;font-size:13px}',
    '@media print{body{padding:10px}}',
    '</style></head><body>',
    '<h1>НикАрин · ПартнёрПромСнаб · г. Челябинск</h1>',
    '<div style="color:#666;font-size:13px;margin-bottom:8px">Коммерческое предложение · '+dateStr+'</div>',
    '<div class="meta"><b>Клиент:</b> '+client+' &nbsp;·&nbsp; <b>Контакт:</b> '+contact+'</div>',
    '<h2 style="font-size:15px;margin-bottom:12px">'+d.title+'</h2>',
    '<table><thead><tr><th>Наименование</th><th>Кол-во</th><th style="text-align:right">Цена ед.</th><th style="text-align:right">Сумма</th></tr></thead>',
    '<tbody>'+trows+'</tbody></table>',
    '<table style="width:280px;margin-left:auto;margin-top:14px">',
    '<tr><td style="padding:4px 0;color:#666">Себестоимость:</td><td style="text-align:right">'+f(d.matT)+'</td></tr>',
    '<tr class="tot"><td style="padding:8px 0">ИТОГО К ОПЛАТЕ:</td><td style="text-align:right">'+f(d.priceT)+'</td></tr>',
    '</table>',
    '<div class="cond"><div><b>Срок поставки:</b> '+days+' дней</div><div><b>Условия оплаты:</b> '+payment+'</div></div>',
    '</body></html>'
  ];

  var html = parts.join('');
  var blob = new Blob([html], {type: 'text/html;charset=utf-8'});
  var url = URL.createObjectURL(blob);
  document.getElementById('kp-modal').classList.remove('on');
  var w = window.open(url, '_blank', 'width=860,height=700,scrollbars=yes,resizable=yes');
  if(!w){
    // Popup blocked - show inline instead
    var printDiv = document.getElementById('kp-inline-print');
    if(!printDiv){
      printDiv = document.createElement('div');
      printDiv.id = 'kp-inline-print';
      printDiv.style.cssText = 'position:fixed;inset:0;background:#fff;z-index:600;overflow:auto;padding:30px';
      printDiv.innerHTML = '<button onclick="this.parentNode.remove();document.getElementById(\'kp-inline-print\')&&document.getElementById(\'kp-inline-print\').remove()" style="position:fixed;top:16px;right:20px;padding:8px 18px;background:#1a3a6b;color:#fff;border:none;border-radius:6px;cursor:pointer;font-size:14px;z-index:601">✕ Закрыть</button><button onclick="window.print()" style="position:fixed;top:16px;right:110px;padding:8px 18px;background:#155f30;color:#fff;border:none;border-radius:6px;cursor:pointer;font-size:14px;z-index:601">⎙ Печать</button><div style=\"max-width:820px;margin:0 auto\">' + html + '</div>';
      document.body.appendChild(printDiv);
    }
  }
}

// ================================================================
//  ПАКЕТНЫЙ РАСЧЁТ
// ================================================================
function loadFile(input){
  var file = input.files[0];
  if(!file) return;
  document.getElementById('batch-fname').textContent = file.name;
  var reader = new FileReader();
  reader.onload = function(e){
    var text = e.target.result;
    var lines = text.split(/[\r\n]+/).filter(function(l){ return l.trim(); });
    var out = [];
    for(var i=0; i<lines.length; i++){
      var row = lines[i].split(/[;,|\t]/);
      if(row.length < 3) continue;
      if(i===0 && (isNaN(row[0]) || row[0].trim().toLowerCase().indexOf('диам')>=0)) continue;
      var dia = (row[0]||'').trim();
      var len = (row[1]||'').trim();
      var qty = (row[2]||'').trim();
      var mkp = (row[3]||'30').trim();
      if(!dia || !len || !qty) continue;
      out.push(dia+'x'+len+', '+qty+', '+mkp);
    }
    document.getElementById('batch-ta').value = out.join('\n');
    if(out.length > 0) runBatch();
  };
  reader.readAsText(file, 'utf-8');
}

function runBatch(){
  var text = document.getElementById('batch-ta').value.trim();
  if(!text){ alert('Введите позиции или загрузите файл'); return; }
  var lines = text.split('\n').filter(function(l){ return l.trim(); });
  var results = [];
  var p = getP();

  for(var i=0; i<lines.length; i++){
    var line = lines[i].trim();
    var clean = line.replace(/[×х]/g, 'x');
    var mt = clean.match(/(\d+)\s*[x]\s*(\d+)\s*[,;]\s*(\d+)\s*(?:[,;]\s*(\d+))?/);
    if(!mt){ results.push({err:true, raw:line}); continue; }
    var d = +mt[1], l = +mt[2], q = +mt[3], mk = +(mt[4]||30);
    if(!TKG[d]){ results.push({err:true, raw:line, msg:'Диаметр '+d+' не найден'}); continue; }
    var m = matRoller(d, l, 22);
    var matU = m.tube + m.shaft + m.kpu + m.bearing + m.lkm + m.tool;
    var matT = matU * q;
    var priceU = Math.round(matU * (1 + mk/100));
    var priceT = priceU * q;
    var profit = priceT - matT;
    var mg = Math.round((profit/priceT)*100);
    var shifts = Math.ceil(q / SHIFT.roliki);
    results.push({d:d, l:l, q:q, mk:mk, matU:matU, matT:matT, priceU:priceU, priceT:priceT, profit:profit, mg:mg, shifts:shifts, err:false});
  }

  var ok = results.filter(function(r){ return !r.err; });
  var totalPrice = ok.reduce(function(s,r){ return s+r.priceT; }, 0);
  var totalProfit = ok.reduce(function(s,r){ return s+r.profit; }, 0);

  var html = '<div class="sp-card"><div class="sp-head">Результаты: '+ok.length+' позиций из '+results.length+'</div>'+
    '<table><thead><tr><th>Позиция</th><th class="tr">Кол-во</th><th class="tr">Себест./шт</th><th class="tr">Цена/шт</th><th class="tr">Цена партии</th><th class="tr">Прибыль</th><th class="tr">Маржа</th><th class="tr">Смен</th></tr></thead><tbody>';

  results.forEach(function(r){
    if(r.err){
      html += '<tr><td colspan="8" style="color:var(--red)">⚠ Ошибка: '+r.raw+(r.msg?' ('+r.msg+')':'')+'</td></tr>';
    } else {
      var cls = r.mg>=25?'green':r.mg>=10?'':'red';
      html += '<tr><td>Ф'+r.d+'×'+r.l+' мм</td><td class="tr">'+fn(r.q)+'</td><td class="tr">'+f(r.matU)+'</td><td class="tr">'+f(r.priceU)+'</td><td class="tr" style="font-weight:700">'+f(r.priceT)+'</td><td class="tr">'+f(r.profit)+'</td><td class="tr '+(cls?cls:'')+'" style="font-weight:'+(r.mg<10?700:400)+'">'+r.mg+'%</td><td class="tr">'+r.shifts+'</td></tr>';
    }
  });
  html += '</tbody><tfoot><tr><td colspan="4"><b>ИТОГО</b></td><td class="tr">'+f(totalPrice)+'</td><td class="tr">'+f(totalProfit)+'</td><td colspan="2"></td></tr></tfoot></table></div>';
  document.getElementById('batch-result').innerHTML = html;
}

// ================================================================
//  ЗАГРУЗКА ПРОИЗВОДСТВА
// ================================================================
var LOAD_IDS = [{id:'ld-r',lbl:'Ролики',tp:'roliki'},{id:'ld-b',lbl:'Барабаны',tp:'barabany'},{id:'ld-ro',lbl:'Роликоопоры',tp:'rolikoopory'},{id:'ld-kl',lbl:'Конвейеры',tp:'konveyery'}];

function renderLoad(){
  var html = '';
  LOAD_IDS.forEach(function(it){
    var busy = +document.getElementById(it.id).value || 0;
    var free = Math.max(0, 5 - busy);
    var pct = Math.min(100, (busy/5)*100);
    var cls = pct>=100?'full':pct>=80?'warn':'';
    html += '<div style="margin-bottom:12px">';
    html += '<div style="display:flex;justify-content:space-between;font-size:13px;margin-bottom:3px">';
    html += '<span><b>'+it.lbl+'</b> · план '+SHIFT[it.tp]+' шт/смена</span>';
    html += '<span>'+busy+'/5 смен занято · <b style="color:'+(free>0?'var(--green)':'var(--red)')+'">свободно '+free+' смен</b></span>';
    html += '</div>';
    html += '<div class="load-bar-wrap"><div class="load-bar '+cls+'" style="width:'+pct+'%"></div></div>';
    html += '</div>';
  });
  document.getElementById('load-bars').innerHTML = html;
}

function checkLoad(){
  var tp = document.getElementById('ld-chk-type').value;
  var qty = +document.getElementById('ld-chk-qty').value || 1;
  var idMap = {roliki:'ld-r',barabany:'ld-b',rolikoopory:'ld-ro',konveyery:'ld-kl'};
  var busy = +document.getElementById(idMap[tp]).value || 0;
  var free = Math.max(0, 5 - busy);
  var needed = Math.ceil(qty / SHIFT[tp]);
  var el = document.getElementById('load-result');
  if(needed <= free){
    el.innerHTML = '<div class="ibox green"><b>✓ Заказ влезает на этой неделе</b>Нужно '+needed+' смен — свободно '+free+' смен. Можно запускать.</div>';
  } else {
    var extra = needed - free;
    el.innerHTML = '<div class="ibox" style="background:var(--rl);border:1px solid #f0b8b8;color:var(--red)"><b>⚠ Не влезает на этой неделе</b>Нужно '+needed+' смен, свободно только '+free+'. Перенос '+extra+' смен на следующую неделю → задержка ~'+extra+' раб. дней.</div>';
  }
}

// ================================================================
//  ЦЕНЫ
// ================================================================
function renderPriceEditor(){
  var p = getP();
  var d = localStorage.getItem('nik_pdate') || 'не сохранялись';
  document.getElementById('prices-date').textContent = d;
  var html = '';
  PRICE_FIELDS.forEach(function(fld){
    html += '<div class="price-item"><label>'+fld.lbl+'</label><input type="number" id="pe-'+fld.k+'" value="'+(p[fld.k]||0)+'" min="0" step="0.01"></div>';
  });
  document.getElementById('price-grid').innerHTML = html;
}

function savePrices(){
  var p = {};
  PRICE_FIELDS.forEach(function(fld){
    p[fld.k] = +document.getElementById('pe-'+fld.k).value || 0;
  });
  localStorage.setItem('nik_p', JSON.stringify(p));
  localStorage.setItem('nik_pdate', new Date().toLocaleDateString('ru-RU'));
  var msg = document.getElementById('prices-msg');
  msg.style.display = 'block';
  setTimeout(function(){ msg.style.display='none'; }, 3000);
  checkPriceAge();
}

function resetPrices(){
  if(!confirm('Сбросить все цены к исходным значениям?')) return;
  localStorage.removeItem('nik_p');
  localStorage.removeItem('nik_pdate');
  renderPriceEditor();
  document.getElementById('prices-date').textContent = 'не сохранялись';
}

function checkPriceAge(){
  var d = localStorage.getItem('nik_pdate');
  var w = document.getElementById('price-age-warn');
  if(!d){ w.style.display='none'; return; }
  var parts = d.split('.');
  if(parts.length<3){ w.style.display='none'; return; }
  var saved = new Date(+parts[2], +parts[1]-1, +parts[0]);
  var days = Math.round((Date.now() - saved.getTime()) / 86400000);
  if(days >= 45){
    document.getElementById('price-age-txt').textContent = 'Цены не обновлялись '+days+' дней';
    w.style.display = 'block';
  } else {
    w.style.display = 'none';
  }
}

// ================================================================
//  ИСТОРИЯ
// ================================================================
var hist = JSON.parse(localStorage.getItem('nik_hist') || '[]');

function pushHist(d){
  hist.unshift({
    ti: d.title, type: d.type,
    pr: d.priceT, mg: Math.round(d.mg),
    ts: new Date().toLocaleString('ru-RU',{day:'2-digit',month:'2-digit',hour:'2-digit',minute:'2-digit'}),
    data: d
  });
  if(hist.length > 50) hist = hist.slice(0,50);
  localStorage.setItem('nik_hist', JSON.stringify(hist));
}

function renderHist(){
  var ft = (document.getElementById('hf-type') || {}).value || '';
  var fm = +((document.getElementById('hf-mg') || {}).value || 0);
  var fq = ((document.getElementById('hf-q') || {}).value || '').toLowerCase();
  var filtered = hist.filter(function(h){
    if(ft && h.type !== ft) return false;
    if(fm && h.mg < fm) return false;
    if(fq && h.ti.toLowerCase().indexOf(fq) < 0) return false;
    return true;
  });
  var el = document.getElementById('hist-list');
  if(!el) return;
  if(!filtered.length){
    el.innerHTML = '<div style="text-align:center;padding:20px;color:var(--t3)">Нет расчётов по заданным фильтрам</div>';
    return;
  }
  el.innerHTML = filtered.map(function(h, i){
    var idx = hist.indexOf(h);
    return '<div class="hitem" onclick="replayHist('+idx+')">'+
      '<div><div class="hitem-n">'+h.ti+'</div><div class="hitem-m">'+h.ts+' · маржа '+h.mg+'%</div></div>'+
      '<div class="hitem-p">'+fn(h.pr)+' ₽</div></div>';
  }).join('');
}

function replayHist(i){
  if(!hist[i]) return;
  lastResult = hist[i].data;
  renderResult(hist[i].data);
  showPage('calc');
}

function clearHist(){
  if(!confirm('Очистить всю историю?')) return;
  hist = [];
  localStorage.removeItem('nik_hist');
  renderHist();
}

// ================================================================
// АНАЛИЗ РЫНОЧНЫХ ЦЕН РФ (без Китая)
// Источники: Русбелт, Борекс, НПФ ПромРегион, Зертех, Flagma (2025)
// ================================================================

var MKT = {
  roliki:{
    comps:['Русбелт (Москва)','Борекс (Екб)','НПФ ПромРегион'],
    coefSmall:2.8, coefMid:2.5, coefLarge:2.2,
    note:'Русбелт: Ф127×310=1605₽, Ф127×750=2855₽, Ф127×950=2450₽ (НПФ ПромРегион). Крупные партии дешевле на 15-20%.'
  },
  barabany:{
    comps:['Борекс (от 30000₽ опт)','Зертех (23% рынка РФ)','ИнтерМаш'],
    coefSmall:2.2, coefMid:1.9, coefLarge:1.7,
    note:'Борекс: приводной барабан 36 000₽ розница, 30 000₽ опт (от 20 шт). Нестандартные размеры — по запросу.'
  },
  buksy:{
    comps:['НПФ ПромРегион','Борекс','Рынок РФ (оценка)'],
    coefSmall:2.2, coefMid:2.0, coefLarge:1.8,
    note:'Буксы под конкретный барабан — прямых аналогов мало. Ориентир: +80-120% к себестоимости производителя.'
  },
  rolikoopory:{
    comps:['Русбелт','Зертех','НПО Аконит'],
    coefSmall:2.6, coefMid:2.4, coefLarge:2.0,
    note:'3-роликовая рядовая для ленты 800мм: 4 000–8 000₽ в зависимости от производителя и диаметра ролика.'
  },
  konveyery:{
    comps:['ИнтерМаш','Зертех (23% рынка)','НПО Аконит'],
    coefSmall:2.4, coefMid:2.2, coefLarge:1.9,
    note:'Цены конвейеров сильно зависят от комплектации. Данные ориентировочные — реальные КП запрашиваются у производителей.'
  }
};

function openMkt(result){
  var d=MKT[result.type]; if(!d) return;
  var coef=result.qty>200?d.coefLarge:result.qty>50?d.coefMid:d.coefSmall;
  var mktU=Math.round(result.matU*coef);
  var ourU=result.priceU;
  var pct=Math.round((ourU/mktU-1)*100);
  var sign=pct>0?'+':'';
  var rows='<div style="border:1px solid var(--bd);border-radius:var(--r2);overflow:hidden;margin-bottom:12px">';
  rows+='<div style="display:grid;grid-template-columns:1fr auto auto;background:var(--blue);color:#fff">';
  rows+='<div style="padding:7px 12px;font-size:11px;font-weight:700;text-transform:uppercase">Поставщик</div>';
  rows+='<div style="padding:7px 12px;font-size:11px;font-weight:700;text-align:right">Цена/шт</div>';
  rows+='<div style="padding:7px 12px;font-size:11px;font-weight:700;text-align:right">Партия</div></div>';
  var coefs=[1.0,0.92,1.08];
  d.comps.forEach(function(name,i){
    var cp=Math.round(mktU*coefs[i]);
    rows+='<div style="display:grid;grid-template-columns:1fr auto auto;border-bottom:1px solid var(--bd)">';
    rows+='<div style="padding:7px 12px;font-size:13px"><b>'+name+'</b></div>';
    rows+='<div style="padding:7px 12px;text-align:right;font-weight:600;font-size:13px">'+f(cp)+'</div>';
    rows+='<div style="padding:7px 12px;text-align:right;font-size:13px">'+f(cp*result.qty)+'</div></div>';
  });
  rows+='<div style="display:grid;grid-template-columns:1fr auto auto;background:var(--bl)">';
  rows+='<div style="padding:7px 12px;font-size:13px"><b style="color:var(--blue)">НикАрин (ваш расчёт)</b></div>';
  rows+='<div style="padding:7px 12px;text-align:right;font-weight:700;font-size:13px;color:var(--blue)">'+f(ourU)+'</div>';
  rows+='<div style="padding:7px 12px;text-align:right;font-weight:700;font-size:13px;color:var(--blue)">'+f(result.priceT)+'</div></div>';
  rows+='</div>';
  var vbg, vcl, vtxt;
  if(pct<-10){vbg=var_gl;vcl='#0f4a25';vtxt='✓ Ваша цена на '+Math.abs(pct)+'% НИЖЕ рынка — сильное конкурентное преимущество!';}
  else if(pct<=10){vbg='var(--ol)';vcl='var(--ora)';vtxt='≈ Ваша цена в рынке ('+sign+pct+'% от среднего). Хорошая позиция.';}
  else{vbg='var(--rl)';vcl='var(--red)';vtxt='⚠ Ваша цена на '+Math.abs(pct)+'% выше рынка. Проверьте наценку.';}
  rows+='<div style="padding:10px 13px;border-radius:var(--r2);font-size:13px;font-weight:600;background:'+vbg+';color:'+vcl+'">'+vtxt+'</div>';
  rows+='<div style="margin-top:10px;padding:9px 13px;background:var(--s3);border-radius:var(--r2);font-size:11.5px;color:var(--t3);line-height:1.65">'+d.note+'</div>';
  document.getElementById('mkt-body').innerHTML=rows;
  document.getElementById('mkt-overlay').classList.add('on');
}
var var_gl='var(--gl)';
function closeMkt(){document.getElementById('mkt-overlay').classList.remove('on');}

// ================================================================
//  INIT
// ================================================================
fillLens();
onQtyChange();
onBuksyChange();
checkPriceAge();
renderLoad();
</script>

<!-- ПОПАП РЫНОЧНОГО АНАЛИЗА -->
<div id="mkt-overlay" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,.55);z-index:400;align-items:center;justify-content:center" onclick="if(event.target===this)closeMkt()">
  <div style="background:var(--s);border-radius:var(--r);padding:24px;max-width:540px;width:92%;box-shadow:0 8px 40px rgba(0,0,0,.22);max-height:85vh;overflow-y:auto">
    <div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:4px">
      <div style="font-size:16px;font-weight:700;color:var(--blue)">📊 Анализ цен рынка РФ</div>
      <button onclick="closeMkt()" style="border:none;background:transparent;font-size:22px;cursor:pointer;color:var(--t3);line-height:1;padding:0">×</button>
    </div>
    <div style="font-size:11.5px;color:var(--t3);margin-bottom:16px">Открытые прайсы производителей РФ: Русбелт, Борекс, НПФ ПромРегион, Зертех · Китай исключён · 2025 г.</div>
    <div id="mkt-body"></div>
  </div>
</div>

</body>
</html>
