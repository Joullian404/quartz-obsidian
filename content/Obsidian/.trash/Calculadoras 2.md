```dataviewjs
// --- CALCULADORAS MÉDICAS INTEGRADAS ---
// Autor da Integração: Gemini
// Data: 31/07/2025
// Descrição: Um conjunto de calculadoras médicas interativas com um menu de seleção.

// --- ETAPA 1: DEFINIÇÃO DOS ESTILOS GLOBAIS (CSS) ---
// Estilos foram combinados para evitar repetição e garantir consistência.
const globalStyles = `
/* --- Estilo do Menu e Contêiner Principal --- */
#med-calc-menu {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 20px;
  padding-bottom: 15px;
  border-bottom: 2px solid #007bff;
}
#med-calc-menu button {
  background-color: #f8f9fa;
  color: #007bff;
  border: 1px solid #007bff;
  padding: 8px 12px;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.2s;
}
#med-calc-menu button:hover {
  background-color: #e2e6ea;
}
#med-calc-menu button.active {
  background-color: #007bff;
  color: white;
  font-weight: bold;
}
.calculator-content {
  display: none; /* Esconde todas as calculadoras por padrão */
}
.calculator-content.active {
  display: block; /* Mostra apenas a calculadora ativa */
}

/* --- Estilos Comuns das Calculadoras --- */
.calculator-container {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 8px;
  font-family: sans-serif;
  border: 1px solid #ddd;
  margin-top: 10px;
}
.input-group, .checkbox-group {
  margin-bottom: 15px;
}
label {
  display: block;
  margin-bottom: 5px;
  font-weight: 500;
}
input[type="number"], input[type="text"], select {
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
  margin-right: 10px;
  width: auto;
  min-width: 18px;
  min-height: 18px;
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
  color: white;
}
.button-group button:first-child {
  background-color: #007bff;
}
.button-group button:first-child:hover {
  background-color: #0056b3;
}
.button-group button.secondary {
  background-color: #6c757d;
}
.button-group button.secondary:hover {
  background-color: #5a6268;
}
.section-header {
  margin-top: 20px;
  border-bottom: 1px solid #ccc;
  padding-bottom: 3px;
  font-size: 1.1em;
}
.result-final {
  font-size: 1.3em;
  font-weight: bold;
  text-align: center;
  padding: 10px;
  border-radius: 5px;
  margin: 10px 0;
}
.exudate { background-color: #f8d7da; color: #721c24; border: 1px solid #f5c6cb; }
.transudate { background-color: #d4edda; color: #155724; border: 1px solid #c3e6cb; }
#results-wrapper { display: flex; gap: 20px; margin-top: 15px; flex-wrap: wrap; }
.result-box {
  flex: 1; min-width: 200px; padding: 15px; background-color: #e9ecef; border-radius: 4px;
}
.result-box h3 { margin-top: 0; border-bottom: 1px solid #ccc; padding-bottom: 5px; }
`;

// --- ETAPA 2: DEFINIÇÃO DO HTML DE CADA CALCULADORA ---
// O HTML de cada calculadora é armazenado em um objeto para fácil acesso.
const calculatorsHTML = {
    ich: `<!-- Conteúdo da Calculadora ICH -->`,
    sirs: `<!-- Conteúdo da Calculadora SIRS -->`,
    qsofa: `<!-- Conteúdo da Calculadora qSOFA -->`,
    sofa: `<!-- Conteúdo da Calculadora SOFA -->`,
    nihss: `<!-- Conteúdo da Calculadora NIHSS -->`,
    mdrd: `<!-- Conteúdo da Calculadora MDRD -->`,
    sedo: `<!-- Conteúdo da Calculadora Sedoanalgesia -->`,
    chadsvasc: `<!-- Conteúdo da Calculadora CHA₂DS₂-VASc -->`,
    wells: `<!-- Conteúdo da Calculadora Wells -->`,
    pesi: `<!-- Conteúdo da Calculadora PESI -->`,
    curb65: `<!-- Conteúdo da Calculadora CURB-65 -->`,
    light: `<!-- Conteúdo da Calculadora Light -->`,
    seringa: `<!-- Conteúdo da Calculadora Seringa -->`,
};

// ** Preenchendo o objeto calculatorsHTML com seu código **
// (O código HTML de cada uma de suas calculadoras foi colado aqui)
calculatorsHTML.ich = `
<div class="calculator-container">
  <h2>Escore ICH para Hemorragia Intracraniana</h2>
  <div class="input-group"><label for="glasgow">Glasgow na Admissão</label><select id="glasgow"><option value="2">3-4</option><option value="1">5-12</option><option value="0">13-15</option></select></div>
  <div class="input-group"><label for="idade-ich">Idade</label><select id="idade-ich"><option value="1">>= 80 anos</option><option value="0">< 80 anos</option></select></div>
  <div class="input-group"><label for="local-hematoma">Local do Hematoma</label><select id="local-hematoma"><option value="1">Infratentorial</option><option value="0">Supratentorial</option></select></div>
  <div class="input-group"><label for="volume-hematoma">Volume do Hematoma</label><select id="volume-hematoma"><option value="1">>= 30ml</option><option value="0">< 30ml</option></select></div>
  <div class="input-group"><label for="hemoventriculo">Hemo-ventrículo</label><select id="hemoventriculo"><option value="1">Sim</option><option value="0">Não</option></select></div>
  <div class="button-group"><button id="ich-button">Calcular Escore ICH</button></div>
  <h3>Escore: <span id="ich-result"></span></h3>
  <h4>Mortalidade em 30 dias: <span id="ich-mortality"></span></h4>
</div>`;

calculatorsHTML.sirs = `
<div class="calculator-container">
  <h2>Calculadora de Critérios SIRS (Sepsis-2)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Lembre-se: O conceito de SIRS foi substituído pelo qSOFA/SOFA no Sepsis-3, mas ainda é útil em alguns contextos clínicos.</p>
  <div class="checkbox-group"><input type="checkbox" id="sirs-temp"><label for="sirs-temp">Temperatura > 38°C ou < 36°C</label></div>
  <div class="checkbox-group"><input type="checkbox" id="sirs-hr"><label for="sirs-hr">Frequência cardíaca > 90 bpm</label></div>
  <div class="checkbox-group"><input type="checkbox" id="sirs-rr"><label for="sirs-rr">Frequência respiratória > 20 ipm ou PaCO₂ < 32 mmHg</label></div>
  <div class="checkbox-group"><input type="checkbox" id="sirs-wbc"><label for="sirs-wbc">Leucócitos > 12.000, < 4.000 ou > 10% de bastões</label></div>
  <div class="button-group"><button id="sirs-calc-button">Calcular SIRS</button><button id="sirs-reset-button" class="secondary">Reiniciar</button></div>
  <h3>Critérios presentes: <span id="sirs-result"></span></h3>
  <h4>Interpretação: <span id="sirs-interpretation" style="font-weight: normal;"></span></h4>
</div>`;

calculatorsHTML.qsofa = `
<div class="calculator-container">
  <h2>Calculadora qSOFA</h2>
  <div class="checkbox-group"><input type="checkbox" id="respiratory-rate"><label for="respiratory-rate">Frequência respiratória >= 22/min</label></div>
  <div class="checkbox-group"><input type="checkbox" id="mental-status"><label for="mental-status">Alteração do estado mental (Glasgow < 15)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="systolic-bp"><label for="systolic-bp">Pressão arterial sistólica <= 100 mmHg</label></div>
  <div class="button-group"><button id="qsofa-button">Calcular qSOFA</button></div>
  <h3>Resultado: <span id="qsofa-result"></span></h3>
  <p id="qsofa-interpretation"></p>
</div>`;

calculatorsHTML.sofa = `
<div class="calculator-container">
  <h2>Calculadora SOFA</h2>
  <div class="input-group"><label for="respiration">Respiratório (PaO2/FiO2, mmHg)</label><select id="respiration"><option value="0">>= 400</option><option value="1">< 400</option><option value="2">< 300</option><option value="3">< 200 com suporte respiratório</option><option value="4">< 100 com suporte respiratório</option></select></div>
  <div class="input-group"><label for="coagulation">Coagulação (Plaquetas, x10³/µL)</label><select id="coagulation"><option value="0">>= 150</option><option value="1">< 150</option><option value="2">< 100</option><option value="3">< 50</option><option value="4">< 20</option></select></div>
  <div class="input-group"><label for="liver">Fígado (Bilirrubina, mg/dL)</label><select id="liver"><option value="0">< 1.2</option><option value="1">1.2 - 1.9</option><option value="2">2.0 - 5.9</option><option value="3">6.0 - 11.9</option><option value="4">>= 12.0</option></select></div>
  <div class="input-group"><label for="cardiovascular">Cardiovascular (Hipotensão)</label><select id="cardiovascular"><option value="0">PAM >= 70 mmHg</option><option value="1">PAM < 70 mmHg</option><option value="2">Dopamina < 5 ou Dobutamina (qualquer dose)</option><option value="3">Dopamina 5.1-15 ou Epinefrina <= 0.1 ou Norepinefrina <= 0.1</option><option value="4">Dopamina > 15 ou Epinefrina > 0.1 ou Norepinefrina > 0.1</option></select></div>
  <div class="input-group"><label for="cns">Sistema Nervoso Central (Escala de Coma de Glasgow)</label><select id="cns"><option value="0">15</option><option value="1">13 - 14</option><option value="2">10 - 12</option><option value="3">6 - 9</option><option value="4">< 6</option></select></div>
  <div class="input-group"><label for="renal">Renal (Creatinina, mg/dL ou débito urinário)</label><select id="renal"><option value="0">< 1.2</option><option value="1">1.2 - 1.9</option><option value="2">2.0 - 3.4</option><option value="3">3.5 - 4.9 ou < 500 mL/dia</option><option value="4">> 5.0 ou < 200 mL/dia</option></select></div>
  <div class="button-group"><button id="sofa-button">Calcular SOFA</button></div>
  <h3>Resultado: <span id="sofa-result"></span></h3>
  <h4>Risco: <span id="sofa-interpretation" style="font-weight: normal;"></span></h4>
</div>`;

calculatorsHTML.nihss = `
<div class="calculator-container">
  <h2>Calculadora NIHSS (National Institutes of Health Stroke Scale)</h2>
  <div class="input-group"><label for="item1a">1a. Nível de Consciência</label><select id="item1a"><option value="0">0 - Alerta</option><option value="1">1 - Desperta a estímulos leves</option><option value="2">2 - Desperta a estímulos vigorosos</option><option value="3">3 - Não desperta</option></select></div>
  <div class="input-group"><label for="item1b">1b. Orientação (Idade e Mês)</label><select id="item1b"><option value="0">0 - Responde adequadamente as 2 questões</option><option value="1">1 - Responde adequadamente 1 questão</option><option value="2">2 - Não responde adequadamente</option></select></div>
  <div class="input-group"><label for="item1c">1c. Resposta a Comandos Simples</label><select id="item1c"><option value="0">0 - Realiza adequadamente os 2 comandos</option><option value="1">1 - Realiza adequadamente 1 comando</option><option value="2">2 - Não realiza adequadamente</option></select></div>
  <div class="input-group"><label for="item2">2. Olhar Conjugado Horizontal</label><select id="item2"><option value="0">0 - Normal</option><option value="1">1 - Desvio conjugado parcial do olhar</option><option value="2">2 - Desvio conjugado forçado do olhar</option></select></div>
  <div class="input-group"><label for="item3">3. Campo Visual</label><select id="item3"><option value="0">0 - Normal</option><option value="1">1 - Hemianopsia parcial</option><option value="2">2 - Hemianopsia completa</option><option value="3">3 - Hemianopsia bilateral (Cegueira)</option></select></div>
  <div class="input-group"><label for="item4">4. Paralisia Facial</label><select id="item4"><option value="0">0 - Normal</option><option value="1">1 - Paresia menor</option><option value="2">2 - Paresia parcial</option><option value="3">3 - Paralisia completa</option></select></div>
  <div class="input-group"><label for="item5a">5a. Motricidade de Membro Superior (Direito)</label><select id="item5a"><option value="0">0 - Sem queda por 10s</option><option value="1">1 - Queda em menos de 10s, não toca o leito</option><option value="2">2 - Queda em menos de 10s, toca o leito</option><option value="3">3 - Não vence gravidade</option><option value="4">4 - Sem movimento</option><option value="0">Não testável (amputação, etc.)</option></select></div>
  <div class="input-group"><label for="item5b">5b. Motricidade de Membro Superior (Esquerdo)</label><select id="item5b"><option value="0">0 - Sem queda por 10s</option><option value="1">1 - Queda em menos de 10s, não toca o leito</option><option value="2">2 - Queda em menos de 10s, toca o leito</option><option value="3">3 - Não vence gravidade</option><option value="4">4 - Sem movimento</option><option value="0">Não testável (amputação, etc.)</option></select></div>
  <div class="input-group"><label for="item6a">6a. Motricidade de Membro Inferior (Direito)</label><select id="item6a"><option value="0">0 - Sem queda por 5s</option><option value="1">1 - Queda em menos de 5s, não toca o leito</option><option value="2">2 - Queda em menos de 5s, toca o leito</option><option value="3">3 - Não vence gravidade</option><option value="4">4 - Sem movimento</option><option value="0">Não testável (amputação, etc.)</option></select></div>
  <div class="input-group"><label for="item6b">6b. Motricidade de Membro Inferior (Esquerdo)</label><select id="item6b"><option value="0">0 - Sem queda por 5s</option><option value="1">1 - Queda em menos de 5s, não toca o leito</option><option value="2">2 - Queda em menos de 5s, toca o leito</option><option value="3">3 - Não vence gravidade</option><option value="4">4 - Sem movimento</option><option value="0">Não testável (amputação, etc.)</option></select></div>
  <div class="input-group"><label for="item7">7. Ataxia de Membro</label><select id="item7"><option value="0">0 - Ausente</option><option value="1">1 - Presente em 1 membro</option><option value="2">2 - Presente em 2 ou mais membros</option><option value="0">Não testável (paralisia, amputação)</option></select></div>
  <div class="input-group"><label for="item8">8. Sensitivo</label><select id="item8"><option value="0">0 - Normal</option><option value="1">1 - Hipoestesia leve a moderada</option><option value="2">2 - Hipoestesia grave a anestesia</option></select></div>
  <div class="input-group"><label for="item9">9. Linguagem (Afasia)</label><select id="item9"><option value="0">0 - Normal</option><option value="1">1 - Afasia leve a moderada</option><option value="2">2 - Afasia grave</option><option value="3">3 - Mutismo / Afasia global</option></select></div>
  <div class="input-group"><label for="item10">10. Disartria</label><select id="item10"><option value="0">0 - Normal</option><option value="1">1 - Leve a moderada</option><option value="2">2 - Grave (ininteligível)</option><option value="0">Não testável (entubado)</option></select></div>
  <div class="input-group"><label for="item11">11. Extinção ou Heminegligência</label><select id="item11"><option value="0">0 - Ausente</option><option value="1">1 - Presente em 1 modalidade</option><option value="2">2 - Presente em mais de 1 modalidade</option></select></div>
  <div class="button-group"><button id="nihss-button">Calcular NIHSS</button><button id="nihss-reset-button" class="secondary">Reiniciar</button></div>
  <h3>Resultado: <span id="nihss-result"></span></h3>
  <h4>Gravidade do AVC e Prognóstico: <span id="nihss-interpretation" style="font-weight: normal;"></span></h4>
</div>`;

calculatorsHTML.mdrd = `
<div class="calculator-container">
  <h2>Calculadora de TFG Estimada (Fórmula MDRD)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">A fórmula MDRD é usada para estimar a Taxa de Filtração Glomerular e estadiar a Doença Renal Crônica (DRC). Nota: A fórmula CKD-EPI é mais moderna e precisa, especialmente para TFG > 60.</p>
  <div class="input-group"><label for="mdrd-creat">Creatinina Sérica (mg/dL)</label><input type="number" id="mdrd-creat" placeholder="Ex: 1.2" step="0.1"></div>
  <div class="input-group"><label for="mdrd-age">Idade (anos)</label><input type="number" id="mdrd-age" placeholder="Ex: 55"></div>
  <div class="input-group"><label for="mdrd-sex">Sexo</label><select id="mdrd-sex"><option value="masculino">Masculino</option><option value="feminino">Feminino</option></select></div>
  <div class="checkbox-group"><input type="checkbox" id="mdrd-ethnicity"><label for="mdrd-ethnicity">Afro-americano</label></div>
  <div class="button-group"><button id="mdrd-calc-button">Calcular TFG</button><button id="mdrd-reset-button" class="secondary">Reiniciar</button></div>
  <h3>Resultado (TFG estimada): <span id="mdrd-result"></span></h3>
  <h4>Estágio da Doença Renal Crônica (DRC): <span id="mdrd-stage" style="font-weight: normal;"></span></h4>
</div>`;

calculatorsHTML.sedo = `
<div id="calculator-wrapper">
    <div class="calculator-container">
      <h2>Calculadora de Diluição e Infusão</h2>
      <div class="input-group"><label for="drug-select">Selecione a Droga:</label><select id="drug-select"><option value="fentanyl">Fentanil</option><option value="midazolam">Midazolam</option><option value="propofol">Propofol</option><option value="noradrenaline">Noradrenalina</option><option value="remifentanil">Remifentanil</option></select></div>
      <h3 class="section-header">1. Preparo da Solução</h3>
      <div class="input-group"><label for="drug-amount">Quantidade de droga na solução (<span id="drug-unit-label">mcg</span>):</label><input type="number" id="drug-amount" placeholder="Ex: 1000"></div>
      <div class="input-group"><label for="total-volume">Volume total da solução (mL):</label><input type="number" id="total-volume" placeholder="Ex: 100"></div>
      <p><strong>Concentração:</strong> <span id="drug-concentration">-</span></p>
      <h3 class="section-header">2. Cálculo da Infusão</h3>
      <div class="input-group" id="weight-group"><label for="patient-weight">Peso do paciente (kg):</label><input type="number" id="patient-weight" placeholder="Ex: 70"></div>
      <div class="input-group"><label for="prescribed-dose">Dose prescrita (<span id="dose-unit-label">mcg/kg/min</span>):</label><input type="number" id="prescribed-dose" placeholder="Ex: 0.05"></div>
      <div class="button-group"><button id="sedo-calc-button">Calcular</button><button id="sedo-reset-button" class="secondary">Reiniciar</button></div>
      <h3>Resultado da Infusão:</h3>
      <p><strong>Velocidade de Infusão: <span id="infusion-rate" style="font-size: 1.2em; color: darkred; font-weight: bold;">-</span></strong></p>
    </div>
</div>
<div class="calculator-container" style="background-color: #e9f5ff; margin-top: 15px;">
    <h2>Guia Rápido: Indicações e Observações</h2>
    <h4 style="border-bottom: 2px solid #007bff; padding-bottom: 5px;">Fentanil</h4><ul><li><strong>Indicação:</strong> Analgesia potente para pacientes em ventilação mecânica.</li><li><strong>Dose usual (infusão):</strong> 0.5 a 2 mcg/kg/hora.</li><li><strong>Observações:</strong> Opioide de início rápido e curta duração. Pode causar depressão respiratória e rigidez torácica em altas doses.</li></ul>
    <h4 style="border-bottom: 2px solid #007bff; padding-bottom: 5px;">Midazolam</h4><ul><li><strong>Indicação:</strong> Sedação, ansiólise e amnésia. Usado para manter a sedação em pacientes na UTI.</li><li><strong>Dose usual (infusão):</strong> 0.02 a 0.1 mg/kg/hora (ou 1 a 7 mg/hora).</li><li><strong>Observações:</strong> Benzodiazepínico. Risco de acúmulo em pacientes com insuficiência renal ou hepática e em idosos, prolongando o tempo de despertar. Pode causar delirium.</li></ul>
    <h4 style="border-bottom: 2px solid #007bff; padding-bottom: 5px;">Propofol</h4><ul><li><strong>Indicação:</strong> Sedativo-hipnótico para indução e manutenção da sedação. Preferido para sedação de curta duração e avaliação neurológica (despertar rápido).</li><li><strong>Dose usual (infusão):</strong> 5 a 50 mcg/kg/minuto.</li><li><strong>Observações:</strong> Solução lipídica (atenção à contaminação e contagem de calorias). Pode causar hipotensão e depressão respiratória. Risco de Síndrome da Infusão do Propofol (PRIS) com doses altas e uso prolongado.</li></ul>
    <h4 style="border-bottom: 2px solid #007bff; padding-bottom: 5px;">Noradrenalina</h4><ul><li><strong>Indicação:</strong> Vasopressor de primeira escolha no choque séptico e outras formas de choque distributivo.</li><li><strong>Dose usual (infusão):</strong> 0.01 a 3 mcg/kg/minuto.</li><li><strong>Observações:</strong> Potente vasoconstritor (alfa-1 agonista). Deve ser infundida preferencialmente em acesso venoso central para evitar necrose tecidual por extravasamento.</li></ul>
    <h4 style="border-bottom: 2px solid #007bff; padding-bottom: 5px;">Remifentanil</h4><ul><li><strong>Indicação:</strong> Analgesia potente de ação ultracurta, ideal para procedimentos dolorosos de curta duração ou quando um despertar muito rápido é necessário.</li><li><strong>Dose usual (infusão):</strong> 0.05 a 0.2 mcg/kg/minuto.</li><li><strong>Observações:</strong> Metabolizado por esterases plasmáticas, não se acumula em insuficiência renal ou hepática. O efeito cessa minutos após a suspensão, exigindo planejamento de analgesia alternativa.</li></ul>
</div>`;

calculatorsHTML.chadsvasc = `
<div class="calculator-container">
  <h2>Calculadora de Escore CHA₂DS₂-VASc</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Avalia o risco de AVC em pacientes com Fibrilação Atrial (FA) não valvar para guiar a terapia de anticoagulação.</p>
  <div class="input-group"><label for="c2v-sex">Sexo Biológico</label><select id="c2v-sex"><option value="masculino">Masculino</option><option value="feminino">Feminino</option></select></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-c" value="1"><label for="c2v-c"><strong>C</strong>ongestive Heart Failure (Insuficiência Cardíaca Congestiva)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-h" value="1"><label for="c2v-h"><strong>H</strong>ypertension (Hipertensão Arterial)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-a2" value="2"><label for="c2v-a2"><strong>A</strong>ge ≥ 75 anos (<strong>2 pontos</strong>)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-d" value="1"><label for="c2v-d"><strong>D</strong>iabetes Mellitus</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-s2" value="2"><label for="c2v-s2"><strong>S</strong>troke / TIA / TE (AVC / AIT / Tromboembolismo prévio) (<strong>2 pontos</strong>)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-v" value="1"><label for="c2v-v"><strong>V</strong>ascular Disease (Doença Vascular: IAM prévio, Doença Arterial Periférica, Placa Aórtica)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="c2v-a" value="1"><label for="c2v-a"><strong>A</strong>ge 65-74 anos</label></div>
  <div class="button-group"><button id="c2v-calc-button">Calcular Escore</button><button id="c2v-reset-button" class="secondary">Reiniciar</button></div>
  <h3>Escore Total: <span id="c2v-result"></span></h3>
  <h4>Risco Anual de AVC e Recomendação Clínica: <span id="c2v-interpretation" style="font-weight: normal;"></span></h4>
</div>`;

calculatorsHTML.wells = `
<div class="calculator-container">
  <h2>Calculadora de Escore de Wells para Embolia Pulmonar (TEP)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Avalia a probabilidade pré-teste de TEP e ajuda a guiar a decisão sobre exames complementares (ex: Dímero-D, AngioTC).</p>
  <div class="checkbox-group"><input type="checkbox" id="wells-dvt" data-points="3"><label for="wells-dvt">Sinais clínicos de Trombose Venosa Profunda (TVP) (<strong>3 pontos</strong>)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="wells-diag" data-points="3"><label for="wells-diag">TEP como diagnóstico nº 1 ou igualmente provável (<strong>3 pontos</strong>)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="wells-hr" data-points="1.5"><label for="wells-hr">Frequência Cardíaca > 100 bpm (<strong>1.5 ponto</strong>)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="wells-imob" data-points="1.5"><label for="wells-imob">Imobilização (≥ 3 dias) ou cirurgia nas últimas 4 semanas (<strong>1.5 ponto</strong>)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="wells-prev" data-points="1.5"><label for="wells-prev">História de TVP ou TEP prévios (<strong>1.5 ponto</strong>)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="wells-hemop" data-points="1"><label for="wells-hemop">Hemoptise (<strong>1 ponto</strong>)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="wells-cancer" data-points="1"><label for="wells-cancer">Malignidade (em tratamento, paliativo ou diagnosticado nos últimos 6 meses) (<strong>1 ponto</strong>)</label></div>
  <div class="button-group"><button id="wells-calc-button">Calcular Escore</button><button id="wells-reset-button" class="secondary">Reiniciar</button></div>
  <h3>Escore Total: <span id="wells-result"></span></h3>
  <h4>Interpretação e Recomendação:</h4>
  <div id="wells-interpretation" style="padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px;"></div>
</div>`;

calculatorsHTML.pesi = `
<div class="calculator-container">
  <h2>Calculadora de Escore PESI e sPESI (Prognóstico da TEP)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Estratifica o risco de mortalidade em 30 dias em pacientes com TEP confirmada, ajudando a identificar candidatos a tratamento ambulatorial.</p>
  <div class="input-group"><label for="pesi-age">Idade do paciente (anos)</label><input type="number" id="pesi-age" placeholder="Ex: 70"></div>
  <div class="input-group"><label for="pesi-sex">Sexo Masculino</label><select id="pesi-sex"><option value="nao">Não</option><option value="sim">Sim</option></select></div>
  <div class="checkbox-group"><input type="checkbox" id="pesi-cancer"><label for="pesi-cancer">História de Câncer</label></div>
  <div class="checkbox-group"><input type="checkbox" id="pesi-chf"><label for="pesi-chf">História de Insuficiência Cardíaca Crônica</label></div>
  <div class="checkbox-group"><input type="checkbox" id="pesi-cpd"><label for="pesi-cpd">História de Doença Pulmonar Crônica</label></div>
  <div class="input-group"><label for="pesi-hr">Frequência Cardíaca (bpm)</label><select id="pesi-hr"><option value="nao">< 110 bpm</option><option value="sim">≥ 110 bpm</option></select></div>
  <div class="input-group"><label for="pesi-sbp">Pressão Arterial Sistólica (mmHg)</label><select id="pesi-sbp"><option value="nao">≥ 100 mmHg</option><option value="sim">< 100 mmHg</option></select></div>
  <div class="input-group"><label for="pesi-rr">Frequência Respiratória (ipm)</label><select id="pesi-rr"><option value="nao">< 30 ipm</option><option value="sim">≥ 30 ipm</option></select></div>
  <div class="input-group"><label for="pesi-temp">Temperatura Corporal</label><select id="pesi-temp"><option value="nao">≥ 36°C</option><option value="sim">< 36°C</option></select></div>
  <div class="input-group"><label for="pesi-ams">Alteração do Nível de Consciência</label><select id="pesi-ams"><option value="nao">Não</option><option value="sim">Sim (Confusão, desorientação, estupor ou coma)</option></select></div>
  <div class="input-group"><label for="pesi-sao2">Saturação de Oxigênio (SaO₂)</label><select id="pesi-sao2"><option value="nao">≥ 90%</option><option value="sim">< 90%</option></select></div>
  <div class="button-group"><button id="pesi-calc-button">Calcular Escores</button><button id="pesi-reset-button" class="secondary">Reiniciar</button></div>
  <div id="results-wrapper">
    <div class="result-box"><h3>Escore PESI</h3><p><strong>Pontuação:</strong> <span id="pesi-result">-</span></p><p><strong>Classe de Risco:</strong> <span id="pesi-class">-</span></p><p><strong>Mortalidade em 30d:</strong> <span id="pesi-mortality">-</span></p></div>
    <div class="result-box"><h3>Escore sPESI (Simplificado)</h3><p><strong>Pontuação:</strong> <span id="spesi-result">-</span></p><p><strong>Risco:</strong> <span id="spesi-class">-</span></p><p><strong>Mortalidade em 30d:</strong> <span id="spesi-mortality">-</span></p></div>
  </div>
  <h4>Recomendação de Manejo: <span id="pesi-recommendation" style="font-weight: normal;"></span></h4>
</div>`;

calculatorsHTML.curb65 = `
<div class="calculator-container">
  <h2>Calculadora de Escore CURB-65 (Gravidade da Pneumonia)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Avalia a mortalidade em 30 dias e ajuda a decidir o local de tratamento para Pneumonia Adquirida na Comunidade (PAC).</p>
  <div class="checkbox-group"><input type="checkbox" id="curb-c" data-points="1"><label for="curb-c"><strong>C</strong>onfusion (Confusão mental nova)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="curb-u" data-points="1"><label for="curb-u"><strong>U</strong>rea > 7 mmol/L (ou BUN > 19 mg/dL)</label></div>
  <div class="checkbox-group"><input type="checkbox" id="curb-r" data-points="1"><label for="curb-r"><strong>R</strong>espiratory Rate (Frequência Respiratória) ≥ 30 ipm</label></div>
  <div class="checkbox-group"><input type="checkbox" id="curb-b" data-points="1"><label for="curb-b"><strong>B</strong>lood Pressure (Pressão Arterial): Sistólica < 90 mmHg ou Diastólica ≤ 60 mmHg</label></div>
  <div class="checkbox-group"><input type="checkbox" id="curb-65" data-points="1"><label for="curb-65">Idade ≥ <strong>65</strong> anos</label></div>
  <div class="button-group"><button id="curb-calc-button">Calcular Escore</button><button id="curb-reset-button" class="secondary">Reiniciar</button></div>
  <h3>Escore Total: <span id="curb-result"></span></h3>
  <h4>Mortalidade e Recomendação de Manejo:</h4>
  <div id="curb-interpretation" style="padding: 10px; background-color: #e9ecef; border-radius: 4px; margin-top: 5px; line-height: 1.5;"></div>
</div>`;

calculatorsHTML.light = `
<div class="calculator-container">
  <h2>Calculadora de Critérios de Light (Derrame Pleural)</h2>
  <p style="font-size: 0.9em; opacity: 0.8;">Diferencia derrames pleurais em transudatos e exsudatos com base em análises do líquido pleural e do soro.</p>
  <h3 class="section-header">Valores do Líquido Pleural</h3>
  <div class="input-group"><label for="light-pleural-protein">Proteína do Líquido Pleural (g/dL)</label><input type="number" id="light-pleural-protein" placeholder="Ex: 4.5" step="0.1"></div>
  <div class="input-group"><label for="light-pleural-ldh">LDH do Líquido Pleural (U/L)</label><input type="number" id="light-pleural-ldh" placeholder="Ex: 350" step="1"></div>
  <h3 class="section-header">Valores do Soro (Sangue)</h3>
  <div class="input-group"><label for="light-serum-protein">Proteína Sérica (g/dL)</label><input type="number" id="light-serum-protein" placeholder="Ex: 7.0" step="0.1"></div>
  <div class="input-group"><label for="light-serum-ldh">LDH Sérico (U/L)</label><input type="number" id="light-serum-ldh" placeholder="Ex: 200" step="1"></div>
  <div class="input-group"><label for="light-ldh-limit">Limite Superior da Normalidade do LDH Sérico (U/L)</label><input type="number" id="light-ldh-limit" placeholder="Ex: 250" step="1"></div>
  <div class="button-group"><button id="light-calc-button">Analisar Critérios</button><button id="light-reset-button" class="secondary">Reiniciar</button></div>
  <div id="light-interpretation" style="padding: 15px; background-color: #e9ecef; border-radius: 4px; margin-top: 20px; line-height: 1.6;"></div>
</div>`;

calculatorsHTML.seringa = `
<div class="calculator-container" style="background-color: #f5f7fa;">
  <h2 style="text-align: center; color: #2c3e50; border-bottom: 2px solid #3498db; padding-bottom: 10px; margin-bottom: 5px;">Calculadora de Preparo de Seringa por Objetivo</h2>
  <p style="text-align: center; font-size: 0.9em; color: #555; margin-bottom: 25px;">Calcule a quantidade de droga necessária para atingir uma dose alvo durante um tempo específico.</p>
  <h3 class="section-header">1. Defina a Dose e o Peso</h3>
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 15px;">
    <div class="input-group"><label for="prep-dose">Dose Alvo</label><input type="number" id="prep-dose" placeholder="Ex: 0.1"></div>
    <div class="input-group"><label for="prep-dose-unit">Unidade da Dose</label><select id="prep-dose-unit"><option value="mg/kg/h">mg/kg/h</option><option value="mcg/kg/h">mcg/kg/h</option><option value="mcg/kg/min" selected>mcg/kg/min</option></select></div>
    <div class="input-group"><label for="prep-weight">Peso do Paciente (kg)</label><input type="number" id="prep-weight" placeholder="Ex: 70"></div>
  </div>
  <p style="background-color: #ecf0f1; padding: 8px; border-radius: 4px; margin-top: 10px; font-size: 0.95em;"><strong>Dose Total Individualizada:</strong> <span id="total-dose-result">-</span></p>
  <h3 class="section-header">2. Escolha o Volume e a Duração</h3>
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 15px;">
    <div class="input-group"><label for="prep-volume">Volume Total da Solução (mL)</label><input type="number" id="prep-volume" placeholder="Ex: 50"></div>
    <div class="input-group"><label for="prep-duration">Duração da Infusão (horas)</label><input type="number" id="prep-duration" placeholder="Ex: 12"></div>
  </div>
  <p style="background-color: #ecf0f1; padding: 8px; border-radius: 4px; margin-top: 10px; font-size: 0.95em;"><strong>Velocidade de Infusão (Bomba):</strong> <span id="infusion-rate-result">-</span></p>
  <div class="button-group"><button id="prep-calc-button" style="font-size: 1.05em; font-weight: bold;">Calcular Preparo</button><button id="prep-reset-button" class="secondary" style="font-size: 1.05em; font-weight: bold;">Reiniciar</button></div>
  <div id="final-results-wrapper" style="display: none;">
    <h3 class="section-header">3. Resultado do Preparo da Seringa</h3>
    <div class="result-box" style="background-color: #e9f5ff; border-color: #aed6f1;"><h4 style="color: #2c3e50;">Passo 4: Concentração Necessária</h4><p id="concentration-result" style="font-size: 1.2em;">-</p></div>
    <div class="result-box" style="background-color: #d4efdf; border-color: #7dcea0; margin-top:10px;"><h4 style="color: #2c3e50;">Passo 5: Total de Droga a Adicionar</h4><p id="total-drug-result" style="color: #1e8449; font-size: 1.4em; text-align: center;">-</p></div>
  </div>
</div>`;


// --- ETAPA 3: ESTRUTURA PRINCIPAL E MENU ---
// Cria o menu e os contêineres para cada calculadora.
const mainContainer = dv.container;

mainContainer.innerHTML = `
  <div id="med-calc-menu">
    <button data-target="ich">ICH</button>
    <button data-target="sirs">SIRS</button>
    <button data-target="qsofa">qSOFA</button>
    <button data-target="sofa">SOFA</button>
    <button data-target="nihss">NIHSS</button>
    <button data-target="mdrd">MDRD</button>
    <button data-target="sedo">Sedoanalgesia</button>
    <button data-target="chadsvasc">CHA₂DS₂-VASc</button>
    <button data-target="wells">Wells (TEP)</button>
    <button data-target="pesi">PESI/sPESI</button>
    <button data-target="curb65">CURB-65</button>
    <button data-target="light">Light</button>
    <button data-target="seringa">Preparo Seringa</button>
  </div>
  <div id="calculator-display-area">
    <div id="ich-container" class="calculator-content"></div>
    <div id="sirs-container" class="calculator-content"></div>
    <div id="qsofa-container" class="calculator-content"></div>
    <div id="sofa-container" class="calculator-content"></div>
    <div id="nihss-container" class="calculator-content"></div>
    <div id="mdrd-container" class="calculator-content"></div>
    <div id="sedo-container" class="calculator-content"></div>
    <div id="chadsvasc-container" class="calculator-content"></div>
    <div id="wells-container" class="calculator-content"></div>
    <div id="pesi-container" class="calculator-content"></div>
    <div id="curb65-container" class="calculator-content"></div>
    <div id="light-container" class="calculator-content"></div>
    <div id="seringa-container" class="calculator-content"></div>
  </div>
`;

// Injeta os estilos CSS no documento
const styleEl = document.createElement('style');
styleEl.innerHTML = globalStyles;
mainContainer.appendChild(styleEl);


// --- ETAPA 4: LÓGICA DE CÁLCULO E EVENTOS ---
// Um objeto que armazena as funções de inicialização de cada calculadora.
const calculatorsLogic = {
    // Flag para saber se os eventos já foram adicionados
    initialized: {},

    // Função para obter elementos do DOM de forma segura
    getEl: (selector) => mainContainer.querySelector(selector),

    // --- Lógica para cada Calculadora ---
    init_ich: () => {
        const button = calculatorsLogic.getEl('#ich-button');
        if (button) button.addEventListener('click', () => {
            const get = (id) => parseInt(calculatorsLogic.getEl('#' + id).value);
            const score = get('glasgow') + get('idade-ich') + get('local-hematoma') + get('volume-hematoma') + get('hemoventriculo');
            calculatorsLogic.getEl('#ich-result').innerText = score;
            const mortalityMap = {0: '0%', 1: '13%', 2: '26%', 3: '72%', 4: '97%', 5: '100%', 6: '100%'};
            calculatorsLogic.getEl('#ich-mortality').innerText = mortalityMap[score] || "N/A";
        });
    },

    init_sirs: () => {
        calculatorsLogic.getEl('#sirs-calc-button')?.addEventListener('click', () => {
            let score = 0;
            if (calculatorsLogic.getEl('#sirs-temp').checked) score++;
            if (calculatorsLogic.getEl('#sirs-hr').checked) score++;
            if (calculatorsLogic.getEl('#sirs-rr').checked) score++;
            if (calculatorsLogic.getEl('#sirs-wbc').checked) score++;
            calculatorsLogic.getEl('#sirs-result').innerText = `${score} de 4`;
            const interp = calculatorsLogic.getEl('#sirs-interpretation');
            if (score >= 2) {
              interp.innerText = "Critérios para SIRS presentes. Se houver suspeita de infecção, isso caracteriza Sepse (pela definição Sepsis-2).";
              interp.style.color = 'darkred';
            } else {
              interp.innerText = "Critérios para SIRS não preenchidos.";
              interp.style.color = 'black';
            }
        });
        calculatorsLogic.getEl('#sirs-reset-button')?.addEventListener('click', () => {
            mainContainer.querySelectorAll('#sirs-container input[type="checkbox"]').forEach(c => c.checked = false);
            calculatorsLogic.getEl('#sirs-result').innerText = "";
            calculatorsLogic.getEl('#sirs-interpretation').innerText = "";
        });
    },

    init_qsofa: () => {
        calculatorsLogic.getEl('#qsofa-button')?.addEventListener('click', () => {
            let score = 0;
            if (calculatorsLogic.getEl('#respiratory-rate').checked) score++;
            if (calculatorsLogic.getEl('#mental-status').checked) score++;
            if (calculatorsLogic.getEl('#systolic-bp').checked) score++;
            calculatorsLogic.getEl('#qsofa-result').innerText = score;
            const interp = calculatorsLogic.getEl('#qsofa-interpretation');
            interp.innerText = (score >= 2) ? "Risco aumentado de desfechos desfavoráveis. Considerar sepse." : "Baixo risco.";
        });
    },

    init_sofa: () => {
        calculatorsLogic.getEl('#sofa-button')?.addEventListener('click', () => {
            const get = (id) => parseInt(calculatorsLogic.getEl('#' + id).value);
            const score = get('respiration') + get('coagulation') + get('liver') + get('cardiovascular') + get('cns') + get('renal');
            calculatorsLogic.getEl('#sofa-result').innerText = score;
            const interp = calculatorsLogic.getEl('#sofa-interpretation');
            interp.innerText = (score >= 2) ? "Risco aumentado de disfunção orgânica. Em paciente com infecção, um aumento ≥ 2 pontos indica sepse." : "Baixo risco de disfunção orgânica significativa.";
        });
    },

    init_nihss: () => {
        calculatorsLogic.getEl('#nihss-button')?.addEventListener('click', () => {
            const get = (id) => parseInt(calculatorsLogic.getEl('#' + id).value);
            const score = get('item1a') + get('item1b') + get('item1c') + get('item2') + get('item3') + get('item4') + get('item5a') + get('item5b') + get('item6a') + get('item6b') + get('item7') + get('item8') + get('item9') + get('item10') + get('item11');
            calculatorsLogic.getEl('#nihss-result').innerText = score;
            let interp = "";
            if (score === 0) interp = "Sem sintomas de AVC.";
            else if (score <= 4) interp = "AVC Menor. Prognóstico geralmente excelente.";
            else if (score <= 15) interp = "AVC Moderado. Necessária reabilitação.";
            else if (score <= 20) interp = "AVC Moderado a Grave. Alta probabilidade de déficit significativo.";
            else interp = "AVC Grave. Alta probabilidade de dependência ou morte.";
            calculatorsLogic.getEl('#nihss-interpretation').innerText = interp;
        });
        calculatorsLogic.getEl('#nihss-reset-button')?.addEventListener('click', () => {
            mainContainer.querySelectorAll('#nihss-container select').forEach(s => s.selectedIndex = 0);
            calculatorsLogic.getEl('#nihss-result').innerText = "";
            calculatorsLogic.getEl('#nihss-interpretation').innerText = "";
        });
    },
    
    init_mdrd: () => {
        calculatorsLogic.getEl('#mdrd-calc-button')?.addEventListener('click', () => {
            const creat = parseFloat(calculatorsLogic.getEl('#mdrd-creat').value);
            const age = parseInt(calculatorsLogic.getEl('#mdrd-age').value);
            if (isNaN(creat) || isNaN(age) || creat <= 0 || age <= 0) {
                calculatorsLogic.getEl('#mdrd-result').innerText = "Por favor, insira valores válidos.";
                return;
            }
            let tfg = 175 * Math.pow(creat, -1.154) * Math.pow(age, -0.203);
            if (calculatorsLogic.getEl('#mdrd-sex').value === 'feminino') tfg *= 0.742;
            if (calculatorsLogic.getEl('#mdrd-ethnicity').checked) tfg *= 1.212;
            calculatorsLogic.getEl('#mdrd-result').innerText = `${tfg.toFixed(2)} mL/min/1.73 m²`;
            let stageText = "";
            if (tfg >= 90) stageText = "Estágio 1: Normal ou alta.";
            else if (tfg >= 60) stageText = "Estágio 2: Levemente diminuída.";
            else if (tfg >= 45) stageText = "Estágio 3a: Leve a moderadamente diminuída.";
            else if (tfg >= 30) stageText = "Estágio 3b: Moderada a gravemente diminuída.";
            else if (tfg >= 15) stageText = "Estágio 4: Gravemente diminuída.";
            else stageText = "Estágio 5: Falência renal (TFG < 15).";
            calculatorsLogic.getEl('#mdrd-stage').innerText = stageText;
        });
        calculatorsLogic.getEl('#mdrd-reset-button')?.addEventListener('click', () => {
            mainContainer.querySelectorAll('#mdrd-container input, #mdrd-container select').forEach(el => {
                if(el.type === 'checkbox') el.checked = false;
                else if (el.tagName === 'SELECT') el.selectedIndex = 0;
                else el.value = '';
            });
            calculatorsLogic.getEl('#mdrd-result').innerText = "";
            calculatorsLogic.getEl('#mdrd-stage').innerText = "";
        });
    },

    init_sedo: () => {
        const drugData = {
            fentanyl: { drugUnit: "mcg", doseUnit: "mcg/kg/hora", weightBased: true, doseFactor: 1, conversion: 1 },
            midazolam: { drugUnit: "mg", doseUnit: "mg/kg/hora", weightBased: true, doseFactor: 1, conversion: 1000 },
            propofol: { drugUnit: "mg", doseUnit: "mcg/kg/min", weightBased: true, doseFactor: 60, conversion: 1000 },
            noradrenaline: { drugUnit: "mg", doseUnit: "mcg/kg/min", weightBased: true, doseFactor: 60, conversion: 1000 },
            remifentanil: { drugUnit: "mg", doseUnit: "mcg/kg/min", weightBased: true, doseFactor: 60, conversion: 1000 }
        };
        const updateUI = () => {
            const selectedDrug = drugData[calculatorsLogic.getEl('#drug-select').value];
            calculatorsLogic.getEl('#drug-unit-label').textContent = selectedDrug.drugUnit;
            calculatorsLogic.getEl('#dose-unit-label').textContent = selectedDrug.doseUnit;
        };
        calculatorsLogic.getEl('#drug-select')?.addEventListener('change', updateUI);
        calculatorsLogic.getEl('#sedo-calc-button')?.addEventListener('click', () => {
            const selectedDrug = drugData[calculatorsLogic.getEl('#drug-select').value];
            const drugAmount = parseFloat(calculatorsLogic.getEl('#drug-amount').value);
            const totalVolume = parseFloat(calculatorsLogic.getEl('#total-volume').value);
            const weight = parseFloat(calculatorsLogic.getEl('#patient-weight').value);
            const prescribedDose = parseFloat(calculatorsLogic.getEl('#prescribed-dose').value);
            if ([drugAmount, totalVolume, weight, prescribedDose].some(isNaN) || totalVolume <= 0) {
                alert("Preencha todos os campos com valores válidos."); return;
            }
            const concentrationMcgMl = (drugAmount * selectedDrug.conversion) / totalVolume;
            calculatorsLogic.getEl('#drug-concentration').textContent = `${concentrationMcgMl.toFixed(2)} mcg/mL`;
            const totalDoseMcgPerHour = prescribedDose * weight * selectedDrug.doseFactor;
            const infusionRate = totalDoseMcgPerHour / concentrationMcgMl;
            calculatorsLogic.getEl('#infusion-rate').textContent = `${infusionRate.toFixed(2)} mL/h`;
        });
        calculatorsLogic.getEl('#sedo-reset-button')?.addEventListener('click', () => {
            calculatorsLogic.getEl('#drug-amount').value = '';
            calculatorsLogic.getEl('#total-volume').value = '';
            calculatorsLogic.getEl('#patient-weight').value = '';
            calculatorsLogic.getEl('#prescribed-dose').value = '';
            calculatorsLogic.getEl('#drug-concentration').textContent = '-';
            calculatorsLogic.getEl('#infusion-rate').textContent = '-';
        });
        updateUI(); // Initial call
    },

    init_chadsvasc: () => {
        calculatorsLogic.getEl('#c2v-calc-button')?.addEventListener('click', () => {
            let score = 0;
            if (calculatorsLogic.getEl('#c2v-sex').value === 'feminino') score += 1;
            mainContainer.querySelectorAll('#chadsvasc-container .checkbox-group input:checked').forEach(box => {
                if (box.id === 'c2v-a' && calculatorsLogic.getEl('#c2v-a2').checked) return;
                score += parseInt(box.value);
            });
            calculatorsLogic.getEl('#c2v-result').innerText = score;
            let recommendation = "";
            if (calculatorsLogic.getEl('#c2v-sex').value === 'masculino') {
                if (score === 0) recommendation = "Risco muito baixo. Anticoagulação não é recomendada.";
                else if (score === 1) recommendation = "Risco baixo a moderado. Considerar anticoagulação.";
                else recommendation = "Risco moderado a alto. Anticoagulação é recomendada.";
            } else { // Feminino
                if (score <= 1) recommendation = "Risco muito baixo. Anticoagulação não é recomendada.";
                else if (score === 2) recommendation = "Risco baixo a moderado. Considerar anticoagulação.";
                else recommendation = "Risco moderado a alto. Anticoagulação é recomendada.";
            }
            calculatorsLogic.getEl('#c2v-interpretation').innerText = recommendation;
        });
        calculatorsLogic.getEl('#c2v-reset-button')?.addEventListener('click', () => {
            mainContainer.querySelectorAll('#chadsvasc-container input[type="checkbox"]').forEach(c => c.checked = false);
            calculatorsLogic.getEl('#c2v-sex').selectedIndex = 0;
            calculatorsLogic.getEl('#c2v-result').innerText = "";
            calculatorsLogic.getEl('#c2v-interpretation').innerText = "";
        });
    },

    init_wells: () => {
        calculatorsLogic.getEl('#wells-calc-button')?.addEventListener('click', () => {
            let score = 0;
            mainContainer.querySelectorAll('#wells-container input:checked').forEach(box => score += parseFloat(box.dataset.points));
            calculatorsLogic.getEl('#wells-result').innerText = score;
            let interp = "";
            if (score > 4) interp += "<strong>Modelo 2 Níveis:</strong> TEP Provável. Recomenda-se AngioTC de tórax.<br>";
            else interp += "<strong>Modelo 2 Níveis:</strong> TEP Improvável. Recomenda-se Dímero-D.<br><br>";
            if (score > 6) interp += "<strong>Modelo 3 Níveis:</strong> Alto Risco.";
            else if (score >= 2) interp += "<strong>Modelo 3 Níveis:</strong> Risco Moderado.";
            else interp += "<strong>Modelo 3 Níveis:</strong> Baixo Risco.";
            calculatorsLogic.getEl('#wells-interpretation').innerHTML = interp;
        });
        calculatorsLogic.getEl('#wells-reset-button')?.addEventListener('click', () => {
            mainContainer.querySelectorAll('#wells-container input[type="checkbox"]').forEach(c => c.checked = false);
            calculatorsLogic.getEl('#wells-result').innerText = "";
            calculatorsLogic.getEl('#wells-interpretation').innerHTML = "";
        });
    },

    init_pesi: () => {
        calculatorsLogic.getEl('#pesi-calc-button')?.addEventListener('click', () => {
            const get = (id) => calculatorsLogic.getEl('#' + id);
            const age = parseInt(get('pesi-age').value);
            if (isNaN(age)) { alert("Insira a idade."); return; }
            let pesiScore = age + (get('pesi-sex').value === 'sim' ? 10 : 0) + (get('pesi-cancer').checked ? 30 : 0) + (get('pesi-chf').checked ? 10 : 0) + (get('pesi-cpd').checked ? 10 : 0) + (get('pesi-hr').value === 'sim' ? 20 : 0) + (get('pesi-sbp').value === 'sim' ? 30 : 0) + (get('pesi-rr').value === 'sim' ? 20 : 0) + (get('pesi-temp').value === 'sim' ? 20 : 0) + (get('pesi-ams').value === 'sim' ? 60 : 0) + (get('pesi-sao2').value === 'sim' ? 20 : 0);
            let spesiScore = (age > 80 ? 1 : 0) + (get('pesi-cancer').checked ? 1 : 0) + ((get('pesi-chf').checked || get('pesi-cpd').checked) ? 1 : 0) + (get('pesi-hr').value === 'sim' ? 1 : 0) + (get('pesi-sbp').value === 'sim' ? 1 : 0) + (get('pesi-sao2').value === 'sim' ? 1 : 0);
            get('pesi-result').innerText = pesiScore;
            let pesiClass = "", pesiMortality = "";
            if (pesiScore <= 65) { pesiClass = "I"; pesiMortality = "0-1.6%"; }
            else if (pesiScore <= 85) { pesiClass = "II"; pesiMortality = "1.7-3.5%"; }
            else if (pesiScore <= 105) { pesiClass = "III"; pesiMortality = "3.2-7.1%"; }
            else if (pesiScore <= 125) { pesiClass = "IV"; pesiMortality = "4.0-11.4%"; }
            else { pesiClass = "V"; pesiMortality = "10.0-24.5%"; }
            get('pesi-class').innerText = pesiClass;
            get('pesi-mortality').innerText = pesiMortality;
            get('spesi-result').innerText = spesiScore;
            get('spesi-class').innerText = spesiScore === 0 ? "Baixo Risco" : "Alto Risco";
            get('spesi-mortality').innerText = spesiScore === 0 ? "~1.0%" : "~10.9%";
            get('pesi-recommendation').innerText = spesiScore === 0 ? "Risco baixo. Considerar tratamento ambulatorial." : "Risco alto. Internação hospitalar recomendada.";
        });
        calculatorsLogic.getEl('#pesi-reset-button')?.addEventListener('click', () => {
             mainContainer.querySelectorAll('#pesi-container input, #pesi-container select').forEach(el => {
                if(el.type === 'checkbox') el.checked = false;
                else if (el.type === 'number') el.value = '';
                else el.selectedIndex = 0;
            });
            ['pesi-result', 'pesi-class', 'pesi-mortality', 'spesi-result', 'spesi-class', 'spesi-mortality', 'pesi-recommendation'].forEach(id => calculatorsLogic.getEl('#'+id).innerText = '-');
        });
    },

    init_curb65: () => {
        calculatorsLogic.getEl('#curb-calc-button')?.addEventListener('click', () => {
            let score = 0;
            mainContainer.querySelectorAll('#curb65-container input:checked').forEach(box => score += parseInt(box.dataset.points));
            calculatorsLogic.getEl('#curb-result').innerText = score;
            let interp = "";
            if (score <= 1) interp = "<strong>Grupo 1 (Baixo Risco):</strong> Mortalidade ~1.5%. Considerar tratamento ambulatorial.";
            else if (score === 2) interp = "<strong>Grupo 2 (Risco Moderado):</strong> Mortalidade ~9.2%. Considerar internação hospitalar.";
            else interp = "<strong>Grupo 3 (Alto Risco):</strong> Mortalidade ~22%. Internação hospitalar urgente, avaliar UTI.";
            calculatorsLogic.getEl('#curb-interpretation').innerHTML = interp;
        });
        calculatorsLogic.getEl('#curb-reset-button')?.addEventListener('click', () => {
            mainContainer.querySelectorAll('#curb65-container input[type="checkbox"]').forEach(c => c.checked = false);
            calculatorsLogic.getEl('#curb-result').innerText = "";
            calculatorsLogic.getEl('#curb-interpretation').innerHTML = "";
        });
    },
    
    init_light: () => {
        calculatorsLogic.getEl('#light-calc-button')?.addEventListener('click', () => {
            const pProt = parseFloat(calculatorsLogic.getEl('#light-pleural-protein').value);
            const sProt = parseFloat(calculatorsLogic.getEl('#light-serum-protein').value);
            const pLDH = parseFloat(calculatorsLogic.getEl('#light-pleural-ldh').value);
            const sLDH = parseFloat(calculatorsLogic.getEl('#light-serum-ldh').value);
            const ldhLimit = parseFloat(calculatorsLogic.getEl('#light-ldh-limit').value);
            if ([pProt, sProt, pLDH, sLDH, ldhLimit].some(isNaN)) { alert("Preencha todos os campos."); return; }
            const proteinRatio = pProt / sProt;
            const ldhRatio = pLDH / sLDH;
            const ldhLimitCheck = (2/3) * ldhLimit;
            const isExudate = proteinRatio > 0.5 || ldhRatio > 0.6 || pLDH > ldhLimitCheck;
            let resultHTML = "<h4>Análise dos Critérios:</h4><ul>";
            resultHTML += `<li>Proteína Pleural / Sérica > 0.5: <strong>${proteinRatio > 0.5 ? 'SIM' : 'NÃO'}</strong> (Ratio: ${proteinRatio.toFixed(2)})</li>`;
            resultHTML += `<li>LDH Pleural / Sérico > 0.6: <strong>${ldhRatio > 0.6 ? 'SIM' : 'NÃO'}</strong> (Ratio: ${ldhRatio.toFixed(2)})</li>`;
            resultHTML += `<li>LDH Pleural > 2/3 do LSN: <strong>${pLDH > ldhLimitCheck ? 'SIM' : 'NÃO'}</strong></li></ul>`;
            if (isExudate) {
                resultHTML += `<div class="result-final exudate">Diagnóstico: EXSUDATO</div><strong>Causas Comuns:</strong> Infecção, Neoplasia, Embolia, etc.`;
            } else {
                resultHTML += `<div class="result-final transudate">Diagnóstico: TRANSUDATO</div><strong>Causas Comuns:</strong> Insuficiência Cardíaca, Cirrose, etc.`;
            }
            calculatorsLogic.getEl('#light-interpretation').innerHTML = resultHTML;
        });
        calculatorsLogic.getEl('#light-reset-button')?.addEventListener('click', () => {
            mainContainer.querySelectorAll('#light-container input').forEach(i => i.value = '');
            calculatorsLogic.getEl('#light-interpretation').innerHTML = "";
        });
    },

    init_seringa: () => {
        const calculate = () => {
            const dose = parseFloat(calculatorsLogic.getEl('#prep-dose').value);
            const unit = calculatorsLogic.getEl('#prep-dose-unit').value;
            const weight = parseFloat(calculatorsLogic.getEl('#prep-weight').value);
            const volume = parseFloat(calculatorsLogic.getEl('#prep-volume').value);
            const duration = parseFloat(calculatorsLogic.getEl('#prep-duration').value);
            if ([dose, weight, volume, duration].some(isNaN) || [weight, volume, duration].some(v => v <= 0)) {
                alert("Preencha todos os campos com valores positivos."); return;
            }
            let doseMgPerHour = 0;
            if (unit === 'mg/kg/h') doseMgPerHour = dose * weight;
            else if (unit === 'mcg/kg/h') doseMgPerHour = (dose * weight) / 1000;
            else doseMgPerHour = (dose * weight * 60) / 1000;
            const infusionRate = volume / duration;
            const concentrationMgMl = doseMgPerHour / infusionRate;
            const totalDrugMg = concentrationMgMl * volume;
            
            calculatorsLogic.getEl('#total-dose-result').textContent = `${doseMgPerHour.toFixed(3)} mg/h`;
            calculatorsLogic.getEl('#infusion-rate-result').textContent = `${infusionRate.toFixed(2)} mL/h`;
            calculatorsLogic.getEl('#concentration-result').textContent = `${concentrationMgMl.toFixed(3)} mg/mL`;
            calculatorsLogic.getEl('#total-drug-result').textContent = `${totalDrugMg.toFixed(2)} mg`;
            calculatorsLogic.getEl('#final-results-wrapper').style.display = 'block';
        };
        const reset = () => {
            mainContainer.querySelectorAll('#seringa-container input').forEach(i => i.value = '');
            calculatorsLogic.getEl('#final-results-wrapper').style.display = 'none';
             ['total-dose-result', 'infusion-rate-result', 'concentration-result', 'total-drug-result'].forEach(id => calculatorsLogic.getEl('#'+id).textContent = '-');
        };
        calculatorsLogic.getEl('#prep-calc-button')?.addEventListener('click', calculate);
        calculatorsLogic.getEl('#prep-reset-button')?.addEventListener('click', reset);
    }
};


// --- ETAPA 5: CONTROLADOR PRINCIPAL DO MENU ---
// Adiciona o listener de evento ao menu para gerenciar a exibição.
const menu = calculatorsLogic.getEl('#med-calc-menu');
menu.addEventListener('click', (event) => {
    const target = event.target;
    if (target.tagName !== 'BUTTON') return;

    const calculatorId = target.dataset.target;
    const containerId = `${calculatorId}-container`;
    const targetContainer = calculatorsLogic.getEl(`#${containerId}`);

    // Gerencia a classe 'active' para os botões e contêineres
    menu.querySelectorAll('button').forEach(btn => btn.classList.remove('active'));
    target.classList.add('active');
    
    mainContainer.querySelectorAll('.calculator-content').forEach(cont => cont.classList.remove('active'));
    targetContainer.classList.add('active');

    // "Lazy Load": Renderiza o HTML e a lógica da calculadora apenas na primeira vez que é clicada.
    if (!calculatorsLogic.initialized[calculatorId]) {
        targetContainer.innerHTML = calculatorsHTML[calculatorId];
        const initFunction = `init_${calculatorId}`;
        if (typeof calculatorsLogic[initFunction] === 'function') {
            calculatorsLogic[initFunction]();
        }
        calculatorsLogic.initialized[calculatorId] = true;
    }
});

// Opcional: Ativa a primeira calculadora por padrão ao carregar a nota.
menu.querySelector('button')?.click();
```