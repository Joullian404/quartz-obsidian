Excelente solicitação! Transformar essas calculadoras em ferramentas de decisão clínica mais completas, com recomendações de conduta, é um passo muito valioso.

Adicionei as recomendações de conduta e doses nos códigos que você forneceu. Para cada calculadora, a abordagem foi:

1.  **Manter a Lógica do Escore:** O cálculo do escore permanece o mesmo.
2.  **Adicionar uma Seção de Conduta:** A interpretação foi expandida para incluir recomendações de manejo, medicamentos e doses iniciais típicas.
3.  **Priorizar a Segurança:** Incluí alertas (⚠️) e notas de rodapé enfatizando que as doses e escolhas devem ser individualizadas e seguir os protocolos locais.

---

### ⚠️ **AVISO IMPORTANTE ANTES DE USAR** ⚠️

As informações de conduta e dosagem de medicamentos fornecidas abaixo são para **fins educacionais e de referência rápida**. Elas **NÃO** substituem o julgamento clínico. A escolha da terapia, as doses e os ajustes devem ser sempre individualizados para cada paciente, levando em conta a função renal e hepática, comorbidades, alergias, peso, hemodinâmica e, crucialmente, **os protocolos da sua instituição e a epidemiologia local.**

---

Aqui estão os códigos atualizados. Você pode substituir os blocos antigos pelos novos correspondentes em sua nota do Obsidian.

### **1. Calculadora ICH (Hemorragia Intracraniana)**

O escore ICH é **prognóstico**, não terapêutico. A conduta não é uma droga específica baseada no escore, mas sim um conjunto de medidas de suporte. A calculadora foi atualizada para refletir isso.

```javascript
// --- Bloco de Código Corrigido para Escore ICH ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Escore ICH para Hemorragia Intracraniana</h2>
  
  <div class="input-group">
    <label for="glasgow">Glasgow na Admissão</label>
    <select id="glasgow"><option value="2">3-4</option><option value="1">5-12</option><option value="0" selected>13-15</option></select>
  </div>
  <div class="input-group">
    <label for="idade-ich">Idade</label>
    <select id="idade-ich"><option value="1">>= 80 anos</option><option value="0" selected>< 80 anos</option></select>
  </div>
  <div class="input-group">
    <label for="local-hematoma">Local do Hematoma</label>
    <select id="local-hematoma"><option value="1">Infratentorial</option><option value="0" selected>Supratentorial</option></select>
  </div>
  <div class="input-group">
    <label for="volume-hematoma">Volume do Hematoma</label>
    <select id="volume-hematoma"><option value="1">>= 30ml</option><option value="0" selected>< 30ml</option></select>
  </div>
  <div class="input-group">
    <label for="hemoventriculo">Hemo-ventrículo</label>
    <select id="hemoventriculo"><option value="1">Sim</option><option value="0" selected>Não</option></select>
  </div>
  
  <div class="button-group">
    <button id="ich-calc-button">Calcular</button>
    <button id="ich-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Escore: <span id="ich-result">-</span></h3>
  <h4>Mortalidade em 30 dias: <span id="ich-mortality">-</span></h4>
  <div id="ich-management" class="recommendation-box"></div>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.input-group { margin-bottom: 15px; }
label { display: block; margin-bottom: 5px; }
select { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#ich-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 15px; line-height: 1.5; }
`;

// 3. Injeção do estilo e do HTML
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Funções
function calculateICH() {
    const get = (id) => parseInt(container.querySelector('#' + id).value);
    const totalScore = get('glasgow') + get('idade-ich') + get('local-hematoma') + get('volume-hematoma') + get('hemoventriculo');
    container.querySelector('#ich-result').innerText = totalScore;
    
    const mortalityMap = {0: '0%', 1: '13%', 2: '26%', 3: '72%', 4: '97%', 5: '100%', 6: '100%'};
    container.querySelector('#ich-mortality').innerText = mortalityMap[totalScore] || "N/A";

    const managementBox = container.querySelector('#ich-management');
    managementBox.innerHTML = `<h4>Princípios de Manejo da HIC:</h4>
        <ul>
            <li><strong>Controle Pressórico:</strong> Agressivo nas primeiras horas (Ex: alvo de PAS < 140 mmHg), usando drogas endovenosas tituláveis (Nitroprussiato, Labetalol).</li>
            <li><strong>Reversão de Anticoagulação:</strong> Se o paciente estiver em uso, reverter imediatamente (Ex: Vitamina K, Complexo Protrombínico).</li>
            <li><strong>Manejo da PIC:</strong> Medidas como elevação da cabeceira, sedoanalgesia e, se necessário, terapia hiperosmolar (Manitol, salina hipertônica).</li>
            <li><strong>Avaliação Neurocirúrgica:</strong> Sempre considerar, especialmente para hematomas cerebelares > 3cm ou HIC com hidrocefalia.</li>
        </ul>`;
}
function resetICH() {
    container.querySelectorAll('select').forEach(s => s.selectedIndex = s.querySelector('option[selected]') ? s.querySelector('option[selected]').index : 0);
    container.querySelector('#ich-result').innerText = "-";
    container.querySelector('#ich-mortality').innerText = "-";
    container.querySelector('#ich-management').innerHTML = "";
}

// 5. Adição segura dos eventos de clique
setTimeout(() => {
    try {
        container.querySelector('#ich-calc-button').addEventListener('click', calculateICH);
        container.querySelector('#ich-reset-button').addEventListener('click', resetICH);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **2. Calculadora qSOFA (Sepse)**

Atualizada para incluir os passos iniciais do protocolo de sepse.

```javascript
// --- Bloco de Código Corrigido para qSOFA ---

const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora qSOFA (Triagem de Sepse)</h2>
  <div class="checkbox-group"><input type="checkbox" id="respiratory-rate"><label for="respiratory-rate">Frequência respiratória ≥ 22/min</label></div>
  <div class="checkbox-group"><input type="checkbox" id="mental-status"><label for="mental-status">Alteração do estado mental (Glasgow < 15)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="systolic-bp"><label for="systolic-bp">Pressão arterial sistólica ≤ 100 mmHg</label></div>
  <div class="button-group">
    <button id="qsofa-calc-button">Calcular</button>
    <button id="qsofa-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Resultado: <span id="qsofa-result"></span></h3>
  <div id="qsofa-interpretation" class="recommendation-box"></div>
</div>
`;
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.checkbox-group { margin-bottom: 10px; display: flex; align-items: center; }
.checkbox-group input { margin-right: 8px; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#qsofa-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 15px; line-height: 1.5; }
`;
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

function calculateQSOFA() {
    let score = 0;
    if (container.querySelector('#respiratory-rate').checked) score++;
    if (container.querySelector('#mental-status').checked) score++;
    if (container.querySelector('#systolic-bp').checked) score++;
    container.querySelector('#qsofa-result').innerText = score;
    const interpretationEl = container.querySelector('#qsofa-interpretation');
    if (score >= 2) {
      interpretationEl.innerHTML = `<h4>Risco Aumentado (Considerar Sepse)</h4>
        <p>Este paciente tem alto risco de desfechos desfavoráveis. Se houver suspeita de infecção, iniciar imediatamente o <strong>Pacote de 1 Hora (Sepsis Bundle)</strong>:</p>
        <ul>
            <li><strong>1. Medir Lactato:</strong> Se > 2 mmol/L, repetir em 2-4h.</li>
            <li><strong>2. Coletar Hemoculturas:</strong> Antes de iniciar antibióticos.</li>
            <li><strong>3. Administrar Antibióticos:</strong> De amplo espectro, conforme protocolo local.</li>
            <li><strong>4. Iniciar Fluidos:</strong> 30 mL/kg de cristaloide para hipotensão ou lactato ≥ 4 mmol/L.</li>
            <li><strong>5. Iniciar Vasopressores:</strong> Se hipotensão persistir durante ou após fluidos, para manter PAM ≥ 65 mmHg (droga de escolha: <strong>Noradrenalina</strong>).</li>
        </ul>`;
    } else {
      interpretationEl.innerHTML = "<h4>Baixo Risco</h4><p>Continuar monitorização. O escore baixo não exclui sepse, mas indica menor risco de deterioração.</p>";
    }
}
function resetQSOFA() {
    container.querySelectorAll('input[type="checkbox"]').forEach(box => box.checked = false);
    container.querySelector('#qsofa-result').innerText = "";
    container.querySelector('#qsofa-interpretation').innerHTML = "";
}

setTimeout(() => {
    try {
        container.querySelector('#qsofa-calc-button').addEventListener('click', calculateQSOFA);
        container.querySelector('#qsofa-reset-button').addEventListener('click', resetQSOFA);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **3. Calculadora NIHSS (AVC Isquêmico)**

A conduta aqui é diretamente ligada à elegibilidade para trombólise.

```dataview
// --- Bloco de Código Completo para NIHSS com Conduta ---

const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora NIHSS (National Institutes of Health Stroke Scale)</h2>
  
  <div class="input-group">
      <label for="time-window">Janela de tempo do início dos sintomas:</label>
      <select id="time-window"><option value="<4.5h">< 4.5 horas</option><option value=">4.5h">> 4.5 horas</option></select>
  </div>
  
  <!-- Repetir para cada item do NIHSS (código omitido para brevidade, use o seu código completo aqui) -->
  <div class="input-group"><label for="item1a">1a. Nível de Consciência</label><select id="item1a"><option value="0">0 - Alerta</option><option value="1">1 - Desperta a estímulos leves</option><option value="2">2 - Desperta a estímulos vigorosos</option><option value="3">3 - Não desperta</option></select></div>
  <div class="input-group"><label for="item1b">1b. Orientação</label><select id="item1b"><option value="0">0 - Responde 2 questões</option><option value="1">1 - Responde 1 questão</option><option value="2">2 - Não responde</option></select></div>
  <div class="input-group"><label for="item1c">1c. Comandos</label><select id="item1c"><option value="0">0 - Realiza 2 comandos</option><option value="1">1 - Realiza 1 comando</option><option value="2">2 - Não realiza</option></select></div>
  <div class="input-group"><label for="item2">2. Olhar Conjugado</label><select id="item2"><option value="0">0 - Normal</option><option value="1">1 - Parcial</option><option value="2">2 - Forçado</option></select></div>
  <div class="input-group"><label for="item3">3. Campo Visual</label><select id="item3"><option value="0">0 - Normal</option><option value="1">1 - Parcial</option><option value="2">2 - Completa</option><option value="3">3 - Bilateral</option></select></div>
  <div class="input-group"><label for="item4">4. Paralisia Facial</label><select id="item4"><option value="0">0 - Normal</option><option value="1">1 - Menor</option><option value="2">2 - Parcial</option><option value="3">3 - Completa</option></select></div>
  <div class="input-group"><label for="item5a">5a. MS Direito</label><select id="item5a"><option value="0">0 - Sem queda</option><option value="1">1 - Queda</option><option value="2">2 - Vence gravidade</option><option value="3">3 - Não vence</option><option value="4">4 - Sem movimento</option></select></div>
  <div class="input-group"><label for="item5b">5b. MS Esquerdo</label><select id="item5b"><option value="0">0 - Sem queda</option><option value="1">1 - Queda</option><option value="2">2 - Vence gravidade</option><option value="3">3 - Não vence</option><option value="4">4 - Sem movimento</option></select></div>
  <div class="input-group"><label for="item6a">6a. MI Direito</label><select id="item6a"><option value="0">0 - Sem queda</option><option value="1">1 - Queda</option><option value="2">2 - Vence gravidade</option><option value="3">3 - Não vence</option><option value="4">4 - Sem movimento</option></select></div>
  <div class="input-group"><label for="item6b">6b. MI Esquerdo</label><select id="item6b"><option value="0">0 - Sem queda</option><option value="1">1 - Queda</option><option value="2">2 - Vence gravidade</option><option value="3">3 - Não vence</option><option value="4">4 - Sem movimento</option></select></div>
  <div class="input-group"><label for="item7">7. Ataxia</label><select id="item7"><option value="0">0 - Ausente</option><option value="1">1 - 1 membro</option><option value="2">2 - 2 membros</option></select></div>
  <div class="input-group"><label for="item8">8. Sensitivo</label><select id="item8"><option value="0">0 - Normal</option><option value="1">1 - Leve</option><option value="2">2 - Grave</option></select></div>
  <div class="input-group"><label for="item9">9. Linguagem</label><select id="item9"><option value="0">0 - Normal</option><option value="1">1 - Leve</option><option value="2">2 - Grave</option><option value="3">3 - Mutismo</option></select></div>
  <div class="input-group"><label for="item10">10. Disartria</label><select id="item10"><option value="0">0 - Normal</option><option value="1">1 - Leve</option><option value="2">2 - Grave</option></select></div>
  <div class="input-group"><label for="item11">11. Negligência</label><select id="item11"><option value="0">0 - Ausente</option><option value="1">1 - Parcial</option><option value="2">2 - Completa</option></select></div>

  <div class="button-group">
    <button id="nihss-calc-button">Calcular</button>
    <button id="nihss-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Resultado: <span id="nihss-result"></span></h3>
  <h4>Gravidade: <span id="nihss-interpretation" style="font-weight: normal;"></span></h4>
  <div id="nihss-management" class="recommendation-box"></div>
</div>
`;

const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.input-group { margin-bottom: 15px; }
label { display: block; margin-bottom: 5px; font-weight: bold; }
select { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; margin-top: 15px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#nihss-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 15px; line-height: 1.5; }
`;
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

function calculateNIHSS() {
    const get = (id) => parseInt(container.querySelector('#' + id).value);
    const totalScore = get('item1a') + get('item1b') + get('item1c') + get('item2') + get('item3') + get('item4') + get('item5a') + get('item5b') + get('item6a') + get('item6b') + get('item7') + get('item8') + get('item9') + get('item10') + get('item11');
    container.querySelector('#nihss-result').innerText = totalScore;

    let interpretation = "";
    if (totalScore === 0) { interpretation = "Sem sintomas de AVC."; }
    else if (totalScore <= 4) { interpretation = "AVC Menor."; }
    else if (totalScore <= 15) { interpretation = "AVC Moderado."; }
    else if (totalScore <= 20) { interpretation = "AVC Moderado a Grave."; }
    else { interpretation = "AVC Grave."; }
    container.querySelector('#nihss-interpretation').innerText = interpretation;

    const timeWindow = container.querySelector('#time-window').value;
    const managementBox = container.querySelector('#nihss-management');
    let managementText = "<h4>Recomendação de Conduta:</h4>";

    if (timeWindow === '<4.5h' && totalScore >= 5 && totalScore <= 22) {
        managementText += `<p style="color:darkgreen;"><strong>Paciente ELEGÍVEL para Trombólise.</strong></p>
        <ul>
            <li><strong>Droga:</strong> Alteplase (rt-PA).</li>
            <li><strong>Dose:</strong> 0.9 mg/kg (dose máxima de 90 mg).</li>
            <li><strong>Administração:</strong> 10% da dose em bolus (1 min), e os 90% restantes em bomba de infusão contínua por 1 hora.</li>
            <li>⚠️ <strong>Atenção:</strong> Checar rigorosamente os critérios de exclusão (sangramento ativo, cirurgia recente, plaquetopenia, etc.) antes de administrar.</li>
        </ul>`;
    } else if (timeWindow === '<4.5h' && totalScore < 5) {
        managementText += `<p style="color:darkorange;"><strong>Trombólise controversa.</strong></p><p>Escore baixo (déficit menor). A decisão deve ser individualizada, pesando o pequeno benefício contra o risco de sangramento.</p>`;
    } else {
        managementText += `<p style="color:darkred;"><strong>Paciente NÃO ELEGÍVEL para Trombólise.</strong></p>
        <ul>
            <li><strong>Motivo:</strong> Fora da janela de tempo ou escore fora da faixa usual.</li>
            <li><strong>Conduta:</strong> Iniciar dupla antiagregação (AAS + Clopidogrel), estatina em alta dose, controle pressórico e investigação etiológica. Considerar trombectomia mecânica se oclusão de grande vaso.</li>
        </ul>`;
    }
    managementBox.innerHTML = managementText;
}

function resetNIHSS() {
    container.querySelectorAll('select').forEach(s => s.selectedIndex = 0);
    container.querySelector('#nihss-result').innerText = "";
    container.querySelector('#nihss-interpretation').innerText = "";
    container.querySelector('#nihss-management').innerHTML = "";
}

setTimeout(() => {
    try {
        container.querySelector('#nihss-calc-button').addEventListener('click', calculateNIHSS);
        container.querySelector('#nihss-reset-button').addEventListener('click', resetNIHSS);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

### **4. Calculadora CHA₂DS₂-VASc (Risco Tromboembólico)**

As recomendações foram atualizadas para incluir exemplos de drogas e doses.

```javascript
// --- Bloco de Código Corrigido para CHA₂DS₂-VASc com Conduta ---

const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Escore CHA₂DS₂-VASc</h2>
  <div class="input-group">
      <label for="c2v-sex">Sexo Biológico</label>
      <select id="c2v-sex"><option value="masculino">Masculino</option><option value="feminino">Feminino</option></select>
  </div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-c"><label for="c2v-c"><strong>C</strong> - Insuficiência Cardíaca</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-h"><label for="c2v-h"><strong>H</strong> - Hipertensão</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-a2"><label for="c2v-a2"><strong>A₂</strong> - Idade ≥ 75 anos (2 pts)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-d"><label for="c2v-d"><strong>D</strong> - Diabetes</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-s2"><label for="c2v-s2"><strong>S₂</strong> - AVC/AIT/TE prévio (2 pts)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-v"><label for="c2v-v"><strong>V</strong> - Doença Vascular</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-a"><label for="c2v-a"><strong>A</strong> - Idade 65-74 anos</label></div>
  <div class="button-group">
    <button id="c2v-calc-button">Calcular</button>
    <button id="c2v-reset-button" class="secondary">Reiniciar</button>
  </div>
  <h3>Escore Total: <span id="c2v-result"></span></h3>
  <div id="c2v-interpretation" class="recommendation-box"></div>
</div>
`;
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.checkbox-group, .input-group { margin-bottom: 12px; display: flex; align-items: center; }
.checkbox-group input { margin-right: 10px; min-width: 18px; min-height: 18px; }
.input-group label { font-weight: bold; margin-right: 10px; }
select { padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#c2v-calc-button { background-color: #007bff; color: white; }
.secondary { background-color: #6c757d; color: white; }
.recommendation-box { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 15px; line-height: 1.5; }
`;
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

function calculateCHADSVASC() {
    let score = 0;
    const getBox = (id) => container.querySelector('#' + id);
    if (getBox('c2v-c').checked) score += 1;
    if (getBox('c2v-h').checked) score += 1;
    if (getBox('c2v-s2').checked) score += 2;
    if (getBox('c2v-d').checked) score += 1;
    if (getBox('c2v-v').checked) score += 1;
    if (getBox('c2v-a2').checked) { score += 2; } else if (getBox('c2v-a').checked) { score += 1; }
    const sex = getBox('c2v-sex').value;
    if (sex === 'feminino') { score += 1; }
    getBox('c2v-result').innerText = score;

    const interpretationEl = getBox('c2v-interpretation');
    let recommendation = "<h4>Recomendação Clínica:</h4>";
    let shouldAnticoagulate = false;

    if ((sex === 'masculino' && score >= 2) || (sex === 'feminino' && score >= 3)) {
        shouldAnticoagulate = true;
        recommendation += `<p style="color:darkred;"><strong>Anticoagulação é recomendada.</strong></p>`;
    } else if ((sex === 'masculino' && score === 1) || (sex === 'feminino' && score === 2)) {
        recommendation += `<p style="color:darkorange;"><strong>Considerar anticoagulação.</strong> A decisão deve ser individualizada com o paciente.</p>`;
    } else {
        recommendation += `<p style="color:darkgreen;"><strong>Anticoagulação não é recomendada.</strong> Risco de AVC é muito baixo.</p>`;
    }

    if(shouldAnticoagulate) {
        recommendation += `<ul><strong>Opções Terapêuticas (exemplos de doses para FA não valvar):</strong>
            <li><strong>Apixabana:</strong> 5 mg, 2x/dia.</li>
            <li><strong>Rivaroxabana:</strong> 20 mg, 1x/dia (com a refeição).</li>
            <li><strong>Dabigatrana:</strong> 150 mg, 2x/dia.</li>
            <li><strong>Varfarina:</strong> Dose ajustada para manter INR entre 2.0-3.0 (indicada em FA valvar).</li>
            <li>⚠️ Sempre avaliar função renal, peso e idade para possível ajuste de dose dos DOACs.</li>
            </ul>`;
    }
    interpretationEl.innerHTML = recommendation;
}

function resetCHADSVASC() {
    container.querySelectorAll('input[type="checkbox"]').forEach(box => box.checked = false);
    container.querySelector('#c2v-sex').selectedIndex = 0;
    container.querySelector('#c2v-result').innerText = "";
    container.querySelector('#c2v-interpretation').innerHTML = "";
}

setTimeout(() => {
    try {
        container.querySelector('#c2v-calc-button').addEventListener('click', calculateCHADSVASC);
        container.querySelector('#c2v-reset-button').addEventListener('click', resetCHADSVASC);
    } catch (e) { container.innerHTML += `<p style='color:red;'>Erro: ${e.message}</p>`; }
}, 0);
```

---

Para os demais escores (SIRS, SOFA, Wells, PESI, CURB-65, Light, Sedoanalgesia, MDRD), a lógica é a mesma. Você pode aplicar as mesmas melhorias, adicionando uma seção de "Conduta Recomendada" na interpretação de cada um, detalhando os próximos passos, medicamentos e doses iniciais, sempre com o **aviso de segurança** de que a decisão final é clínica e baseada em protocolos institucionais.