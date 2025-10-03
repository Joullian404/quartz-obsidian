```dataviewjs
// Estilos CSS para a aparência do questionário
const style = `
<style>
  body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; line-height: 1.6; color: #333; background-color: #fdfdfd; margin: 0; padding: 20px; }
  h1 { text-align: center; color: #333; }
  .quiz-container { background-color: #fff; border: 1px solid #ddd; border-radius: 8px; padding: 20px; margin-bottom: 25px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
  .quiz-container h4 { margin-top: 0; color: #0056b3; border-bottom: 2px solid #e0e0e0; padding-bottom: 10px; }
  .quiz-container .options label { display: block; margin: 10px 0; padding: 12px; border: 1px solid #eee; border-radius: 5px; cursor: pointer; transition: background-color 0.3s, border-color 0.3s; }
  .quiz-container .options label:hover { background-color: #f0f8ff; border-color: #b3d7ff; }
  .quiz-container .options .correct-answer { background-color: #d4edda !important; border-color: #c3e6cb !important; color: #155724; font-weight: bold; }
  .quiz-container .options .incorrect-selection { background-color: #f8d7da !important; border-color: #f5c6cb !important; color: #721c24; text-decoration: line-through; }
  .quiz-container button { margin-top: 15px; padding: 10px 20px; border: none; background-color: #007bff; color: white; border-radius: 5px; cursor: pointer; font-size: 16px; transition: background-color 0.3s; }
  .quiz-container button:hover { background-color: #0056b3; }
  .quiz-container button:disabled { background-color: #ccc; cursor: not-allowed; }
  .quiz-container table { width: 100%; border-collapse: collapse; margin: 15px 0; }
  .quiz-container th, .quiz-container td { border: 1px solid #ddd; padding: 8px; text-align: left; }
</style>
`;

// Conteúdo HTML de todas as questões
const html = `
<h1>Questionário Interativo: Intoxicações Exógenas</h1>

<!-- Questão 1 -->
<div class="quiz-container" id="quiz-1">
  <h4>Questão 1</h4>
  <p>Quanto à intoxicação exógena, considere as seguintes possibilidades de quadros clínicos, agentes causadores e medidas de tratamento específicas.</p>
  <table>
    <tr><td><b>paciente A:</b></td><td>pupilas rapidamente variáveis, convulsão, pele fria, bradicardia</td></tr>
    <tr><td><b>paciente B:</b></td><td>pupilas mióticas, broncorreia, hipersalivação, bradicardia</td></tr>
    <tr><td><b>paciente C:</b></td><td>pupilas muito mióticas, hipoventilação, bradipneia</td></tr>
  </table>
  <table>
    <tr><td><b>agente 1:</b></td><td>opioide</td></tr>
    <tr><td><b>agente 2:</b></td><td>betabloqueador</td></tr>
    <tr><td><b>agente 3:</b></td><td>organofosforado</td></tr>
  </table>
  <table>
    <tr><td><b>medida X:</b></td><td>glucagon, gluconato de cálcio</td></tr>
    <tr><td><b>medida Y:</b></td><td>naloxone</td></tr>
    <tr><td><b>medida Z:</b></td><td>atropina e pralidoxima</td></tr>
  </table>
  <p>A partir dessas informações, assinale a alternativa que apresenta a correlação mais adequada entre o quadro clínico, o agente causador e a medida de tratamento.</p>
  <div class="options">
    <label><input type="radio" name="q1" value="A"> A) A-1-X; B-2-Y; C-3-Z</label>
    <label><input type="radio" name="q1" value="B"> B) A-2-X; B-3-Z; C-1-Y</label>
    <label><input type="radio" name="q1" value="C"> C) A-3-Z; B-1-Y; C-2-X</label>
    <label><input type="radio" name="q1" value="D"> D) A-1-Z; B-2-X; C-3-Y</label>
    <label><input type="radio" name="q1" value="E"> E) A-2-Y; B-1-X; C-3-Z</label>
  </div>
  <button data-question="1" data-correct="B">Conferir</button>
</div>

<!-- Questão 2 -->
<div class="quiz-container" id="quiz-2">
  <h4>Questão 2</h4>
  <p>Homem, 55 anos, é trazido ao pronto-socorro após ingerir grande quantidade de uma substância que causou quadro de sudorese profusa, bradicardia, miose, hipotensão e broncorreia.</p>
  <p>Qual é a substância que apresentaria efeito similar quando ingerida em grande quantidade?</p>
  <div class="options">
    <label><input type="radio" name="q2" value="A"> A) Loperamida.</label>
    <label><input type="radio" name="q2" value="B"> B) Rivastigmina.</label>
    <label><input type="radio" name="q2" value="C"> C) Escopolamina.</label>
    <label><input type="radio" name="q2" value="D"> D) Imipramina.</label>
  </div>
  <button data-question="2" data-correct="B">Conferir</button>
</div>

<!-- Questão 3 -->
<div class="quiz-container" id="quiz-3">
  <h4>Questão 3</h4>
  <p>Um menino de dois anos de idade, previamente hígido, foi levado ao pronto-socorro infantil com histórico de sonolência súbita...</p>
  <p>Entre as alternativas a seguir, assinale aquela que apresenta a provável causa da intoxicação exógena no caso clínico acima e o seu tratamento adequado, respectivamente:</p>
  <div class="options">
    <label><input type="radio" name="q3" value="A"> A) morfina — naloxona</label>
    <label><input type="radio" name="q3" value="B"> B) nafazolina — naloxona</label>
    <label><input type="radio" name="q3" value="C"> C) nafazolina — medidas de suporte</label>
    <label><input type="radio" name="q3" value="D"> D) morfina — medidas de suporte</label>
    <label><input type="radio" name="q3" value="E"> E) morfina — flumazenil</label>
  </div>
  <button data-question="3" data-correct="C">Conferir</button>
</div>

<!-- Questão 4 -->
<div class="quiz-container" id="quiz-4">
  <h4>Questão 4</h4>
  <p>São considerados medicamentos que causam quadro de intoxicação com alteração pupilar tipo midríase:</p>
  <div class="options">
    <label><input type="radio" name="q4" value="A"> A) opioides.</label>
    <label><input type="radio" name="q4" value="B"> B) anticolinérgicos.</label>
    <label><input type="radio" name="q4" value="C"> C) colinérgicos.</label>
    <label><input type="radio" name="q4" value="D"> D) carbamatos.</label>
    <label><input type="radio" name="q4" value="E"> E) fenotiazidas.</label>
  </div>
  <button data-question="4" data-correct="B">Conferir</button>
</div>

<!-- Questão 5 -->
<div class="quiz-container" id="quiz-5">
  <h4>Questão 5</h4>
  <p>Menino, 2 anos de idade, é levado à UPA com relato de sonolência, naúseas e vômitos há 50 minutos...</p>
  <p>No caso de ocorrer a complicação, considere as opções abaixo e indique a conduta adequada:</p>
  <div class="options">
    <label><input type="radio" name="q5" value="A"> A) Administrar carvão ativado.</label>
    <label><input type="radio" name="q5" value="B"> B) Fazer lavagem gástrica.</label>
    <label><input type="radio" name="q5" value="C"> C) Administrar azul de metileno.</label>
    <label><input type="radio" name="q5" value="D"> D) Administrar atropina.</label>
  </div>
  <button data-question="5" data-correct="C">Conferir</button>
</div>

<!-- Questão 6 -->
<div class="quiz-container" id="quiz-6">
  <h4>Questão 6</h4>
  <p>Menino, 2 anos de idade, é levado à UPA com relato de sonolência, naúseas e vômitos há 50 minutos...</p>
  <p>O paciente, em questão, pode apresentar complicação decorrente de:</p>
  <div class="options">
    <label><input type="radio" name="q6" value="A"> A) Lesões cáusticas pela acidez.</label>
    <label><input type="radio" name="q6" value="B"> B) Lesões cáusticas pela alcalinidade.</label>
    <label><input type="radio" name="q6" value="C"> C) Síndrome hipercolinérgica.</label>
    <label><input type="radio" name="q6" value="D"> D) Metahemoglobinemia com cianose.</label>
  </div>
  <button data-question="6" data-correct="D">Conferir</button>
</div>

<!-- Questão 7 -->
<div class="quiz-container" id="quiz-7">
  <h4>Questão 7</h4>
  <p>Menino, 2 anos de idade, é levado à UPA com relato de sonolência, naúseas e vômitos há 50 minutos...</p>
  <p>Considerando o potencial tóxico do produto, e que a criança permaneceu por 8 horas em observação, sem sintomas, indique a conduta correta:</p>
  <div class="options">
    <label><input type="radio" name="q7" value="A"> A) Manter internado por mais 12 horas, verificando sintomas respiratórios.</label>
    <label><input type="radio" name="q7" value="B"> B) Manter internado por mais 48 horas, verificando sintomas neurológicos.</label>
    <label><input type="radio" name="q7" value="C"> C) Conceder alta, com retorno, após 5 dias, para realizar Hemograma e Sumário de Urina.</label>
    <label><input type="radio" name="q7" value="D"> D) Conceder alta com observação domiciliar, por 5 a 7 dias, e retorno se tiver sintomas.</label>
  </div>
  <button data-question="7" data-correct="C">Conferir</button>
</div>

<!-- Questão 8 -->
<div class="quiz-container" id="quiz-8">
  <h4>Questão 8</h4>
  <p>Um pré-escolar de 4 anos e 12 kg foi submetido a cirurgia abdominal de baixa complexidade...</p>
  <p>Com base no quadro clinico acima, qual o tratamento farmacológico imediato mais adequado para esta situação clínica?</p>
  <div class="options">
    <label><input type="radio" name="q8" value="A"> A) Haloperidol.</label>
    <label><input type="radio" name="q8" value="B"> B) Flumazenil.</label>
    <label><input type="radio" name="q8" value="C"> C) Glicose.</label>
    <label><input type="radio" name="q8" value="D"> D) Naloxona.</label>
  </div>
  <button data-question="8" data-correct="D">Conferir</button>
</div>

<!-- Questão 9 -->
<div class="quiz-container" id="quiz-9">
  <h4>Questão 9</h4>
  <p>A "crise dos opioides", muito citada na literatura estadunidense, decorre do uso abusivo e indevido desta classe de drogas...</p>
  <p>O melhor preditor da toxicidade por opioides é:</p>
  <div class="options">
    <label><input type="radio" name="q9" value="A"> A) Miose.</label>
    <label><input type="radio" name="q9" value="B"> B) Frequência respiratória < 12irpm.</label>
    <label><input type="radio" name="q9" value="C"> C) Confusão mental.</label>
    <label><input type="radio" name="q9" value="D"> D) Frequência cardíaca < 60bpm.</label>
    <label><input type="radio" name="q9" value="E"> E) Peristalse débil.</label>
  </div>
  <button data-question="9" data-correct="B">Conferir</button>
</div>

<!-- Questão 10 -->
<div class="quiz-container" id="quiz-10">
  <h4>Questão 10</h4>
  <p>Uma mulher de 23 anos de idade foi encaminhada para a UTI, após tentativa de suicídio...</p>
  <p>A causa mais provável pela sintomatologia de intoxicação exógena da paciente, dentre as substâncias abaixo, é:</p>
  <div class="options">
    <label><input type="radio" name="q10" value="A"> A) tramadol.</label>
    <label><input type="radio" name="q10" value="B"> B) diazepam.</label>
    <label><input type="radio" name="q10" value="C"> C) aldicarb ("chumbinho").</label>
    <label><input type="radio" name="q10" value="D"> D) imipramina.</label>
  </div>
  <button data-question="10" data-correct="D">Conferir</button>
</div>

<!-- Questão 11 -->
<div class="quiz-container" id="quiz-11">
    <h4>Questão 11</h4>
    <p>Jovem, 21 anos, é admitido no pronto atendimento com suspeita de intoxicação exógena por droga anticolinérgica...</p>
    <p>Assinale a alternativa que apresenta o quadro clínico mais compatível.</p>
    <div class="options">
        <label><input type="radio" name="q11" value="A"> A) Midríase, hipertensão, taquicardia, hipertermia, hiperemia cutânea e mucosas secas.</label>
        <label><input type="radio" name="q11" value="B"> B) Midríase, hipertensão, bradicardia, hipotermia, hiperemia cutânea e hipersecreção.</label>
        <label><input type="radio" name="q11" value="C"> C) Miose, hipotensão, bradicardia, hipertermia, palidez cutânea e hipersecreção.</label>
        <label><input type="radio" name="q11" value="D"> D) Miose, hipertensão, taquicardia, hipertermia, hiperemia cutânea e hipersecreção.</label>
        <label><input type="radio" name="q11" value="E"> E) Midríase, hipotensão, bradicardia, hipotermia, palidez cutânea e mucosas secas.</label>
    </div>
    <button data-question="11" data-correct="A">Conferir</button>
</div>

<!-- Questão 12 -->
<div class="quiz-container" id="quiz-12">
    <h4>Questão 12</h4>
    <p>Paciente de 46 anos de idade, agricultor, é levado por familiares para a emergência...</p>
    <p>Diante desse cenário, quais são: o provável diagnóstico e o antídoto a ser administrado?</p>
    <div class="options">
        <label><input type="radio" name="q12" value="A"> A) Intoxicação por carbamato - administrar naloxona.</label>
        <label><input type="radio" name="q12" value="B"> B) Intoxicação por organofosforado – administrar atropina.</label>
        <label><input type="radio" name="q12" value="C"> C) Intoxicação por tricíclico - administrar pralidoxima.</label>
        <label><input type="radio" name="q12" value="D"> D) Intoxicação por organofosforado - administrar n-acetilcisteína.</label>
    </div>
    <button data-question="12" data-correct="B">Conferir</button>
</div>

<!-- Questão 13 -->
<div class="quiz-container" id="quiz-13">
    <h4>Questão 13</h4>
    <p>Pré-escolar de 3 anos e 4 meses de idade deu entrada no pronto-socorro...</p>
    <p>As evidências clínicas dessa história induzem a necessidade de o médico investigar:</p>
    <div class="options">
        <label><input type="radio" name="q13" value="A"> A) cardiopatia congênita cianótica.</label>
        <label><input type="radio" name="q13" value="B"> B) intoxicação exógena por captopril.</label>
        <label><input type="radio" name="q13" value="C"> C) intoxicação exógena de haloperidol.</label>
        <label><input type="radio" name="q13" value="D"> D) ingestão exógena por benzodiazepínico.</label>
    </div>
    <button data-question="13" data-correct="C">Conferir</button>
</div>

<!-- Questão 14 -->
<div class="quiz-container" id="quiz-14">
    <h4>Questão 14</h4>
    <p>Um escolar de oito anos de idade foi levado ao serviço de emergência...</p>
    <p>Com base nesse caso hipotético, é correto afirmar que, após a monitorização e a estabilização inicial, deverão ser realizadas as seguintes medidas:</p>
    <div class="options">
        <label><input type="radio" name="q14" value="A"> A) lavagem gástrica; carvão ativado; e fisostigmina.</label>
        <label><input type="radio" name="q14" value="B"> B) lavagem gástrica; carvão ativado; e gluconato de cálcio.</label>
        <label><input type="radio" name="q14" value="C"> C) lavagem gástrica; carvão ativado; e flumazenil.</label>
        <label><input type="radio" name="q14" value="D"> D) lavagem intestinal; alcalinização urinária; e hemodiálise.</label>
        <label><input type="radio" name="q14" value="E"> E) lavagem intestinal; alcalinização urinária; e piridoxina.</label>
    </div>
    <button data-question="14" data-correct="B">Conferir</button>
</div>

<!-- Questão 15 -->
<div class="quiz-container" id="quiz-15">
    <h4>Questão 15</h4>
    <p>Uma mulher de 23 anos de idade foi levada por seus familiares ao setor de emergência...</p>
    <p>Com base nesse caso hipotético, assinale a alternativa que apresenta a melhor escolha de antídoto para a paciente.</p>
    <div class="options">
        <label><input type="radio" name="q15" value="A"> A) flumazenil</label>
        <label><input type="radio" name="q15" value="B"> B) fisostigmina</label>
        <label><input type="radio" name="q15" value="C"> C) glicose e tiamina</label>
        <label><input type="radio" name="q15" value="D"> D) naloxona</label>
        <label><input type="radio" name="q15" value="E"> E) glucagon</label>
    </div>
    <button data-question="15" data-correct="D">Conferir</button>
</div>

<!-- Questão 16 -->
<div class="quiz-container" id="quiz-16">
    <h4>Questão 16</h4>
    <p>A correta correlação entre tóxico e antídoto é:</p>
    <div class="options">
        <label><input type="radio" name="q16" value="A"> A) metanol e etilenoglicol.</label>
        <label><input type="radio" name="q16" value="B"> B) opioide e flumazenil.</label>
        <label><input type="radio" name="q16" value="C"> C) benzodiazepínico e naloxona.</label>
        <label><input type="radio" name="q16" value="D"> D) cianeto e hidroxicobalamina.</label>
        <label><input type="radio" name="q16" value="E"> E) betabloqueador e gluconato de cálcio.</label>
    </div>
    <button data-question="16" data-correct="D">Conferir</button>
</div>

<!-- Questão 17 -->
<div class="quiz-container" id="quiz-17">
    <h4>Questão 17</h4>
    <p>Criança de 2,5 anos, sexo masculino, foi levada ao pronto-socorro com suspeita de ter ingerido uma caixa de medicamentos...</p>
    <p>Dentre os seguintes medicamentos, o que mais provavelmente corresponde ao quadro da criança é:</p>
    <div class="options">
        <label><input type="radio" name="q17" value="A"> A) Amiodarona 200 mg.</label>
        <label><input type="radio" name="q17" value="B"> B) Sertralina 50 mg.</label>
        <label><input type="radio" name="q17" value="C"> C) Diazepam 10 mg.</label>
        <label><input type="radio" name="q17" value="D"> D) Levotiroxina 50 mg.</label>
        <label><input type="radio" name="q17" value="E"> E) Loratadina 10 mg.</label>
    </div>
    <button data-question="17" data-correct="E">Conferir</button>
</div>

<!-- Questão 18 -->
<div class="quiz-container" id="quiz-18">
    <h4>Questão 18</h4>
    <p>Lactente, 3 m, previamente hígido, é trazido a emergência com história de coriza e obstrução nasal...</p>
    <p>O DIAGNÓSTICO SINDRÔMICO É:</p>
    <div class="options">
        <label><input type="radio" name="q18" value="A"> A) Síndrome Colinérgica</label>
        <label><input type="radio" name="q18" value="B"> B) Síndrome Anticolinérgica</label>
        <label><input type="radio" name="q18" value="C"> C) Síndrome Simpaticomimética/Adrenérgica</label>
        <label><input type="radio" name="q18" value="D"> D) Síndrome Sedativo-Hipnótica</label>
    </div>
    <button disabled>Conferir (Resposta não disponível)</button>
</div>

<!-- Questão 19 -->
<div class="quiz-container" id="quiz-19">
    <h4>Questão 19</h4>
    <p>Homem, 39 a, chega à emergência com confusão mental, náuseas e vômitos há 4 horas...</p>
    <p>A HIPÓTESE DIAGNÓSTICA É:</p>
    <div class="options">
        <label><input type="radio" name="q19" value="A"> A) Intoxicação por salicilatos.</label>
        <label><input type="radio" name="q19" value="B"> B) Intoxicação por antidepressivo tricíclico.</label>
        <label><input type="radio" name="q19" value="C"> C) Sepse.</label>
        <label><input type="radio" name="q19" value="D"> D) Crise tireotóxica.</label>
    </div>
    <button data-question="19" data-correct="A">Conferir</button>
</div>

<!-- Questão 20 -->
<div class="quiz-container" id="quiz-20">
    <h4>Questão 20</h4>
    <p>Menino de 1 ano dá entrada em hospital após quadro convulsivo...</p>
    <p>Considerando o agente farmacológico provável, trata-se de uma:</p>
    <div class="options">
        <label><input type="radio" name="q20" value="A"> A) toxíndrome simpatomimética, que resulta da estimulação de nervos simpáticos...</label>
        <label><input type="radio" name="q20" value="B"> B) toxíndrome anticolinérgica, que resulta da inibição das fibras parassimpáticas...</label>
        <label><input type="radio" name="q20" value="C"> C) toxíndrome anticolinesterásica, em que ocorre inibição da enzima acetilcolinesterase...</label>
        <label><input type="radio" name="q20" value="D"> D) toxíndrome depressiva, que resulta da interferência na função adrenérgica do SNC...</label>
        <label><input type="radio" name="q20" value="E"> E) toxíndrome extrapiramidal, que resulta do aumento da ação da acetilcolina...</label>
    </div>
    <button data-question="20" data-correct="A">Conferir</button>
</div>

<!-- Questão 21 -->
<div class="quiz-container" id="quiz-21">
    <h4>Questão 21</h4>
    <p>Jovem, 21 anos, é admitida no pronto atendimento com suspeita de intoxicação exógena por droga anticolinérgica...</p>
    <p>Assinale a alternativa que apresenta o quadro clínico mais compatível.</p>
    <div class="options">
        <label><input type="radio" name="q21" value="A"> A) Miose, hipotensão, bradicardia, hipertermia, palidez cutânea e hipersecreção.</label>
        <label><input type="radio" name="q21" value="B"> B) Miose, hipertensão, taquicardia, hipertermia, hiperemia cutânea e hipersecreção.</label>
        <label><input type="radio" name="q21" value="C"> C) Midríase, hipotensão, bradicardia, hipotermia, palidez cutânea e mucosas secas.</label>
        <label><input type="radio" name="q21" value="D"> D) Midríase, hipertensão, taquicardia, hipertermia, hiperemia cutânea e mucosas secas.</label>
        <label><input type="radio" name="q21" value="E"> E) Midríase, hipertensão, bradicardia, hipotermia, hiperemia cutânea e hipersecreção.</label>
    </div>
    <button data-question="21" data-correct="D">Conferir</button>
</div>

<!-- Questão 22 -->
<div class="quiz-container" id="quiz-22">
    <h4>Questão 22</h4>
    <p>Nas intoxicações exógenas está indicado a realização de lavagem gástrica e carvão ativado nas primeiras horas...</p>
    <p>Assinale a alternativa que possui uma substância em que NÃO é indicado esse procedimento.</p>
    <div class="options">
        <label><input type="radio" name="q22" value="A"> A) Álcalis fortes (Substâncias causticas).</label>
        <label><input type="radio" name="q22" value="B"> B) Carbamazepina.</label>
        <label><input type="radio" name="q22" value="C"> C) Fenitoina.</label>
        <label><input type="radio" name="q22" value="D"> D) Digoxina.</label>
    </div>
    <button data-question="22" data-correct="A">Conferir</button>
</div>

<!-- Questão 23 -->
<div class="quiz-container" id="quiz-23">
    <h4>Questão 23</h4>
    <p>Paciente de 62 anos de idade é trazida pelos familiares ao serviço de emergência...</p>
    <p>Sobre intoxicação por substâncias com efeitos anticolinérgicos, é correto afirmar:</p>
    <div class="options">
        <label><input type="radio" name="q23" value="A"> A) Sialorreia é um achado comum.</label>
        <label><input type="radio" name="q23" value="B"> B) Alterações eletrocardiográficas são raras.</label>
        <label><input type="radio" name="q23" value="C"> C) Dosagem do nível sérico de colinesterase é mandatória.</label>
        <label><input type="radio" name="q23" value="D"> D) O uso de atropina está indicado em alguns casos.</label>
        <label><input type="radio" name="q23" value="E"> E) Exame físico abdominal com presença de globo vesical pode estar presente.</label>
    </div>
    <button data-question="23" data-correct="E">Conferir</button>
</div>

<!-- Questão 24 -->
<div class="quiz-container" id="quiz-24">
    <h4>Questão 24</h4>
    <p>Qual é a hipótese diagnóstica mais provável para paciente com história de uso de várias substâncias de abuso e que se apresenta com taquicardia, midríase e hipertensão arterial?</p>
    <div class="options">
        <label><input type="radio" name="q24" value="A"> A) Acatisia por antipsicótico.</label>
        <label><input type="radio" name="q24" value="B"> B) Intoxicação por álcool.</label>
        <label><input type="radio" name="q24" value="C"> C) Intoxicação por estimulante.</label>
        <label><input type="radio" name="q24" value="D"> D) Abstinência por benzodiazepínicos.</label>
    </div>
    <button data-question="24" data-correct="C">Conferir</button>
</div>

<!-- Questão 25 -->
<div class="quiz-container" id="quiz-25">
    <h4>Questão 25</h4>
    <p>Paciente masculino, 25 anos, é levado por um amigo, desacordado, para a UPA mais próxima...</p>
    <p>Diante dessa situação, você imediatamente suspeita de um quadro causado por intoxicação exógena e decide utilizar o seguinte antídoto:</p>
    <div class="options">
        <label><input type="radio" name="q25" value="A"> A) Fomepizole</label>
        <label><input type="radio" name="q25" value="B"> B) Pralidoxima</label>
        <label><input type="radio" name="q25" value="C"> C) Flumazenil</label>
        <label><input type="radio" name="q25" value="D"> D) N-acetilcisteína</label>
        <label><input type="radio" name="q25" value="E"> E) Naloxona.</label>
    </div>
    <button data-question="25" data-correct="B">Conferir</button>
</div>

<!-- Questão 26 -->
<div class="quiz-container" id="quiz-26">
    <h4>Questão 26</h4>
    <p>Faça rapidamente o exame inicial do paciente suspeito de intoxicações agudas com inibidores de colinesterase...</p>
    <p>Considerando o correto:</p>
    <div class="options">
        <label><input type="radio" name="q26" value="A"> A) Atente para a presença de odores aliáceos (semelhantes a alho e cebola, característicos das intoxicações por organofosforados.</label>
        <label><input type="radio" name="q26" value="B"> B) Atente para a presença de odores aliáceos (semelhantes a alho e cebola, característicos das intoxicações por opioides.</label>
        <label><input type="radio" name="q26" value="C"> C) Atente para a presença de odores aliáceos (semelhantes a alho e cebola, característicos das intoxicações por cocaína.</label>
        <label><input type="radio" name="q26" value="D"> D) Atente para a presença de odores aliáceos (semelhantes a alho e cebola, que excluem as por organofosforados.</label>
    </div>
    <button data-question="26" data-correct="A">Conferir</button>
</div>

<!-- Questão 27 -->
<div class="quiz-container" id="quiz-27">
    <h4>Questão 27</h4>
    <p>Uma criança de 3 anos é trazida ao pronto-socorro por ter ingerido, há cerca de 3 horas, alguns medicamentos de sua avó...</p>
    <p>O mais provável medicamento envolvido na intoxicação desta criança é um:</p>
    <div class="options">
        <label><input type="radio" name="q27" value="A"> A) Diurético.</label>
        <label><input type="radio" name="q27" value="B"> B) Corticoide.</label>
        <label><input type="radio" name="q27" value="C"> C) Bloqueador do canal de cálcio.</label>
        <label><input type="radio" name="q27" value="D"> D) Inibidor da monoamina oxidase.</label>
        <label><input type="radio" name="q27" value="E"> E) Hipoglicemiante oral.</label>
    </div>
    <button data-question="27" data-correct="C">Conferir</button>
</div>

<!-- Questão 28 -->
<div class="quiz-container" id="quiz-28">
    <h4>Questão 28</h4>
    <p>Adolescente, 14 anos de idade, sem antecedentes prévios, ingeriu 20 comprimidos de um anti-hipertensivo...</p>
    <p>Qual é o anti-hipertensivo que ele deve ter ingerido?</p>
    <div class="options">
        <label><input type="radio" name="q28" value="A"> A) Hidralazina.</label>
        <label><input type="radio" name="q28" value="B"> B) Amlodipina.</label>
        <label><input type="radio" name="q28" value="C"> C) Hidroclorotiazida.</label>
        <label><input type="radio" name="q28" value="D"> D) Losartana.</label>
    </div>
    <button data-question="28" data-correct="B">Conferir</button>
</div>

<!-- Questão 29 -->
<div class="quiz-container" id="quiz-29">
    <h4>Questão 29</h4>
    <p>Paciente 23 anos, chega ao pronto atendimento com quadro de intoxicação exógena por paracetamol 750 mg...</p>
    <div class="options">
        <label><input type="radio" name="q29" value="A"> A) não atingiu dose toxica ou letal...</label>
        <label><input type="radio" name="q29" value="B"> B) não atingiu dose letal, porém deve ser monitorizado...</label>
        <label><input type="radio" name="q29" value="C"> C) atingiu a dose tóxica/letal, deve ser internado, realizar soro glicosado 5% e o antidoto que é a acetilcisteína...</label>
        <label><input type="radio" name="q29" value="D"> D) atingiu a dose letal, deve ser feito lavagem gástrica...</label>
        <label><input type="radio" name="q29" value="E"> E) não atingiu dose letal, deve ser feito lavagem gástrica...</label>
    </div>
    <button data-question="29" data-correct="C">Conferir</button>
</div>

<!-- Questão 30 -->
<div class="quiz-container" id="quiz-30">
    <h4>Questão 30</h4>
    <p>Considere as assertivas abaixo em relação às intoxicações exógenas...</p>
    <p>Quais as CORRETAS?</p>
    <div class="options">
        <label><input type="radio" name="q30" value="A"> A) Apenas I</label>
        <label><input type="radio" name="q30" value="B"> B) Apenas II</label>
        <label><input type="radio" name="q30" value="C"> C) Apenas I e II</label>
        <label><input type="radio" name="q30" value="D"> D) I, II e III</label>
    </div>
    <button data-question="30" data-correct="C">Conferir</button>
</div>

<!-- Questão 31 -->
<div class="quiz-container" id="quiz-31">
    <h4>Questão 31</h4>
    <p>Homem, 60 anos, internado devido a câncer de estômago metastático...</p>
    <p>A medicação mais provavelmente implicada na intoxicação e o antídoto são, respectivamente,</p>
    <div class="options">
        <label><input type="radio" name="q31" value="A"> A) benzodiazepínico e flumazenil.</label>
        <label><input type="radio" name="q31" value="B"> B) metanol e fomepizol.</label>
        <label><input type="radio" name="q31" value="C"> C) tricíclico e bicarbonato de sódio.</label>
        <label><input type="radio" name="q31" value="D"> D) paracetamol e acetilcisteína.</label>
        <label><input type="radio" name="q31" value="E"> E) opioide e naloxona.</label>
    </div>
    <button data-question="31" data-correct="E">Conferir</button>
</div>

<!-- Questão 32 -->
<div class="quiz-container" id="quiz-32">
    <h4>Questão 32</h4>
    <p>Homem de 30 anos tira uma lata de cerveja da geladeira e rapidamente engole um bocado do seu conteúdo...</p>
    <p>Para neutralizar a atividade de inibição da colinesterase do veneno de organofosforado, o homem deve receber qual dos seguintes antídotos:</p>
    <div class="options">
        <label><input type="radio" name="q32" value="A"> A) Metacolina</label>
        <label><input type="radio" name="q32" value="B"> B) Piridostigmina</label>
        <label><input type="radio" name="q32" value="C"> C) Edrofônio</label>
        <label><input type="radio" name="q32" value="D"> D) Atropina</label>
    </div>
    <button data-question="32" data-correct="D">Conferir</button>
</div>

<!-- Questão 33 -->
<div class="quiz-container" id="quiz-33">
    <h4>Questão 33</h4>
    <p>Um paciente de 68 anos começou a desenvolver sintomas neurológicos após episódio de diarreia e vômitos...</p>
    <p>Com relação ao caso, assinale a alternativa INCORRETA.</p>
    <div class="options">
        <label><input type="radio" name="q33" value="A"> A) Hidratação venosa vigorosa deve ser realizada e pode melhorar o quadro clínico.</label>
        <label><input type="radio" name="q33" value="B"> B) A intoxicação crônica pode levar a diabetes insipidus nefrogênico...</label>
        <label><input type="radio" name="q33" value="C"> C) Hemodiálise é o tratamento de escolha em casos graves.</label>
        <label><input type="radio" name="q33" value="D"> D) O paciente pode evoluir com sequelas neurológicas...</label>
        <label><input type="radio" name="q33" value="E"> E) Esse paciente deve ter feito ingestão intencional de dose supraterapêutica do lítio...</label>
    </div>
    <button data-question="33" data-correct="E">Conferir</button>
</div>

<!-- Questão 34 -->
<div class="quiz-container" id="quiz-34">
    <h4>Questão 34</h4>
    <p>O uso do carvão ativado está indicado na intoxicação por:</p>
    <div class="options">
        <label><input type="radio" name="q34" value="A"> A) chumbo.</label>
        <label><input type="radio" name="q34" value="B"> B) monóxido de carbono.</label>
        <label><input type="radio" name="q34" value="C"> C) paracetamol.</label>
        <label><input type="radio" name="q34" value="D"> D) ácido muriático.</label>
    </div>
    <button data-question="34" data-correct="C">Conferir</button>
</div>

<!-- Questão 35 -->
<div class="quiz-container" id="quiz-35">
    <h4>Questão 35</h4>
    <p>Menino de 2 anos deu entrada no pronto-socorro após ter ingerido um frasco de paracetamol.</p>
    <p>O pediatra de plantão deverá estar atento para o risco de a criança apresenta:</p>
    <div class="options">
        <label><input type="radio" name="q35" value="A"> A) sinais de hepatotoxicidade.</label>
        <label><input type="radio" name="q35" value="B"> B) hemólise maciça.</label>
        <label><input type="radio" name="q35" value="C"> C) depressão respiratória.</label>
        <label><input type="radio" name="q35" value="D"> D) coma.</label>
        <label><input type="radio" name="q35" value="E"> E) sintomas de liberação extrapiramidal.</label>
    </div>
    <button data-question="35" data-correct="A">Conferir</button>
</div>

<!-- Questão 36 -->
<div class="quiz-container" id="quiz-36">
    <h4>Questão 36</h4>
    <p>Paciente sexo masculino, 45 anos, agricultor, foi levado ao pronto-socorro por quadro de fraqueza...</p>
    <p>Diante do quadro clínico, o diagnóstico mais provável e seu tratamento:</p>
    <div class="options">
        <label><input type="radio" name="q36" value="A"> A) Síndrome colinérgica. Atropina, pralidoxima e suporte clínico.</label>
        <label><input type="radio" name="q36" value="B"> B) Síndrome colinérgica. Inibidor da acetilcolinesterase, diazepam e suporte clínico.</label>
        <label><input type="radio" name="q36" value="C"> C) Gastroenterocolite aguda. Hidratação venosa, antieméticos e dieta obstipante.</label>
        <label><input type="radio" name="q36" value="D"> D) Síndrome anticolinérgica. Atropina, pralidoxima e suporte clínico.</label>
        <label><input type="radio" name="q36" value="E"> E) Síndrome anticolinérgica. Inibidor da acetilcolinesterase, diazepam e suporte clínico.</label>
    </div>
    <button data-question="36" data-correct="A">Conferir</button>
</div>

<!-- Questão 37 -->
<div class="quiz-container" id="quiz-37">
    <h4>Questão 37</h4>
    <p>Mulher, 55 anos, em tratamento de transtorno bipolar há 12 semanas, é admitida no hospital...</p>
    <p>Pode-se afirmar que o fármaco mais provavelmente relacionado a essa nefropatia é:</p>
    <div class="options">
        <label><input type="radio" name="q37" value="A"> A) resperidona.</label>
        <label><input type="radio" name="q37" value="B"> B) lítio.</label>
        <label><input type="radio" name="q37" value="C"> C) quetiapina.</label>
        <label><input type="radio" name="q37" value="D"> D) citalopram.</label>
    </div>
    <button data-question="37" data-correct="B">Conferir</button>
</div>

<!-- Questão 38 -->
<div class="quiz-container" id="quiz-38">
    <h4>Questão 38</h4>
    <p>Um paciente é admitido no pronto atendimento com quadro de hipersalivação, miose e bradicardia...</p>
    <p>Qual dos agentes abaixo pode ser responsável pelo quadro apresentado?</p>
    <div class="options">
        <label><input type="radio" name="q38" value="A"> A) Carbamato</label>
        <label><input type="radio" name="q38" value="B"> B) Amitriptilina</label>
        <label><input type="radio" name="q38" value="C"> C) Hipoclorito de Sódio</label>
        <label><input type="radio" name="q38" value="D"> D) Sertralina</label>
    </div>
    <button data-question="38" data-correct="A">Conferir</button>
</div>

<!-- Questão 39 -->
<div class="quiz-container" id="quiz-39">
    <h4>Questão 39</h4>
    <p>A mãe, inadvertidamente, enquanto falava ao celular, pegou um solvente na dispensa de sua casa...</p>
    <p>Nesse caso, deve ser prescrito ao lactente:</p>
    <div class="options">
        <label><input type="radio" name="q39" value="A"> A) glucagon.</label>
        <label><input type="radio" name="q39" value="B"> B) bicarbonato de sódio.</label>
        <label><input type="radio" name="q39" value="C"> C) etanol a 10%.</label>
        <label><input type="radio" name="q39" value="D"> D) octreotida.</label>
    </div>
    <button data-question="39" data-correct="C">Conferir</button>
</div>

<!-- Questão 40 -->
<div class="quiz-container" id="quiz-40">
    <h4>Questão 40</h4>
    <p>Garoto de cinco anos, cerca de três horas depois que voltou da fazenda com seus avós, inicia quadro de sudorese...</p>
    <p>Diante disso, ele faz diagnóstico de intoxicação por:</p>
    <div class="options">
        <label><input type="radio" name="q40" value="A"> A) cianeto.</label>
        <label><input type="radio" name="q40" value="B"> B) organofosforado.</label>
        <label><input type="radio" name="q40" value="C"> C) opioide.</label>
        <label><input type="radio" name="q40" value="D"> D) acetaminofeno.</label>
    </div>
    <button data-question="40" data-correct="B">Conferir</button>
</div>

<!-- Questão 41 -->
<div class="quiz-container" id="quiz-41">
    <h4>Questão 41</h4>
    <p>Avalie o conjunto de manifestações descrito abaixo...</p>
    <p>Assinale a alternativa com a respectiva droga (ou classe farmacológica) que se associa a cada conjunto de manifestações acima.</p>
    <div class="options">
        <label><input type="radio" name="q41" value="A"> A) 1. Cocaína; 2. Fluoxetina; 3. Haloperidol; 4. Lítio</label>
        <label><input type="radio" name="q41" value="B"> B) 1. Carbamato; 2. Tricíclico; 3. Lítio; 4. Fluoxetina</label>
        <label><input type="radio" name="q41" value="C"> C) 1. Carbamato; 2. Cocaína; 3. Fluoxetina; 4. Lítio</label>
        <label><input type="radio" name="q41" value="D"> D) 1. Fluoxetina; 2. Lítio; 3. Cocaína; 4. Haloperidol</label>
        <label><input type="radio" name="q41" value="E"> E) 1. Organofosforado; 2. Haloperidol; 3. Lítio; 4. Fluoxetina</label>
    </div>
    <button data-question="41" data-correct="C">Conferir</button>
</div>

<!-- Questão 42 -->
<div class="quiz-container" id="quiz-42">
    <h4>Questão 42</h4>
    <p>A mãe, inadvertidamente, enquanto falava ao celular, pegou um solvente na dispensa de sua casa...</p>
    <p>Nesse caso, deve ser prescrito ao lactente:</p>
    <div class="options">
        <label><input type="radio" name="q42" value="A"> A) glucagon.</label>
        <label><input type="radio" name="q42" value="B"> B) bicarbonato de sódio.</label>
        <label><input type="radio" name="q42" value="C"> C) etanol a 10%.</label>
        <label><input type="radio" name="q42" value="D"> D) octreotida.</label>
    </div>
    <button data-question="42" data-correct="C">Conferir</button>
</div>

<!-- Questão 43 -->
<div class="quiz-container" id="quiz-43">
    <h4>Questão 43</h4>
    <p>Um médico da Estratégia Saúde da Família, em zona rural de um pequeno município do interior de Goiás...</p>
    <p>Seguindo os protocolos do Ministério da Saúde do Brasil, a principal suspeita diagnóstica que deve ser levantada é:</p>
    <div class="options">
        <label><input type="radio" name="q43" value="A"> A) intoxicação crônica por chumbo metálico.</label>
        <label><input type="radio" name="q43" value="B"> B) intoxicação aguda grave por agrotóxicos.</label>
        <label><input type="radio" name="q43" value="C"> C) dengue.</label>
        <label><input type="radio" name="q43" value="D"> D) Covid-19.</label>
    </div>
    <button data-question="43" data-correct="B">Conferir</button>
</div>

<!-- Questão 44 -->
<div class="quiz-container" id="quiz-44">
    <h4>Questão 44</h4>
    <p>Paciente, 45 anos, chega ao setor de emergência do pronto socorro com quadro de sialorreia...</p>
    <p>Baseado no caso clínico, o médico que fez o atendimento indicou o uso da seguinte droga:</p>
    <div class="options">
        <label><input type="radio" name="q44" value="A"> A) Fomepizole.</label>
        <label><input type="radio" name="q44" value="B"> B) Pralidoxima.</label>
        <label><input type="radio" name="q44" value="C"> C) Flumazonil.</label>
        <label><input type="radio" name="q44" value="D"> D) N-acetilcisteína</label>
        <label><input type="radio" name="q44" value="E"> E) Naloxone.</label>
    </div>
    <button data-question="44" data-correct="B">Conferir</button>
</div>

<!-- Questão 45 -->
<div class="quiz-container" id="quiz-45">
    <h4>Questão 45</h4>
    <p>Adolescente de 12 anos chega ao pronto-atendimento após ter tomado todo o Rivotril da irmã...</p>
    <p>Frente a esse quadro de intoxicação exógena, a conduta correta é:</p>
    <div class="options">
        <label><input type="radio" name="q45" value="A"> A) lavagem gástrica com soro fisiológico, xarope de ipeca e internação hospitalar.</label>
        <label><input type="radio" name="q45" value="B"> B) lavagem gástrica com soro fisiológico, prescrever flumazenil e dar alta após melhorada sonolência.</label>
        <label><input type="radio" name="q45" value="C"> C) lavagem gástrica com água destilada, carvão ativado a 10%, e manter a criança em observação...</label>
        <label><input type="radio" name="q45" value="D"> D) lavagem gástrica com soro fisiológico, passar carvão ativado e internação.</label>
        <label><input type="radio" name="q45" value="E"> E) comunicar o CEATOX (Central de Intoxicações), dar água para beber, internar para realização de endoscopia.</label>
    </div>
    <button data-question="45" data-correct="D">Conferir</button>
</div>

<!-- Questão 46 -->
<div class="quiz-container" id="quiz-46">
    <h4>Questão 46</h4>
    <p>Qual o antidoto da intoxicação por beta bloqueador?</p>
    <div class="options">
        <label><input type="radio" name="q46" value="A"> A) Glucagon.</label>
        <label><input type="radio" name="q46" value="B"> B) Flumazenil.</label>
        <label><input type="radio" name="q46" value="C"> C) Adrenalina.</label>
        <label><input type="radio" name="q46" value="D"> D) Dexametosona.</label>
    </div>
    <button data-question="46" data-correct="A">Conferir</button>
</div>

<!-- Questão 47 -->
<div class="quiz-container" id="quiz-47">
    <h4>Questão 47</h4>
    <p>Menina, 13 anos de idade, é trazida pelos pais ao pronto socorro...</p>
    <p>Frente aos achados, está indicada a administração de:</p>
    <div class="options">
        <label><input type="radio" name="q47" value="A"> A) acetilcisteína.</label>
        <label><input type="radio" name="q47" value="B"> B) atropina.</label>
        <label><input type="radio" name="q47" value="C"> C) bicarbonato de sódio.</label>
        <label><input type="radio" name="q47" value="D"> D) flumazenil.</label>
        <label><input type="radio" name="q47" value="E"> E) naloxone.</label>
    </div>
    <button data-question="47" data-correct="B">Conferir</button>
</div>

<!-- Questão 48 -->
<div class="quiz-container" id="quiz-48">
    <h4>Questão 48</h4>
    <p>No pronto-socorro pediátrico, a família traz um adolescente de 15 anos, que ingeriu voluntariamente, há 7 horas, vários comprimidos de acetaminofeno (Paracetamol)...</p>
    <p>O tratamento indicado nesse caso é:</p>
    <div class="options">
        <label><input type="radio" name="q48" value="A"> A) realizar lavagem gástrica.</label>
        <label><input type="radio" name="q48" value="B"> B) ministrar carvão ativado.</label>
        <label><input type="radio" name="q48" value="C"> C) realizar hidratação parenteral.</label>
        <label><input type="radio" name="q48" value="D"> D) administrar diuréticos.</label>
        <label><input type="radio" name="q48" value="E"> E) administrar aceticisteína.</label>
    </div>
    <button data-question="48" data-correct="E">Conferir</button>
</div>

<!-- Questão 49 -->
<div class="quiz-container" id="quiz-49">
    <h4>Questão 49</h4>
    <p>Lactente de 18 meses é trazido ao pronto atendimento com história de ter ingerido 1 frasco de paracetamol há 1 hora...</p>
    <p>O risco dessa criança:</p>
    <div class="options">
        <label><input type="radio" name="q49" value="A"> A) está descartado, pois ela está assintomática.</label>
        <label><input type="radio" name="q49" value="B"> B) é apresentar depressão respiratória.</label>
        <label><input type="radio" name="q49" value="C"> C) é evoluir com insuficiência hepática.</label>
        <label><input type="radio" name="q49" value="D"> D) é apresentar insuficiência renal secundária à rabdomiólise.</label>
        <label><input type="radio" name="q49" value="E"> E) é evoluir com depressão neurológica progressiva.</label>
    </div>
    <button data-question="49" data-correct="C">Conferir</button>
</div>

<!-- Questão 50 -->
<div class="quiz-container" id="quiz-50">
    <h4>Questão 50</h4>
    <p>Uma criança de 3 anos, previamente saudável, é levada ao pronto-socorro com queixa de sonolência...</p>
    <p>Dentre as alternativas abaixo, a medicação mais indicada para o quadro descrito é:</p>
    <div class="options">
        <label><input type="radio" name="q50" value="A"> A) Atropina, 0,02 mg/kg, intravenosa.</label>
        <label><input type="radio" name="q50" value="B"> B) Naloxone, 0,5 mg/kg, intramuscular.</label>
        <label><input type="radio" name="q50" value="C"> C) Flumazenil, 0,01 mg/kg, intravenoso.</label>
        <label><input type="radio" name="q50" value="D"> D) Adrenalina, 0,1 mg/kg, intravenosa.</label>
        <label><input type="radio" name="q50" value="E"> E) Diazepam, 0,2 mg/kg, intravenoso.</label>
    </div>
    <button data-question="50" data-correct="A">Conferir</button>
</div>

<!-- Questão 51 -->
<div class="quiz-container" id="quiz-51">
    <h4>Questão 51</h4>
    <p>Qual das opções abaixo contém o antidoto adequado para o tratamento de uma intoxicação grave por atenolol?</p>
    <div class="options">
        <label><input type="radio" name="q51" value="A"> A) Adrenalina</label>
        <label><input type="radio" name="q51" value="B"> B) Digoxina</label>
        <label><input type="radio" name="q51" value="C"> C) Amiodarona</label>
        <label><input type="radio" name="q51" value="D"> D) Glucagon</label>
        <label><input type="radio" name="q51" value="E"> E) Insulina NPH</label>
    </div>
    <button data-question="51" data-correct="D">Conferir</button>
</div>

<!-- Questão 52 -->
<div class="quiz-container" id="quiz-52">
    <h4>Questão 52</h4>
    <p>Menino, 3 anos, é trazido ao Pronto Socorro pelos pais que relatam que o filho ingeriu seis comprimidos de paracetamol...</p>
    <p>Para um atendimento adequado o plantonista deve saber que: Escolha a alternativa correta:</p>
    <div class="options">
        <label><input type="radio" name="q52" value="A"> A) A dose tóxica de paracetamol para crianças, com menos de 6 anos, é 100 mg/Kg de peso...</label>
        <label><input type="radio" name="q52" value="B"> B) O antidoto é a N-acetilcisteína, que somente deve ser administrado aos pacientes com alto risco...</label>
        <label><input type="radio" name="q52" value="C"> C) A realização de lavagem gástrica e a administração de carvão ativado é mais eficaz quando realizados no prazo de 1 hora...</label>
        <label><input type="radio" name="q52" value="D"> D) O antidoto é a Piridoxina, que pode ser administrado a todos os pacientes independente do risco de lesão.</label>
    </div>
    <button data-question="52" data-correct="C">Conferir</button>
</div>

<!-- Questão 53 -->
<div class="quiz-container" id="quiz-53">
    <h4>Questão 53</h4>
    <p>Pode indicar um sinal de intoxicação aguda por carbonato de lítio:</p>
    <div class="options">
        <label><input type="radio" name="q53" value="A"> A) Ganho de peso.</label>
        <label><input type="radio" name="q53" value="B"> B) Diarréia.</label>
        <label><input type="radio" name="q53" value="C"> C) Poliúria.</label>
        <label><input type="radio" name="q53" value="D"> D) Hipotiroidismo.</label>
    </div>
    <button data-question="53" data-correct="B">Conferir</button>
</div>

<!-- Questão 54 -->
<div class="quiz-container" id="quiz-54">
    <h4>Questão 54</h4>
    <p>J.C.S, mulher, estudante, 22 anos, vem ao pronto socorro por tentativa de suicídio após ingestão oral proposital de 400 mg de amitriptilina...</p>
    <div class="options">
        <!-- As opções para a questão 54 não foram fornecidas no código original, então este espaço fica em branco -->
    </div>
    <button disabled>Conferir</button>
</div>
`;

// Renderiza o CSS e o HTML na nota do Obsidian
const container = dv.container;
container.innerHTML = style + html;

// Lógica JavaScript para a verificação das respostas
function checkAnswer(questionId, correctAnswer) {
  const quizContainer = container.querySelector('#quiz-' + questionId);
  if (!quizContainer) {
      console.error('Container do quiz para a questão ' + questionId + ' não encontrado.');
      return;
  }
  const radioButtons = quizContainer.querySelectorAll('input[type="radio"]');
  let selectedAnswer = null;

  radioButtons.forEach(radio => {
    const label = radio.parentElement;
    // Reseta os estilos de verificações anteriores
    label.classList.remove('correct-answer', 'incorrect-selection');
    if (radio.checked) {
      selectedAnswer = radio.value;
    }
  });

  if (selectedAnswer) {
    radioButtons.forEach(radio => {
      const label = radio.parentElement;
      // Marca a resposta correta em verde
      if (radio.value === correctAnswer) {
        label.classList.add('correct-answer');
      }
      // Se a selecionada estiver errada, marca em vermelho
      if (radio.checked && radio.value !== correctAnswer) {
        label.classList.add('incorrect-selection');
      }
    });
  } else {
    alert("Por favor, selecione uma alternativa.");
  }
}

// Adiciona os 'escutadores de evento' aos botões para que funcionem ao clicar
container.querySelectorAll('button[data-question]').forEach(button => {
  button.addEventListener('click', () => {
    const questionId = button.dataset.question;
    const correctAnswer = button.dataset.correct;
    checkAnswer(questionId, correctAnswer);
  });
});
```