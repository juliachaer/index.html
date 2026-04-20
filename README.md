<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<meta name="apple-mobile-web-app-title" content="Enxoval Bebê">
<title>🌸 Enxoval da Bebê</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Nunito:wght@400;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --rose: #f472b6;
    --lilac: #c084fc;
    --deep: #7e22ce;
    --soft: #fdf4ff;
    --card: #ffffff;
    --green: #86efac;
    --green-dark: #15803d;
    --text: #3b0764;
    --muted: #a78bbc;
    --border: #f0e0ff;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
  body { font-family: 'Nunito', sans-serif; background: linear-gradient(160deg, #fdf4ff 0%, #fce8f3 60%, #ede9fe 100%); min-height: 100vh; color: var(--text); padding-bottom: 60px; }
  .header { background: linear-gradient(135deg, #c084fc 0%, #f472b6 100%); padding: 32px 20px 24px; text-align: center; box-shadow: 0 6px 30px rgba(192,132,252,0.35); position: sticky; top: 0; z-index: 100; }
  .header-icon { font-size: 38px; margin-bottom: 4px; }
  .header h1 { font-family: 'Playfair Display', serif; color: white; font-size: 24px; font-weight: 700; letter-spacing: 0.5px; }
  .header p { color: rgba(255,255,255,0.82); font-size: 13px; margin-top: 3px; }
  .global-progress { max-width: 340px; margin: 14px auto 0; }
  .progress-label { display: flex; justify-content: space-between; color: white; font-size: 12px; margin-bottom: 5px; font-weight: 600; }
  .progress-track { background: rgba(255,255,255,0.28); border-radius: 99px; height: 10px; overflow: hidden; }
  .progress-fill { height: 100%; background: white; border-radius: 99px; transition: width 0.5s cubic-bezier(.4,0,.2,1); }
  .filter-wrap { text-align: center; padding: 14px 16px 0; }
  .filter-btn { font-family: 'Nunito', sans-serif; font-size: 13px; font-weight: 700; padding: 8px 22px; border-radius: 99px; cursor: pointer; border: 2px solid var(--rose); transition: all 0.2s; background: white; color: var(--deep); }
  .filter-btn.active { background: var(--rose); color: white; }
  .tabs-wrap { display: flex; overflow-x: auto; padding: 14px 12px 0; gap: 8px; scrollbar-width: none; }
  .tabs-wrap::-webkit-scrollbar { display: none; }
  .tab-btn { flex-shrink: 0; font-family: 'Nunito', sans-serif; background: white; color: var(--deep); border: 2px solid var(--border); border-radius: 16px; padding: 8px 12px; cursor: pointer; font-size: 11px; font-weight: 600; display: flex; flex-direction: column; align-items: center; gap: 3px; min-width: 78px; transition: all 0.2s; }
  .tab-btn.active { background: linear-gradient(135deg, #c084fc, #f472b6); color: white; border-color: transparent; box-shadow: 0 4px 14px rgba(192,132,252,0.45); }
  .tab-emoji { font-size: 20px; }
  .tab-label { line-height: 1.25; text-align: center; font-size: 10.5px; }
  .tab-pct { background: #f3e8ff; color: var(--deep); border-radius: 99px; padding: 1px 8px; font-size: 9.5px; font-weight: 700; }
  .tab-btn.active .tab-pct { background: rgba(255,255,255,0.28); color: white; }
  .section-title { display: flex; align-items: center; gap: 8px; margin: 16px 12px 10px; font-family: 'Playfair Display', serif; font-size: 17px; color: var(--deep); flex-wrap: wrap; }
  .section-badge { background: #f3e8ff; color: var(--deep); border-radius: 99px; padding: 2px 12px; font-size: 11px; font-family: 'Nunito', sans-serif; font-weight: 700; }
  .items-list { padding: 0 12px; display: flex; flex-direction: column; gap: 10px; }
  .item-card { background: white; border-radius: 18px; padding: 14px 14px 12px; box-shadow: 0 2px 14px rgba(192,132,252,0.09); border: 2px solid var(--border); transition: border-color 0.3s, box-shadow 0.3s; }
  .item-card.done { border-color: var(--green); box-shadow: 0 2px 14px rgba(134,239,172,0.4); }
  .item-top { display: flex; justify-content: space-between; align-items: flex-start; gap: 10px; }
  .item-info { flex: 1; }
  .item-name { font-size: 13.5px; font-weight: 700; color: var(--text); line-height: 1.35; display: flex; align-items: center; gap: 5px; }
  .item-name.done { color: var(--green-dark); }
  .item-note { font-size: 11px; color: var(--muted); margin-top: 4px; line-height: 1.45; }
  .qty-wrap { display: flex; flex-direction: column; align-items: center; gap: 3px; flex-shrink: 0; }
  .qty-controls { display: flex; align-items: center; gap: 5px; background: #faf5ff; border-radius: 99px; padding: 4px 8px; }
  .qty-btn { width: 28px; height: 28px; border-radius: 50%; border: none; font-size: 18px; cursor: pointer; display: flex; align-items: center; justify-content: center; line-height: 1; font-family: 'Nunito', sans-serif; font-weight: 700; transition: transform 0.1s; -webkit-user-select: none; user-select: none; }
  .qty-btn:active { transform: scale(0.9); }
  .qty-btn.minus { background: #e9d5ff; color: var(--deep); }
  .qty-btn.plus { background: var(--lilac); color: white; }
  .qty-input { width: 36px; text-align: center; border: none; background: transparent; font-size: 17px; font-weight: 700; color: var(--deep); font-family: 'Nunito', sans-serif; -moz-appearance: textfield; }
  .qty-input::-webkit-outer-spin-button, .qty-input::-webkit-inner-spin-button { -webkit-appearance: none; }
  .qty-meta { font-size: 9.5px; color: var(--muted); font-weight: 600; }
  .item-progress { margin-top: 10px; }
  .item-track { background: #f3e8ff; border-radius: 99px; height: 6px; overflow: hidden; }
  .item-fill { height: 100%; background: linear-gradient(90deg, #c084fc, #f472b6); border-radius: 99px; transition: width 0.3s ease; }
  .item-remaining { font-size: 10px; color: var(--muted); margin-top: 3px; font-weight: 600; }
  .empty { text-align: center; padding: 40px 20px; color: var(--lilac); font-size: 15px; }
  .footer { text-align: center; color: var(--muted); font-size: 11px; padding: 22px 20px 0; line-height: 1.7; }
</style>
</head>
<body>
<div class="header">
  <div class="header-icon">🌸</div>
  <h1>Enxoval da Bebê</h1>
  <p>Nascimento em julho • Inverno 🧥</p>
  <div class="global-progress">
    <div class="progress-label"><span>Progresso geral</span><span id="global-pct">0%</span></div>
    <div class="progress-track"><div class="progress-fill" id="global-bar" style="width:0%"></div></div>
  </div>
</div>
<div class="filter-wrap"><button class="filter-btn" id="filter-btn" onclick="toggleFilter()">Mostrar só o que falta</button></div>
<div class="tabs-wrap" id="tabs"></div>
<div class="section-title" id="section-title"></div>
<div class="items-list" id="items-list"></div>
<div class="footer">📋 Baseado no Guia de Enxoval Johnny's<br>As quantidades são salvas automaticamente no seu dispositivo</div>
<script>
const DATA=[{key:"amamentacao",label:"Amamentação",emoji:"🍼",items:[{id:"a1",name:"Kit mamadeira com esterilizador",rec:1,note:"Espere para ver se o bebê aceita antes de comprar mais"},{id:"a2",name:"Escorredor de mamadeira",rec:1,note:"Útil para separar os itens do bebê na cozinha"},{id:"a3",name:"Bomba de tirar leite (pode alugar)",rec:1,note:"Tenha em casa ANTES do leite descer — faz toda diferença!"},{id:"a4",name:"Almofada de amamentação",rec:1,note:"Muito usada nos primeiros meses"},{id:"a5",name:"Talheres de silicone",rec:2,note:"Compre quando chegar na fase da papinha"},{id:"a6",name:"Jogo de pratos (doce e salgado)",rec:2,note:"Potinhos de silicone com borda alta"},{id:"a7",name:"Tupperware de vidro para papinha",rec:10,note:"Para congelar papinhas — evite plástico no micro-ondas"},{id:"a8",name:"Pote térmico para papinha",rec:1,note:"Ótimo para passeios e viagens"},{id:"a9",name:"Bolsa térmica para mamadeira",rec:1,note:"Útil para levar frutas geladinhas também"},{id:"a10",name:"Babador de silicone (com bolsinho)",rec:2,note:"Fácil de lavar, muito prático"},{id:"a11",name:"Copinho com bico (a partir de 6m)",rec:1,note:"Compre com alças para facilitar a pega"}]},{key:"cama",label:"Cama & Banho",emoji:"🛁",items:[{id:"b1",name:"Banheira (com trocador)",rec:1,note:"Com trocador facilita muito se for trocar no banheiro"},{id:"b2",name:"Toalha com capuz",rec:3,note:"Costuma ganhar de presente — espere antes de comprar tudo"},{id:"b3",name:"Toalha fralda / cueiro",rec:3,note:"Para usar no banho e fazer o famoso charutinho"},{id:"b4",name:"Fralda de boca",rec:15,note:"Bebê regurgita muito — nunca faltarão!"},{id:"b5",name:"Manta / cobertor",rec:1,note:"Atenção: não use cobertor solto à noite por segurança"},{id:"b6",name:"Berço / mini berço",rec:1,note:"Mini berço é ótimo para os primeiros meses"},{id:"b7",name:"Protetor de berço (bumper vazado)",rec:1,note:"Escolha o modelo vazado por segurança"},{id:"b8",name:"Lençol com elástico para berço",rec:3,note:"Troca frequente — pelo menos 3 unidades"},{id:"b9",name:"Travesseiro anti-refluxo",rec:1,note:"Muito útil se o bebê tiver refluxo"}]},{key:"higiene",label:"Higiene",emoji:"🧴",items:[{id:"h1",name:"Shampoo e condicionador infantil",rec:1,note:"Use pouco — bebê tem pouco cabelo!"},{id:"h2",name:"Sabonete líquido infantil",rec:1,note:"Para corpo e rosto"},{id:"h3",name:"Óleo de massagem / hidratante",rec:1,note:"Ótimo para a massagem após o banho"},{id:"h4",name:"Pomada para assaduras",rec:2,note:"Sempre ter em casa! Use preventivamente"},{id:"h5",name:"Algodão / disco de algodão",rec:1,note:"Para limpeza delicada do rosto"},{id:"h6",name:"Termômetro digital",rec:1,note:"Axilar é o mais prático"},{id:"h7",name:"Aspirador nasal",rec:1,note:"O manual tipo bulbo funciona muito bem"},{id:"h8",name:"Cortador de unhas infantil",rec:1,note:"Ou lima — nunca use tesoura!"},{id:"h9",name:"Kit higiene (pente, escova)",rec:1,note:"Escovinha de pelo macio para cabelo e couro cabeludo"},{id:"h10",name:"Trocador",rec:1,note:"Pode ser portátil — coloque em cima da cômoda"},{id:"h11",name:"Fraldas (estoque inicial)",rec:1,note:"Compre poucos de cada tamanho — o bebê cresce rápido"},{id:"h12",name:"Lenços umedecidos",rec:3,note:"Sempre ter bastante em casa e na bolsa"}]},{key:"saindo",label:"Saindo",emoji:"🚗",items:[{id:"s1",name:"Carrinho de bebê",rec:1,note:"Nos primeiros meses use um com moisés ou reclinado"},{id:"s2",name:"Bebê conforto (cadeirinha)",rec:1,note:"Obrigatório! Não saia sem ele. Compre também a trava"},{id:"s3",name:"Bolsa maternidade",rec:1,note:"Grande o suficiente para fraldas, trocador, roupinha extra"},{id:"s4",name:"Sling / wrap de carregar",rec:1,note:"Libera as mãos e o bebê adora o calor do colo"},{id:"s5",name:"Trocador portátil impermeável",rec:1,note:"Leva na bolsa sempre"},{id:"s6",name:"Almofada de apoio (para colo)",rec:1,note:"Usada até ~3 meses, quando o bebê começa a virar"}]},{key:"rn",label:"Roupas RN",emoji:"👶",items:[{id:"rn1",name:"Body manga longa branco (algodão)",rec:5,note:"Essencial! A base de tudo"},{id:"rn2",name:"Body manga longa colorido",rec:3,note:"Branco é mais versátil — coloque mais coloridos se quiser"},{id:"rn3",name:"Calça com pé",rec:3,note:"Prefira à meia, que fica caindo"},{id:"rn4",name:"Macacão/pijaminha algodão manga longa",rec:5,note:"Muito prático para ficar em casa"},{id:"rn5",name:"Macacão plush com pé (inverno 🧥)",rec:2,note:"Para dias mais frios — inverno em julho!"},{id:"rn6",name:"Saída de maternidade quentinha",rec:1,note:"Já vem no kit maternidade geralmente"},{id:"rn7",name:"Meias",rec:7,note:"Um par por dia da semana"},{id:"rn8",name:"Luvinhas RN",rec:1,note:"Para não se arranhar — depois aprenda a cortar as unhinhas"},{id:"rn9",name:"Gorro/touca de lã ou algodão 🧢",rec:2,note:"Fundamental no inverno!"}]},{key:"0a3",label:"0–3 meses",emoji:"🌸",items:[{id:"03_1",name:"Body manga longa branco (algodão)",rec:5,note:"Essencial — base de qualquer look"},{id:"03_2",name:"Body manga longa colorido",rec:3,note:"Para variar os looks"},{id:"03_3",name:"Calça com pé",rec:3,note:"Cores neutras para combinar com tudo"},{id:"03_4",name:"Calça sem pé",rec:3,note:"Cores neutras — branco, cinza, marinho"},{id:"03_5",name:"Macacão/pijaminha manga longa",rec:4,note:"Inverno: prefira plush ou fleece mais quentinho"},{id:"03_6",name:"Casaquinho",rec:2,note:"Inverno: até 3 unidades. Cores neutras para combinar"},{id:"03_7",name:"Meias",rec:7,note:"Mesmas do RN — numeração 0-3 meses"},{id:"03_8",name:"Roupinha arrumadinha (para sair)",rec:2,note:"Não exagere — cresce rápido!"}]},{key:"3a6",label:"3–6 meses",emoji:"🌼",items:[{id:"36_1",name:"Body manga longa branco (algodão)",rec:5,note:"Continue usando muito!"},{id:"36_2",name:"Body manga curta branco (algodão)",rec:5,note:"Para usar em camadas"},{id:"36_3",name:"Body manga longa colorido",rec:3,note:"Para variar"},{id:"36_4",name:"Body manga curta colorido",rec:3,note:"Para variar"},{id:"36_5",name:"Calça com pé e sem pé",rec:5,note:"2 com pé, 3 sem pé. Sempre cores neutras"},{id:"36_6",name:"Macacão/pijaminha manga longa",rec:3,note:"Tecido mais quentinho (plush/fleece)"},{id:"36_7",name:"Casaquinho",rec:3,note:"Cores neutras — combina com tudo"},{id:"36_8",name:"Meias antiderrapante",rec:10,note:"Carter's: numeração 3-12 meses, antiderrapante"},{id:"36_9",name:"Roupinha arrumadinha (para sair)",rec:4,note:"Agora cresce um pouco mais devagar"}]},{key:"extras",label:"Extras",emoji:"✨",items:[{id:"v1",name:"Chupeta (experimentar)",rec:2,note:"Nem todos os bebês aceitam — tenha 2 modelos para testar"},{id:"v2",name:"Móbile sensorial",rec:1,note:"Estimula a visão — preto e branco nos primeiros meses"},{id:"v3",name:"Tapete de atividades",rec:1,note:"Usado a partir de ~2 meses, por muito tempo!"},{id:"v4",name:"Cadeira de descanso (pode alugar)",rec:1,note:"Muito usada nos primeiros meses"},{id:"v5",name:"Monitor de bebê / babá eletrônica",rec:1,note:"Muito útil para ouvir o bebê dormindo"},{id:"v6",name:"Pijama pós-parto para mamãe",rec:3,note:"Com botões na frente, para amamentação"},{id:"v7",name:"Sutiã de amamentação",rec:3,note:"Compre próximo ao nascimento — o tamanho muda"}]}];
const STORAGE_KEY="enxoval-bebe-v1";let quantities={};let activeKey=DATA[0].key;let showMissing=false;
function load(){try{const s=localStorage.getItem(STORAGE_KEY);if(s)quantities=JSON.parse(s);}catch(e){}}
function save(){try{localStorage.setItem(STORAGE_KEY,JSON.stringify(quantities));}catch(e){}}
function getQty(id){return quantities[id]||0;}
function setQty(id,val){const v=Math.max(0,parseInt(val)||0);quantities[id]=v;save();renderItems();renderTabs();renderGlobal();}
function catProgress(cat){let have=0,total=0;cat.items.forEach(i=>{have+=Math.min(getQty(i.id),i.rec);total+=i.rec;});return total>0?Math.round(have/total*100):0;}
function globalProgress(){let have=0,total=0;DATA.forEach(cat=>cat.items.forEach(i=>{have+=Math.min(getQty(i.id),i.rec);total+=i.rec;}));return total>0?Math.round(have/total*100):0;}
function renderGlobal(){const p=globalProgress();document.getElementById('global-pct').textContent=p+'%';document.getElementById('global-bar').style.width=p+'%';}
function renderTabs(){const wrap=document.getElementById('tabs');wrap.innerHTML=DATA.map(cat=>{const p=catProgress(cat);const active=cat.key===activeKey;return`<button class="tab-btn ${active?'active':''}" onclick="switchTab('${cat.key}')"><span class="tab-emoji">${cat.emoji}</span><span class="tab-label">${cat.label}</span><span class="tab-pct">${p}%</span></button>`;}).join('');}
function renderItems(){const cat=DATA.find(c=>c.key===activeKey);document.getElementById('section-title').innerHTML=`${cat.emoji} ${cat.label} <span class="section-badge">${catProgress(cat)}% completo</span>`;const items=showMissing?cat.items.filter(i=>getQty(i.id)<i.rec):cat.items;const wrap=document.getElementById('items-list');if(items.length===0){wrap.innerHTML=`<div class="empty">🎉 Tudo certo nessa categoria!</div>`;return;}wrap.innerHTML=items.map(item=>{const qty=getQty(item.id);const done=qty>=item.rec;const pct=Math.min(100,Math.round(qty/item.rec*100));return`<div class="item-card ${done?'done':''}"><div class="item-top"><div class="item-info"><div class="item-name ${done?'done':''}">${done?'✅ ':''}${item.name}</div><div class="item-note">💡 ${item.note}</div></div><div class="qty-wrap"><div class="qty-controls"><button class="qty-btn minus" onclick="setQty('${item.id}',${qty-1})">−</button><input class="qty-input" type="number" min="0" value="${qty}" onchange="setQty('${item.id}',this.value)" oninput="setQty('${item.id}',this.value)"><button class="qty-btn plus" onclick="setQty('${item.id}',${qty+1})">+</button></div><div class="qty-meta">meta: ${item.rec} un.</div></div></div>${!done?`<div class="item-progress"><div class="item-track"><div class="item-fill" style="width:${pct}%"></div></div><div class="item-remaining">${qty} de ${item.rec} — faltam ${item.rec-qty}</div></div>`:''}</div>`;}).join('');}
function switchTab(key){activeKey=key;renderTabs();renderItems();setTimeout(()=>{const btn=document.querySelector('.tab-btn.active');if(btn)btn.scrollIntoView({behavior:'smooth',block:'nearest',inline:'center'});},50);}
function toggleFilter(){showMissing=!showMissing;const btn=document.getElementById('filter-btn');btn.classList.toggle('active',showMissing);btn.textContent=showMissing?'✓ Mostrando só o que falta':'Mostrar só o que falta';renderItems();}
load();renderGlobal();renderTabs();renderItems();
</script>
</body>
</html>
