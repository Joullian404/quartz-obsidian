Com certeza! Dando continuidade, atualizei todas as calculadoras restantes para incluir recomendações de conduta, medicamentos e doses, mantendo o foco na segurança e na utilidade clínica.

---

### ⚠️ **AVISO IMPORTANTE ANTES DE USAR** ⚠️

As informações de conduta e dosagem de medicamentos fornecidas abaixo são para **fins educacionais e de referência rápida**. Elas **NÃO** substituem o julgamento clínico. A escolha da terapia, as doses e os ajustes devem ser sempre individualizados para cada paciente, levando em conta a função renal e hepática, comorbidades, alergias, peso, hemodinâmica e, crucialmente, **os protocolos da sua instituição e a epidemiologia local.**

---

Aqui estão os códigos atualizados. Você pode substituir os blocos antigos pelos novos correspondentes em sua nota do Obsidian.

### **1. Calculadora SIRS (Sepse-2)**

```javascript
// --- Bloco de Código para Calculadora SIRS com Conduta ---

const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Critérios SIRS (Sepsis-2)</h2>
  <div class="checkbox-group"><input type="checkbox" id="sirs-temp"><label for="sirs-temp">Temperatura > 38°C ou < 36°C</label></div>
  <div class="checkbox-group"><input type="checkbox" id="sirs-hr"><label for="sirs-hr">Frequência cardíaca > 90 bpm</label></div>
  <div class="checkbox-group"><input type="checkbox" id="sirs-rr"><label for="sirs-rr">Frequência respiratória > 20 ipm ou PaCO₂ < 32 mmHg</label></div>
  <div class="checkbox-group"><input type="checkbox" id="sirs-wbc"><label for="sirs-wbc">Leucócitos > 12.000, < 4.000 ou > 10% de bastões</label></div>
  <div class="button-group">
    <button id="sirs-calc-button">Calcular</button>
    <button id="sirs-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Critérios presentes: <span id="sirs-result"></span></h3>
  <div id="sirs-interpretation" class="recommendation-box"></div>
</div>
`;
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.checkbox-group { margin-bottom: 12px; display: flex; align-items: center; }
.checkbox-group input { margin-right: 10px; min-width: 18px; min-height: 18px; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#sirs-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 15px; line-height: 1.5; }
`;
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

function calculateSIRS() {
    let score = 0;
    if (container.querySelector('#sirs-temp').checked) score++;
    if (container.querySelector('#sirs-hr').checked) score++;
    if (container.querySelector('#sirs-rr').checked) score++;
    if (container.querySelector('#sirs-wbc').checked) score++;
    container.querySelector('#sirs-result').innerText = `${score} de 4`;
    const interpretationEl = container.querySelector('#sirs-interpretation');
    if (score >= 2) {
      interpretationEl.innerHTML = `<h4 style="color:darkred;">Critérios para SIRS Presentes</h4><p>Se houver suspeita de infecção, isso caracteriza Sepse (pela definição Sepsis-2). A conduta deve seguir o <strong>Pacote de 1 Hora (Sepsis Bundle)</strong>:</p>
        <ul>
            <li><strong>Medir Lactato:</strong> Se > 2 mmol/L, repetir em 2-4h.</li>
            <li><strong>Coletar Hemoculturas:</strong> Antes de iniciar antibióticos.</li>
            <li><strong>Administrar Antibióticos:</strong> De amplo espectro (ex: Cefepime + Vancomicina ou Piperacilina-Tazobactam), guiado pela epidemiologia local.</li>
            <li><strong>Iniciar Fluidos:</strong> 30 mL/kg de cristaloide para hipotensão ou lactato ≥ 4 mmol/L.</li>
            <li><strong>Iniciar Vasopressores:</strong> Se PAM < 65 mmHg após fluidos, iniciar <strong>Noradrenalina</strong>.</li>
        </ul>`;
    } else {
      interpretationEl.innerHTML = `<h4>Critérios para SIRS não preenchidos</h4><p>Continuar monitorização. Risco de sepse é menor, mas não excluído.</p>`;
    }
}
function resetSIRS() {
    container.querySelectorAll('input[type="checkbox"]').forEach(box => box.checked = false);
    container.querySelector('#sirs-result').innerText = "";
    container.querySelector('#sirs-interpretation').innerHTML = "";
}

setTimeout(() => {
    try {
        container.querySelector('#sirs-calc-button').addEventListener('click', calculateSIRS);
        container.querySelector('#sirs-reset-button').addEventListener('click', resetSIRS);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **2. Calculadora SOFA (Sepse)**

```javascript
// --- Bloco de Código Corrigido para SOFA com Conduta ---

const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora SOFA (Sequential Organ Failure Assessment)</h2>
  <div class="input-group"><label>Respiratório (PaO2/FiO2)</label><select id="sofa-respiration"><option value="0">≥400</option><option value="1"><400</option><option value="2"><300</option><option value="3"><200</option><option value="4"><100</option></select></div>
  <div class="input-group"><label>Coagulação (Plaquetas)</label><select id="sofa-coagulation"><option value="0">≥150k</option><option value="1"><150k</option><option value="2"><100k</option><option value="3"><50k</option><option value="4"><20k</option></select></div>
  <div class="input-group"><label>Fígado (Bilirrubina)</label><select id="sofa-liver"><option value="0"><1.2</option><option value="1">1.2-1.9</option><option value="2">2.0-5.9</option><option value="3">6.0-11.9</option><option value="4">≥12.0</option></select></div>
  <div class="input-group"><label>Cardiovascular (PAM e drogas)</label><select id="sofa-cardiovascular"><option value="0">PAM ≥70</option><option value="1">PAM <70</option><option value="2">Dopa ≤5</option><option value="3">Dopa >5 ou Nora/Epi ≤0.1</option><option value="4">Dopa >15 ou Nora/Epi >0.1</option></select></div>
  <div class="input-group"><label>SNC (Glasgow)</label><select id="sofa-cns"><option value="0">15</option><option value="1">13-14</option><option value="2">10-12</option><option value="3">6-9</option><option value="4"><6</option></select></div>
  <div class="input-group"><label>Renal (Creatinina)</label><select id="sofa-renal"><option value="0"><1.2</option><option value="1">1.2-1.9</option><option value="2">2.0-3.4</option><option value="3">3.5-4.9</option><option value="4">≥5.0 ou diálise</option></select></div>
  <div class="button-group">
    <button id="sofa-calc-button">Calcular</button>
    <button id="sofa-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Resultado: <span id="sofa-result"></span></h3>
  <div id="sofa-interpretation" class="recommendation-box"></div>
</div>
`;
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.input-group { margin-bottom: 12px; display: flex; justify-content: space-between; align-items: center; }
.input-group label { flex-basis: 50%; }
select { flex-basis: 48%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; margin-top: 20px; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#sofa-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 15px; line-height: 1.5; }
`;
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

function calculateSOFA() {
    const get = (id) => parseInt(container.querySelector('#' + id).value);
    const totalScore = get('sofa-respiration') + get('sofa-coagulation') + get('sofa-liver') + get('sofa-cardiovascular') + get('sofa-cns') + get('sofa-renal');
    container.querySelector('#sofa-result').innerText = totalScore;
    const interpretationEl = container.querySelector('#sofa-interpretation');
    let text = `<h4>Interpretação e Conduta</h4>
        <p>Um aumento no SOFA ≥ 2 pontos em um paciente com infecção define <strong>Sepse</strong>. A pontuação quantifica a disfunção orgânica e tem valor prognóstico. A conduta é focada em tratar a causa base e suportar cada sistema falho:</p><ul>`;
    if (get('sofa-respiration') > 0) text += "<li><strong>Respiratório:</strong> Otimizar PEEP, considerar posição prona, avaliar bloqueio neuromuscular.</li>";
    if (get('sofa-cardiovascular') > 0) text += "<li><strong>Cardiovascular:</strong> Titular vasopressores (Noradrenalina) para PAM ≥ 65 mmHg, considerar ecocardiograma.</li>";
    if (get('sofa-renal') > 0) text += "<li><strong>Renal:</strong> Evitar nefrotóxicos, manejar volemia, considerar Terapia de Substituição Renal (Diálise).</li>";
    if (get('sofa-coagulation') > 0) text += "<li><strong>Coagulação:</strong> Monitorar plaquetas, avaliar risco de sangramento, transfundir apenas se sangramento ativo ou plaquetas < 10-20k.</li>";
    if (get('sofa-liver') > 0) text += "<li><strong>Hepático:</strong> Suporte, evitar drogas com metabolismo hepático intenso.</li>";
    if (get('sofa-cns') > 0) text += "<li><strong>SNC:</strong> Investigar causas de coma (metabólica, sedação), realizar TC de crânio se necessário.</li>";
    text += "</ul>";
    interpretationEl.innerHTML = text;
}
function resetSOFA() {
    container.querySelectorAll('select').forEach(s => s.selectedIndex = 0);
    container.querySelector('#sofa-result').innerText = "";
    container.querySelector('#sofa-interpretation').innerHTML = "";
}

setTimeout(() => {
    try {
        container.querySelector('#sofa-calc-button').addEventListener('click', calculateSOFA);
        container.querySelector('#sofa-reset-button').addEventListener('click', resetSOFA);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **3. Calculadora MDRD (Função Renal)**

```javascript
// --- Bloco de Código para Calculadora TFG (MDRD) com Conduta ---

const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de TFG Estimada (Fórmula MDRD)</h2>
  <div class="input-group"><label>Creatinina Sérica (mg/dL)</label><input type="number" id="mdrd-creat" placeholder="Ex: 1.2" step="0.1"></div>
  <div class="input-group"><label>Idade (anos)</label><input type="number" id="mdrd-age" placeholder="Ex: 55"></div>
  <div class="input-group"><label>Sexo</label><select id="mdrd-sex"><option value="masculino">Masculino</option><option value="feminino">Feminino</option></select></div>
  <div class="checkbox-group"><input type="checkbox" id="mdrd-ethnicity"><label for="mdrd-ethnicity">Afro-americano</label></div>
  <div class="button-group">
    <button id="mdrd-calc-button">Calcular</button>
    <button id="mdrd-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Resultado (TFG): <span id="mdrd-result"></span></h3>
  <div id="mdrd-interpretation" class="recommendation-box"></div>
</div>
`;
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.input-group, .checkbox-group { margin-bottom: 15px; display:flex; align-items:center; }
.input-group label { flex-basis:50%; }
input[type="number"], select { flex-basis:50%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.checkbox-group input { margin-right: 8px; }
.button-group { display: flex; gap: 10px; margin-top: 20px; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#mdrd-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 15px; line-height: 1.5; }
`;
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

function calculateMDRD() {
    const creat = parseFloat(container.querySelector('#mdrd-creat').value);
    const age = parseInt(container.querySelector('#mdrd-age').value);
    if (isNaN(creat) || isNaN(age) || creat <= 0 || age <= 0) { alert("Insira valores válidos."); return; }
    let tfg = 175 * Math.pow(creat, -1.154) * Math.pow(age, -0.203);
    if (container.querySelector('#mdrd-sex').value === 'feminino') { tfg *= 0.742; }
    if (container.querySelector('#mdrd-ethnicity').checked) { tfg *= 1.212; }
    container.querySelector('#mdrd-result').innerText = `${tfg.toFixed(2)} mL/min/1.73 m²`;
    const interpretationEl = container.querySelector('#mdrd-interpretation');
    let stageText = "<h4>Estágio da DRC e Conduta:</h4>";
    if (tfg >= 90) stageText += "<strong>Estágio 1:</strong> TFG normal. Diagnóstico e tratamento da condição de base, redução de risco cardiovascular.";
    else if (tfg >= 60) stageText += "<strong>Estágio 2:</strong> Levemente diminuída. Estimar progressão, controle de PA, evitar nefrotóxicos.";
    else if (tfg >= 45) stageText += "<strong>Estágio 3a:</strong> Leve a moderadamente diminuída. Tratar complicações (anemia, DMO), ajustar doses de medicamentos.";
    else if (tfg >= 30) stageText += "<strong>Estágio 3b:</strong> Moderada a gravemente diminuída. Encaminhar ao nefrologista.";
    else if (tfg >= 15) stageText += "<strong>Estágio 4:</strong> Gravemente diminuída. Preparação para terapia de substituição renal (diálise, transplante).";
    else stageText += "<strong>Estágio 5:</strong> Falência renal (TFG < 15). Iniciar terapia de substituição renal.";
    interpretationEl.innerHTML = stageText;
}
function resetMDRD() {
    container.querySelectorAll('input').forEach(i => i.type === 'checkbox' ? i.checked = false : i.value = '');
    container.querySelector('select').selectedIndex = 0;
    container.querySelector('#mdrd-result').innerText = "";
    container.querySelector('#mdrd-interpretation').innerHTML = "";
}
setTimeout(() => {
    try {
        container.querySelector('#mdrd-calc-button').addEventListener('click', calculateMDRD);
        container.querySelector('#mdrd-reset-button').addEventListener('click', resetMDRD);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **4. Calculadora de Wells para TEP**

```javascript
// --- Bloco de Código para Wells (TEP) com Conduta ---

const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Escore de Wells para Embolia Pulmonar (TEP)</h2>
  <div class="checkbox-group"><input type="checkbox" data-points="3" id="wells-dvt"><label for="wells-dvt">Sinais clínicos de TVP (3 pts)</label></div>
  <div class="checkbox-group"><input type="checkbox" data-points="3" id="wells-diag"><label for="wells-diag">TEP como diagnóstico nº 1 (3 pts)</label></div>
  <div class="checkbox-group"><input type="checkbox" data-points="1.5" id="wells-hr"><label for="wells-hr">FC > 100 bpm (1.5 pt)</label></div>
  <div class="checkbox-group"><input type="checkbox" data-points="1.5" id="wells-imob"><label for="wells-imob">Imobilização / Cirurgia < 4 sem (1.5 pt)</label></div>
  <div class="checkbox-group"><input type="checkbox" data-points="1.5" id="wells-prev"><label for="wells-prev">TVP/TEP prévios (1.5 pt)</label></div>
  <div class="checkbox-group"><input type="checkbox" data-points="1" id="wells-hemop"><label for="wells-hemop">Hemoptise (1 pt)</label></div>
  <div class="checkbox-group"><input type="checkbox" data-points="1" id="wells-cancer"><label for="wells-cancer">Malignidade (1 pt)</label></div>
  <div class="button-group">
    <button id="wells-calc-button">Calcular</button>
    <button id="wells-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Escore Total: <span id="wells-result"></span></h3>
  <div id="wells-interpretation" class="recommendation-box"></div>
</div>
`;
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.checkbox-group { margin-bottom: 12px; display: flex; align-items: center; }
.checkbox-group input { margin-right: 10px; min-width: 18px; min-height: 18px; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#wells-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 15px; line-height: 1.5; }
`;
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

function calculateWellsPE() {
    let score = 0;
    container.querySelectorAll('.checkbox-group input[type="checkbox"]').forEach(box => { if (box.checked) score += parseFloat(box.dataset.points); });
    container.querySelector('#wells-result').innerText = score;
    const interpretationEl = container.querySelector('#wells-interpretation');
    let text = "<h4>Interpretação e Conduta Diagnóstica (Modelo 2 Níveis):</h4>";
    if (score > 4) {
        text += `<p style="color:darkred;"><strong>TEP Provável.</strong> Recomenda-se AngioTC de tórax como exame inicial.</p>`;
    } else {
        text += `<p style="color:darkgreen;"><strong>TEP Improvável.</strong> Recomenda-se iniciar com Dímero-D. Se negativo, exclui TEP. Se positivo, prosseguir para AngioTC.</p>`;
    }
    text += `<h4>Conduta se TEP for confirmada:</h4>
        <p>Iniciar <strong>anticoagulação plena</strong>, a menos que contraindicado.</p>
        <ul>
            <li><strong>Paciente Estável:</strong> DOACs são preferíveis. Ex: <strong>Apixabana</strong> 10 mg 12/12h por 7 dias, depois 5 mg 12/12h. ou <strong>Rivaroxabana</strong> 15 mg 12/12h por 21 dias, depois 20 mg 1x/dia.</li>
            <li><strong>Paciente Instável / TEP Maciço:</strong> Heparina Não Fracionada (HNF) em BIC e considerar trombólise.</li>
        </ul>`;
    interpretationEl.innerHTML = text;
}
function resetWellsPE() {
    container.querySelectorAll('.checkbox-group input[type="checkbox"]').forEach(box => box.checked = false);
    container.querySelector('#wells-result').innerText = "";
    container.querySelector('#wells-interpretation').innerHTML = "";
}
setTimeout(() => {
    try {
        container.querySelector('#wells-calc-button').addEventListener('click', calculateWellsPE);
        container.querySelector('#wells-reset-button').addEventListener('click', resetWellsPE);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **5. Calculadora CURB-65 (Pneumonia)**

```javascript
// --- Bloco de Código para CURB-65 com Conduta ---

const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Escore CURB-65 (Gravidade da PAC)</h2>
  <div class="checkbox-group"><input type="checkbox" id="curb-c"><label for="curb-c"><strong>C</strong>onfusão mental nova</label></div>
  <div class="checkbox-group"><input type="checkbox" id="curb-u"><label for="curb-u"><strong>U</strong>reia > 7 mmol/L (BUN > 19)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="curb-r"><label for="curb-r"><strong>R</strong>espiração ≥ 30 ipm</label></div>
  <div class="checkbox-group"><input type="checkbox" id="curb-b"><label for="curb-b"><strong>B</strong>P Sistólica < 90 ou Diastólica ≤ 60</label></div>
  <div class="checkbox-group"><input type="checkbox" id="curb-65"><label for="curb-65">Idade ≥ <strong>65</strong> anos</label></div>
  <div class="button-group">
    <button id="curb-calc-button">Calcular</button>
    <button id="curb-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Escore Total: <span id="curb-result"></span></h3>
  <div id="curb-interpretation" class="recommendation-box"></div>
</div>
`;
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.checkbox-group { margin-bottom: 12px; display: flex; align-items: center; }
.checkbox-group input { margin-right: 10px; min-width: 18px; min-height: 18px; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#curb-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 15px; line-height: 1.5; }
`;
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

function calculateCURB65() {
    let score = 0;
    container.querySelectorAll('.checkbox-group input[type="checkbox"]').forEach(box => { if (box.checked) score++; });
    container.querySelector('#curb-result').innerText = score;
    const interpretationEl = container.querySelector('#curb-interpretation');
    let text = "<h4>Mortalidade e Recomendação de Manejo:</h4>";
    switch(score) {
        case 0:
        case 1:
            text += `<p><strong>Grupo 1 (Baixo Risco):</strong> Mortalidade ~1.5%.<br><strong>Conduta:</strong> Tratamento ambulatorial.<br><strong>Exemplo de ATB:</strong> Amoxicilina 1g 8/8h ou Doxiciclina 100mg 12/12h.</p>`;
            break;
        case 2:
            text += `<p><strong>Grupo 2 (Risco Moderado):</strong> Mortalidade ~9.2%.<br><strong>Conduta:</strong> Considerar internação hospitalar.<br><strong>Exemplo de ATB:</strong> Ceftriaxona 1-2g 1x/dia + Azitromicina 500mg 1x/dia.</p>`;
            break;
        default:
            text += `<p><strong>Grupo 3 (Alto Risco):</strong> Mortalidade ~22%.<br><strong>Conduta:</strong> Internação hospitalar urgente. Avaliar necessidade de UTI.<br><strong>Exemplo de ATB:</strong> Cefepime 2g 8/8h + Azitromicina 500mg 1x/dia (ou Levofloxacino). Considerar Vancomicina se risco de MRSA.</p>`;
            break;
    }
    interpretationEl.innerHTML = text + "<p>⚠️ <strong>A escolha do antibiótico depende da epidemiologia local e dos protocolos institucionais.</strong></p>";
}
function resetCURB65() {
    container.querySelectorAll('.checkbox-group input[type="checkbox"]').forEach(box => box.checked = false);
    container.querySelector('#curb-result').innerText = "";
    container.querySelector('#curb-interpretation').innerHTML = "";
}
setTimeout(() => {
    try {
        container.querySelector('#curb-calc-button').addEventListener('click', calculateCURB65);
        container.querySelector('#curb-reset-button').addEventListener('click', resetCURB65);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **6. Calculadora Critérios de Light**

```javascript
// --- Bloco de Código para Critérios de Light com Conduta ---

const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Critérios de Light (Derrame Pleural)</h2>
  <h3 class="section-header">Valores do Líquido Pleural</h3>
  <div class="input-group"><label>Proteína Pleural (g/dL)</label><input type="number" id="light-pleural-protein" step="0.1"></div>
  <div class="input-group"><label>LDH Pleural (U/L)</label><input type="number" id="light-pleural-ldh" step="1"></div>
  <h3 class="section-header">Valores do Soro (Sangue)</h3>
  <div class="input-group"><label>Proteína Sérica (g/dL)</label><input type="number" id="light-serum-protein" step="0.1"></div>
  <div class="input-group"><label>LDH Sérico (U/L)</label><input type="number" id="light-serum-ldh" step="1"></div>
  <div class="input-group"><label>Limite Superior LDH Sérico (U/L)</label><input type="number" id="light-ldh-limit" step="1"></div>
  <div class="button-group">
    <button id="light-calc-button">Analisar</button>
    <button id="light-reset-button" class="secondary">Reiniciar</button>
  </div>
  <div id="light-interpretation" class="recommendation-box"></div>
</div>
`;
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.section-header { margin-top: 20px; border-bottom: 1px solid #ccc; padding-bottom: 3px; }
.input-group { margin-bottom: 15px; display:flex; justify-content:space-between; align-items:center; }
input[type="number"] { width:50%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; margin-top: 20px; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#light-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 15px; background-color: #e9ecef; border-radius: 4px; margin-top: 20px; line-height: 1.6; }
.result-final { font-size: 1.3em; font-weight: bold; text-align: center; padding: 10px; border-radius: 5px; margin: 10px 0; }
.exudate { background-color: #f8d7da; color: #721c24; border: 1px solid #f5c6cb; }
.transudate { background-color: #d4edda; color: #155724; border: 1px solid #c3e6cb; }
`;
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

function calculateLightsCriteria() {
    const pProt = parseFloat(container.querySelector('#light-pleural-protein').value);
    const sProt = parseFloat(container.querySelector('#light-serum-protein').value);
    const pLDH = parseFloat(container.querySelector('#light-pleural-ldh').value);
    const sLDH = parseFloat(container.querySelector('#light-serum-ldh').value);
    const ldhLimit = parseFloat(container.querySelector('#light-ldh-limit').value);
    if ([pProt, sProt, pLDH, sLDH, ldhLimit].some(isNaN)) { alert("Preencha todos os campos."); return; }
    const proteinRatio = pProt / sProt;
    const ldhRatio = pLDH / sLDH;
    const ldhLimitCheck = (2/3) * ldhLimit;
    const isExudate = proteinRatio > 0.5 || ldhRatio > 0.6 || pLDH > ldhLimitCheck;
    let resultHTML = "<h4>Análise dos Critérios:</h4><ul>";
    resultHTML += `<li>Proteína Pleural / Sérica > 0.5: <strong>${proteinRatio > 0.5 ? 'SIM' : 'NÃO'}</strong> (Ratio: ${proteinRatio.toFixed(2)})</li>`;
    resultHTML += `<li>LDH Pleural / Sérico > 0.6: <strong>${ldhRatio > 0.6 ? 'SIM' : 'NÃO'}</strong> (Ratio: ${ldhRatio.toFixed(2)})</li>`;
    resultHTML += `<li>LDH Pleural > 2/3 do Limite: <strong>${pLDH > ldhLimitCheck ? 'SIM' : 'NÃO'}</strong> (Valor: ${pLDH.toFixed(0)} vs Limite: ${ldhLimitCheck.toFixed(0)})</li></ul>`;
    if (isExudate) {
        resultHTML += `<div class="result-final exudate">Diagnóstico: EXSUDATO</div><strong>Conduta Sugerida:</strong> Investigar a causa local. Prosseguir com a análise do líquido pleural (citologia, microbiologia, ADA, etc.). As causas mais comuns são pneumonia, neoplasia e embolia pulmonar.`;
    } else {
        resultHTML += `<div class="result-final transudate">Diagnóstico: TRANSUDATO</div><strong>Conduta Sugerida:</strong> Não há necessidade de mais análise do líquido pleural. Focar no tratamento da condição sistêmica de base, que geralmente é Insuficiência Cardíaca Congestiva, Cirrose ou Síndrome Nefrótica.`;
    }
    container.querySelector('#light-interpretation').innerHTML = resultHTML;
}
function resetLights() {
    container.querySelectorAll('input[type="number"]').forEach(input => input.value = '');
    container.querySelector('#light-interpretation').innerHTML = "";
}
setTimeout(() => {
    try {
        container.querySelector('#light-calc-button').addEventListener('click', calculateLightsCriteria);
        container.querySelector('#light-reset-button').addEventListener('click', resetLights);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

As demais calculadoras do seu arquivo original (PESI, Sedoanalgesia) já continham recomendações bastante completas, mas se desejar alguma modificação específica nelas, é só pedir