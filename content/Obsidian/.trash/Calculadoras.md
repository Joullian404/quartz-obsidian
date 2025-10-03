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
  
  <button onclick="calculateSOFA()">Calcular SOFA</button>
  
  <h3>Resultado: <span id="sofa-result"></span></h3>
</div>

<script>
  function calculateSOFA() {
    const respiration = parseInt(document.getElementById('respiration').value);
    const coagulation = parseInt(document.getElementById('coagulation').value);
    const liver = parseInt(document.getElementById('liver').value);
    const cardiovascular = parseInt(document.getElementById('cardiovascular').value);
    const cns = parseInt(document.getElementById('cns').value);
    const renal = parseInt(document.getElementById('renal').value);
    
    const totalScore = respiration + coagulation + liver + cardiovascular + cns + renal;
    
    document.getElementById('sofa-result').innerText = totalScore;
  }
</script>

<style>
  .calculator-container {
    background-color: #f0f0f0;
    padding: 20px;
    border-radius: 8px;
    font-family: sans-serif;
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
  }
  button:hover {
    background-color: #0056b3;
  }
</style>