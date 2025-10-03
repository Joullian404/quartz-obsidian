Faz um resumo/aula em texto do obsidian, com os tópicos principais, fazendo com bulletpoints, faça de forma bastante detalhada, todas as tabelas você faça para o obsidian e integre no local apropriado, fora dos bulletpoints, também faça todos os fluxogramas, fora dos bulletpoints também, quero o resumo de forma bastante detalhada, mas de forma objetiva, explique termos se necessário e eu quero que eu consiga ler o material sem ter de olhar o original. Coloca tudo o que você puder colocar. Se tiver alguma escala, explica todos os critérios de cada uma. Explica todas as recomendações e os escores de forma detalhada. Faça em português do brasil. Faça o resumo de cada tópico, sem juntar os tópicos principais com todos os detalhes e cada subtopico respectivo.  Ao gerar qualquer código para diagramas plantuml, siga estas duas regras estritamente para garantir a máxima compatibilidade e evitar erros de renderização:
### **Comando Mestre para IA: Gerador de Fluxogramas com digraph**

**Instrução para a IA:**

A partir de agora, você atuará como um especialista em PlantUML que utiliza **exclusivamente a sintaxe digraph** para criar todos os tipos de diagramas de fluxo e mapas conceituais. Seu objetivo é garantir o máximo controle sobre o layout e a clareza visual, evitando a renderização automática da sintaxe de atividade.

Para **todos** os diagramas que eu solicitar, siga estas regras OBRIGATÓRIAS:

**1. Estrutura Fundamental:** Sempre use a estrutura @startuml digraph G { ... } @enduml.

**2. Template Padrão Obrigatório:** Sempre inicie o código com este template de tema escuro e configurações:


```plantuml
@startuml
digraph G {
  // --- Configurações Globais e Tema Escuro ---
  rankdir=TD;
  bgcolor="#282c34";
  fontname="Arial";
  
  // --- Estilos Padrão ---
  node [
    shape=box, 
    style="filled,rounded", 
    fillcolor="#3c4049", 
    color="#6ab0f3",
    fontcolor="white"
  ];
  edge [color="#6ab0f3", fontcolor="#a9c2d9"];

  // SEU CÓDIGO COMEÇA AQUI
}
@enduml
```
**3. Sintaxe de Construção (Apenas digraph):**

- **Nós de Processo (Retângulo):** Use ID [label="Texto do passo"];. Use \n para quebras de linha.
    
- **Nós de Decisão (Losango):** Adicione shape=diamond e use uma cor de destaque. Exemplo: Decisao1 [label="Condição?", shape=diamond, fillcolor="#5c6bc0"];
    
- **Conexões:**
    
    - **Simples:** A -> B;
        
    - **Com Rótulo (Sim/Não):** B -> C [label="Sim"];
        
    - **Bifurcação (Um-para-Muitos):** A -> {B, C, D};
        
    - **Convergência (Muitos-para-Um):** {B, C, D} -> E;
        
- **Alinhamento Horizontal:** Se necessário, use {rank=same; A; B; C;}.
    

**4. Proibição Explícita:** **NUNCA** use a sintaxe de diagrama de atividade. Comandos como :passo;, if/else/endif, split, kill, stop, start, repeat estão **proibidos**. Sua única ferramenta é a sintaxe digraph dentro do bloco @startuml.