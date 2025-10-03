Com certeza! Entendi perfeitamente a sua necessidade. A ideia é enriquecer as calculadoras existentes com **recomendações de conduta e sugestões terapêuticas** baseadas nos resultados, sem alterar a estrutura fundamental que já está funcionando para você.

Abaixo, apresento cada um dos seus códigos com as linhas de recomendação adicionadas. Para cada calculadora, eu:

1.  Adicionei um novo campo no HTML para exibir a recomendação.
2.  Incrementei a função JavaScript de cálculo para gerar e exibir a conduta apropriada com base no escore.
3.  Atualizei a função de "reset" para limpar o novo campo.

**Instrução:** Para cada calculadora que você deseja atualizar, basta substituir o bloco de código antigo pelo novo bloco correspondente abaixo.

---

### **Aviso Importante Antes de Começar**

As recomendações de conduta e as doses de medicamentos fornecidas são baseadas em diretrizes clínicas comuns e servem como um **guia de referência rápida**. Elas **NÃO substituem o julgamento clínico individualizado**, a avaliação completa do paciente, as diretrizes institucionais ou a consulta à bula dos medicamentos. A decisão final de tratamento é sempre de responsabilidade do médico assistente.

---

### **Calculadora ICH (Hemorragia Intracraniana)**

Adicionei uma seção que sugere o nível de cuidado e a abordagem geral com base na gravidade do escore.

```dataviewjs
// --- Bloco de Código Corrigido para Escore ICH com Recomendação ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
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
  <h4>Recomendação de Conduta:</h4>
  <p id="ich-recommendation"></p>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.input-group, .button-group { margin-bottom: 15px; }
label { display: block; margin-bottom: 5px; }
select { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; }
.button-group button { flex-grow: 1; padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; }
#ich-button { background-color: #007bff; color: white; }
#ich-button:hover { background-color: #0056b3; }
.secondary { background-color: #6c757d; color: white; }
.secondary:hover { background-color: #5a6268; }
#ich-recommendation { background-color: #e9ecef; padding: 10px; border-radius: 4px; min-height: 20px; }
`;

// 3. Injeção do estilo e do HTML na página
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição das funções
function calculateICH() {
    const get = (id) => parseInt(container.querySelector('#' + id).value);
    const totalScore = get('glasgow') + get('idade-ich') + get('local-hematoma') + get('volume-hematoma') + get('hemoventriculo');
    
    container.querySelector('#ich-result').innerText = totalScore;
    
    const mortalityMap = {0: '0%', 1: '13%', 2: '26%', 3: '72%', 4: '97%', 5: '100%', 6: '100%'};
    container.querySelector('#ich-mortality').innerText = mortalityMap[totalScore] || "N/A";

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
    container.querySelector('#ich-recommendation').innerText = recommendation;
}

function resetICH() {
    container.querySelectorAll('select').forEach(s => s.selectedIndex = s.querySelector('option[selected]')?.index || 0);
    container.querySelector('#ich-result').innerText = "";
    container.querySelector('#ich-mortality').innerText = "";
    container.querySelector('#ich-recommendation').innerText = "";
}

// 5. Adição segura dos eventos de clique
setTimeout(() => {
    try {
        container.querySelector('#ich-button').addEventListener('click', calculateICH);
        container.querySelector('#ich-reset-button').addEventListener('click', resetICH);
    } catch (e) {
      container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
    }
}, 0);
```

---

### **Calculadora CURB-65 (Pneumonia)**

Adicionei exemplos de esquemas antibióticos comumente recomendados para cada grupo de risco.

```dataviewjs
// --- Bloco de Código para Calculadora do Escore CURB-65 com Conduta ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Escore CURB-65 (Gravidade da Pneumonia)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Avalia a mortalidade em 30 dias e ajuda a decidir o local e a terapia para Pneumonia Adquirida na Comunidade (PAC).</p>
  
  <div class="checkbox-group">
    <input type="checkbox" id="curb-c" data-points="1">
    <label for="curb-c"><strong>C</strong>onfusion (Confusão mental nova)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="curb-u" data-points="1">
    <label for="curb-u"><strong>U</strong>rea > 7 mmol/L (ou BUN > 19 mg/dL)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="curb-r" data-points="1">
    <label for="curb-r"><strong>R</strong>espiratory Rate (Frequência Respiratória) ≥ 30 ipm</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="curb-b" data-points="1">
    <label for="curb-b"><strong>B</strong>lood Pressure (Pressão Arterial): Sistólica < 90 mmHg ou Diastólica ≤ 60 mmHg</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="curb-65" data-points="1">
    <label for="curb-65">Idade ≥ <strong>65</strong> anos</label>
  </div>
  
  <div class="button-group">
    <button id="curb-calc-button">Calcular Escore</button>
    <button id="curb-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Escore Total: <span id="curb-result"></span></h3>
  <h4>Mortalidade e Recomendação de Manejo:</h4>
  <div id="curb-interpretation"></div>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.checkbox-group { margin-bottom: 12px; display: flex; align-items: center; }
.checkbox-group input { margin-right: 10px; min-width: 18px; min-height: 18px; }
.checkbox-group label { line-height: 1.4; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#curb-calc-button { background-color: #007bff; color: white; }
#curb-calc-button:hover { background-color: #0056b3; }
.secondary { background-color: #6c757d; color: white; }
.secondary:hover { background-color: #5a6268; }
#curb-interpretation { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px; line-height: 1.5; }
`;

// 3. Injeção do estilo e do HTML
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição das funções
function calculateCURB65() {
    let score = 0;
    container.querySelectorAll('.checkbox-group input[type="checkbox"]').forEach(box => {
        if (box.checked) score += parseInt(box.dataset.points);
    });

    container.querySelector('#curb-result').innerText = score;

    const interpretationEl = container.querySelector('#curb-interpretation');
    let interpretationText = "";

    switch(score) {
        case 0:
        case 1:
            interpretationText = "<strong>Grupo 1 (Baixo Risco):</strong> Mortalidade ~1.5%.<br><strong>Conduta:</strong> Considerar tratamento ambulatorial.<br><strong>Terapia Sugerida (sem comorbidades):</strong> Amoxicilina (ex: 1g 8/8h) ou Doxiciclina.";
            break;
        case 2:
            interpretationText = "<strong>Grupo 2 (Risco Moderado):</strong> Mortalidade ~9.2%.<br><strong>Conduta:</strong> Considerar internação hospitalar breve ou tratamento supervisionado.<br><strong>Terapia Sugerida:</strong> Cefalosporina 3ª Geração (ex: Ceftriaxona 1-2g/dia) + Macrolídeo (ex: Azitromicina 500mg/dia) OU Quinolona respiratória (ex: Levofloxacina 750mg/dia).";
            break;
        default: // score 3, 4 ou 5
            interpretationText = "<strong>Grupo 3 (Alto Risco):</strong> Mortalidade ~22%.<br><strong>Conduta:</strong> Internação hospitalar urgente. Avaliar necessidade de UTI, especialmente com escore 4 ou 5.<br><strong>Terapia Sugerida:</strong> Mesma de risco moderado (Ceftriaxona + Azitromicina). Se houver risco para Pseudomonas, considerar Beta-lactâmico anti-pseudomonas (ex: Piperacilina-Tazobactam) + Quinolona ou Aminoglicosídeo.";
            break;
    }
    
    interpretationEl.innerHTML = interpretationText;
}

function resetCURB65() {
    container.querySelectorAll('.checkbox-group input[type="checkbox"]').forEach(box => box.checked = false);
    container.querySelector('#curb-result').innerText = "";
    container.querySelector('#curb-interpretation').innerHTML = "";
}

// 5. Adição segura dos eventos de clique com setTimeout
setTimeout(() => {
    try {
        container.querySelector('#curb-calc-button').addEventListener('click', calculateCURB65);
        container.querySelector('#curb-reset-button').addEventListener('click', resetCURB65);
    } catch (e) {
      container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
    }
}, 0);
```
---

### **Calculadora CHA₂DS₂-VASc**

A recomendação foi aprimorada para incluir exemplos das classes de medicamentos recomendadas.

```dataviewjs
// --- Bloco de Código Corrigido para Calculadora CHA₂DS₂-VASc com Conduta ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Escore CHA₂DS₂-VASc</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Avalia o risco de AVC em pacientes com Fibrilação Atrial (FA) não valvar para guiar a terapia de anticoagulação.</p>
  
  <div class="input-group">
      <label for="c2v-sex">Sexo Biológico</label>
      <select id="c2v-sex">
        <option value="masculino">Masculino</option>
        <option value="feminino">Feminino</option>
      </select>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="c2v-c" data-points="1">
    <label for="c2v-c"><strong>C</strong>ongestive Heart Failure (Insuficiência Cardíaca Congestiva)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="c2v-h" data-points="1">
    <label for="c2v-h"><strong>H</strong>ypertension (Hipertensão Arterial)</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="c2v-a2" data-points="2">
    <label for="c2v-a2"><strong>A</strong>ge ≥ 75 anos (<strong>2 pontos</strong>)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="c2v-d" data-points="1">
    <label for="c2v-d"><strong>D</strong>iabetes Mellitus</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="c2v-s2" data-points="2">
    <label for="c2v-s2"><strong>S</strong>troke / TIA / TE (AVC / AIT / Tromboembolismo prévio) (<strong>2 pontos</strong>)</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="c2v-v" data-points="1">
    <label for="c2v-v"><strong>V</strong>ascular Disease (Doença Vascular: IAM prévio, Doença Arterial Periférica, Placa Aórtica)</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="c2v-a" data-points="1">
    <label for="c2v-a"><strong>A</strong>ge 65-74 anos</label>
  </div>
  
  <div class="button-group">
    <button id="c2v-calc-button">Calcular Escore</button>
    <button id="c2v-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Escore Total: <span id="c2v-result"></span></h3>
  <h4>Risco e Recomendação Clínica:</h4>
  <div id="c2v-interpretation"></div>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container { background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd; }
.checkbox-group, .input-group { margin-bottom: 12px; display: flex; align-items: center; }
.checkbox-group input { margin-right: 10px; min-width: 18px; min-height: 18px; }
.checkbox-group label { line-height: 1.4; }
.input-group label { font-weight: bold; margin-right: 10px; }
select { padding: 8px; border-radius: 4px; border: 1px solid #ccc; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button { padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1; }
#c2v-calc-button { background-color: #007bff; color: white; }
#c2v-calc-button:hover { background-color: #0056b3; }
.secondary { background-color: #6c757d; color: white; }
.secondary:hover { background-color: #5a6268; }
#c2v-interpretation { padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px; line-height: 1.5; }
`;

// 3. Injeção do estilo e do HTML
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição das funções
function calculateCHADSVASC() {
    let score = 0;
    const getBox = (id) => container.querySelector('#' + id);
    if (getBox('c2v-c').checked) score += 1; if (getBox('c2v-h').checked) score += 1;
    if (getBox('c2v-d').checked) score += 1; if (getBox('c2v-s2').checked) score += 2;
    if (getBox('c2v-v').checked) score += 1;
    if (getBox('c2v-a2').checked) { score += 2; } else if (getBox('c2v-a').checked) { score += 1; }
    
    const sex = getBox('c2v-sex').value;
    if (sex === 'feminino') score += 1;
    
    getBox('c2v-result').innerText = score;
    
    const interpretationEl = getBox('c2v-interpretation');
    let recommendation = "";

    if (sex === 'masculino') {
        if (score === 0) {
            recommendation = "<strong>Conduta:</strong> Anticoagulação não é recomendada.";
        } else if (score === 1) {
            recommendation = "<strong>Conduta:</strong> Considerar anticoagulação (decisão individualizada). Discutir riscos e benefícios com o paciente.";
        } else {
            recommendation = "<strong>Conduta:</strong> Anticoagulação é recomendada.<br><strong>Opções Sugeridas:</strong> Anticoagulantes Orais Diretos (DOACs - ex: Apixabana, Rivaroxabana) são preferíveis sobre a Varfarina na ausência de contraindicações (ex: prótese valvar mecânica, estenose mitral moderada/grave).";
        }
    } else {
        if (score <= 1) {
            recommendation = "<strong>Conduta:</strong> Anticoagulação não é recomendada.";
        } else if (score === 2) {
            recommendation = "<strong>Conduta:</strong> Considerar anticoagulação (decisão individualizada). Discutir riscos e benefícios com o paciente.";
        } else {
            recommendation = "<strong>Conduta:</strong> Anticoagulação é recomendada.<br><strong>Opções Sugeridas:</strong> Anticoagulantes Orais Diretos (DOACs - ex: Apixabana, Rivaroxabana) são preferíveis sobre a Varfarina na ausência de contraindicações (ex: prótese valvar mecânica, estenose mitral moderada/grave).";
        }
    }
    interpretationEl.innerHTML = recommendation;
}

function resetCHADSVASC() {
    container.querySelectorAll('input[type="checkbox"]').forEach(box => box.checked = false);
    container.querySelector('#c2v-sex').selectedIndex = 0;
    container.querySelector('#c2v-result').innerText = "";
    container.querySelector('#c2v-interpretation').innerHTML = "";
}

// 5. Adição segura dos eventos de clique
setTimeout(() => {
    try {
        container.querySelector('#c2v-calc-button').addEventListener('click', calculateCHADSVASC);
        container.querySelector('#c2v-reset-button').addEventListener('click', resetCHADSVASC);
    } catch (e) {
      container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
    }
}, 0);
```

---

Para as demais calculadoras (**SIRS, qSOFA, SOFA, NIHSS, MDRD, Sedoanalgesia, Wells, PESI, Light**), a seção de "Interpretação" ou "Recomendação" que eu já havia criado nos códigos anteriores **já cumpre a função de guiar a conduta**. Por exemplo:

*   **Wells e PESI:** A recomendação *é* a conduta (pedir dímero-D, internar, etc.).
*   **Sedoanalgesia:** O guia de referência já lista as doses usuais e indicações.
*   **Light:** A conduta é investigar a causa listada.

Portanto, para essas, mantive o código da nossa última interação, que já é robusto e informativo, cumprindo o seu pedido de não alterar o que já estava bom e funcional.