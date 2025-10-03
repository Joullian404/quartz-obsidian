# Calculadora ICH, AVE

```dataviewjs
// --- Bloco de Código Corrigido para Escore ICH ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Escore ICH para Hemorragia Intracraniana</h2>
  
  <div class="input-group">
    <label for="glasgow">Glasgow na Admissão</label>
    <select id="glasgow">
      <option value="2">3-4</option>
      <option value="1">5-12</option>
      <option value="0">13-15</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="idade-ich">Idade</label>
    <select id="idade-ich">
      <option value="1">>= 80 anos</option>
      <option value="0">< 80 anos</option>
    </select>
  </div>

  <div class="input-group">
    <label for="local-hematoma">Local do Hematoma</label>
    <select id="local-hematoma">
      <option value="1">Infratentorial</option>
      <option value="0">Supratentorial</option>
    </select>
  </div>

  <div class="input-group">
    <label for="volume-hematoma">Volume do Hematoma</label>
    <select id="volume-hematoma">
      <option value="1">>= 30ml</option>
      <option value="0">< 30ml</option>
    </select>
  </div>

  <div class="input-group">
    <label for="hemoventriculo">Hemo-ventrículo</label>
    <select id="hemoventriculo">
      <option value="1">Sim</option>
      <option value="0">Não</option>
    </select>
  </div>
  
  <button id="ich-button">Calcular Escore ICH</button>
  
  <h3>Escore: <span id="ich-result"></span></h3>
  <h4>Mortalidade em 30 dias: <span id="ich-mortality"></span></h4>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.input-group {
  margin-bottom: 15px;
}
label {
  display: block;
  margin-bottom: 5px;
}
select {
  width: 100%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
}
button {
  background-color: #007bff;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
}
button:hover {
  background-color: #0056b3;
}
`;

// 3. Injeção do estilo e do HTML na página
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição da função de cálculo
function calculateICH() {
    const get = (id) => parseInt(container.querySelector('#' + id).value);
    
    const totalScore = get('glasgow') + get('idade-ich') + get('local-hematoma') + get('volume-hematoma') + get('hemoventriculo');
    
    container.querySelector('#ich-result').innerText = totalScore;
    
    const mortalityMap = {0: '0%', 1: '13%', 2: '26%', 3: '72%', 4: '97%', 5: '100%', 6: '100%'};
    container.querySelector('#ich-mortality').innerText = mortalityMap[totalScore] || "N/A";
}

// 5. Adição segura do evento de clique
try {
  const button = container.querySelector('#ich-button');
  if (button) {
    button.addEventListener('click', calculateICH);
  }
} catch (e) {
  container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
}
```

# Calculadora SIRS, Sepse
```dataviewjs
// --- Bloco de Código para Calculadora SIRS ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Critérios SIRS (Sepsis-2)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Lembre-se: O conceito de SIRS foi substituído pelo qSOFA/SOFA no Sepsis-3, mas ainda é útil em alguns contextos clínicos.</p>
  
  <div class="checkbox-group">
    <input type="checkbox" id="sirs-temp">
    <label for="sirs-temp">Temperatura > 38°C ou < 36°C</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="sirs-hr">
    <label for="sirs-hr">Frequência cardíaca > 90 bpm</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="sirs-rr">
    <label for="sirs-rr">Frequência respiratória > 20 ipm ou PaCO₂ < 32 mmHg</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="sirs-wbc">
    <label for="sirs-wbc">Leucócitos > 12.000, < 4.000 ou > 10% de bastões</label>
  </div>
  
  <div class="button-group">
    <button id="sirs-calc-button">Calcular SIRS</button>
    <button id="sirs-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Critérios presentes: <span id="sirs-result"></span></h3>
  <h4>Interpretação: <span id="sirs-interpretation" style="font-weight: normal;"></span></h4>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.checkbox-group {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
}
.checkbox-group input {
  margin-right: 10px;
  min-width: 18px; /* Garante tamanho do checkbox */
  min-height: 18px;
}
.checkbox-group label {
  line-height: 1.4;
}
.button-group {
  display: flex;
  gap: 10px;
  margin-top: 20px;
  flex-wrap: wrap;
}
.button-group button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  flex-grow: 1;
}
#sirs-calc-button {
  background-color: #007bff;
  color: white;
}
#sirs-calc-button:hover {
  background-color: #0056b3;
}
.button-group .secondary {
  background-color: #6c757d;
  color: white;
}
.button-group .secondary:hover {
  background-color: #5a6268;
}
`;

// 3. Injeção do estilo e do HTML
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição das funções
function calculateSIRS() {
    let score = 0;
    if (container.querySelector('#sirs-temp').checked) score++;
    if (container.querySelector('#sirs-hr').checked) score++;
    if (container.querySelector('#sirs-rr').checked) score++;
    if (container.querySelector('#sirs-wbc').checked) score++;
    
    container.querySelector('#sirs-result').innerText = `${score} de 4`;
    
    const interpretationEl = container.querySelector('#sirs-interpretation');
    if (score >= 2) {
      interpretationEl.innerText = "Critérios para SIRS presentes. Se houver suspeita de infecção, isso caracteriza Sepse (pela definição Sepsis-2).";
      interpretationEl.style.color = 'darkred';
    } else {
      interpretationEl.innerText = "Critérios para SIRS não preenchidos.";
      interpretationEl.style.color = 'black';
    }
}

function resetSIRS() {
    const allCheckboxes = container.querySelectorAll('.checkbox-group input[type="checkbox"]');
    allCheckboxes.forEach(checkbox => {
        checkbox.checked = false;
    });

    container.querySelector('#sirs-result').innerText = "";
    container.querySelector('#sirs-interpretation').innerText = "";
    container.querySelector('#sirs-interpretation').style.color = 'black';
}

// 5. Adição segura dos eventos de clique
try {
  const calcButton = container.querySelector('#sirs-calc-button');
  if (calcButton) {
    calcButton.addEventListener('click', calculateSIRS);
  }

  const resetButton = container.querySelector('#sirs-reset-button');
  if (resetButton) {
    resetButton.addEventListener('click', resetSIRS);
  }
} catch (e) {
  container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
}
```

# Calculadora Qsofa, Sepse
```dataviewjs
// --- Bloco de Código Corrigido para qSOFA ---

// 1. Primeiro, definimos a estrutura HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora qSOFA</h2>
  
  <div class="checkbox-group">
    <input type="checkbox" id="respiratory-rate">
    <label for="respiratory-rate">Frequência respiratória >= 22/min</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="mental-status">
    <label for="mental-status">Alteração do estado mental (Glasgow < 15)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="systolic-bp">
    <label for="systolic-bp">Pressão arterial sistólica <= 100 mmHg</label>
  </div>
  
  <button id="qsofa-button">Calcular qSOFA</button>
  
  <h3>Resultado: <span id="qsofa-result"></span></h3>
  <p id="qsofa-interpretation"></p>
</div>
`;

// 2. Separadamente, definimos o estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.checkbox-group {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
}
.checkbox-group input {
  margin-right: 8px;
}
button {
  background-color: #007bff;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
}
button:hover {
  background-color: #0056b3;
}
`;

// 3. Pegamos o container da nota e injetamos o estilo
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);

// 4. Agora, adicionamos o HTML da calculadora
// Usamos += para não apagar o estilo que acabamos de adicionar
container.innerHTML += calculatorHTML;

// 5. Definimos a função que faz o cálculo
function calculateQSOFA() {
    let score = 0;
    // Usamos 'container.querySelector' para garantir que estamos pegando os elementos certos
    if (container.querySelector('#respiratory-rate').checked) score++;
    if (container.querySelector('#mental-status').checked) score++;
    if (container.querySelector('#systolic-bp').checked) score++;
    
    container.querySelector('#qsofa-result').innerText = score;
    
    const interpretationEl = container.querySelector('#qsofa-interpretation');
    if (score >= 2) {
      interpretationEl.innerText = "Risco aumentado de desfechos desfavoráveis. Considerar sepse.";
    } else {
      interpretationEl.innerText = "Baixo risco.";
    }
}

// 6. Finalmente, adicionamos o evento de clique ao botão
// Este bloco 'try...catch' ajuda a previnir o 'Evaluation Error'
try {
  const button = container.querySelector('#qsofa-button');
  if (button) {
    button.addEventListener('click', calculateQSOFA);
  }
} catch (e) {
  // Se ainda der erro, esta linha vai mostrar uma mensagem na nota
  container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
}
```

# Calculadora SOFA, Sepse

```dataviewjs
// --- Bloco de Código Corrigido para SOFA com Mensagem de Risco ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora SOFA</h2>
  
  <div class="input-group">
    <label for="respiration">Respiratório (PaO2/FiO2, mmHg)</label>
    <select id="respiration">
      <option value="0">>= 400</option>
      <option value="1">< 400</option>
      <option value="2">< 300</option>
      <option value="3">< 200 com suporte respiratório</option>
      <option value="4">< 100 com suporte respiratório</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="coagulation">Coagulação (Plaquetas, x10³/µL)</label>
    <select id="coagulation">
      <option value="0">>= 150</option>
      <option value="1">< 150</option>
      <option value="2">< 100</option>
      <option value="3">< 50</option>
      <option value="4">< 20</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="liver">Fígado (Bilirrubina, mg/dL)</label>
    <select id="liver">
      <option value="0">< 1.2</option>
      <option value="1">1.2 - 1.9</option>
      <option value="2">2.0 - 5.9</option>
      <option value="3">6.0 - 11.9</option>
      <option value="4">>= 12.0</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="cardiovascular">Cardiovascular (Hipotensão)</label>
    <select id="cardiovascular">
      <option value="0">PAM >= 70 mmHg</option>
      <option value="1">PAM < 70 mmHg</option>
      <option value="2">Dopamina < 5 ou Dobutamina (qualquer dose)</option>
      <option value="3">Dopamina 5.1-15 ou Epinefrina <= 0.1 ou Norepinefrina <= 0.1</option>
      <option value="4">Dopamina > 15 ou Epinefrina > 0.1 ou Norepinefrina > 0.1</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="cns">Sistema Nervoso Central (Escala de Coma de Glasgow)</label>
    <select id="cns">
      <option value="0">15</option>
      <option value="1">13 - 14</option>
      <option value="2">10 - 12</option>
      <option value="3">6 - 9</option>
      <option value="4">< 6</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="renal">Renal (Creatinina, mg/dL ou débito urinário)</label>
    <select id="renal">
      <option value="0">< 1.2</option>
      <option value="1">1.2 - 1.9</option>
      <option value="2">2.0 - 3.4</option>
      <option value="3">3.5 - 4.9 ou < 500 mL/dia</option>
      <option value="4">> 5.0 ou < 200 mL/dia</option>
    </select>
  </div>
  
  <button id="sofa-button">Calcular SOFA</button>
  
  <h3>Resultado: <span id="sofa-result"></span></h3>
  <h4>Risco: <span id="sofa-interpretation" style="font-weight: normal;"></span></h4>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.input-group {
  margin-bottom: 15px;
}
label {
  display: block;
  margin-bottom: 5px;
}
select {
  width: 100%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
}
button {
  background-color: #007bff;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
}
button:hover {
  background-color: #0056b3;
}
`;

// 3. Injeção do estilo e do HTML na página
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição da função de cálculo
function calculateSOFA() {
    const get = (id) => parseInt(container.querySelector('#' + id).value);
    
    const totalScore = get('respiration') + get('coagulation') + get('liver') + get('cardiovascular') + get('cns') + get('renal');
    
    container.querySelector('#sofa-result').innerText = totalScore;

    // Adiciona a interpretação do risco
    const interpretationEl = container.querySelector('#sofa-interpretation');
    if (totalScore >= 2) {
        interpretationEl.innerText = "Risco aumentado de disfunção orgânica. Em paciente com infecção, um aumento ≥ 2 pontos indica sepse.";
    } else {
        interpretationEl.innerText = "Baixo risco de disfunção orgânica significativa.";
    }
}

// 5. Adição segura do evento de clique
try {
  const button = container.querySelector('#sofa-button');
  if (button) {
    button.addEventListener('click', calculateSOFA);
  }
} catch (e) {
  container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
}
```

# Calculadora NIHSS, AVC

```dataviewjs
// --- Bloco de Código Completo para NIHSS com Botão de Reiniciar ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora NIHSS (National Institutes of Health Stroke Scale)</h2>
  
  <div class="input-group">
    <label for="item1a">1a. Nível de Consciência</label>
    <select id="item1a">
      <option value="0">0 - Alerta</option>
      <option value="1">1 - Desperta a estímulos leves</option>
      <option value="2">2 - Desperta a estímulos vigorosos</option>
      <option value="3">3 - Não desperta</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item1b">1b. Orientação (Idade e Mês)</label>
    <select id="item1b">
      <option value="0">0 - Responde adequadamente as 2 questões</option>
      <option value="1">1 - Responde adequadamente 1 questão</option>
      <option value="2">2 - Não responde adequadamente</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="item1c">1c. Resposta a Comandos Simples</label>
    <select id="item1c">
      <option value="0">0 - Realiza adequadamente os 2 comandos</option>
      <option value="1">1 - Realiza adequadamente 1 comando</option>
      <option value="2">2 - Não realiza adequadamente</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item2">2. Olhar Conjugado Horizontal</label>
    <select id="item2">
      <option value="0">0 - Normal</option>
      <option value="1">1 - Desvio conjugado parcial do olhar</option>
      <option value="2">2 - Desvio conjugado forçado do olhar</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item3">3. Campo Visual</label>
    <select id="item3">
      <option value="0">0 - Normal</option>
      <option value="1">1 - Hemianopsia parcial</option>
      <option value="2">2 - Hemianopsia completa</option>
      <option value="3">3 - Hemianopsia bilateral (Cegueira)</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item4">4. Paralisia Facial</label>
    <select id="item4">
      <option value="0">0 - Normal</option>
      <option value="1">1 - Paresia menor</option>
      <option value="2">2 - Paresia parcial</option>
      <option value="3">3 - Paralisia completa</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item5a">5a. Motricidade de Membro Superior (Direito)</label>
    <select id="item5a">
      <option value="0">0 - Sem queda por 10s</option>
      <option value="1">1 - Queda em menos de 10s, não toca o leito</option>
      <option value="2">2 - Queda em menos de 10s, toca o leito</option>
      <option value="3">3 - Não vence gravidade</option>
      <option value="4">4 - Sem movimento</option>
      <option value="0">Não testável (amputação, etc.)</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item5b">5b. Motricidade de Membro Superior (Esquerdo)</label>
    <select id="item5b">
      <option value="0">0 - Sem queda por 10s</option>
      <option value="1">1 - Queda em menos de 10s, não toca o leito</option>
      <option value="2">2 - Queda em menos de 10s, toca o leito</option>
      <option value="3">3 - Não vence gravidade</option>
      <option value="4">4 - Sem movimento</option>
      <option value="0">Não testável (amputação, etc.)</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item6a">6a. Motricidade de Membro Inferior (Direito)</label>
    <select id="item6a">
      <option value="0">0 - Sem queda por 5s</option>
      <option value="1">1 - Queda em menos de 5s, não toca o leito</option>
      <option value="2">2 - Queda em menos de 5s, toca o leito</option>
      <option value="3">3 - Não vence gravidade</option>
      <option value="4">4 - Sem movimento</option>
      <option value="0">Não testável (amputação, etc.)</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item6b">6b. Motricidade de Membro Inferior (Esquerdo)</label>
    <select id="item6b">
      <option value="0">0 - Sem queda por 5s</option>
      <option value="1">1 - Queda em menos de 5s, não toca o leito</option>
      <option value="2">2 - Queda em menos de 5s, toca o leito</option>
      <option value="3">3 - Não vence gravidade</option>
      <option value="4">4 - Sem movimento</option>
      <option value="0">Não testável (amputação, etc.)</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item7">7. Ataxia de Membro</label>
    <select id="item7">
      <option value="0">0 - Ausente</option>
      <option value="1">1 - Presente em 1 membro</option>
      <option value="2">2 - Presente em 2 ou mais membros</option>
      <option value="0">Não testável (paralisia, amputação)</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item8">8. Sensitivo</label>
    <select id="item8">
      <option value="0">0 - Normal</option>
      <option value="1">1 - Hipoestesia leve a moderada</option>
      <option value="2">2 - Hipoestesia grave a anestesia</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item9">9. Linguagem (Afasia)</label>
    <select id="item9">
      <option value="0">0 - Normal</option>
      <option value="1">1 - Afasia leve a moderada</option>
      <option value="2">2 - Afasia grave</option>
      <option value="3">3 - Mutismo / Afasia global</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item10">10. Disartria</label>
    <select id="item10">
      <option value="0">0 - Normal</option>
      <option value="1">1 - Leve a moderada</option>
      <option value="2">2 - Grave (ininteligível)</option>
      <option value="0">Não testável (entubado)</option>
    </select>
  </div>

  <div class="input-group">
    <label for="item11">11. Extinção ou Heminegligência</label>
    <select id="item11">
      <option value="0">0 - Ausente</option>
      <option value="1">1 - Presente em 1 modalidade</option>
      <option value="2">2 - Presente em mais de 1 modalidade</option>
    </select>
  </div>
  
  <div class="button-group">
    <button id="nihss-button">Calcular NIHSS</button>
    <button id="nihss-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Resultado: <span id="nihss-result"></span></h3>
  <h4>Gravidade do AVC e Prognóstico: <span id="nihss-interpretation" style="font-weight: normal;"></span></h4>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.input-group {
  margin-bottom: 15px;
}
label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}
select {
  width: 100%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
}
.button-group {
  display: flex;
  gap: 10px;
  margin-top: 15px;
  flex-wrap: wrap;
}
.button-group button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  flex-grow: 1; /* Faz os botões ocuparem o espaço disponível */
}
#nihss-button {
  background-color: #007bff;
  color: white;
}
#nihss-button:hover {
  background-color: #0056b3;
}
.button-group .secondary {
  background-color: #6c757d;
  color: white;
}
.button-group .secondary:hover {
  background-color: #5a6268;
}
`;

// 3. Injeção do estilo e do HTML
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição das funções
function calculateNIHSS() {
    const get = (id) => parseInt(container.querySelector('#' + id).value);
    
    const totalScore = get('item1a') + get('item1b') + get('item1c') + get('item2') + get('item3') +
                       get('item4') + get('item5a') + get('item5b') + get('item6a') + get('item6b') +
                       get('item7') + get('item8') + get('item9') + get('item10') + get('item11');
    
    container.querySelector('#nihss-result').innerText = totalScore;

    const interpretationEl = container.querySelector('#nihss-interpretation');
    let interpretation = "";
    if (totalScore === 0) {
        interpretation = "Sem sintomas de AVC.";
    } else if (totalScore >= 1 && totalScore <= 4) {
        interpretation = "AVC Menor. Prognóstico geralmente excelente.";
    } else if (totalScore >= 5 && totalScore <= 15) {
        interpretation = "AVC Moderado. Necessária reabilitação.";
    } else if (totalScore >= 16 && totalScore <= 20) {
        interpretation = "AVC Moderado a Grave. Alta probabilidade de déficit significativo.";
    } else if (totalScore >= 21) {
        interpretation = "AVC Grave. Alta probabilidade de dependência ou morte.";
    }
    interpretationEl.innerText = interpretation;
}

function resetNIHSS() {
    // Reseta todos os menus para a primeira opção (valor 0)
    const allSelects = container.querySelectorAll('.input-group select');
    allSelects.forEach(select => {
        select.selectedIndex = 0;
    });

    // Limpa os campos de resultado e interpretação
    container.querySelector('#nihss-result').innerText = "";
    container.querySelector('#nihss-interpretation').innerText = "";
}

// 5. Adição segura dos eventos de clique
try {
  const calcButton = container.querySelector('#nihss-button');
  if (calcButton) {
    calcButton.addEventListener('click', calculateNIHSS);
  }

  const resetButton = container.querySelector('#nihss-reset-button');
  if (resetButton) {
    resetButton.addEventListener('click', resetNIHSS);
  }
} catch (e) {
  container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
}
```

# Calculadora MDRD, Função Renal
```dataviewjs
// --- Bloco de Código para Calculadora TFG (MDRD) ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de TFG Estimada (Fórmula MDRD)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">A fórmula MDRD é usada para estimar a Taxa de Filtração Glomerular e estadiar a Doença Renal Crônica (DRC). Nota: A fórmula CKD-EPI é mais moderna e precisa, especialmente para TFG > 60.</p>
  
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
    <select id="mdrd-sex">
      <option value="masculino">Masculino</option>
      <option value="feminino">Feminino</option>
    </select>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="mdrd-ethnicity">
    <label for="mdrd-ethnicity">Afro-americano</label>
  </div>

  <div class="button-group">
    <button id="mdrd-calc-button">Calcular TFG</button>
    <button id="mdrd-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Resultado (TFG estimada): <span id="mdrd-result"></span></h3>
  <h4>Estágio da Doença Renal Crônica (DRC): <span id="mdrd-stage" style="font-weight: normal;"></span></h4>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.input-group, .checkbox-group {
  margin-bottom: 15px;
}
label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="number"], select {
  width: 100%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}
.checkbox-group {
  display: flex;
  align-items: center;
}
.checkbox-group input {
  margin-right: 8px;
}
.button-group {
  display: flex;
  gap: 10px;
  margin-top: 20px;
  flex-wrap: wrap;
}
.button-group button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  flex-grow: 1;
}
#mdrd-calc-button {
  background-color: #007bff;
  color: white;
}
#mdrd-calc-button:hover {
  background-color: #0056b3;
}
.button-group .secondary {
  background-color: #6c757d;
  color: white;
}
.button-group .secondary:hover {
  background-color: #5a6268;
}
`;

// 3. Injeção do estilo e do HTML
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição das funções
function calculateMDRD() {
    const creat = parseFloat(container.querySelector('#mdrd-creat').value);
    const age = parseInt(container.querySelector('#mdrd-age').value);
    const sex = container.querySelector('#mdrd-sex').value;
    const isAfro = container.querySelector('#mdrd-ethnicity').checked;
    
    // Validação de entrada
    if (isNaN(creat) || isNaN(age) || creat <= 0 || age <= 0) {
        container.querySelector('#mdrd-result').innerText = "Por favor, insira valores válidos.";
        container.querySelector('#mdrd-stage').innerText = "";
        return;
    }

    // Fórmula MDRD: 175 × (Creatinina)^-1.154 × (Idade)^-0.203 × (0.742 se mulher) × (1.212 se afro-americano)
    let tfg = 175 * Math.pow(creat, -1.154) * Math.pow(age, -0.203);
    
    if (sex === 'feminino') {
        tfg *= 0.742;
    }
    
    if (isAfro) {
        tfg *= 1.212;
    }
    
    container.querySelector('#mdrd-result').innerText = `${tfg.toFixed(2)} mL/min/1.73 m²`;
    
    // Determinação do estágio da DRC
    const stageEl = container.querySelector('#mdrd-stage');
    let stageText = "";
    if (tfg >= 90) {
        stageText = "Estágio 1: Normal ou alta (Necessário avaliar outros sinais de lesão renal, como proteinúria).";
    } else if (tfg >= 60) {
        stageText = "Estágio 2: Levemente diminuída (Necessário avaliar outros sinais de lesão renal).";
    } else if (tfg >= 45) {
        stageText = "Estágio 3a: Leve a moderadamente diminuída.";
    } else if (tfg >= 30) {
        stageText = "Estágio 3b: Moderada a gravemente diminuída.";
    } else if (tfg >= 15) {
        stageText = "Estágio 4: Gravemente diminuída.";
    } else {
        stageText = "Estágio 5: Falência renal (TFG < 15).";
    }
    stageEl.innerText = stageText;
}

function resetMDRD() {
    container.querySelector('#mdrd-creat').value = '';
    container.querySelector('#mdrd-age').value = '';
    container.querySelector('#mdrd-sex').selectedIndex = 0;
    container.querySelector('#mdrd-ethnicity').checked = false;
    container.querySelector('#mdrd-result').innerText = "";
    container.querySelector('#mdrd-stage').innerText = "";
}

// 5. Adição segura dos eventos de clique
try {
  container.querySelector('#mdrd-calc-button').addEventListener('click', calculateMDRD);
  container.querySelector('#mdrd-reset-button').addEventListener('click', resetMDRD);
} catch (e) {
  container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
}
```

# Calculadora sedoanalgesia
```dataviewjs
// --- Bloco de Código para Calculadora de Sedoanalgesia e Guia Rápido ---

// --- PARTE 1: HTML E ESTILOS ---

const toolHTML = `
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

      <!-- Seção de Preparo -->
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

      <!-- Seção de Cálculo -->
      <h3 class="section-header">2. Cálculo da Infusão</h3>
      <div class="input-group" id="weight-group">
        <label for="patient-weight">Peso do paciente (kg):</label>
        <input type="number" id="patient-weight" placeholder="Ex: 70">
      </div>
      <div class="input-group">
        <label for="prescribed-dose">Dose prescrita (<span id="dose-unit-label">mcg/kg/min</span>):</label>
        <input type="number" id="prescribed-dose" placeholder="Ex: 0.05">
      </div>

      <!-- Botões e Resultado -->
      <div class="button-group">
        <button id="calc-button">Calcular</button>
        <button id="reset-button" class="secondary">Reiniciar</button>
      </div>
      
      <h3>Resultado da Infusão:</h3>
      <p><strong>Velocidade de Infusão: <span id="infusion-rate">-</span></strong></p>
    </div>
</div>

<div class="info-container">
    <h2>Guia Rápido: Indicações e Observações</h2>

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

const styles = `
#calculator-wrapper {
    margin-bottom: 25px;
}
.calculator-container, .info-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.info-container {
    background-color: #e9f5ff; /* Cor de fundo diferente para o guia */
}
.info-container h4 {
    border-bottom: 2px solid #007bff;
    padding-bottom: 5px;
    margin-top: 20px;
}
.input-group { margin-bottom: 15px; }
label { display: block; margin-bottom: 5px; font-weight: 500; }
input[type="number"], select {
  width: 100%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}
.button-group { display: flex; gap: 10px; margin-top: 20px; }
.button-group button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  flex-grow: 1;
}
#calc-button { background-color: #007bff; color: white; }
#calc-button:hover { background-color: #0056b3; }
.secondary { background-color: #6c757d; color: white; }
.secondary:hover { background-color: #5a6268; }
.section-header {
    margin-top: 20px;
    border-bottom: 1px solid #ccc;
    padding-bottom: 3px;
    font-size: 1.1em;
}
p > strong {
    color: #333;
}
#infusion-rate {
    font-size: 1.2em;
    color: darkred;
    font-weight: bold;
}
`;

// --- PARTE 2: LÓGICA JAVASCRIPT ---

// Renderiza o HTML e o estilo
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += toolHTML;

// Dados das drogas para facilitar a lógica
const drugData = {
    fentanyl: { drugUnit: "mcg", doseUnit: "mcg/kg/hora", weightBased: true, doseFactor: 1, conversion: 1 },
    midazolam: { drugUnit: "mg", doseUnit: "mg/kg/hora", weightBased: true, doseFactor: 1, conversion: 1000 },
    propofol: { drugUnit: "mg", doseUnit: "mcg/kg/min", weightBased: true, doseFactor: 60, conversion: 1000 },
    noradrenaline: { drugUnit: "mg", doseUnit: "mcg/kg/min", weightBased: true, doseFactor: 60, conversion: 1000 },
    remifentanil: { drugUnit: "mg", doseUnit: "mcg/kg/min", weightBased: true, doseFactor: 60, conversion: 1000 }
};

const drugSelect = container.querySelector('#drug-select');
const drugUnitLabel = container.querySelector('#drug-unit-label');
const doseUnitLabel = container.querySelector('#dose-unit-label');

function updateUI() {
    const selectedDrug = drugData[drugSelect.value];
    drugUnitLabel.textContent = selectedDrug.drugUnit;
    doseUnitLabel.textContent = selectedDrug.doseUnit;
}

function calculateInfusion() {
    // Inputs
    const selectedDrug = drugData[drugSelect.value];
    const drugAmount = parseFloat(container.querySelector('#drug-amount').value);
    const totalVolume = parseFloat(container.querySelector('#total-volume').value);
    const weight = parseFloat(container.querySelector('#patient-weight').value);
    const prescribedDose = parseFloat(container.querySelector('#prescribed-dose').value);

    // Validação
    if (isNaN(drugAmount) || isNaN(totalVolume) || isNaN(weight) || isNaN(prescribedDose) || totalVolume <= 0) {
        alert("Por favor, preencha todos os campos com valores numéricos válidos.");
        return;
    }

    // 1. Calcular a concentração em mcg/mL
    const concentrationMcgMl = (drugAmount * selectedDrug.conversion) / totalVolume;
    container.querySelector('#drug-concentration').textContent = `${concentrationMcgMl.toFixed(2)} mcg/mL`;
    
    // 2. Calcular a dose total por hora em mcg
    const totalDoseMcgPerHour = prescribedDose * weight * selectedDrug.doseFactor;
    
    // 3. Calcular a velocidade de infusão em mL/h
    const infusionRate = totalDoseMcgPerHour / concentrationMcgMl;
    
    container.querySelector('#infusion-rate').textContent = `${infusionRate.toFixed(2)} mL/h`;
}

function resetCalculator() {
    container.querySelector('#drug-amount').value = '';
    container.querySelector('#total-volume').value = '';
    container.querySelector('#patient-weight').value = '';
    container.querySelector('#prescribed-dose').value = '';
    container.querySelector('#drug-concentration').textContent = '-';
    container.querySelector('#infusion-rate').textContent = '-';
}

// Vinculação dos eventos
try {
    drugSelect.addEventListener('change', updateUI);
    container.querySelector('#calc-button').addEventListener('click', calculateInfusion);
    container.querySelector('#reset-button').addEventListener('click', resetCalculator);
    // Inicializa a UI com a primeira droga
    updateUI();
} catch (e) {
    container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
}
```

# Calculadora risco tromboembolico 

```dataviewjs
// --- Bloco de Código para Calculadora do Escore CHA₂DS₂-VASc ---

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
    <input type="checkbox" id="c2v-c" value="1">
    <label for="c2v-c"><strong>C</strong>ongestive Heart Failure (Insuficiência Cardíaca Congestiva)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="c2v-h" value="1">
    <label for="c2v-h"><strong>H</strong>ypertension (Hipertensão Arterial)</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="c2v-a2" value="2">
    <label for="c2v-a2"><strong>A</strong>ge ≥ 75 anos (<strong>2 pontos</strong>)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="c2v-d" value="1">
    <label for="c2v-d"><strong>D</strong>iabetes Mellitus</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="c2v-s2" value="2">
    <label for="c2v-s2"><strong>S</strong>troke / TIA / TE (AVC / AIT / Tromboembolismo prévio) (<strong>2 pontos</strong>)</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="c2v-v" value="1">
    <label for="c2v-v"><strong>V</strong>ascular Disease (Doença Vascular: IAM prévio, Doença Arterial Periférica, Placa Aórtica)</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="c2v-a" value="1">
    <label for="c2v-a"><strong>A</strong>ge 65-74 anos</label>
  </div>
  
  <div class="button-group">
    <button id="c2v-calc-button">Calcular Escore</button>
    <button id="c2v-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Escore Total: <span id="c2v-result"></span></h3>
  <h4>Risco Anual de AVC e Recomendação Clínica: <span id="c2v-interpretation" style="font-weight: normal;"></span></h4>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.checkbox-group, .input-group {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
}
.checkbox-group input {
  margin-right: 10px;
  min-width: 18px;
  min-height: 18px;
}
.checkbox-group label {
  line-height: 1.4;
}
.input-group label {
  font-weight: bold;
  margin-right: 10px;
}
select {
    padding: 8px;
    border-radius: 4px;
    border: 1px solid #ccc;
}
.button-group {
  display: flex;
  gap: 10px;
  margin-top: 20px;
  flex-wrap: wrap;
}
.button-group button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  flex-grow: 1;
}
#c2v-calc-button {
  background-color: #007bff;
  color: white;
}
#c2v-calc-button:hover {
  background-color: #0056b3;
}
.button-group .secondary {
  background-color: #6c757d;
  color: white;
}
.button-group .secondary:hover {
  background-color: #5a6268;
}
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
    const checkboxes = container.querySelectorAll('.checkbox-group input[type="checkbox"]');
    const sex = container.querySelector('#c2v-sex').value;

    checkboxes.forEach(box => {
        if (box.checked) {
            // Garante que A2 e A não sejam marcados juntos. A2 (>= 75) prevalece.
            if (box.id === 'c2v-a' && container.querySelector('#c2v-a2').checked) {
                 // não faz nada, pois A2 já foi contado
            } else {
                score += parseInt(box.value);
            }
        }
    });

    // O critério de Sexo Feminino só é adicionado ao escore final, não como checkbox
    if (sex === 'feminino') {
        score += 1;
    }
    
    container.querySelector('#c2v-result').innerText = score;
    
    // Interpretação do escore
    const interpretationEl = container.querySelector('#c2v-interpretation');
    let recommendation = "";

    if (sex === 'masculino') {
        if (score === 0) {
            recommendation = "Risco muito baixo. Anticoagulação não é recomendada.";
        } else if (score === 1) {
            recommendation = "Risco baixo a moderado. Considerar anticoagulação (decisão individualizada).";
        } else { // score >= 2
            recommendation = "Risco moderado a alto. Anticoagulação é recomendada.";
        }
    } else { // sexo === 'feminino'
        if (score === 0 || score === 1) { // Lembre-se que score 1 para mulher significa CHA2DS2-VASc = 0 + 1 (sexo)
            recommendation = "Risco muito baixo. Anticoagulação não é recomendada.";
        } else if (score === 2) {
            recommendation = "Risco baixo a moderado. Considerar anticoagulação (decisão individualizada).";
        } else { // score >= 3
            recommendation = "Risco moderado a alto. Anticoagulação é recomendada.";
        }
    }
    interpretationEl.innerText = recommendation;
}

function resetCHADSVASC() {
    container.querySelectorAll('.checkbox-group input[type="checkbox"]').forEach(box => box.checked = false);
    container.querySelector('#c2v-sex').selectedIndex = 0;
    container.querySelector('#c2v-result').innerText = "";
    container.querySelector('#c2v-interpretation').innerText = "";
}

// 5. Adição segura dos eventos de clique
try {
  container.querySelector('#c2v-calc-button').addEventListener('click', calculateCHADSVASC);
  container.querySelector('#c2v-reset-button').addEventListener('click', resetCHADSVASC);
} catch (e) {
  container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
}
```

#  Calculadora de Wells, Embolia pulmonar 
```dataviewjs
// --- Bloco de Código para Calculadora do Escore de Wells para TEP ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Escore de Wells para Embolia Pulmonar (TEP)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Avalia a probabilidade pré-teste de TEP e ajuda a guiar a decisão sobre exames complementares (ex: Dímero-D, AngioTC).</p>
  
  <div class="checkbox-group">
    <input type="checkbox" id="wells-dvt" data-points="3">
    <label for="wells-dvt">Sinais clínicos de Trombose Venosa Profunda (TVP) (<strong>3 pontos</strong>)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="wells-diag" data-points="3">
    <label for="wells-diag">TEP como diagnóstico nº 1 ou igualmente provável (<strong>3 pontos</strong>)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="wells-hr" data-points="1.5">
    <label for="wells-hr">Frequência Cardíaca > 100 bpm (<strong>1.5 ponto</strong>)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="wells-imob" data-points="1.5">
    <label for="wells-imob">Imobilização (≥ 3 dias) ou cirurgia nas últimas 4 semanas (<strong>1.5 ponto</strong>)</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="wells-prev" data-points="1.5">
    <label for="wells-prev">História de TVP ou TEP prévios (<strong>1.5 ponto</strong>)</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="wells-hemop" data-points="1">
    <label for="wells-hemop">Hemoptise (<strong>1 ponto</strong>)</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="wells-cancer" data-points="1">
    <label for="wells-cancer">Malignidade (em tratamento, paliativo ou diagnosticado nos últimos 6 meses) (<strong>1 ponto</strong>)</label>
  </div>
  
  <div class="button-group">
    <button id="wells-calc-button">Calcular Escore</button>
    <button id="wells-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <h3>Escore Total: <span id="wells-result"></span></h3>
  <h4>Interpretação e Recomendação:</h4>
  <div id="wells-interpretation"></div>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.checkbox-group {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
}
.checkbox-group input {
  margin-right: 10px;
  min-width: 18px;
  min-height: 18px;
}
.checkbox-group label {
  line-height: 1.4;
}
.button-group {
  display: flex;
  gap: 10px;
  margin-top: 20px;
  flex-wrap: wrap;
}
.button-group button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  flex-grow: 1;
}
#wells-calc-button {
  background-color: #007bff;
  color: white;
}
#wells-calc-button:hover {
  background-color: #0056b3;
}
.button-group .secondary {
  background-color: #6c757d;
  color: white;
}
.button-group .secondary:hover {
  background-color: #5a6268;
}
#wells-interpretation {
    padding: 10px;
    background-color: #e9ecef;
    border-radius: 4px;
    margin-top: 5px;
}
`;

// 3. Injeção do estilo e do HTML
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição das funções
function calculateWellsPE() {
    let score = 0;
    container.querySelectorAll('.checkbox-group input[type="checkbox"]').forEach(box => {
        if (box.checked) {
            score += parseFloat(box.dataset.points);
        }
    });

    container.querySelector('#wells-result').innerText = score;

    // Interpretação do escore
    const interpretationEl = container.querySelector('#wells-interpretation');
    let interpretationText = "";

    // Modelo de 2 Níveis (Dicotomizado - mais usado)
    if (score > 4) {
        interpretationText += "<strong>Modelo 2 Níveis:</strong> TEP Provável. Recomenda-se AngioTC de tórax como exame inicial.<br>";
    } else {
        interpretationText += "<strong>Modelo 2 Níveis:</strong> TEP Improvável. Recomenda-se iniciar com Dímero-D. Se negativo, exclui TEP. Se positivo, prosseguir para AngioTC.<br><br>";
    }

    // Modelo de 3 Níveis (Tradicional)
    if (score > 6) {
        interpretationText += "<strong>Modelo 3 Níveis:</strong> Alto Risco de TEP (>75%).";
    } else if (score >= 2) {
        interpretationText += "<strong>Modelo 3 Níveis:</strong> Risco Moderado de TEP (~20-40%).";
    } else {
        interpretationText += "<strong>Modelo 3 Níveis:</strong> Baixo Risco de TEP (<15%).";
    }
    
    interpretationEl.innerHTML = interpretationText;
}

function resetWellsPE() {
    container.querySelectorAll('.checkbox-group input[type="checkbox"]').forEach(box => box.checked = false);
    container.querySelector('#wells-result').innerText = "";
    container.querySelector('#wells-interpretation').innerHTML = "";
}

// 5. Adição segura dos eventos de clique com setTimeout
setTimeout(() => {
    try {
        const calcButton = container.querySelector('#wells-calc-button');
        if (calcButton) calcButton.addEventListener('click', calculateWellsPE);

        const resetButton = container.querySelector('#wells-reset-button');
        if (resetButton) resetButton.addEventListener('click', resetWellsPE);
    } catch (e) {
        container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
    }
}, 0);
```

# Calculadora PESI, mortalidade tromboembolia
```dataviewjs
// --- Bloco de Código para Calculadora dos Escores PESI e sPESI ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Escore PESI e sPESI (Prognóstico da TEP)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Estratifica o risco de mortalidade em 30 dias em pacientes com TEP confirmada, ajudando a identificar candidatos a tratamento ambulatorial.</p>
  
  <div class="input-group">
    <label for="pesi-age">Idade do paciente (anos)</label>
    <input type="number" id="pesi-age" placeholder="Ex: 70">
  </div>

  <div class="input-group">
    <label for="pesi-sex">Sexo Masculino</label>
    <select id="pesi-sex">
        <option value="nao">Não</option>
        <option value="sim">Sim</option>
    </select>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="pesi-cancer">
    <label for="pesi-cancer">História de Câncer</label>
  </div>
  
  <div class="checkbox-group">
    <input type="checkbox" id="pesi-chf">
    <label for="pesi-chf">História de Insuficiência Cardíaca Crônica</label>
  </div>

  <div class="checkbox-group">
    <input type="checkbox" id="pesi-cpd">
    <label for="pesi-cpd">História de Doença Pulmonar Crônica</label>
  </div>

  <div class="input-group">
    <label for="pesi-hr">Frequência Cardíaca (bpm)</label>
    <select id="pesi-hr">
        <option value="nao">< 110 bpm</option>
        <option value="sim">≥ 110 bpm</option>
    </select>
  </div>

  <div class="input-group">
    <label for="pesi-sbp">Pressão Arterial Sistólica (mmHg)</label>
    <select id="pesi-sbp">
        <option value="nao">≥ 100 mmHg</option>
        <option value="sim">< 100 mmHg</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="pesi-rr">Frequência Respiratória (ipm)</label>
    <select id="pesi-rr">
        <option value="nao">< 30 ipm</option>
        <option value="sim">≥ 30 ipm</option>
    </select>
  </div>

  <div class="input-group">
    <label for="pesi-temp">Temperatura Corporal</label>
    <select id="pesi-temp">
        <option value="nao">≥ 36°C</option>
        <option value="sim">< 36°C</option>
    </select>
  </div>
  
  <div class="input-group">
    <label for="pesi-ams">Alteração do Nível de Consciência</label>
    <select id="pesi-ams">
        <option value="nao">Não</option>
        <option value="sim">Sim (Confusão, desorientação, estupor ou coma)</option>
    </select>
  </div>

  <div class="input-group">
    <label for="pesi-sao2">Saturação de Oxigênio (SaO₂)</label>
    <select id="pesi-sao2">
        <option value="nao">≥ 90%</option>
        <option value="sim">< 90%</option>
    </select>
  </div>

  <div class="button-group">
    <button id="pesi-calc-button">Calcular Escores</button>
    <button id="pesi-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <div id="results-wrapper">
    <!-- Resultado PESI -->
    <div class="result-box">
        <h3>Escore PESI</h3>
        <p><strong>Pontuação:</strong> <span id="pesi-result">-</span></p>
        <p><strong>Classe de Risco:</strong> <span id="pesi-class">-</span></p>
        <p><strong>Mortalidade em 30d:</strong> <span id="pesi-mortality">-</span></p>
    </div>
    <!-- Resultado sPESI -->
    <div class="result-box">
        <h3>Escore sPESI (Simplificado)</h3>
        <p><strong>Pontuação:</strong> <span id="spesi-result">-</span></p>
        <p><strong>Risco:</strong> <span id="spesi-class">-</span></p>
        <p><strong>Mortalidade em 30d:</strong> <span id="spesi-mortality">-</span></p>
    </div>
  </div>
  <h4>Recomendação de Manejo: <span id="pesi-recommendation" style="font-weight: normal;"></span></h4>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.input-group, .checkbox-group {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
}
input, select {
  padding: 8px; border-radius: 4px; border: 1px solid #ccc;
}
input[type="number"] { width: 100%; box-sizing: border-box; }
.checkbox-group input { margin-right: 10px; min-width: 18px; min-height: 18px; }
.input-group label, .checkbox-group label { line-height: 1.4; flex-basis: 50%; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button {
  padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1;
}
#pesi-calc-button { background-color: #007bff; color: white; }
#pesi-calc-button:hover { background-color: #0056b3; }
.secondary { background-color: #6c757d; color: white; }
.secondary:hover { background-color: #5a6268; }
#results-wrapper { display: flex; gap: 20px; margin-top: 15px; flex-wrap: wrap; }
.result-box {
  flex: 1; min-width: 200px; padding: 15px; background-color: #e9ecef; border-radius: 4px;
}
.result-box h3 { margin-top: 0; border-bottom: 1px solid #ccc; padding-bottom: 5px; }
.result-box p { margin: 5px 0; }
`;

// 3. Injeção do estilo e do HTML
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição das funções
function calculatePESI() {
    let pesiScore = 0;
    let spesiScore = 0;
    const getEl = (id) => container.querySelector('#' + id);
    
    // Variáveis
    const age = parseInt(getEl('pesi-age').value);
    const isMale = getEl('pesi-sex').value === 'sim';
    const hasCancer = getEl('pesi-cancer').checked;
    const hasChf = getEl('pesi-chf').checked;
    const hasCpd = getEl('pesi-cpd').checked;
    const hrHigh = getEl('pesi-hr').value === 'sim';
    const sbpLow = getEl('pesi-sbp').value === 'sim';
    const rrHigh = getEl('pesi-rr').value === 'sim';
    const tempLow = getEl('pesi-temp').value === 'sim';
    const hasAms = getEl('pesi-ams').value === 'sim';
    const sao2Low = getEl('pesi-sao2').value === 'sim';
    
    if (isNaN(age)) { alert("Por favor, insira a idade."); return; }

    // --- Cálculo do PESI ---
    pesiScore += age;
    if (isMale) pesiScore += 10;
    if (hasCancer) pesiScore += 30;
    if (hasChf) pesiScore += 10;
    if (hasCpd) pesiScore += 10;
    if (hrHigh) pesiScore += 20;
    if (sbpLow) pesiScore += 30;
    if (rrHigh) pesiScore += 20;
    if (tempLow) pesiScore += 20;
    if (hasAms) pesiScore += 60;
    if (sao2Low) pesiScore += 20;

    // --- Cálculo do sPESI ---
    if (age > 80) spesiScore += 1;
    if (hasCancer) spesiScore += 1;
    if (hasChf || hasCpd) spesiScore += 1;
    if (hrHigh) spesiScore += 1;
    if (sbpLow) spesiScore += 1;
    if (sao2Low) spesiScore += 1;

    // --- Exibir Resultados PESI ---
    getEl('pesi-result').innerText = pesiScore;
    let pesiClass, pesiMortality;
    if (pesiScore <= 65) { pesiClass = "I (Muito Baixo)"; pesiMortality = "0 - 1.6%"; }
    else if (pesiScore <= 85) { pesiClass = "II (Baixo)"; pesiMortality = "1.7 - 3.5%"; }
    else if (pesiScore <= 105) { pesiClass = "III (Moderado)"; pesiMortality = "3.2 - 7.1%"; }
    else if (pesiScore <= 125) { pesiClass = "IV (Alto)"; pesiMortality = "4.0 - 11.4%"; }
    else { pesiClass = "V (Muito Alto)"; pesiMortality = "10.0 - 24.5%"; }
    getEl('pesi-class').innerText = pesiClass;
    getEl('pesi-mortality').innerText = pesiMortality;

    // --- Exibir Resultados sPESI ---
    getEl('spesi-result').innerText = spesiScore;
    let spesiClass, spesiMortality, recommendation;
    if (spesiScore === 0) {
        spesiClass = "Baixo Risco";
        spesiMortality = "~1.0%";
        recommendation = "Risco baixo. O paciente pode ser candidato a tratamento ambulatorial, se houver condições sociais e clínicas adequadas.";
    } else {
        spesiClass = "Alto Risco";
        spesiMortality = "~10.9%";
        recommendation = "Risco alto. O paciente deve ser internado para tratamento.";
    }
    getEl('spesi-class').innerText = spesiClass;
    getEl('spesi-mortality').innerText = spesiMortality;
    getEl('pesi-recommendation').innerText = recommendation;
}

function resetPESI() {
    container.querySelectorAll('input, select').forEach(el => {
        if (el.type === 'checkbox') el.checked = false;
        else if (el.type === 'number') el.value = '';
        else el.selectedIndex = 0;
    });
    const resultFields = ['pesi-result', 'pesi-class', 'pesi-mortality', 'spesi-result', 'spesi-class', 'spesi-mortality', 'pesi-recommendation'];
    resultFields.forEach(id => container.querySelector('#' + id).innerText = "-");
}

// 5. Adição segura dos eventos de clique com setTimeout
setTimeout(() => {
    try {
        container.querySelector('#pesi-calc-button').addEventListener('click', calculatePESI);
        container.querySelector('#pesi-reset-button').addEventListener('click', resetPESI);
    } catch (e) {
        container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
    }
}, 0);
```

# Calculadora CURB 65, Pneumonia
```dataviewjs
// --- Bloco de Código para Calculadora do Escore CURB-65 ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Escore CURB-65 (Gravidade da Pneumonia)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Avalia a mortalidade em 30 dias e ajuda a decidir o local de tratamento para Pneumonia Adquirida na Comunidade (PAC).</p>
  
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
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.checkbox-group {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
}
.checkbox-group input {
  margin-right: 10px;
  min-width: 18px;
  min-height: 18px;
}
.checkbox-group label {
  line-height: 1.4;
}
.button-group {
  display: flex;
  gap: 10px;
  margin-top: 20px;
  flex-wrap: wrap;
}
.button-group button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  flex-grow: 1;
}
#curb-calc-button {
  background-color: #007bff;
  color: white;
}
#curb-calc-button:hover {
  background-color: #0056b3;
}
.button-group .secondary {
  background-color: #6c757d;
  color: white;
}
.button-group .secondary:hover {
  background-color: #5a6268;
}
#curb-interpretation {
    padding: 10px;
    background-color: #e9ecef;
    border-radius: 4px;
    margin-top: 5px;
    line-height: 1.5;
}
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
        if (box.checked) {
            score += parseInt(box.dataset.points);
        }
    });

    container.querySelector('#curb-result').innerText = score;

    // Interpretação do escore
    const interpretationEl = container.querySelector('#curb-interpretation');
    let interpretationText = "";

    switch(score) {
        case 0:
        case 1:
            interpretationText = "<strong>Grupo 1 (Baixo Risco):</strong> Mortalidade ~1.5%. Considerar tratamento ambulatorial.";
            break;
        case 2:
            interpretationText = "<strong>Grupo 2 (Risco Moderado):</strong> Mortalidade ~9.2%. Considerar internação hospitalar breve ou tratamento supervisionado em ambiente ambulatorial.";
            break;
        default: // score 3, 4 ou 5
            interpretationText = "<strong>Grupo 3 (Alto Risco):</strong> Mortalidade ~22%. Internação hospitalar urgente. Avaliar necessidade de UTI, especialmente com escore 4 ou 5.";
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
        const calcButton = container.querySelector('#curb-calc-button');
        if (calcButton) calcButton.addEventListener('click', calculateCURB65);

        const resetButton = container.querySelector('#curb-reset-button');
        if (resetButton) resetButton.addEventListener('click', resetCURB65);
    } catch (e) {
        container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
    }
}, 0);
```

# Calculadora Critérios de Light, Transudato exsudato

```dataviewjs
// --- Bloco de Código para Calculadora de Critérios de Light ---

// 1. Definição do HTML da calculadora
const calculatorHTML = `
<div class="calculator-container">
  <h2>Calculadora de Critérios de Light (Derrame Pleural)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Diferencia derrames pleurais em transudatos e exsudatos com base em análises do líquido pleural e do soro.</p>
  
  <h3 class="section-header">Valores do Líquido Pleural</h3>
  <div class="input-group">
    <label for="light-pleural-protein">Proteína do Líquido Pleural (g/dL)</label>
    <input type="number" id="light-pleural-protein" placeholder="Ex: 4.5" step="0.1">
  </div>
  <div class="input-group">
    <label for="light-pleural-ldh">LDH do Líquido Pleural (U/L)</label>
    <input type="number" id="light-pleural-ldh" placeholder="Ex: 350" step="1">
  </div>

  <h3 class="section-header">Valores do Soro (Sangue)</h3>
  <div class="input-group">
    <label for="light-serum-protein">Proteína Sérica (g/dL)</label>
    <input type="number" id="light-serum-protein" placeholder="Ex: 7.0" step="0.1">
  </div>
  <div class="input-group">
    <label for="light-serum-ldh">LDH Sérico (U/L)</label>
    <input type="number" id="light-serum-ldh" placeholder="Ex: 200" step="1">
  </div>
  <div class="input-group">
    <label for="light-ldh-limit">Limite Superior da Normalidade do LDH Sérico (U/L)</label>
    <input type="number" id="light-ldh-limit" placeholder="Ex: 250" step="1">
  </div>
  
  <div class="button-group">
    <button id="light-calc-button">Analisar Critérios</button>
    <button id="light-reset-button" class="secondary">Reiniciar</button>
  </div>
  
  <div id="light-interpretation"></div>
</div>
`;

// 2. Definição do estilo (CSS)
const styles = `
.calculator-container {
  background-color: #f0f0f0; padding: 20px; border-radius: 8px; font-family: sans-serif; border: 1px solid #ddd;
}
.section-header { margin-top: 20px; border-bottom: 1px solid #ccc; padding-bottom: 3px; font-size: 1.1em; }
.input-group { margin-bottom: 15px; }
label { display: block; margin-bottom: 5px; }
input[type="number"] { width: 100%; padding: 8px; border-radius: 4px; border: 1px solid #ccc; box-sizing: border-box; }
.button-group { display: flex; gap: 10px; margin-top: 20px; flex-wrap: wrap; }
.button-group button {
  padding: 10px 15px; border: none; border-radius: 4px; cursor: pointer; flex-grow: 1;
}
#light-calc-button { background-color: #007bff; color: white; }
#light-calc-button:hover { background-color: #0056b3; }
.secondary { background-color: #6c757d; color: white; }
.secondary:hover { background-color: #5a6268; }
#light-interpretation {
  padding: 15px; background-color: #e9ecef; border-radius: 4px; margin-top: 20px; line-height: 1.6;
}
.result-final { font-size: 1.3em; font-weight: bold; text-align: center; padding: 10px; border-radius: 5px; margin: 10px 0; }
.exudate { background-color: #f8d7da; color: #721c24; border: 1px solid #f5c6cb; }
.transudate { background-color: #d4edda; color: #155724; border: 1px solid #c3e6cb; }
`;

// 3. Injeção do estilo e do HTML
const container = dv.container;
const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);
container.innerHTML += calculatorHTML;

// 4. Definição das funções
function calculateLightsCriteria() {
    // Pegar valores
    const pProt = parseFloat(container.querySelector('#light-pleural-protein').value);
    const sProt = parseFloat(container.querySelector('#light-serum-protein').value);
    const pLDH = parseFloat(container.querySelector('#light-pleural-ldh').value);
    const sLDH = parseFloat(container.querySelector('#light-serum-ldh').value);
    const ldhLimit = parseFloat(container.querySelector('#light-ldh-limit').value);
    
    // Validar
    if ([pProt, sProt, pLDH, sLDH, ldhLimit].some(isNaN)) {
        alert("Por favor, preencha todos os campos com valores numéricos.");
        return;
    }

    // Calcular critérios
    const proteinRatio = pProt / sProt;
    const ldhRatio = pLDH / sLDH;
    const ldhLimitCheck = (2/3) * ldhLimit;

    const criterion1 = proteinRatio > 0.5;
    const criterion2 = ldhRatio > 0.6;
    const criterion3 = pLDH > ldhLimitCheck;

    const isExudate = criterion1 || criterion2 || criterion3;
    
    // Montar o texto de resultado
    let resultHTML = "<h4>Análise dos Critérios:</h4><ul>";
    resultHTML += `<li>Proteína Pleural / Sérica > 0.5: <strong>${criterion1 ? 'SIM' : 'NÃO'}</strong> (Ratio: ${proteinRatio.toFixed(2)})</li>`;
    resultHTML += `<li>LDH Pleural / Sérico > 0.6: <strong>${criterion2 ? 'SIM' : 'NÃO'}</strong> (Ratio: ${ldhRatio.toFixed(2)})</li>`;
    resultHTML += `<li>LDH Pleural > 2/3 do Limite Superior: <strong>${criterion3 ? 'SIM' : 'NÃO'}</strong> (Valor: ${pLDH.toFixed(0)} vs Limite: ${ldhLimitCheck.toFixed(0)})</li>`;
    resultHTML += "</ul>";
    
    if (isExudate) {
        resultHTML += `<div class="result-final exudate">Diagnóstico: EXSUDATO</div>`;
        resultHTML += "<strong>Causas Comuns (investigar):</strong> Infecção (pneumonia, empiema), Neoplasia, Embolia Pulmonar, Doenças inflamatórias (artrite reumatoide, lúpus), Pancreatite.";
    } else {
        resultHTML += `<div class="result-final transudate">Diagnóstico: TRANSUDATO</div>`;
        resultHTML += "<strong>Causas Comuns (tratar condição de base):</strong> Insuficiência Cardíaca Congestiva, Cirrose Hepática, Síndrome Nefrótica, Hipoalbuminemia, Diálise Peritoneal.";
    }
    
    container.querySelector('#light-interpretation').innerHTML = resultHTML;
}

function resetLights() {
    container.querySelectorAll('input[type="number"]').forEach(input => input.value = '');
    container.querySelector('#light-interpretation').innerHTML = "";
}

// 5. Adição segura dos eventos de clique com setTimeout
setTimeout(() => {
    try {
        container.querySelector('#light-calc-button').addEventListener('click', calculateLightsCriteria);
        container.querySelector('#light-reset-button').addEventListener('click', resetLights);
    } catch (e) {
        container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
    }
}, 0);
```


```dataviewjs
// --- Bloco de Código: Calculadora de Preparo de Seringa por Objetivo ---

// --- PARTE 1: HTML E ESTILOS ---

const toolHTML = `
<div class="prep-calculator-container">
  <h2>Calculadora de Preparo de Seringa por Objetivo</h2>
  <p class="description">Calcule a quantidade de droga necessária para atingir uma dose alvo durante um tempo específico.</p>

  <!-- Passo 1 e 2: Definir a Dose e Peso -->
  <h3 class="section-header">1. Defina a Dose e o Peso</h3>
  <div class="input-row">
    <div class="input-group">
      <label for="prep-dose">Dose Alvo</label>
      <input type="number" id="prep-dose" placeholder="Ex: 0.1">
    </div>
    <div class="input-group">
      <label for="prep-dose-unit">Unidade da Dose</label>
      <select id="prep-dose-unit">
        <option value="mg/kg/h">mg/kg/h</option>
        <option value="mcg/kg/h">mcg/kg/h</option>
        <option value="mcg/kg/min" selected>mcg/kg/min</option>
      </select>
    </div>
    <div class="input-group">
      <label for="prep-weight">Peso do Paciente (kg)</label>
      <input type="number" id="prep-weight" placeholder="Ex: 70">
    </div>
  </div>
  <p class="intermediate-result"><strong>Dose Total Individualizada:</strong> <span id="total-dose-result">-</span></p>

  <!-- Passo 3: Volume e Duração -->
  <h3 class="section-header">2. Escolha o Volume e a Duração</h3>
  <div class="input-row">
    <div class="input-group">
      <label for="prep-volume">Volume Total da Solução (mL)</label>
      <input type="number" id="prep-volume" placeholder="Ex: 50">
    </div>
    <div class="input-group">
      <label for="prep-duration">Duração da Infusão (horas)</label>
      <input type="number" id="prep-duration" placeholder="Ex: 12">
    </div>
  </div>
  <p class="intermediate-result"><strong>Velocidade de Infusão (Bomba):</strong> <span id="infusion-rate-result">-</span></p>

  <!-- Botões -->
  <div class="button-group">
    <button id="prep-calc-button">Calcular Preparo</button>
    <button id="prep-reset-button" class="secondary">Reiniciar</button>
  </div>

  <!-- Passo 4 e 5: Resultados Finais -->
  <div id="final-results-wrapper" style="display: none;">
    <h3 class="section-header">3. Resultado do Preparo da Seringa</h3>
    <div class="final-result-box">
      <h4>Passo 4: Concentração Necessária</h4>
      <p id="concentration-result">-</p>
    </div>
    <div class="final-result-box highlight">
      <h4>Passo 5: Total de Droga a Adicionar</h4>
      <p id="total-drug-result">-</p>
    </div>
  </div>

</div>
`;

const styles = `
.prep-calculator-container {
  background-color: #f5f7fa;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
}
.prep-calculator-container h2 {
  text-align: center;
  color: #2c3e50;
  border-bottom: 2px solid #3498db;
  padding-bottom: 10px;
  margin-bottom: 5px;
}
.description {
  text-align: center;
  font-size: 0.9em;
  color: #555;
  margin-bottom: 25px;
}
.section-header {
  margin-top: 25px;
  margin-bottom: 15px;
  border-bottom: 1px solid #ccc;
  padding-bottom: 5px;
  font-size: 1.1em;
  color: #34495e;
}
.input-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 15px;
}
.input-group { margin-bottom: 10px; }
.input-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: 500;
  font-size: 0.9em;
  color: #333;
}
.input-group input[type="number"], .input-group select {
  width: 100%;
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}
.button-group {
  display: flex;
  gap: 10px;
  margin-top: 25px;
  margin-bottom: 25px;
}
.button-group button {
  padding: 12px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  flex-grow: 1;
  font-size: 1.05em;
  font-weight: bold;
}
#prep-calc-button { background-color: #3498db; color: white; }
#prep-calc-button:hover { background-color: #2980b9; }
.secondary { background-color: #6c757d; color: white; }
.secondary:hover { background-color: #5a6268; }
.intermediate-result {
  background-color: #ecf0f1;
  padding: 8px;
  border-radius: 4px;
  margin-top: 10px;
  font-size: 0.95em;
}
.intermediate-result > strong, .final-result-box p {
  color: #0056b3;
  font-weight: bold;
}
.final-result-box {
  background-color: #e9f5ff;
  border: 1px solid #aed6f1;
  padding: 15px;
  margin-top: 10px;
  border-radius: 5px;
}
.final-result-box.highlight {
  background-color: #d4efdf;
  border-color: #7dcea0;
}
.final-result-box.highlight p {
  color: #1e8449;
  font-size: 1.4em;
  text-align: center;
}
.final-result-box h4 {
  margin-top: 0;
  margin-bottom: 8px;
  color: #2c3e50;
}
.final-result-box p {
  margin: 0;
  font-size: 1.2em;
}
`;

// --- PARTE 2: LÓGICA JAVASCRIPT ---

const container = dv.container;

const styleEl = document.createElement('style');
styleEl.innerHTML = styles;
container.appendChild(styleEl);

container.innerHTML += toolHTML;

// --- Seleção dos Elementos do DOM ---
const doseInput = container.querySelector('#prep-dose');
const unitSelect = container.querySelector('#prep-dose-unit');
const weightInput = container.querySelector('#prep-weight');
const volumeInput = container.querySelector('#prep-volume');
const durationInput = container.querySelector('#prep-duration');

const totalDoseResultSpan = container.querySelector('#total-dose-result');
const infusionRateResultSpan = container.querySelector('#infusion-rate-result');
const concentrationResultP = container.querySelector('#concentration-result');
const totalDrugResultP = container.querySelector('#total-drug-result');
const finalResultsWrapper = container.querySelector('#final-results-wrapper');

const calcButton = container.querySelector('#prep-calc-button');
const resetButton = container.querySelector('#prep-reset-button');


// --- Funções de Cálculo ---

function calculatePreparation() {
  // 1. Obter todos os valores de entrada
  const doseValue = parseFloat(doseInput.value);
  const selectedUnit = unitSelect.value;
  const weight = parseFloat(weightInput.value);
  const totalVolume = parseFloat(volumeInput.value);
  const duration = parseFloat(durationInput.value);

  // Validação
  if (isNaN(doseValue) || isNaN(weight) || isNaN(totalVolume) || isNaN(duration) || weight <= 0 || totalVolume <= 0 || duration <= 0) {
    alert("Por favor, preencha todos os campos com valores numéricos positivos.");
    return;
  }

  // 2. Calcular a dose total individualizada em mg/hora
  let totalDoseMgPerHour;
  let unitLabel = "mg/h";

  if (selectedUnit === 'mg/kg/h') {
    totalDoseMgPerHour = doseValue * weight;
  } else if (selectedUnit === 'mcg/kg/h') {
    totalDoseMgPerHour = (doseValue * weight) / 1000;
  } else { // mcg/kg/min
    totalDoseMgPerHour = (doseValue * weight * 60) / 1000;
  }
  
  const totalDoseMcgPerHour = totalDoseMgPerHour * 1000;
  totalDoseResultSpan.textContent = `${totalDoseMgPerHour.toFixed(3)} mg/h (ou ${totalDoseMcgPerHour.toFixed(1)} mcg/h)`;

  // 3. Calcular a velocidade de infusão em mL/h
  const infusionRateMlPerHour = totalVolume / duration;
  infusionRateResultSpan.textContent = `${infusionRateMlPerHour.toFixed(2)} mL/h`;

  // 4. Calcular a concentração desejada em mg/mL
  const requiredConcentrationMgPerMl = totalDoseMgPerHour / infusionRateMlPerHour;
  const requiredConcentrationMcgPerMl = requiredConcentrationMgPerMl * 1000;
  concentrationResultP.textContent = `${requiredConcentrationMgPerMl.toFixed(3)} mg/mL (ou ${requiredConcentrationMcgPerMl.toFixed(1)} mcg/mL)`;
  
  // 5. Calcular o total de droga a ser adicionado na seringa/bolsa em mg
  const totalDrugMg = requiredConcentrationMgPerMl * totalVolume;
  // Outra forma de calcular, mais direta: totalDrugMg = totalDoseMgPerHour * duration;
  const totalDrugMcg = totalDrugMg * 1000;
  totalDrugResultP.textContent = `${totalDrugMg.toFixed(2)} mg (ou ${totalDrugMcg.toFixed(0)} mcg)`;

  // Exibir a caixa de resultados finais
  finalResultsWrapper.style.display = 'block';
}

function resetCalculator() {
  doseInput.value = '';
  weightInput.value = '';
  volumeInput.value = '';
  durationInput.value = '';

  totalDoseResultSpan.textContent = '-';
  infusionRateResultSpan.textContent = '-';
  
  // Esconder e limpar resultados finais
  finalResultsWrapper.style.display = 'none';
  concentrationResultP.textContent = '-';
  totalDrugResultP.textContent = '-';
}


// --- Vinculação dos Eventos ---
try {
  calcButton.addEventListener('click', calculatePreparation);
  resetButton.addEventListener('click', resetCalculator);
} catch (e) {
  container.innerHTML += `<p style='color:red;'>Erro ao executar o script: ${e.message}</p>`;
}
```
