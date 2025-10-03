Com certeza. Entendi perfeitamente. Você quer um único arquivo de texto com **todas as calculadoras completas**, uma após a outra, prontas para serem copiadas e coladas diretamente em uma única nota do Obsidian.

Abaixo está o código completo. Cada calculadora está dentro de seu próprio bloco `dataviewjs` para que funcionem de forma independente na mesma página.

**Instrução:** Copie todo o conteúdo abaixo (começando de `### 1. Calculadora ICH` até o final do último bloco de código) e cole em uma nova nota no seu Obsidian. Depois, mude para o Modo de Leitura (`Ctrl+E`) para ver todas as calculadoras funcionando.

---

### **Aviso Importante Antes de Começar**

As recomendações de conduta e as doses de medicamentos fornecidas são baseadas em diretrizes clínicas comuns e servem como um **guia de referência rápida**. Elas **NÃO substituem o julgamento clínico individualizado**, a avaliação completa do paciente, as diretrizes institucionais ou a consulta à bula dos medicamentos. A decisão final de tratamento é sempre de responsabilidade do médico assistente.

---

### **1. Calculadora ICH (Hemorragia Intracraniana)**


```dataviewjs
// --- Bloco de Código Corrigido para Escore ICH com Recomendação ---

// 1. Definição do HTML da calculadora
const calculatorHTML_ICH = `
<div class="calculator-container">
  <h2>Escore ICH para Hemorragia Intracraniana</h2>
  
  <div class="input-group">
    <label for="glasgow">Glasgow na Admissão</label>
    <select id="glasgow">
      <option value="2">3-4</option>
      <option value="1">5-12</option>
      <option value="0" selected>13-15</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="idade-ich">Idade</label>
    <select id="idade-ich">
      <option value="1">>= 80 anos</option>
      <option value="0" selected>< 80 anos</option>
    </select>
  </div>

  <div class="input-group">
    <label for="local-hematoma">Local do Hematoma</label>
    <select id="local-hematoma">
      <option value="1">Infratentorial</option>
      <option value="0" selected>Supratentorial</option>
    </select>
  </div>

  <div class="input-group">
    <label for="volume-hematoma">Volume do Hematoma</label>
    <select id="volume-hematoma">
      <option value="1">>= 30ml</option>
      <option value="0" selected>< 30ml</option>
    </select>
  </div>

  <div class="input-group">
    <label for="hemoventriculo">Hemo-ventrículo</label>
    <select id="hemoventriculo">
      <option value="1">Sim</option>
      <option value="0" selected>Não</option>
    </select>
  </div>
  
  <div class="button-group">
      <button id="ich-button">Calcular Escore ICH</button>
      <button id="ich-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Escore: <span id="ich-result"></span></h3>
  <h4>Mortalidade em 30 dias: <span id="ich-mortality"></span></h4>
  <h4>Conduta Recomendada:</h4>
  <p id="ich-recommendation" class="conduct-box"></p>
</div>
`;

// 2. Definição do estilo (CSS)
const styles_ICH = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; margin-bottom: 20px; }
.input-group, .button-group { margin-bottom: 15px; }
.input-group label { display: block; margin-bottom: 5px; }
.input-group select { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; margin-top: 20px; }
.button-group button { flex-grow: 1; padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; }
#ich-button { background-color: #007bff; color: white; }
#ich-button:hover { background-color: #0056b3; }
.secondary { background-color: #6c757d; color: white; }
.secondary:hover { background-color: #5a6268; }
.conduct-box { background-color: #e9ecef; padding: 10px; border-radius: 4px; min-height: 20px; line-height: 1.5; }
`;

// 3. Injeção do estilo e do HTML na página
const container_ICH = dv.container;
const styleEl_ICH = document.createElement('style');
styleEl_ICH.innerHTML = styles_ICH;
container_ICH.appendChild(styleEl_ICH);
container_ICH.innerHTML += calculatorHTML_ICH;

// 4. Definição das funções
function calculateICH() {
    const get = (id) => parseInt(container_ICH.querySelector('#' + id).value);
    const totalScore = get('glasgow') + get('idade-ich') + get('local-hematoma') + get('volume-hematoma') + get('hemoventriculo');
    
    container_ICH.querySelector('#ich-result').innerText = totalScore;
    
    const mortalityMap = {0: '0%', 1: '13%', 2: '26%', 3: '72%', 4: '97%', 5: '100%', 6: '100%'};
    container_ICH.querySelector('#ich-mortality').innerText = mortalityMap[totalScore] || "N/A";

    let recommendation = "";
    switch(totalScore) {
        case 0: case 1:
            recommendation = "Risco baixo. Monitorização em unidade de internação ou UTI. Controle pressórico rigoroso.";
            break;
        case 2:
            recommendation = "Risco intermediário. Internação em UTI, controle pressórico agressivo e monitorização neurológica seriada.";
            break;
        case 3: case 4:
            recommendation = "Risco alto. UTI, avaliar com neurocirurgia a possibilidade de intervenção (ex: drenagem, craniotomia). Discutir prognóstico com a família.";
            break;
        default: // 5 e 6
            recommendation = "Risco altíssimo. Prognóstico extremamente reservado. Considerar discussão sobre limitação de suporte terapêutico com a família.";
            break;
    }
    container_ICH.querySelector('#ich-recommendation').innerText = recommendation;
}

function resetICH() {
    container_ICH.querySelectorAll('select').forEach(s => s.selectedIndex = s.querySelector('option[selected]')?.index || 0);
    container_ICH.querySelector('#ich-result').innerText = "";
    container_ICH.querySelector('#ich-mortality').innerText = "";
    container_ICH.querySelector('#ich-recommendation').innerText = "";
}

// 5. Adição segura dos eventos de clique
setTimeout(() => {
    try {
        container_ICH.querySelector('#ich-button').addEventListener('click', calculateICH);
        container_ICH.querySelector('#ich-reset-button').addEventListener('click', resetICH);
    } catch (e) {
      container_ICH.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
    }
}, 0);
```


### **2. Calculadora SIRS**


```dataviewjs
// --- Bloco de Código para Calculadora SIRS com Conduta ---

const calculatorHTML_SIRS = `
<div class="calculator-container">
  <h2>Calculadora de Critérios SIRS (Sepsis-2)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Lembre-se: O conceito de SIRS foi substituído pelo qSOFA/SOFA no Sepsis-3.</p>
  
  <div class="checkbox-group">
    <input type="checkbox" id="sirs-temp"><label for="sirs-temp">Temperatura > 38°C ou < 36°C</label>
  </div>
  <div class="checkbox-group">
    <input type="checkbox" id="sirs-hr"><label for="sirs-hr">Frequência cardíaca > 90 bpm</label>
  </div>
  <div class="checkbox-group">
    <input type="checkbox" id="sirs-rr"><label for="sirs-rr">Frequência respiratória > 20 ipm ou PaCO₂ < 32 mmHg</label>
  </div>
  <div class="checkbox-group">
    <input type="checkbox" id="sirs-wbc"><label for="sirs-wbc">Leucócitos > 12.000, < 4.000 ou > 10% de bastões</label>
  </div>
  
  <div class="button-group">
    <button id="sirs-calc-button">Calcular SIRS</button>
    <button id="sirs-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Critérios presentes: <span id="sirs-result"></span></h3>
  <h4>Interpretação: <span id="sirs-interpretation" style="font-weight: normal;"></span></h4>
  <h4>Conduta Recomendada:</h4>
  <div id="sirs-conduct" class="conduct-box"></div>
</div>
`;
const styles_SIRS = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; margin-bottom: 20px; }
.checkbox-group { margin-bottom: 12px; display: flex; align-items: center; }
.checkbox-group input { margin-right: 10px; min-width: 18px; min-height: 18px; }
.checkbox-group label { line-height: 1.4; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#sirs-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.conduct-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px; line-height: 1.5; }
`;
const container_SIRS = dv.container;
const styleEl_SIRS = document.createElement('style');
styleEl_SIRS.innerHTML = styles_SIRS;
container_SIRS.appendChild(styleEl_SIRS);
container_SIRS.innerHTML += calculatorHTML_SIRS;

function calculateSIRS() {
    let score = 0;
    if (container_SIRS.querySelector('#sirs-temp').checked) score++; if (container_SIRS.querySelector('#sirs-hr').checked) score++;
    if (container_SIRS.querySelector('#sirs-rr').checked) score++; if (container_SIRS.querySelector('#sirs-wbc').checked) score++;
    container_SIRS.querySelector('#sirs-result').innerText = `${score} de 4`;
    const interpretationEl = container_SIRS.querySelector('#sirs-interpretation');
    const conductEl = container_SIRS.querySelector('#sirs-conduct');
    if (score >= 2) {
      interpretationEl.innerText = "Critérios para SIRS presentes. Se houver suspeita de infecção, isso caracteriza Sepse (pela definição Sepsis-2).";
      conductEl.innerHTML = "<strong>Iniciar pacote de 1ª hora:</strong><br>1. Coletar lactato e culturas.<br>2. Iniciar antibiótico de amplo espectro.<br>3. Iniciar reposição volêmica (ex: 30 mL/kg de cristaloide para hipotensão).";
    } else {
      interpretationEl.innerText = "Critérios para SIRS não preenchidos.";
      conductEl.innerText = "Nenhuma conduta específica para SIRS. Tratar a causa base dos sintomas.";
    }
}
function resetSIRS() {
    container_SIRS.querySelectorAll('input[type="checkbox"]').forEach(box => box.checked = false);
    container_SIRS.querySelector('#sirs-result').innerText = "";
    container_SIRS.querySelector('#sirs-interpretation').innerText = "";
    container_SIRS.querySelector('#sirs-conduct').innerHTML = "";
}
setTimeout(() => {
    try {
        container_SIRS.querySelector('#sirs-calc-button').addEventListener('click', calculateSIRS);
        container_SIRS.querySelector('#sirs-reset-button').addEventListener('click', resetSIRS);
    } catch (e) { container_SIRS.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```


### **3. Calculadora qSOFA**

```dataviewjs
// --- Bloco de Código Corrigido para qSOFA com Conduta ---

const calculatorHTML_qSOFA = `
<div class="calculator-container">
  <h2>Calculadora qSOFA (Quick SOFA)</h2>
  <div class="checkbox-group">
    <input type="checkbox" id="qsofa-respiratory-rate"><label for="qsofa-respiratory-rate">Frequência respiratória ≥ 22/min</label>
  </div>
  <div class="checkbox-group">
    <input type="checkbox" id="qsofa-mental-status"><label for="qsofa-mental-status">Alteração do estado mental (Glasgow < 15)</label>
  </div>
  <div class="checkbox-group">
    <input type="checkbox" id="qsofa-systolic-bp"><label for="qsofa-systolic-bp">Pressão arterial sistólica ≤ 100 mmHg</label>
  </div>
  <div class="button-group">
      <button id="qsofa-button">Calcular qSOFA</button>
      <button id="qsofa-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Resultado: <span id="qsofa-result"></span></h3>
  <h4>Interpretação: <span id="qsofa-interpretation" style="font-weight: normal;"></span></h4>
  <h4>Conduta Recomendada:</h4>
  <div id="qsofa-conduct" class="conduct-box"></div>
</div>
`;
const styles_qSOFA = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; margin-bottom: 20px; }
.checkbox-group { margin-bottom: 12px; display: flex; align-items: center; }
.checkbox-group input { margin-right: 10px; min-width: 18px; min-height: 18px; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#qsofa-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.conduct-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px; line-height: 1.5; }
`;
const container_qSOFA = dv.container;
const styleEl_qSOFA = document.createElement('style');
styleEl_qSOFA.innerHTML = styles_qSOFA;
container_qSOFA.appendChild(styleEl_qSOFA);
container_qSOFA.innerHTML += calculatorHTML_qSOFA;

function calculateQSOFA() {
    let score = 0;
    if (container_qSOFA.querySelector('#qsofa-respiratory-rate').checked) score++;
    if (container_qSOFA.querySelector('#qsofa-mental-status').checked) score++;
    if (container_qSOFA.querySelector('#qsofa-systolic-bp').checked) score++;
    container_qSOFA.querySelector('#qsofa-result').innerText = score;
    const interpretationEl = container_qSOFA.querySelector('#qsofa-interpretation');
    const conductEl = container_qSOFA.querySelector('#qsofa-conduct');
    if (score >= 2) {
      interpretationEl.innerText = "Risco aumentado de desfechos desfavoráveis.";
      conductEl.innerHTML = "<strong>Suspeita de sepse.</strong> Agilizar investigação com exames (lactato, culturas) e considerar início do pacote de manejo de sepse (antibióticos, fluidos). Avaliar SOFA completo.";
    } else {
      interpretationEl.innerText = "Baixo risco para desfechos desfavoráveis por sepse.";
      conductEl.innerText = "Continuar monitorização e investigar outras causas para os sintomas.";
    }
}
function resetQSOFA() {
    container_qSOFA.querySelectorAll('input[type="checkbox"]').forEach(box => box.checked = false);
    container_qSOFA.querySelector('#qsofa-result').innerText = "";
    container_qSOFA.querySelector('#qsofa-interpretation').innerText = "";
    container_qSOFA.querySelector('#qsofa-conduct').innerHTML = "";
}
setTimeout(() => {
    try {
        container_qSOFA.querySelector('#qsofa-button').addEventListener('click', calculateQSOFA);
        container_qSOFA.querySelector('#qsofa-reset-button').addEventListener('click', resetQSOFA);
    } catch (e) { container_qSOFA.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **4. Calculadora SOFA**


```dataviewjs
// --- Bloco de Código Corrigido para SOFA com Conduta ---

const calculatorHTML_SOFA = `
<div class="calculator-container">
  <h2>Calculadora SOFA (Sequential Organ Failure Assessment)</h2>
  <div class="input-grid">
      <div class="input-group"><label>Respiratório (PaO2/FiO2)</label><select id="sofa-respiration"><option value="0">≥400</option><option value="1"><400</option><option value="2"><300</option><option value="3"><200</option><option value="4"><100</option></select></div>
      <div class="input-group"><label>Coagulação (Plaquetas)</label><select id="sofa-coagulation"><option value="0">≥150k</option><option value="1"><150k</option><option value="2"><100k</option><option value="3"><50k</option><option value="4"><20k</option></select></div>
      <div class="input-group"><label>Fígado (Bilirrubina)</label><select id="sofa-liver"><option value="0"><1.2</option><option value="1">1.2-1.9</option><option value="2">2.0-5.9</option><option value="3">6.0-11.9</option><option value="4">≥12.0</option></select></div>
      <div class="input-group"><label>Cardiovascular (DVA)</label><select id="sofa-cardiovascular"><option value="0">PAM≥70</option><option value="1">PAM<70</option><option value="2">Dopa<5</option><option value="3">Dopa>5</option><option value="4">Dopa>15</option></select></div>
      <div class="input-group"><label>SNC (Glasgow)</label><select id="sofa-cns"><option value="0">15</option><option value="1">13-14</option><option value="2">10-12</option><option value="3">6-9</option><option value="4"><6</option></select></div>
      <div class="input-group"><label>Renal (Creatinina/DU)</label><select id="sofa-renal"><option value="0"><1.2</option><option value="1">1.2-1.9</option><option value="2">2.0-3.4</option><option value="3">3.5-4.9</option><option value="4">>5.0</option></select></div>
  </div>
  <div class="button-group">
    <button id="sofa-button">Calcular SOFA</button>
    <button id="sofa-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Resultado: <span id="sofa-result"></span></h3>
  <h4>Risco: <span id="sofa-interpretation" style="font-weight: normal;"></span></h4>
  <h4>Conduta Recomendada:</h4>
  <div id="sofa-conduct" class="conduct-box"></div>
</div>
`;
const styles_SOFA = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; margin-bottom: 20px; }
.input-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.input-group label { display: block; margin-bottom: 5px; }
.input-group select { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#sofa-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.conduct-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px; line-height: 1.5; }
`;
const container_SOFA = dv.container;
const styleEl_SOFA = document.createElement('style');
styleEl_SOFA.innerHTML = styles_SOFA;
container_SOFA.appendChild(styleEl_SOFA);
container_SOFA.innerHTML += calculatorHTML_SOFA;

function calculateSOFA() {
    const get = (id) => parseInt(container_SOFA.querySelector('#' + id).value);
    const totalScore = get('sofa-respiration') + get('sofa-coagulation') + get('sofa-liver') + get('sofa-cardiovascular') + get('sofa-cns') + get('sofa-renal');
    container_SOFA.querySelector('#sofa-result').innerText = totalScore;
    const interpretationEl = container_SOFA.querySelector('#sofa-interpretation');
    const conductEl = container_SOFA.querySelector('#sofa-conduct');
    if (totalScore >= 2) {
        interpretationEl.innerText = "Disfunção orgânica significativa. Em paciente com infecção, um aumento ≥ 2 pontos indica sepse.";
        conductEl.innerText = "Otimizar suporte orgânico para cada sistema acometido (ex: ventilação protetora, DVA para PAM alvo, avaliar necessidade de TRS). Reavaliar antibioticoterapia e controle de foco infeccioso.";
    } else {
        interpretationEl.innerText = "Baixo risco de disfunção orgânica significativa.";
        conductEl.innerText = "Manter monitorização e tratamento da condição de base.";
    }
}
function resetSOFA() {
    container_SOFA.querySelectorAll('select').forEach(s => s.selectedIndex = 0);
    container_SOFA.querySelector('#sofa-result').innerText = "";
    container_SOFA.querySelector('#sofa-interpretation').innerText = "";
    container_SOFA.querySelector('#sofa-conduct').innerText = "";
}
setTimeout(() => {
    try {
        container_SOFA.querySelector('#sofa-button').addEventListener('click', calculateSOFA);
        container_SOFA.querySelector('#sofa-reset-button').addEventListener('click', resetSOFA);
    } catch (e) { container_SOFA.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```


### **5. Calculadora NIHSS**


```dataviewjs
// --- Bloco de Código Completo para NIHSS com Conduta ---

const calculatorHTML_NIHSS = `
<div class="calculator-container">
  <h2>Calculadora NIHSS</h2>
  <div class="input-grid">
    <div class="input-group"><label for="item1a">1a. Nível de Consciência</label><select id="item1a"><option value="0">0-Alerta</option><option value="1">1-Sonolento</option><option value="2">2-Torporoso</option><option value="3">3-Coma</option></select></div>
    <div class="input-group"><label for="item1b">1b. Orientação</label><select id="item1b"><option value="0">0-Acerta 2</option><option value="1">1-Acerta 1</option><option value="2">2-Acerta 0</option></select></div>
    <div class="input-group"><label for="item1c">1c. Comandos</label><select id="item1c"><option value="0">0-Obedece 2</option><option value="1">1-Obedece 1</option><option value="2">2-Obedece 0</option></select></div>
    <div class="input-group"><label for="item2">2. Olhar Conjugado</label><select id="item2"><option value="0">0-Normal</option><option value="1">1-Paresia</option><option value="2">2-Desvio</option></select></div>
    <div class="input-group"><label for="item3">3. Campo Visual</label><select id="item3"><option value="0">0-Normal</option><option value="1">1-Parcial</option><option value="2">2-Completa</option><option value="3">3-Bilateral</option></select></div>
    <div class="input-group"><label for="item4">4. Paralisia Facial</label><select id="item4"><option value="0">0-Normal</option><option value="1">1-Menor</option><option value="2">2-Parcial</option><option value="3">3-Completa</option></select></div>
    <div class="input-group"><label for="item5a">5a. Motor MS Dir</label><select id="item5a"><option value="0">0-Normal</option><option value="1">1-Drift</option><option value="2">2-Vence G</option><option value="3">3-Não Vence G</option><option value="4">4-Plegia</option></select></div>
    <div class="input-group"><label for="item5b">5b. Motor MS Esq</label><select id="item5b"><option value="0">0-Normal</option><option value="1">1-Drift</option><option value="2">2-Vence G</option><option value="3">3-Não Vence G</option><option value="4">4-Plegia</option></select></div>
    <div class="input-group"><label for="item6a">6a. Motor MI Dir</label><select id="item6a"><option value="0">0-Normal</option><option value="1">1-Drift</option><option value="2">2-Vence G</option><option value="3">3-Não Vence G</option><option value="4">4-Plegia</option></select></div>
    <div class="input-group"><label for="item6b">6b. Motor MI Esq</label><select id="item6b"><option value="0">0-Normal</option><option value="1">1-Drift</option><option value="2">2-Vence G</option><option value="3">3-Não Vence G</option><option value="4">4-Plegia</option></select></div>
    <div class="input-group"><label for="item7">7. Ataxia</label><select id="item7"><option value="0">0-Ausente</option><option value="1">1-1 membro</option><option value="2">2-≥2 membros</option></select></div>
    <div class="input-group"><label for="item8">8. Sensitivo</label><select id="item8"><option value="0">0-Normal</option><option value="1">1-Leve</option><option value="2">2-Grave</option></select></div>
    <div class="input-group"><label for="item9">9. Linguagem</label><select id="item9"><option value="0">0-Normal</option><option value="1">1-Leve</option><option value="2">2-Grave</option><option value="3">3-Global</option></select></div>
    <div class="input-group"><label for="item10">10. Disartria</label><select id="item10"><option value="0">0-Normal</option><option value="1">1-Leve</option><option value="2">2-Grave</option></select></div>
    <div class="input-group"><label for="item11">11. Extinção</label><select id="item11"><option value="0">0-Nenhuma</option><option value="1">1-Parcial</option><option value="2">2-Completa</option></select></div>
  </div>
  <div class="button-group">
    <button id="nihss-button">Calcular NIHSS</button>
    <button id="nihss-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Resultado: <span id="nihss-result"></span></h3>
  <h4>Gravidade e Prognóstico: <span id="nihss-interpretation" style="font-weight: normal;"></span></h4>
  <h4>Conduta Recomendada:</h4>
  <div id="nihss-conduct" class="conduct-box"></div>
</div>
`;
const styles_NIHSS = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; margin-bottom: 20px; }
.input-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px; }
.input-group label { display: block; margin-bottom: 5px; font-weight: bold; }
.input-group select { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; margin-top: 15px; }
.button-group button { flex-grow: 1; padding: 10px; border: none; border-radius: 4px; cursor: pointer; }
#nihss-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.conduct-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px; line-height: 1.5; }
`;
const container_NIHSS = dv.container;
const styleEl_NIHSS = document.createElement('style');
styleEl_NIHSS.innerHTML = styles_NIHSS;
container_NIHSS.appendChild(styleEl_NIHSS);
container_NIHSS.innerHTML += calculatorHTML_NIHSS;

function calculateNIHSS() {
    let totalScore = 0;
    const get = (id) => parseInt(container_NIHSS.querySelector('#' + id).value);
    totalScore += get('item1a') + get('item1b') + get('item1c') + get('item2') + get('item3') + get('item4');
    totalScore += get('item5a') + get('item5b') + get('item6a') + get('item6b');
    totalScore += get('item7') + get('item8') + get('item9') + get('item10') + get('item11');
    
    container_NIHSS.querySelector('#nihss-result').innerText = totalScore;
    let interpretation = ""; let conduct = "";
    if (totalScore === 0) { interpretation = "Sem sintomas de AVC."; conduct = "Investigar outras causas. Se AIT, iniciar prevenção secundária."; }
    else if (totalScore <= 4) { interpretation = "AVC Menor."; conduct = "<strong>Dentro da janela (< 4.5h):</strong> Candidato a trombólise venosa com Alteplase (IV), se não houver contraindicações."; }
    else if (totalScore <= 15) { interpretation = "AVC Moderado."; conduct = "<strong>Dentro da janela (< 4.5h):</strong> Forte candidato a trombólise. <strong>Se oclusão de grande vaso (AngioTC):</strong> considerar Trombectomia Mecânica (< 24h)."; }
    else if (totalScore <= 20) { interpretation = "AVC Moderado a Grave."; conduct = "<strong>Dentro da janela (< 4.5h):</strong> Avaliar trombólise. <strong>Se oclusão de grande vaso (AngioTC):</strong> forte candidato a Trombectomia Mecânica (< 24h)."; }
    else { interpretation = "AVC Grave."; conduct = "Prognóstico reservado. Avaliar para Trombectomia Mecânica se oclusão de grande vaso. Discutir prognóstico e cuidados com a família."; }
    container_NIHSS.querySelector('#nihss-interpretation').innerText = interpretation;
    container_NIHSS.querySelector('#nihss-conduct').innerHTML = conduct;
}
function resetNIHSS() {
    container_NIHSS.querySelectorAll('select').forEach(s => s.selectedIndex = 0);
    container_NIHSS.querySelector('#nihss-result').innerText = "";
    container_NIHSS.querySelector('#nihss-interpretation').innerText = "";
    container_NIHSS.querySelector('#nihss-conduct').innerHTML = "";
}
setTimeout(() => {
    try {
        container_NIHSS.querySelector('#nihss-button').addEventListener('click', calculateNIHSS);
        container_NIHSS.querySelector('#nihss-reset-button').addEventListener('click', resetNIHSS);
    } catch (e) { container_NIHSS.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```


### **6. Calculadora MDRD**


```dataviewjs
// --- Bloco de Código para Calculadora TFG (MDRD) com Conduta ---

const calculatorHTML_MDRD = `
<div class="calculator-container">
  <h2>Calculadora de TFG Estimada (Fórmula MDRD)</h2>
  <div class="input-group">
    <label for="mdrd-creat">Creatinina Sérica (mg/dL)</label>
    <input type="number" id="mdrd-creat" placeholder="Ex: 1.2" step="0.1">
  </div>
  <div class="input-group">
    <label for="mdrd-age">Idade (anos)</label>
    <input type="number" id="mdrd-age" placeholder="Ex: 55">
  </div>
  <div class="input-group">
    <label for="mdrd-sex">Sexo</label>
    <select id="mdrd-sex"><option value="masculino">Masculino</option><option value="feminino">Feminino</option></select>
  </div>
  <div class="checkbox-group">
    <input type="checkbox" id="mdrd-ethnicity"><label for="mdrd-ethnicity">Afro-americano</label>
  </div>
  <div class="button-group">
    <button id="mdrd-calc-button">Calcular TFG</button>
    <button id="mdrd-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Resultado (TFG estimada): <span id="mdrd-result"></span></h3>
  <h4>Estágio da DRC: <span id="mdrd-stage" style="font-weight: normal;"></span></h4>
  <h4>Conduta Recomendada:</h4>
  <div id="mdrd-conduct" class="conduct-box"></div>
</div>
`;
const styles_MDRD = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; margin-bottom: 20px; }
.input-group, .checkbox-group { margin-bottom: 15px; }
label { display: block; margin-bottom: 5px; font-weight: bold; }
input[type="number"], select { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; box-sizing: border-box; }
.checkbox-group { display: flex; align-items: center; }
.checkbox-group input { margin-right: 8px; }
.button-group { display: flex; gap: 10px; margin-top: 20px; }
.button-group button { flex-grow: 1; padding: 10px; border: none; border-radius: 4px; cursor: pointer; }
#mdrd-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.conduct-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px; line-height: 1.5; }
`;
const container_MDRD = dv.container;
const styleEl_MDRD = document.createElement('style');
styleEl_MDRD.innerHTML = styles_MDRD;
container_MDRD.appendChild(styleEl_MDRD);
container_MDRD.innerHTML += calculatorHTML_MDRD;

function calculateMDRD() {
    const creat = parseFloat(container_MDRD.querySelector('#mdrd-creat').value);
    const age = parseInt(container_MDRD.querySelector('#mdrd-age').value);
    const sex = container_MDRD.querySelector('#mdrd-sex').value;
    const isAfro = container_MDRD.querySelector('#mdrd-ethnicity').checked;
    if (isNaN(creat) || isNaN(age) || creat <= 0 || age <= 0) {
        alert("Por favor, insira valores válidos."); return;
    }
    let tfg = 175 * Math.pow(creat, -1.154) * Math.pow(age, -0.203);
    if (sex === 'feminino') tfg *= 0.742;
    if (isAfro) tfg *= 1.212;
    container_MDRD.querySelector('#mdrd-result').innerText = `${tfg.toFixed(2)} mL/min/1.73 m²`;
    const stageEl = container_MDRD.querySelector('#mdrd-stage');
    const conductEl = container_MDRD.querySelector('#mdrd-conduct');
    let stageText = "", conductText = "";
    if (tfg >= 90) { stageText = "Estágio 1"; conductText = "Diagnóstico e tratamento da causa base. Controle de comorbidades (HAS, DM) e redução de fatores de risco CV."; }
    else if (tfg >= 60) { stageText = "Estágio 2"; conductText = "Estimativa da progressão. Monitoramento anual da TFG. Evitar drogas nefroxóticas."; }
    else if (tfg >= 45) { stageText = "Estágio 3a"; conductText = "Tratamento de complicações (anemia, DMO). Encaminhar ao nefrologista. Ajuste de dose de medicamentos."; }
    else if (tfg >= 30) { stageText = "Estágio 3b"; conductText = "Acompanhamento nefrológico regular (3-6 meses). Manejo intensivo de complicações."; }
    else if (tfg >= 15) { stageText = "Estágio 4"; conductText = "Preparação para Terapia Renal Substitutiva (TRS): fístula, diálise peritoneal, planejamento de transplante."; }
    else { stageText = "Estágio 5"; conductText = "Iniciar TRS (Diálise ou Transplante Renal)."; }
    stageEl.innerText = stageText;
    conductEl.innerText = conductText;
}
function resetMDRD() {
    container_MDRD.querySelectorAll('input, select').forEach(el => {
        if (el.type === 'checkbox') el.checked = false;
        else if (el.type === 'number') el.value = '';
        else el.selectedIndex = 0;
    });
    container_MDRD.querySelector('#mdrd-result').innerText = "";
    container_MDRD.querySelector('#mdrd-stage').innerText = "";
    container_MDRD.querySelector('#mdrd-conduct').innerText = "";
}
setTimeout(() => {
    try {
        container_MDRD.querySelector('#mdrd-calc-button').addEventListener('click', calculateMDRD);
        container_MDRD.querySelector('#mdrd-reset-button').addEventListener('click', resetMDRD);
    } catch (e) { container_MDRD.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```


### **7. Calculadora de Sedoanalgesia**


```dataviewjs
// --- Bloco de Código para Calculadora de Sedoanalgesia e Guia Rápido ---

const toolHTML_Sedo = `
<div id="calculator-wrapper">
    <div class="calculator-container">
      <h2>Calculadora de Diluição e Infusão</h2>
      
      <div class="input-group">
        <label for="drug-select">Selecione a Droga:</label>
        <select id="drug-select">
          <option value="fentanyl">Fentanil</option>
          <option value="midazolam">Midazolam</option>
          <option value="propofol">Propofol</option>
          <option value="noradrenaline">Noradrenalina</option>
          <option value="remifentanil">Remifentanil</option>
        </select>
      </div>

      <h3 class="section-header">1. Preparo da Solução</h3>
      <div class="input-group">
        <label for="drug-amount">Quantidade de droga na solução (<span id="drug-unit-label">mcg</span>):</label>
        <input type="number" id="drug-amount" placeholder="Ex: 1000">
      </div>
      <div class="input-group">
        <label for="total-volume">Volume total da solução (mL):</label>
        <input type="number" id="total-volume" placeholder="Ex: 100">
      </div>
      <p><strong>Concentração:</strong> <span id="drug-concentration">-</span></p>

      <h3 class="section-header">2. Cálculo da Infusão</h3>
      <div class="input-group" id="weight-group">
        <label for="patient-weight">Peso do paciente (kg):</label>
        <input type="number" id="patient-weight" placeholder="Ex: 70">
      </div>
      <div class="input-group">
        <label for="prescribed-dose">Dose prescrita (<span id="dose-unit-label">mcg/kg/min</span>):</label>
        <input type="number" id="prescribed-dose" placeholder="Ex: 0.05">
      </div>

      <div class="button-group">
        <button id="calc-button">Calcular</button>
        <button id="reset-button" class="secondary">Reiniciar</button>
      </div>
      
      <h3>Resultado da Infusão:</h3>
      <p><strong>Velocidade de Infusão: <span id="infusion-rate">-</span></strong></p>
    </div>
</div>

<div class="info-container">
    <h2>Guia de Conduta: Indicações e Doses Usuais</h2>

    <h4>Fentanil</h4>
    <ul>
        <li><strong>Indicação:</strong> Analgesia potente para pacientes em ventilação mecânica.</li>
        <li><strong>Dose usual (infusão):</strong> 0.5 a 2 mcg/kg/hora.</li>
        <li><strong>Observações:</strong> Opioide de início rápido e curta duração. Pode causar depressão respiratória e rigidez torácica em altas doses.</li>
    </ul>

    <h4>Midazolam</h4>
    <ul>
        <li><strong>Indicação:</strong> Sedação, ansiólise e amnésia. Usado para manter a sedação em pacientes na UTI.</li>
        <li><strong>Dose usual (infusão):</strong> 0.02 a 0.1 mg/kg/hora (ou 1 a 7 mg/hora).</li>
        <li><strong>Observações:</strong> Benzodiazepínico. Risco de acúmulo em pacientes com insuficiência renal ou hepática e em idosos, prolongando o tempo de despertar. Pode causar delirium.</li>
    </ul>

    <h4>Propofol</h4>
    <ul>
        <li><strong>Indicação:</strong> Sedativo-hipnótico para indução e manutenção da sedação. Preferido para sedação de curta duração e avaliação neurológica (despertar rápido).</li>
        <li><strong>Dose usual (infusão):</strong> 5 a 50 mcg/kg/minuto.</li>
        <li><strong>Observações:</strong> Solução lipídica (atenção à contaminação e contagem de calorias). Pode causar hipotensão e depressão respiratória. Risco de Síndrome da Infusão do Propofol (PRIS) com doses altas e uso prolongado.</li>
    </ul>

    <h4>Noradrenalina</h4>
    <ul>
        <li><strong>Indicação:</strong> Vasopressor de primeira escolha no choque séptico e outras formas de choque distributivo.</li>
        <li><strong>Dose usual (infusão):</strong> 0.01 a 3 mcg/kg/minuto.</li>
        <li><strong>Observações:</strong> Potente vasoconstritor (alfa-1 agonista). Deve ser infundida preferencialmente em acesso venoso central para evitar necrose tecidual por extravasamento.</li>
    </ul>
    
    <h4>Remifentanil</h4>
    <ul>
        <li><strong>Indicação:</strong> Analgesia potente de ação ultracurta, ideal para procedimentos dolorosos de curta duração ou quando um despertar muito rápido é necessário.</li>
        <li><strong>Dose usual (infusão):</strong> 0.05 a 0.2 mcg/kg/minuto.</li>
        <li><strong>Observações:</strong> Metabolizado por esterases plasmáticas, não se acumula em insuficiência renal ou hepática. O efeito cessa minutos após a suspensão, exigindo planejamento de analgesia alternativa.</li>
    </ul>
</div>
`;

const styles_Sedo = `
.calculator-container, .info-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; margin-bottom: 20px; }
.info-container { background-color: #e9f5ff; }
.info-container h4 { border-bottom: 2px solid #007bff; padding-bottom: 5px; margin-top: 20px; }
.input-group { margin-bottom: 15px; }
label { display: block; margin-bottom: 5px; font-weight: 500; }
input[type="number"], select { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; box-sizing: border-box; }
.button-group { display: flex; gap: 10px; margin-top: 20px; }
.button-group button { flex-grow: 1; padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; }
#calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.section-header { margin-top: 20px; border-bottom: 1px solid #ccc; padding-bottom: 3px; font-size: 1.1em; }
#infusion-rate { font-size: 1.2em; color: darkred; font-weight: bold; }
`;

const container_Sedo = dv.container;
const styleEl_Sedo = document.createElement('style');
styleEl_Sedo.innerHTML = styles_Sedo;
container_Sedo.appendChild(styleEl_Sedo);
container_Sedo.innerHTML += toolHTML_Sedo;

const drugData_Sedo = {
    fentanyl: { drugUnit: "mcg", doseUnit: "mcg/kg/hora", weightBased: true, doseFactor: 1, conversion: 1 },
    midazolam: { drugUnit: "mg", doseUnit: "mg/kg/hora", weightBased: true, doseFactor: 1, conversion: 1000 },
    propofol: { drugUnit: "mg", doseUnit: "mcg/kg/min", weightBased: true, doseFactor: 60, conversion: 1000 },
    noradrenaline: { drugUnit: "mg", doseUnit: "mcg/kg/min", weightBased: true, doseFactor: 60, conversion: 1000 },
    remifentanil: { drugUnit: "mg", doseUnit: "mcg/kg/min", weightBased: true, doseFactor: 60, conversion: 1000 }
};

function updateUI_Sedo() {
    const drugSelect = container_Sedo.querySelector('#drug-select');
    const selectedDrug = drugData_Sedo[drugSelect.value];
    container_Sedo.querySelector('#drug-unit-label').textContent = selectedDrug.drugUnit;
    container_Sedo.querySelector('#dose-unit-label').textContent = selectedDrug.doseUnit;
}

function calculateInfusion_Sedo() {
    const selectedDrug = drugData_Sedo[container_Sedo.querySelector('#drug-select').value];
    const drugAmount = parseFloat(container_Sedo.querySelector('#drug-amount').value);
    const totalVolume = parseFloat(container_Sedo.querySelector('#total-volume').value);
    const weight = parseFloat(container_Sedo.querySelector('#patient-weight').value);
    const prescribedDose = parseFloat(container_Sedo.querySelector('#prescribed-dose').value);
    if ([drugAmount, totalVolume, weight, prescribedDose].some(isNaN) || totalVolume <= 0) {
        alert("Por favor, preencha todos os campos com valores válidos."); return;
    }
    const concentrationMcgMl = (drugAmount * selectedDrug.conversion) / totalVolume;
    container_Sedo.querySelector('#drug-concentration').textContent = `${concentrationMcgMl.toFixed(2)} mcg/mL`;
    const totalDoseMcgPerHour = prescribedDose * weight * selectedDrug.doseFactor;
    const infusionRate = totalDoseMcgPerHour / concentrationMcgMl;
    container_Sedo.querySelector('#infusion-rate').textContent = `${infusionRate.toFixed(2)} mL/h`;
}

function resetCalculator_Sedo() {
    container_Sedo.querySelectorAll('input[type="number"]').forEach(input => input.value = '');
    container_Sedo.querySelector('#drug-concentration').textContent = '-';
    container_Sedo.querySelector('#infusion-rate').textContent = '-';
}

setTimeout(() => {
    try {
        container_Sedo.querySelector('#drug-select').addEventListener('change', updateUI_Sedo);
        container_Sedo.querySelector('#calc-button').addEventListener('click', calculateInfusion_Sedo);
        container_Sedo.querySelector('#reset-button').addEventListener('click', resetCalculator_Sedo);
        updateUI_Sedo();
    } catch (e) { container_Sedo.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```


### **8. Calculadora de Wells (TEP)**



### **9. Calculadora PESI**


```dataviewjs
// --- Bloco de Código para Calculadora dos Escores PESI e sPESI com Conduta ---

const calculatorHTML_PESI = `
<div class="calculator-container">
  <h2>Calculadora de Escore PESI e sPESI (Prognóstico da TEP)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Estratifica o risco de mortalidade em 30 dias em pacientes com TEP confirmada, ajudando a identificar candidatos a tratamento ambulatorial.</p>
  
  <div class="input-grid">
      <div class="input-group"><label for="pesi-age">Idade (anos)</label><input type="number" id="pesi-age" placeholder="Ex: 70"></div>
      <div class="input-group"><label for="pesi-sex">Sexo Masculino</label><select id="pesi-sex"><option value="nao">Não</option><option value="sim">Sim</option></select></div>
      <div class="input-group"><label for="pesi-hr">FC ≥ 110 bpm</label><select id="pesi-hr"><option value="nao">Não</option><option value="sim">Sim</option></select></div>
      <div class="input-group"><label for="pesi-sbp">PAS < 100 mmHg</label><select id="pesi-sbp"><option value="nao">Não</option><option value="sim">Sim</option></select></div>
      <div class="input-group"><label for="pesi-rr">FR ≥ 30 ipm</label><select id="pesi-rr"><option value="nao">Não</option><option value="sim">Sim</option></select></div>
      <div class="input-group"><label for="pesi-temp">Temp < 36°C</label><select id="pesi-temp"><option value="nao">Não</option><option value="sim">Sim</option></select></div>
      <div class="input-group"><label for="pesi-ams">Nível de Consciência Alterado</label><select id="pesi-ams"><option value="nao">Não</option><option value="sim">Sim</option></select></div>
      <div class="input-group"><label for="pesi-sao2">SaO₂ < 90%</label><select id="pesi-sao2"><option value="nao">Não</option><option value="sim">Sim</option></select></div>
  </div>
  <div class="checkbox-grid">
      <div class="checkbox-group"><input type="checkbox" id="pesi-cancer"><label for="pesi-cancer">História de Câncer</label></div>
      <div class="checkbox-group"><input type="checkbox" id="pesi-chf"><label for="pesi-chf">História de IC Crônica</label></div>
      <div class="checkbox-group"><input type="checkbox" id="pesi-cpd"><label for="pesi-cpd">História de Doença Pulmonar Crônica</label></div>
  </div>

  <div class="button-group">
    <button id="pesi-calc-button">Calcular Escores</button>
    <button id="pesi-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <div id="results-wrapper">
    <div class="result-box"><h3>Escore PESI</h3><p><strong>Pontuação:</strong> <span id="pesi-result">-</span></p><p><strong>Classe:</strong> <span id="pesi-class">-</span></p><p><strong>Mortalidade:</strong> <span id="pesi-mortality">-</span></p></div>
    <div class="result-box"><h3>Escore sPESI</h3><p><strong>Pontuação:</strong> <span id="spesi-result">-</span></p><p><strong>Risco:</strong> <span id="spesi-class">-</span></p><p><strong>Mortalidade:</strong> <span id="spesi-mortality">-</span></p></div>
  </div>
  <h4>Conduta Recomendada (baseado no sPESI):</h4>
  <div id="pesi-conduct" class="conduct-box"></div>
</div>
`;
const styles_PESI = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; margin-bottom: 20px; }
.input-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 15px; }
.checkbox-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 5px; }
.input-group label, .checkbox-group label { display: block; margin-bottom: 5px; }
.checkbox-group { display: flex; align-items: center; }
input, select { padding: 8px; border-radius: 4px; border: 1px solid #ccc; width: 100%; box-sizing: border-box; }
.checkbox-group input { width: auto; margin-right: 10px; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#pesi-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
#results-wrapper { display: flex; gap: 20px; margin-top: 15px; flex-wrap: wrap; }
.result-box { flex: 1; min-width: 200px; padding: 15px; background-color: #e9ecef; border-radius: 4px; }
.result-box h3 { margin-top: 0; border-bottom: 1px solid #ccc; padding-bottom: 5px; }
.result-box p { margin: 5px 0; }
.conduct-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px; line-height: 1.5; }
`;

const container_PESI = dv.container;
const styleEl_PESI = document.createElement('style');
styleEl_PESI.innerHTML = styles_PESI;
container_PESI.appendChild(styleEl_PESI);
container_PESI.innerHTML += calculatorHTML_PESI;

function calculatePESI() {
    let pesiScore = 0; let spesiScore = 0;
    const getEl = (id) => container_PESI.querySelector('#' + id);
    const age = parseInt(getEl('pesi-age').value);
    if (isNaN(age)) { alert("Por favor, insira a idade."); return; }
    pesiScore += age;
    if (getEl('pesi-sex').value === 'sim') pesiScore += 10;
    if (getEl('pesi-cancer').checked) { pesiScore += 30; spesiScore += 1; }
    if (getEl('pesi-chf').checked) pesiScore += 10;
    if (getEl('pesi-cpd').checked) pesiScore += 10;
    if (getEl('pesi-chf').checked || getEl('pesi-cpd').checked) spesiScore += 1;
    if (getEl('pesi-hr').value === 'sim') { pesiScore += 20; spesiScore += 1; }
    if (getEl('pesi-sbp').value === 'sim') { pesiScore += 30; spesiScore += 1; }
    if (getEl('pesi-rr').value === 'sim') pesiScore += 20;
    if (getEl('pesi-temp').value === 'sim') pesiScore += 20;
    if (getEl('pesi-ams').value === 'sim') pesiScore += 60;
    if (getEl('pesi-sao2').value === 'sim') { pesiScore += 20; spesiScore += 1; }
    if (age > 80) spesiScore += 1;
    getEl('pesi-result').innerText = pesiScore;
    let pesiClass, pesiMortality;
    if (pesiScore <= 65) { pesiClass = "I"; pesiMortality = "0-1.6%"; }
    else if (pesiScore <= 85) { pesiClass = "II"; pesiMortality = "1.7-3.5%"; }
    else if (pesiScore <= 105) { pesiClass = "III"; pesiMortality = "3.2-7.1%"; }
    else if (pesiScore <= 125) { pesiClass = "IV"; pesiMortality = "4.0-11.4%"; }
    else { pesiClass = "V"; pesiMortality = "10.0-24.5%"; }
    getEl('pesi-class').innerText = pesiClass; getEl('pesi-mortality').innerText = pesiMortality;
    getEl('spesi-result').innerText = spesiScore;
    let spesiClass, spesiMortality, recommendation;
    if (spesiScore === 0) {
        spesiClass = "Baixo Risco"; spesiMortality = "~1.0%";
        recommendation = "Risco baixo. O paciente pode ser candidato a tratamento ambulatorial, se houver condições sociais e clínicas adequadas (ex: ausência de dor severa, sangramento recente, necessidade de O2).";
    } else {
        spesiClass = "Alto Risco"; spesiMortality = "~10.9%";
        recommendation = "Risco alto. O paciente deve ser internado para tratamento e monitorização.";
    }
    getEl('spesi-class').innerText = spesiClass; getEl('spesi-mortality').innerText = spesiMortality;
    getEl('pesi-conduct').innerText = recommendation;
}
function resetPESI() {
    container_PESI.querySelectorAll('input, select').forEach(el => {
        if (el.type === 'checkbox') el.checked = false;
        else if (el.type === 'number') el.value = '';
        else el.selectedIndex = 0;
    });
    const fields = ['pesi-result', 'pesi-class', 'pesi-mortality', 'spesi-result', 'spesi-class', 'spesi-mortality', 'pesi-conduct'];
    fields.forEach(id => container_PESI.querySelector('#' + id).innerText = "-");
}
setTimeout(() => {
    try {
        container_PESI.querySelector('#pesi-calc-button').addEventListener('click', calculatePESI);
        container_PESI.querySelector('#pesi-reset-button').addEventListener('click', resetPESI);
    } catch (e) { container_PESI.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **10. Calculadora Critérios de Light**


```dataviewjs
// --- Bloco de Código para Calculadora de Critérios de Light com Conduta ---

const calculatorHTML_Light = `
<div class="calculator-container">
  <h2>Calculadora de Critérios de Light (Derrame Pleural)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Diferencia derrames pleurais em transudatos e exsudatos.</p>
  
  <h3 class="section-header">Valores do Líquido Pleural</h3>
  <div class="input-group">
    <label for="light-pleural-protein">Proteína Pleural (g/dL)</label><input type="number" id="light-pleural-protein" placeholder="Ex: 4.5" step="0.1">
  </div>
  <div class="input-group">
    <label for="light-pleural-ldh">LDH Pleural (U/L)</label><input type="number" id="light-pleural-ldh" placeholder="Ex: 350" step="1">
  </div>

  <h3 class="section-header">Valores do Soro (Sangue)</h3>
  <div class="input-group">
    <label for="light-serum-protein">Proteína Sérica (g/dL)</label><input type="number" id="light-serum-protein" placeholder="Ex: 7.0" step="0.1">
  </div>
  <div class="input-group">
    <label for="light-serum-ldh">LDH Sérico (U/L)</label><input type="number" id="light-serum-ldh" placeholder="Ex: 200" step="1">
  </div>
  <div class="input-group">
    <label for="light-ldh-limit">Limite Superior do LDH Sérico (U/L)</label><input type="number" id="light-ldh-limit" placeholder="Ex: 250" step="1">
  </div>
  
  <div class="button-group">
    <button id="light-calc-button">Analisar Critérios</button>
    <button id="light-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <div id="light-interpretation" class="conduct-box"></div>
</div>
`;
const styles_Light = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; margin-bottom: 20px; }
.section-header { margin-top: 20px; border-bottom: 1px solid #ccc; padding-bottom: 3px; font-size: 1.1em; }
.input-group { margin-bottom: 15px; }
label { display: block; margin-bottom: 5px; }
input[type="number"] { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; box-sizing: border-box; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#light-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.conduct-box { padding: 15px; background-color: #e9ecef; border-radius: 4px; margin-top: 20px; line-height: 1.6; }
.result-final { font-size: 1.3em; font-weight: bold; text-align: center; padding: 10px; border-radius: 5px; margin: 10px 0; }
.exudate { background-color: #f8d7da; color: #721c24; border: 1px solid #f5c6cb; }
.transudate { background-color: #d4edda; color: #155724; border: 1px solid #c3e6cb; }
`;
const container_Light = dv.container;
const styleEl_Light = document.createElement('style');
styleEl_Light.innerHTML = styles_Light;
container_Light.appendChild(styleEl_Light);
container_Light.innerHTML += calculatorHTML_Light;

function calculateLightsCriteria() {
    const pProt = parseFloat(container_Light.querySelector('#light-pleural-protein').value);
    const sProt = parseFloat(container_Light.querySelector('#light-serum-protein').value);
    const pLDH = parseFloat(container_Light.querySelector('#light-pleural-ldh').value);
    const sLDH = parseFloat(container_Light.querySelector('#light-serum-ldh').value);
    const ldhLimit = parseFloat(container_Light.querySelector('#light-ldh-limit').value);
    if ([pProt, sProt, pLDH, sLDH, ldhLimit].some(isNaN)) {
        alert("Por favor, preencha todos os campos."); return;
    }
    const proteinRatio = pProt / sProt; const ldhRatio = pLDH / sLDH; const ldhLimitCheck = (2/3) * ldhLimit;
    const criterion1 = proteinRatio > 0.5; const criterion2 = ldhRatio > 0.6; const criterion3 = pLDH > ldhLimitCheck;
    const isExudate = criterion1 || criterion2 || criterion3;
    let resultHTML = "<h4>Análise dos Critérios:</h4><ul>";
    resultHTML += `<li>Proteína Pleural / Sérica > 0.5: <strong>${criterion1 ? 'SIM' : 'NÃO'}</strong> (Ratio: ${proteinRatio.toFixed(2)})</li>`;
    resultHTML += `<li>LDH Pleural / Sérico > 0.6: <strong>${criterion2 ? 'SIM' : 'NÃO'}</strong> (Ratio: ${ldhRatio.toFixed(2)})</li>`;
    resultHTML += `<li>LDH Pleural > 2/3 do Limite Superior: <strong>${criterion3 ? 'SIM' : 'NÃO'}</strong> (Valor: ${pLDH.toFixed(0)} vs Limite: ${ldhLimitCheck.toFixed(0)})</li>`;
    resultHTML += "</ul>";
    if (isExudate) {
        resultHTML += `<div class="result-final exudate">Diagnóstico: EXSUDATO</div>`;
        resultHTML += "<strong>Conduta Recomendada:</strong> Investigar a causa do processo inflamatório/infeccioso local. Considerar: citologia, culturas (bacteriana, fúngica, BK), ADA (tuberculose), análise de glicose e pH, e biópsia pleural se necessário.<br><strong>Causas Comuns:</strong> Infecção (pneumonia, empiema), Neoplasia, Embolia Pulmonar.";
    } else {
        resultHTML += `<div class="result-final transudate">Diagnóstico: TRANSUDATO</div>`;
        resultHTML += "<strong>Conduta Recomendada:</strong> O foco é tratar a condição sistêmica de base. Não são necessários mais exames invasivos no líquido pleural, a menos que a apresentação seja atípica.<br><strong>Causas Comuns:</strong> Insuficiência Cardíaca Congestiva, Cirrose Hepática, Síndrome Nefrótica.";
    }
    container_Light.querySelector('#light-interpretation').innerHTML = resultHTML;
}
function resetLights() {
    container_Light.querySelectorAll('input[type="number"]').forEach(input => input.value = '');
    container_Light.querySelector('#light-interpretation').innerHTML = "";
}
setTimeout(() => {
    try {
        container_Light.querySelector('#light-calc-button').addEventListener('click', calculateLightsCriteria);
        container_Light.querySelector('#light-reset-button').addEventListener('click', resetLights);
    } catch (e) { container_Light.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```
```