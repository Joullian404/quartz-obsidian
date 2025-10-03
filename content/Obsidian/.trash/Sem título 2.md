```plantuml
@startuml
digraph G {
    graph [bgcolor="#1a1a1a", fontcolor=white, splines=ortho];
    node [shape=box, style="rounded,filled", fontname="Arial", fontsize=12, color="#a9a9a9", fillcolor="#333333", fontcolor=white];
    edge [fontname="Arial", fontsize=10, color="#a9a9a9", fontcolor="#a9a9a9"];

    Start [label="Paciente com Dor Torácica\nna Sala de Emergência"];
    
    ECG [label="Realizar ECG em até 10 minutos"];
    
    DecisionECG [label="ECG mostra\nSupradesnivelamento de ST?", shape=diamond, fillcolor="#5c6bc0"];
    
    IAMCSST [label="Diagnóstico: IAMCSST\n(Infarto com Supra de ST)\n\n- Iniciar protocolo de SCA\n- Terapia de reperfusão (Angioplastia ou Trombolítico)\n- Transferir para unidade coronariana"];
    
    NoSupra [label="Ausência de Supra de ST"];
    
    Investigate [label="Continuar investigação para as outras\n5 causas catastróficas e SCA sem Supra"];
    
    ExamesComplementares [label="Coletar História e Exame Físico Detalhado\n\n- PA em ambos os braços\n- Simetria de pulsos\n- Radiografia de Tórax\n- Marcadores de necrose miocárdica (Troponina)\n- D-dímero (se indicado)"];

    Start -> ECG;
    ECG -> DecisionECG;
    DecisionECG -> IAMCSST [label="Sim"];
    DecisionECG -> NoSupra [label="Não"];
    NoSupra -> Investigate;
    Investigate -> ExamesComplementares;
}
@enduml
```

```plantuml
@startuml
'--- Estilização Dark Theme ---
skinparam backgroundColor #1a1a1a
skinparam shadowing false
skinparam roundCorner 10

skinparam activity {
    FontColor white
    FontName Arial
    FontSize 12
    BorderColor #a9a9a9
    BackgroundColor #333333
    ArrowColor #a9a9a9
    ArrowFontColor #a9a9a9
    ArrowFontName Arial
    ArrowFontSize 10
}

skinparam diamond {
    FontColor white
    FontName Arial
    FontSize 12
    BorderColor #a9a9a9
    BackgroundColor #5c6bc0
    ArrowColor #a9a9a9
    ArrowFontColor #a9a9a9
    ArrowFontName Arial
    ArrowFontSize 10
}
'--- Fim da Estilização ---

start
:Paciente com Dor Torácica
na Sala de Emergência;

:Realizar ECG em até 10 minutos;

if (ECG mostra
Supradesnivelamento de ST?) then (Sim)
    :<b>Diagnóstico: IAMCSST</b>
    (Infarto com Supra de ST)
    
    - Iniciar protocolo de SCA
    - Terapia de reperfusão (Angioplastia ou Trombolítico)
    - Transferir para unidade coronariana;
    stop
else (Não)
    :Ausência de Supra de ST;
    :Continuar investigação para as outras
    5 causas catastróficas e SCA sem Supra;
    :<b>Coletar História e Exame Físico Detalhado</b>
    
    - PA em ambos os braços
    - Simetria de pulsos
    - Radiografia de Tórax
    - Marcadores de necrose miocárdica (Troponina)
    - D-dímero (se indicado);
    stop
endif
@enduml
```
```plantuml
@startuml
digraph G {
    // --- Configurações de Estilo (Dark Theme) ---
    graph [bgcolor="#1a1a1a", fontcolor=white, rankdir=TB];
    node [shape=box, style="rounded,filled", fontname="Arial", fontsize=12, color="#a9a9a9", fillcolor="#333333", fontcolor=white];
    edge [fontname="Arial", fontsize=10, color="#a9a9a9", fontcolor="#a9a9a9"];

    // --- Definição dos Nós (Caixas e Decisões) ---
    Start [label="Paciente com Dor Torácica\nna Sala de Emergência"];
    ECG [label="Realizar ECG em até 10 minutos"];
    DecisionECG [label="ECG mostra\nSupradesnivelamento de ST?", shape=diamond, fillcolor="#5c6bc0"];
    IAMCSST [label="Diagnóstico: IAMCSST\n(Infarto com Supra de ST)\n\n- Iniciar protocolo de SCA\n- Terapia de reperfusão (Angioplastia ou Trombolítico)\n- Transferir para unidade coronariana"];
    NoSupra [label="Ausência de Supra de ST"];
    Investigate [label="Continuar investigação para as outras\n5 causas catastróficas e SCA sem Supra"];
    ExamesComplementares [label="Coletar História e Exame Físico Detalhado\n\n- PA em ambos os braços\n- Simetria de pulsos\n- Radiografia de Tórax\n- Marcadores de necrose miocárdica (Troponina)\n- D-dímero (se indicado)"];

    // --- Definição das Conexões (Setas) ---
    Start -> ECG;
    ECG -> DecisionECG;
    DecisionECG -> IAMCSST [label="  Sim"];
    DecisionECG -> NoSupra [label="  Não"];
    NoSupra -> Investigate;
    Investigate -> ExamesComplementares;
}
@enduml
```
```plantuml
@startuml
digraph G {
    // --- Configurações de Estilo (Dark Theme) ---
    graph [bgcolor="#1a1a1a", fontcolor=white, rankdir=TB];
    node [shape=box, style="rounded,filled", fontname="Arial", fontsize=12, color="#a9a9a9", fillcolor="#333333", fontcolor=white];
    edge [fontname="Arial", fontsize=10, color="#a9a9a9", fontcolor="#a9a9a9"];

    // --- Definição dos Nós (Caixas e Decisões) ---
    Start [label="Paciente com Dor Torácica\nSugestiva de SCA"];
    ECG [label="Realizar ECG em 10 minutos"];
    DecisionECG [label="ECG mostra\nSupradesnivelamento de ST?", shape=diamond, fillcolor="#5c6bc0"];
    IAMCSST [label="IAMCSST\n\n- Iniciar MONABCH (Morfina, O2 se Sat<90%, Nitrato, AAS, Betabloq, Clopidogrel, Heparina)\n- Contatar hemodinâmica/UTI coronariana"];
    Reperfusion [label="Terapia de Reperfusão Urgente\n- Angioplastia Primária (se <90-120 min)\n- Trombolítico (se Angioplastia indisponível)"];
    NoSupra [label="SCA sem Supra de ST\n(IAMSSST ou Angina Instável)"];
    Investigate [label="- Iniciar MONABCH (exceto trombolítico)\n- Coletar Troponina Ultrassensível (0h e 1-3h)\n- Estratificar risco (Escores HEART, TIMI, GRACE)"];
    DecisionRisk [label="Qual o risco do paciente?", shape=diamond, fillcolor="#8e44ad"];
    HighRisk [label="Alto Risco\n\n- Cateterismo em < 24h"];
    LowRisk [label="Baixo/Intermediário Risco\n\n- Internar para observação\n- Considerar testes não-invasivos\n(Cintilografia, Teste Ergométrico)"];

    // --- Definição das Conexões (Setas) ---
    Start -> ECG;
    ECG -> DecisionECG;
    DecisionECG -> IAMCSST [label="  Sim"];
    IAMCSST -> Reperfusion;
    DecisionECG -> NoSupra [label="  Não"];
    NoSupra -> Investigate;
    Investigate -> DecisionRisk;
    DecisionRisk -> HighRisk [label="  Alto"];
    DecisionRisk -> LowRisk [label="  Baixo/Intermediário"];
}
@enduml
```
```plantuml
@startuml
digraph G {
    // --- Configurações de Estilo (Dark Theme) ---
    graph [bgcolor="#1a1a1a", fontcolor=white, rankdir=TB];
    node [shape=box, style="rounded,filled", fontname="Arial", fontsize=12, color="#a9a9a9", fillcolor="#333333", fontcolor=white];
    edge [fontname="Arial", fontsize=10, color="#a9a9a9", fontcolor="#a9a9a9"];

    // --- Definição dos Nós (Caixas e Decisões) ---
    Start [label="Paciente com Dor Torácica\nECG e Troponina Iniciais Inconclusivos"];
    ScoreHeart [label="Calcular Escore HEART"];
    DecisionScore [label="Qual o resultado do Escore?", shape=diamond, fillcolor="#5c6bc0"];
    BaixoRisco [label="Escore 0-3: Baixo Risco\n(~1.7% MACE em 6 semanas)\n\n- Considerar alta hospitalar segura\n- Orientar retorno se necessário"];
    RiscoIntermediario [label="Escore 4-6: Risco Intermediário\n(~20% MACE em 6 semanas)\n\n- Admitir para observação\n- Seriar marcadores\n- Realizar testes não-invasivos (Cintilografia, Teste Ergométrico)"];
    AltoRisco [label="Escore 7-10: Alto Risco\n(~72% MACE em 6 semanas)\n\n- Admitir para unidade coronariana\n- Iniciar terapia para SCA\n- Considerar fortemente cateterismo precoce"];

    // --- Definição das Conexões (Setas) ---
    Start -> ScoreHeart;
    ScoreHeart -> DecisionScore;
    DecisionScore -> BaixoRisco [label="  0-3"];
    DecisionScore -> RiscoIntermediario [label="  4-6"];
    DecisionScore -> AltoRisco [label="  7-10"];
}
@enduml
```
```plantuml
@startuml
digraph G {
    // --- Configurações de Estilo (Dark Theme) ---
    graph [bgcolor="#1a1a1a", fontcolor=white, rankdir=TB];
    node [shape=box, style="rounded,filled", fontname="Arial", fontsize=12, color="#a9a9a9", fillcolor="#333333", fontcolor=white];
    edge [fontname="Arial", fontsize=10, color="#a9a9a9", fontcolor="#a9a9a9"];

    // --- Definição dos Nós (Caixas e Decisões) ---
    Start [label="Paciente com Dor Torácica\nECG e Troponina Iniciais Inconclusivos"];
    ScoreHeart [label="Calcular Escore HEART"];
    DecisionScore [label="Qual o resultado do Escore?", shape=diamond, fillcolor="#5c6bc0"];
    BaixoRisco [label="Escore 0-3: Baixo Risco\n(~1.7% MACE em 6 semanas)\n\n- Considerar alta hospitalar segura\n- Orientar retorno se necessário"];
    RiscoIntermediario [label="Escore 4-6: Risco Intermediário\n(~20% MACE em 6 semanas)\n\n- Admitir para observação\n- Seriar marcadores\n- Realizar testes não-invasivos (Cintilografia, Teste Ergométrico)"];
    AltoRisco [label="Escore 7-10: Alto Risco\n(~72% MACE em 6 semanas)\n\n- Admitir para unidade coronariana\n- Iniciar terapia para SCA\n- Considerar fortemente cateterismo precoce"];

    // --- Definição das Conexões (Setas) ---
    Start -> ScoreHeart;
    ScoreHeart -> DecisionScore;
    DecisionScore -> BaixoRisco [label="  0-3"];
    DecisionScore -> RiscoIntermediario [label="  4-6"];
    DecisionScore -> AltoRisco [label="  7-10"];
}
@enduml
```