<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SPCE — Comparador</title>
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>⚡</text></svg>">
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --bg:#f7f9f7;--bg2:#ffffff;--bg3:#f0f4f1;--bg4:#e8efe9;
  --green:#16a34a;--green2:#15803d;--green3:#dcfce7;--green4:#bbf7d0;--greenbright:#22c55e;
  --text:#0f1f14;--text2:#3d6349;--text3:#7a9e82;
  --border:#e2ede4;--border2:#c8deca;
  --red:#dc2626;--amber:#d97706;--blue:#0284c7;
  --fh:'Outfit',sans-serif;--fm:'JetBrains Mono',monospace;
  --r:10px;--r2:16px;
  --shadow:0 1px 3px rgba(0,0,0,.06),0 4px 16px rgba(0,0,0,.04);
  --shadow2:0 2px 8px rgba(0,0,0,.08),0 8px 32px rgba(0,0,0,.06);
}
body{background:var(--bg);color:var(--text);font-family:var(--fh);height:100vh;overflow:hidden;display:flex;flex-direction:column}

/* TOPO */
.top{flex-shrink:0;display:flex;align-items:center;justify-content:space-between;padding:.65rem 2rem;border-bottom:1px solid var(--border);background:var(--bg2);box-shadow:var(--shadow)}
.logo{font-family:var(--fh);font-weight:800;font-size:1.1rem;color:var(--green);display:flex;align-items:center;gap:.4rem}
.logo-dot{width:7px;height:7px;border-radius:50%;background:var(--greenbright);animation:pulse 2s infinite}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(.8)}}
.grupo-nav{display:flex;align-items:center;gap:.6rem}
.gnav-btn{background:none;border:1px solid var(--border2);color:var(--text2);width:30px;height:30px;border-radius:50%;font-size:1rem;display:flex;align-items:center;justify-content:center;cursor:pointer;transition:all .2s}
.gnav-btn:hover:not(:disabled){border-color:var(--green);color:var(--green);background:var(--green3)}
.gnav-btn:disabled{opacity:.3;cursor:not-allowed}
.grupo-info{text-align:center}
.grupo-num{font-family:var(--fm);font-size:.65rem;color:var(--text3);letter-spacing:.06em}
.grupo-nome{font-family:var(--fh);font-size:.95rem;font-weight:700;color:var(--text);letter-spacing:-.02em}
.top-right{display:flex;align-items:center;gap:.75rem}
.progresso{display:flex;gap:.25rem}
.pdot{width:24px;height:3px;border-radius:2px;background:var(--border2);transition:all .3s}
.pdot.on{background:var(--green)}
.fechar{background:none;border:1px solid var(--border);color:var(--text3);width:30px;height:30px;border-radius:50%;font-size:.85rem;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .2s}
.fechar:hover{border-color:var(--red);color:var(--red);background:#fff5f5}

/* CARROS HEADER */
.carros-header{flex-shrink:0;display:grid;border-bottom:1px solid var(--border);background:var(--bg2)}
.carro-col{padding:.75rem 1.25rem;display:flex;align-items:center;gap:.85rem;border-right:1px solid var(--border)}
.carro-col:last-child{border-right:none}
.cfoto-wrap{width:80px;height:52px;border-radius:var(--r);overflow:hidden;background:var(--bg3);flex-shrink:0;border:1px solid var(--border)}
.cfoto-wrap img{width:100%;height:100%;object-fit:cover}
.cfoto-ph{width:100%;height:100%;display:flex;align-items:center;justify-content:center;font-family:var(--fh);font-size:1.2rem;font-weight:800;color:var(--border2)}
.cinfo{flex:1;min-width:0}
.cmarca-tag{font-family:var(--fm);font-size:.62rem;color:var(--text3);letter-spacing:.06em;text-transform:uppercase;margin-bottom:.1rem}
.cmodelo{font-family:var(--fh);font-size:.95rem;font-weight:700;line-height:1.1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;letter-spacing:-.02em}
.cversao{font-size:.72rem;color:var(--text2);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.cpreco-tag{font-family:var(--fh);font-size:.82rem;font-weight:700;color:var(--green);margin-top:.15rem}
.vplacar{background:var(--green3);border:1px solid var(--green4);border-radius:100px;padding:.18rem .55rem;font-family:var(--fm);font-size:.7rem;font-weight:500;color:var(--green);margin-left:auto;flex-shrink:0}

/* CONTEÚDO */
.content{flex:1;overflow:hidden;position:relative}
.grupo-slide{position:absolute;inset:0;display:flex;flex-direction:column;padding:1.25rem 2rem;opacity:0;transform:translateX(40px);transition:all .35s cubic-bezier(.4,0,.2,1);pointer-events:none}
.grupo-slide.active{opacity:1;transform:translateX(0);pointer-events:all}
.grupo-slide.saindo{opacity:0;transform:translateX(-40px)}

/* CRITÉRIOS */
.criterios{display:flex;flex-direction:column;gap:.45rem;flex:1;overflow-y:auto}
.criterio{display:grid;align-items:center;background:var(--bg2);border:1px solid var(--border);border-radius:var(--r2);padding:.6rem 1rem;transition:all .3s;animation:slideIn .35s ease both;box-shadow:var(--shadow)}
@keyframes slideIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
.criterio:hover{border-color:var(--border2);box-shadow:var(--shadow2)}
.criterio-label{font-family:var(--fm);font-size:.68rem;color:var(--text3);padding-right:.75rem;letter-spacing:.02em}
.criterio-val{text-align:center;font-size:.9rem;font-weight:500;color:var(--text);padding:.18rem .45rem;border-radius:var(--r);transition:all .3s}
.criterio-val.melhor{color:#fff;background:var(--green);font-weight:600}
.criterio-val.pior{color:var(--red)}

/* SLIDE PLACAR FINAL */
.placar-final{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:1.5rem}
.placar-titulo{font-family:var(--fm);font-size:.75rem;font-weight:500;color:var(--text3);letter-spacing:.1em;text-transform:uppercase}
.placar-carros{display:flex;align-items:flex-end;gap:2rem;justify-content:center}
.placar-carro{display:flex;flex-direction:column;align-items:center;gap:.6rem;transition:all .4s}
.placar-foto{border-radius:var(--r2);overflow:hidden;background:var(--bg3);border:2px solid var(--border)}
.placar-foto img{width:100%;height:100%;object-fit:cover;display:block}
.placar-foto-ph{width:100%;height:100%;display:flex;align-items:center;justify-content:center;font-family:var(--fh);font-weight:800;color:var(--border2)}
.placar-nome{font-family:var(--fh);font-weight:700;text-align:center;line-height:1.1;letter-spacing:-.02em}
.placar-pts{font-family:var(--fm);font-size:2.2rem;font-weight:500;color:var(--green);line-height:1}
.placar-pts-label{font-family:var(--fm);font-size:.65rem;color:var(--text3);letter-spacing:.06em;text-transform:uppercase}
.placar-carro.vencedor .placar-foto{border-color:var(--green);box-shadow:0 0 0 4px var(--green3)}
.placar-carro.vencedor .placar-nome{color:var(--green)}
.coroa{font-size:1.4rem;animation:float 2s ease-in-out infinite}
@keyframes float{0%,100%{transform:translateY(0)}50%{transform:translateY(-5px)}}
.empate-tag{background:var(--green3);border:1px solid var(--green4);color:var(--green2);font-family:var(--fm);font-size:.72rem;font-weight:500;padding:.35rem .9rem;border-radius:100px;letter-spacing:.04em}

/* BARRA INFERIOR */
.bottom{flex-shrink:0;display:flex;align-items:center;justify-content:space-between;padding:.65rem 2rem;border-top:1px solid var(--border);background:var(--bg2)}
.bnav-btn{display:flex;align-items:center;gap:.4rem;background:none;border:1px solid var(--border2);color:var(--text2);padding:.42rem 1rem;border-radius:100px;font-size:.78rem;font-family:var(--fh);cursor:pointer;transition:all .2s}
.bnav-btn:hover:not(:disabled){border-color:var(--green);color:var(--green);background:var(--green3)}
.bnav-btn:disabled{opacity:.3;cursor:not-allowed}
.bnav-btn.proximo{background:var(--green);border-color:var(--green);color:#fff;font-weight:600}
.bnav-btn.proximo:hover{background:var(--green2)}
.grupo-dots{display:flex;gap:.35rem}
.gdot{width:6px;height:6px;border-radius:50%;background:var(--border2);border:none;cursor:pointer;transition:all .2s;padding:0}
.gdot.on{background:var(--green);width:16px;border-radius:3px}

/* KEYBOARD HINT */
.kbd-hint{font-family:var(--fm);font-size:.62rem;color:var(--text3);display:flex;align-items:center;gap:.3rem}
.kbd{background:var(--bg3);border:1px solid var(--border2);border-radius:4px;padding:.1rem .35rem;font-size:.6rem}
</style>
</head>
<body>

<!-- TOPO -->
<div class="top">
  <div class="logo">
    <div class="logo-dot"></div>
    SPCE
  </div>
  <div class="grupo-nav">
    <button class="gnav-btn" id="btn-prev" onclick="navGrupo(-1)" disabled>‹</button>
    <div class="grupo-info">
      <div class="grupo-num" id="gnav-num">GRUPO 1 DE 8</div>
      <div class="grupo-nome" id="gnav-nome">Fabricante</div>
    </div>
    <button class="gnav-btn" id="btn-next" onclick="navGrupo(1)">›</button>
  </div>
  <div class="top-right">
    <div class="kbd-hint"><span class="kbd">←</span><span class="kbd">→</span> navegar</div>
    <div class="progresso" id="progresso"></div>
    <button class="fechar" onclick="window.close()" title="Fechar">✕</button>
  </div>
</div>

<!-- HEADER CARROS -->
<div class="carros-header" id="carros-header"></div>

<!-- CONTEÚDO -->
<div class="content" id="content"></div>

<!-- BARRA INFERIOR -->
<div class="bottom">
  <button class="bnav-btn" id="bbtn-prev" onclick="navGrupo(-1)" disabled>‹ Anterior</button>
  <div class="grupo-dots" id="grupo-dots"></div>
  <button class="bnav-btn proximo" id="bbtn-next" onclick="navGrupo(1)">Próximo ›</button>
</div>

<script>
let CARROS=[], grupoAtual=0, pontos=[]

const GRUPOS=[
  {n:'1',nome:'Fabricante',criterios:[
    {l:'Nota Reclame Aqui',k:'reclame_aqui_nota',tp:'num',m:'maior',suf:'/10'},
    {l:'Fabricado em',k:'fabricado_em',tp:'txt'},
    {l:'Status',k:'status_venda',tp:'txt'},
    {l:'Isenção PcD',k:'pcd_isencao',tp:'bool'},
  ]},
  {n:'2',nome:'Bateria e Motor',criterios:[
    {l:'Bateria',k:'bateria_kwh',tp:'num',m:'maior',suf:' kWh'},
    {l:'Potência elétrica',k:'potencia_cv',tp:'num',m:'maior',suf:' cv'},
    {l:'Potência combinada',k:'potencia_combinada_cv',tp:'num',m:'maior',suf:' cv'},
    {l:'Torque',k:'torque_kgfm',tp:'num',m:'maior',suf:' kgf.m'},
    {l:'0–100 km/h',k:'zero_100_s',tp:'num',m:'menor',suf:'s'},
    {l:'Vel. máxima',k:'vel_max_kmh',tp:'num',m:'maior',suf:' km/h'},
    {l:'Tração',k:'tracao',tp:'txt'},
  ]},
  {n:'3',nome:'Autonomia INMETRO',criterios:[
    {l:'Autonomia elétrica',k:'autonomia_km',tp:'num',m:'maior',suf:' km'},
    {l:'Consumo',k:'consumo_kmkwh',tp:'num',m:'maior',suf:' km/kWh'},
    {l:'Consumo cidade (HEV)',k:'autonomia_hev_cidade',tp:'num',m:'maior',suf:' km/l'},
    {l:'Consumo estrada (HEV)',k:'autonomia_hev_estrada',tp:'num',m:'maior',suf:' km/l'},
    {l:'Eficiência',k:'eficiencia_mj_km',tp:'num',m:'menor',suf:' MJ/km'},
  ]},
  {n:'4',nome:'Recarga',criterios:[
    {l:'Recarga AC',k:'recarga_ac_kw',tp:'num',m:'maior',suf:' kW'},
    {l:'Tempo AC',k:'recarga_ac_tempo_h',tp:'num',m:'menor',suf:'h'},
    {l:'Recarga DC',k:'recarga_dc_kw',tp:'num',m:'maior',suf:' kW'},
    {l:'DC 30→80%',k:'recarga_dc_tempo_min',tp:'num',m:'menor',suf:' min'},
    {l:'Protocolo DC',k:'protocolo_dc',tp:'txt'},
  ]},
  {n:'5',nome:'Dimensões',criterios:[
    {l:'Comprimento',k:'comprimento_mm_v',tp:'num',suf:' mm'},
    {l:'Largura',k:'largura_mm_v',tp:'num',suf:' mm'},
    {l:'Altura',k:'altura_mm_v',tp:'num',suf:' mm'},
    {l:'Porta-malas',k:'porta_malas_l',tp:'num',m:'maior',suf:' L'},
    {l:'Frunk',k:'frunk_l',tp:'num',m:'maior',suf:' L'},
    {l:'Peso',k:'peso_kg',tp:'num',m:'menor',suf:' kg'},
    {l:'Passageiros',k:'passageiros',tp:'num'},
    {l:'Suspensão dianteira',k:'suspensao_diant',tp:'txt'},
    {l:'Suspensão traseira',k:'suspensao_tras',tp:'txt'},
  ]},
  {n:'6',nome:'Segurança',criterios:[
    {l:'Airbags',k:'airbags_qtd',tp:'num',m:'maior',suf:' airbags'},
    {l:'Nível ADAS',k:'adas_nivel',tp:'txt'},
    {l:'HUD',k:'hud',tp:'txt'},
  ]},
  {n:'7',nome:'Garantias',criterios:[
    {l:'Garantia veículo',k:'garantia_veiculo_anos',tp:'num',m:'maior',suf:' anos'},
    {l:'Garantia bateria',k:'garantia_bateria_anos',tp:'num',m:'maior',suf:' anos'},
  ]},
  {n:'$',nome:'Preço',criterios:[
    {l:'Preço 0km',k:'preco_atual',tp:'preco',m:'menor'},
  ]},
]

function fp(v){return v?'R$ '+Math.round(v).toLocaleString('pt-BR'):null}
function gi(m,mo){return((m||'')[0]+((mo||'')[0]||'')).toUpperCase()}

function initComparador(carros){
  CARROS=carros
  pontos=carros.map(()=>0)
  renderHeader()
  renderSlides()
  renderDots()
  renderProgresso()
  irPara(0)
}

function renderHeader(){
  const h=document.getElementById('carros-header')
  h.style.gridTemplateColumns=`repeat(${CARROS.length},1fr)`
  h.innerHTML=CARROS.map((d,i)=>`
    <div class="carro-col">
      <div class="cfoto-wrap">
        ${d.foto_principal
          ?`<img src="${d.foto_principal}" alt="${d.marca} ${d.modelo}">`
          :`<div class="cfoto-ph">${gi(d.marca,d.modelo)}</div>`}
      </div>
      <div class="cinfo">
        <div class="cmarca-tag">${d.marca||''}</div>
        <div class="cmodelo">${d.modelo||''}</div>
        <div class="cversao">${d.versao||''}</div>
        ${d.preco_atual?`<div class="cpreco-tag">${fp(d.preco_atual)}</div>`:''}
      </div>
      <div class="vplacar" id="placar-${i}">0 pts</div>
    </div>
  `).join('')
}

function renderSlides(){
  const content=document.getElementById('content')
  content.innerHTML=''
  GRUPOS.forEach((g,gi)=>{
    const div=document.createElement('div')
    div.className='grupo-slide'
    div.id=`slide-${gi}`
    const crits=g.criterios.filter(f=>CARROS.some(d=>{
      const v=d[f.k];return v!==null&&v!==undefined&&v!==''
    }))
    const ncols=CARROS.length
    div.innerHTML=`<div class="criterios" id="crits-${gi}">
      ${crits.map((f,fi)=>{
        const vals=CARROS.map(d=>d[f.k])
        let bi=-1,wi=-1
        if((f.tp==='num'||f.tp==='preco')&&f.m){
          const ns=vals.map(v=>parseFloat(v)||null)
          const vl=ns.filter(v=>v!==null)
          if(vl.length>1){
            const bv=f.m==='maior'?Math.max(...vl):Math.min(...vl)
            const wv=f.m==='maior'?Math.min(...vl):Math.max(...vl)
            bi=ns.indexOf(bv);wi=ns.indexOf(wv)
            if(bi===wi)wi=-1
          }
        }
        const colunas=vals.map((v,i)=>{
          const disp=v===null||v===undefined||v===''?'—'
            :f.tp==='preco'?fp(v)
            :f.tp==='bool'?(v?'✓ Sim':'Não')
            :f.tp==='num'?(Number(v).toLocaleString('pt-BR')+(f.suf||''))
            :v+(f.suf||'')
          const cls=i===bi?'melhor':i===wi?'pior':''
          return`<div class="criterio-val ${cls}">${disp}</div>`
        }).join('')
        return`<div class="criterio" style="grid-template-columns:170px ${Array(ncols).fill('1fr').join(' ')};animation-delay:${fi*.05}s">
          <div class="criterio-label">${f.l}</div>${colunas}
        </div>`
      }).join('')}
    </div>`
    content.appendChild(div)
  })

  // Slide placar final
  const pDiv=document.createElement('div')
  pDiv.className='grupo-slide'
  pDiv.id=`slide-${GRUPOS.length}`
  pDiv.innerHTML=`<div class="placar-final" id="placar-final"></div>`
  content.appendChild(pDiv)
}

function renderDots(){
  const total=GRUPOS.length+1
  document.getElementById('grupo-dots').innerHTML=
    Array.from({length:total},(_,i)=>
      `<button class="gdot${i===0?' on':''}" onclick="irPara(${i})"></button>`
    ).join('')
}

function renderProgresso(){
  const total=GRUPOS.length+1
  document.getElementById('progresso').innerHTML=
    Array.from({length:total},(_,i)=>
      `<div class="pdot${i===0?' on':''}" id="pd-${i}"></div>`
    ).join('')
}

function calcularPontos(){
  pontos=CARROS.map(()=>0)
  GRUPOS.forEach(g=>{
    g.criterios.forEach(f=>{
      if(!(f.tp==='num'||f.tp==='preco')||!f.m) return
      const vals=CARROS.map(d=>parseFloat(d[f.k])||null)
      const vl=vals.filter(v=>v!==null)
      if(vl.length<2) return
      const bv=f.m==='maior'?Math.max(...vl):Math.min(...vl)
      const bi=vals.indexOf(bv)
      if(bi>=0) pontos[bi]++
    })
  })
  CARROS.forEach((_,i)=>{
    const el=document.getElementById(`placar-${i}`)
    if(el) el.textContent=`${pontos[i]} pts`
  })
}

function renderPlacarFinal(){
  const maxPts=Math.max(...pontos)
  const vencedores=pontos.map((p,i)=>p===maxPts?i:-1).filter(i=>i>=0)
  const empate=vencedores.length>1
  const pf=document.getElementById('placar-final')
  if(!pf) return
  pf.innerHTML=`
    <div class="placar-titulo">Resultado Final</div>
    ${empate?`<div class="empate-tag">🤝 Empate técnico</div>`:''}
    <div class="placar-carros">
      ${CARROS.map((d,i)=>{
        const isVencedor=!empate&&vencedores.includes(i)
        const larg=isVencedor?180:150
        const alt=isVencedor?108:90
        return`<div class="placar-carro${isVencedor?' vencedor':''}">
          ${isVencedor?'<div class="coroa">👑</div>':'<div style="height:28px"></div>'}
          <div class="placar-foto" style="width:${larg}px;height:${alt}px">
            ${d.foto_principal
              ?`<img src="${d.foto_principal}" alt="${d.marca}">`
              :`<div class="placar-foto-ph" style="font-size:${isVencedor?'1.8rem':'1.4rem'}">${gi(d.marca,d.modelo)}</div>`}
          </div>
          <div class="placar-nome" style="font-size:${isVencedor?'.9rem':'.78rem'};max-width:${larg}px">
            ${d.marca}<br>${d.modelo}
          </div>
          <div class="placar-pts">${pontos[i]}</div>
          <div class="placar-pts-label">critérios</div>
        </div>`
      }).join('')}
    </div>
  `
}

function irPara(idx){
  const total=GRUPOS.length+1
  if(idx<0||idx>=total) return
  if(idx===GRUPOS.length){calcularPontos();renderPlacarFinal()}
  const anterior=document.querySelector('.grupo-slide.active')
  if(anterior){anterior.classList.remove('active');anterior.classList.add('saindo');setTimeout(()=>anterior.classList.remove('saindo'),350)}
  setTimeout(()=>{const novo=document.getElementById(`slide-${idx}`);if(novo)novo.classList.add('active')},50)
  grupoAtual=idx
  const isPlaycar=idx===GRUPOS.length
  document.getElementById('gnav-num').textContent=isPlaycar?'RESULTADO FINAL':`GRUPO ${idx+1} DE ${GRUPOS.length}`
  document.getElementById('gnav-nome').textContent=isPlaycar?'🏆 Placar Final':GRUPOS[idx].nome
  document.getElementById('btn-prev').disabled=idx===0
  document.getElementById('btn-next').disabled=idx===total-1
  document.getElementById('bbtn-prev').disabled=idx===0
  document.getElementById('bbtn-next').disabled=idx===total-1
  document.getElementById('bbtn-next').textContent=idx===total-2?'🏆 Ver Placar ›':'Próximo ›'
  document.querySelectorAll('.gdot').forEach((d,i)=>d.classList.toggle('on',i===idx))
  document.querySelectorAll('.pdot').forEach((d,i)=>d.classList.toggle('on',i===idx))
}

function navGrupo(dir){irPara(grupoAtual+dir)}

document.addEventListener('keydown',e=>{
  if(e.key==='ArrowRight'||e.key==='ArrowDown') navGrupo(1)
  if(e.key==='ArrowLeft'||e.key==='ArrowUp') navGrupo(-1)
  if(e.key==='Escape') window.close()
})

// ── DADOS DEMO ────────────────────────────────────────────────
const DEMO=[
  {marca:'BYD',modelo:'Dolphin',versao:'SE',foto_principal:null,preco_atual:159990,reclame_aqui_nota:7.2,fabricado_em:'China',status_venda:'Ativo',pcd_isencao:true,bateria_kwh:44.9,potencia_cv:95,torque_kgfm:18.35,zero_100_s:10.9,vel_max_kmh:150,autonomia_km:291,consumo_kmkwh:6.7,eficiencia_mj_km:0.42,recarga_ac_kw:7.5,recarga_ac_tempo_h:7,recarga_dc_kw:60,recarga_dc_tempo_min:30,protocolo_dc:'CCS2',comprimento_mm_v:4290,largura_mm_v:1770,altura_mm_v:1570,porta_malas_l:345,peso_kg:1490,passageiros:5,airbags_qtd:6,adas_nivel:'L2',hud:'Não',garantia_veiculo_anos:6,garantia_bateria_anos:8,tracao:'FWD'},
  {marca:'BYD',modelo:'Yuan Plus',versao:'EV',foto_principal:null,preco_atual:189990,reclame_aqui_nota:7.2,fabricado_em:'China',status_venda:'Ativo',pcd_isencao:true,bateria_kwh:60.5,potencia_cv:204,torque_kgfm:31.6,zero_100_s:7.3,vel_max_kmh:160,autonomia_km:422,consumo_kmkwh:7.1,eficiencia_mj_km:0.51,recarga_ac_kw:11,recarga_ac_tempo_h:6,recarga_dc_kw:88,recarga_dc_tempo_min:28,protocolo_dc:'CCS2',comprimento_mm_v:4455,largura_mm_v:1875,altura_mm_v:1615,porta_malas_l:440,peso_kg:1810,passageiros:5,airbags_qtd:6,adas_nivel:'L2',hud:'Sim',garantia_veiculo_anos:6,garantia_bateria_anos:8,tracao:'FWD'},
  {marca:'MG',modelo:'MG4',versao:'EV Luxury',foto_principal:null,preco_atual:179990,reclame_aqui_nota:7.5,fabricado_em:'China',status_venda:'Ativo',pcd_isencao:false,bateria_kwh:64,potencia_cv:204,torque_kgfm:25,zero_100_s:7.7,vel_max_kmh:160,autonomia_km:425,consumo_kmkwh:6.6,eficiencia_mj_km:0.54,recarga_ac_kw:11,recarga_ac_tempo_h:7,recarga_dc_kw:117,recarga_dc_tempo_min:28,protocolo_dc:'CCS2',comprimento_mm_v:4287,largura_mm_v:1836,altura_mm_v:1504,porta_malas_l:363,peso_kg:1685,passageiros:5,airbags_qtd:6,adas_nivel:'L2',hud:'Não',garantia_veiculo_anos:5,garantia_bateria_anos:8,tracao:'FWD'}
]

try{
  const salvo=sessionStorage.getItem('spce_comparar')
  if(salvo){
    const carros=JSON.parse(salvo)
    sessionStorage.removeItem('spce_comparar')
    initComparador(carros)
  } else {
    initComparador(DEMO)
  }
}catch(e){
  console.error('Erro ao carregar dados:',e)
  initComparador(DEMO)
}
</script>
</body>
</html>
