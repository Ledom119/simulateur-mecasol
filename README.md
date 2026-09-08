<style>
#solar-tool, #solar-tool * { box-sizing: border-box; }
    #solar-tool {
      --green: #c5f90b; --dark: #172019; --muted: #657067; --line: #dfe5df;
      width: min(1980px, 99vw);
      max-width: none;
      position: relative;
      left: 50%;
      transform: translateX(-50%);
      margin: 6px 0;
      padding: 2px;
      font-family: Arial, Helvetica, sans-serif; color: var(--dark);
    }
    #solar-tool .ms-grid { display:grid; grid-template-columns:1fr 1fr; gap:18px; align-items:stretch; }
    #solar-tool .ms-card { width:100%; min-width:0; border: 1px solid var(--line); border-radius: 18px; padding: 14px 18px; background: #fff; box-shadow: 0 12px 35px rgba(20,35,23,.08); }
    #solar-tool .ms-number { display:inline-grid; place-items:center; width:28px; height:28px; margin-bottom:5px; border-radius:50%; background:var(--green); font-weight:800; }
    #solar-tool h2 { margin: 0 0 8px; font-size: clamp(1.15rem,1.35vw,1.45rem); line-height:1.2; }
    #solar-tool .ms-intro { min-height:0; margin:0 0 8px; color:var(--muted); line-height:1.25; }
    #solar-tool label { display:block; margin: 0 0 7px; font-size:.94rem; font-weight:700; }
    #solar-tool input, #solar-tool select { width:100%; min-height:38px; padding:7px 10px; border:1px solid #bcc6bd; border-radius:10px; background:#fff; color:var(--dark); font-size:1rem; }
    #solar-tool .ms-card:first-child .ms-fields { grid-template-columns:minmax(290px,1.25fr) minmax(190px,.75fr); }
    #solar-tool .ms-first-layout { display:grid; grid-template-columns:minmax(0,1.15fr) minmax(250px,.85fr); gap:12px; align-items:end; }
    #solar-tool .ms-first-layout .ms-result { margin-top:0; }
    #solar-tool input:focus, #solar-tool select:focus { outline:3px solid rgba(197,249,11,.35); border-color:#718d08; }
    #solar-tool #ms-period { font-size:.96rem; padding-right:34px; }
    #solar-tool .ms-fields { display:grid; grid-template-columns:1fr 1fr; gap:14px; }
    #solar-tool .ms-field-wide { grid-column:1/-1; }
    #solar-tool .ms-result { margin-top:8px; padding:10px 12px; border-radius:14px; background:var(--dark); color:#fff; }
    #solar-tool .ms-result small { display:block; color:#cfd6d0; font-size:.82rem; }
    #solar-tool .ms-result strong { display:block; margin:4px 0; color:var(--green); font-size:clamp(1.45rem,2.2vw,1.9rem); line-height:1; }
    #solar-tool .ms-result p { margin:5px 0 0; line-height:1.35; }
    #solar-tool .ms-stats { display:grid; grid-template-columns:repeat(3,1fr); gap:8px; margin-top:0; }
    #solar-tool .ms-second-top { display:grid; grid-template-columns:minmax(0,.9fr) minmax(360px,1.1fr); gap:12px; align-items:end; }
    #solar-tool .ms-stat { padding:6px 6px; border-radius:10px; background:#f2f5f2; text-align:center; }
    #solar-tool .ms-stat strong { display:block; font-size:1.1rem; }
    #solar-tool .ms-stat span { color:var(--muted); font-size:.76rem; }
    #solar-tool .ms-chart-wrap { margin:0; min-width:0; }
    #solar-tool .ms-charts { display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-top:8px; }
    #solar-tool .ms-chart-title { margin:0 0 5px; font-size:.88rem; }
    #solar-tool canvas { display:block; width:100%; height:100px; border-radius:10px; background:#fafcf9; }

    @media (max-width: 1180px) {
      #solar-tool {
        width: calc(100vw - 16px);
      }
      #solar-tool .ms-first-layout,
      #solar-tool .ms-second-top { grid-template-columns:1fr; }
      #solar-tool .ms-stats { margin-top:8px; }
    }
    @media (max-width: 800px) {
      #solar-tool { left:0; transform:none; width:100%; }
      #solar-tool .ms-grid { grid-template-columns:1fr; }
      #solar-tool .ms-card { padding:18px 16px; }
      #solar-tool .ms-intro { min-height:0; }
    }

    @media (max-width: 650px) {
      #solar-tool .ms-charts { grid-template-columns:1fr; }
    }
    @media (max-width: 430px) {
      #solar-tool .ms-fields,
      #solar-tool .ms-card:first-child .ms-fields { grid-template-columns:1fr; }
      #solar-tool .ms-field-wide { grid-column:auto; }
    }
</style>

<section id="solar-tool" aria-label="Calcul solaire">
  <div class="ms-grid">
    <article class="ms-card">
      <span class="ms-number">1</span>
      <h2>Estimez la puissance solaire nécessaire</h2>
      <p class="ms-intro">Indiquez votre consommation annuelle ou journalière pour obtenir une première estimation de la puissance photovoltaïque à installer.</p>
      <div class="ms-first-layout">
        <div class="ms-fields">
          <div>
            <label for="ms-period">Type de consommation</label>
            <select id="ms-period">
              <option value="daily">Consommation journalière</option>
              <option value="annual">Consommation annuelle</option>
            </select>
          </div>
          <div>
            <label for="ms-consumption" id="ms-consumption-label">Consommation (kWh/jour)</label>
            <input id="ms-consumption" type="number" min="0" step="0.1" value="20" inputmode="decimal">
          </div>
        </div>
        <div class="ms-result" aria-live="polite">
          <small>Puissance photovoltaïque estimée</small>
          <strong id="ms-required-kwp">5,00 kWc</strong>
          <p id="ms-required-detail">Soit environ 12 panneaux de 450 Wc.</p>
        </div>
      </div>
    </article>

    <article class="ms-card">
      <span class="ms-number">2</span>
      <h2>Simulez la production de vos panneaux</h2>
      <p class="ms-intro">Choisissez le nombre de panneaux pour visualiser la production solaire moyenne sur une journée et sa répartition sur l’année.</p>
      <div class="ms-second-top">
        <div class="ms-fields">
          <div>
            <label for="ms-panels">Nombre de panneaux</label>
            <input id="ms-panels" type="number" min="1" max="500" step="1" value="12" inputmode="numeric">
          </div>
          <div>
            <label for="ms-panel-power">Puissance d’un panneau</label>
            <select id="ms-panel-power">
              <option value="400">400 Wc</option><option value="450" selected>450 Wc</option><option value="500">500 Wc</option><option value="550">550 Wc</option>
            </select>
          </div>
        </div>
        <div class="ms-stats" aria-live="polite">
        <div class="ms-stat"><strong id="ms-installed">5,40 kWc</strong><span>puissance installée</span></div>
        <div class="ms-stat"><strong id="ms-daily">21,6 kWh</strong><span>production/jour</span></div>
        <div class="ms-stat"><strong id="ms-annual">7 884 kWh</strong><span>production/an</span></div>
        </div>
      </div>
      <div class="ms-charts">
        <div class="ms-chart-wrap"><h3 class="ms-chart-title">Production moyenne au cours d’une journée</h3><canvas id="ms-day-chart" width="560" height="100" role="img" aria-label="Graphique de production solaire journalière"></canvas></div>
        <div class="ms-chart-wrap"><h3 class="ms-chart-title">Production estimée par mois</h3><canvas id="ms-year-chart" width="560" height="100" role="img" aria-label="Graphique de production solaire annuelle"></canvas></div>
      </div>
    </article>
  </div>
</section>

<script>
(function () {
  const root = document.getElementById('solar-tool');
  if (!root) return;
  const q = s => root.querySelector(s);
  const fmt = (n, d=1) => new Intl.NumberFormat('fr-FR',{minimumFractionDigits:d,maximumFractionDigits:d}).format(n);
  const period=q('#ms-period'), consumption=q('#ms-consumption'), label=q('#ms-consumption-label');
  const panels=q('#ms-panels'), panelPower=q('#ms-panel-power');

  function updateRequired(){
    const amount=Math.max(0,Number(consumption.value)||0);
    const daily=period.value==='annual'?amount/365:amount;
    const kwp=daily/4, count=Math.ceil((kwp*1000)/450);
    label.textContent=period.value==='annual'?'Consommation (kWh/an)':'Consommation (kWh/jour)';
    q('#ms-required-kwp').textContent=fmt(kwp,2)+' kWc';
    q('#ms-required-detail').textContent='Soit environ '+count+' panneau'+(count>1?'x':'')+' de 450 Wc.';
  }

  function drawBars(canvas, values, labels, color){
    const ctx=canvas.getContext('2d'), dpr=window.devicePixelRatio||1;
    const w=Math.max(220,canvas.clientWidth), h=100;
    canvas.width=w*dpr; canvas.height=h*dpr; ctx.scale(dpr,dpr); ctx.clearRect(0,0,w,h);
    const pad={l:28,r:6,t:6,b:18}, cw=w-pad.l-pad.r, ch=h-pad.t-pad.b, max=Math.max(...values,1);
    ctx.strokeStyle='#dfe5df'; ctx.lineWidth=1;
    for(let i=0;i<4;i++){const y=pad.t+ch*i/3;ctx.beginPath();ctx.moveTo(pad.l,y);ctx.lineTo(w-pad.r,y);ctx.stroke();}
    const slot=cw/values.length, bw=Math.max(3,slot*.62);
    values.forEach((v,i)=>{const bh=v/max*ch,x=pad.l+i*slot+(slot-bw)/2,y=pad.t+ch-bh;ctx.fillStyle=color;ctx.beginPath();ctx.roundRect(x,y,bw,bh,Math.min(4,bw/2));ctx.fill();});
    ctx.fillStyle='#657067';ctx.font='10px Arial';ctx.textAlign='center';
    labels.forEach((t,i)=>{if(values.length<=12||i%3===0)ctx.fillText(t,pad.l+i*slot+slot/2,h-8);});
    ctx.textAlign='right';ctx.fillText(fmt(max,0),pad.l-5,pad.t+4);ctx.fillText('0',pad.l-5,pad.t+ch+4);
  }

  function updateProduction(){
    const n=Math.max(1,Math.round(Number(panels.value)||1)), watts=Number(panelPower.value)||450;
    panels.value=n; const kwp=n*watts/1000, daily=kwp*4, annual=daily*365;
    q('#ms-installed').textContent=fmt(kwp,2)+' kWc';q('#ms-daily').textContent=fmt(daily,1)+' kWh';q('#ms-annual').textContent=fmt(annual,0)+' kWh';
    const shape=[0,0,0,0,0,0.03,0.08,0.13,0.17,0.20,0.22,0.24,0.24,0.22,0.19,0.15,0.09,0.04,0,0,0,0,0,0];
    const sum=shape.reduce((a,b)=>a+b,0), hours=shape.map(x=>x/sum*daily);
    drawBars(q('#ms-day-chart'),hours,Array.from({length:24},(_,i)=>i+'h'),'#c5f90b');
    const factors=[1.05,1.08,1.12,1.08,0.98,0.88,0.82,0.90,0.98,1.02,1.03,1.06];
    const days=[31,28,31,30,31,30,31,31,30,31,30,31], weighted=factors.reduce((s,f,i)=>s+f*days[i],0);
    const months=factors.map((f,i)=>annual*f*days[i]/weighted);
    drawBars(q('#ms-year-chart'),months,['J','F','M','A','M','J','J','A','S','O','N','D'],'#172019');
  }
  period.addEventListener('change',()=>{consumption.value=period.value==='annual'?7300:20;updateRequired();});
  consumption.addEventListener('input',updateRequired);panels.addEventListener('input',updateProduction);panelPower.addEventListener('change',updateProduction);
  window.addEventListener('resize',updateProduction);updateRequired();updateProduction();
})();
</script>
