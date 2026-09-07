# FEP 2026 — Engenharia de Prompt na era dos agentes
## Plano: o que mudou do FEP original para a versão que devemos ter hoje

> **Repo:** `inematds/FEP2026` (nome escolhido por mim; `FEP2` já é outro curso). **Formato:** o plano previa v2, mas a skill `formato-curso-v2` só roda por invocação direta do usuário; a pedido ("crie um curso novo com isso"), o curso foi construído em **v5** (página única, dark editorial), a skill carregada nesta sessão. Título final: **"A AGI chegou e o prompt quase morreu"**. Os seis módulos da §4 viraram sete aulas (`curso.html`), mais `de-para.html` e `kit.html`. Publicado em https://inematds.github.io/FEP2026/ em 2026-09-07.
> **Tese:** o FEP ensinou a *escrever o programa inteiro dentro do prompt*. Em 2026, com modelos que operam a partir da intenção (Claude Fable 5.1, GPT-6 Astra) e agentes com ferramentas e memória, metade dessas técnicas virou muleta. Este curso é o FEP reescrito técnica por técnica: o que morreu, o que só serve em certas condições, o que continua, e o que faltava.

---

## 1. Diagnóstico do FEP original

| Item | Fato |
|---|---|
| Origem | outubro de 2025 (primeiro commit 2025-10-23); 3 níveis (Iniciante 12–15h · Técnico 35–45h · Masterclass 50–60h), "97–120 horas" |
| Formato hoje | **já está no formato v2** desde 2026-09-03 ("feat: migra curso FEP para formato v2"). Logo, este plano é **reescrita de conteúdo**, não troca de formato |
| Tamanho | 8 módulos, 47 tópicos em `conteudo/modulo*.md` (~60 mil palavras nos tópicos + ~34 mil nos md dos níveis) |
| Peças datadas visíveis | banner "NOVO: Guia de Prompting GPT-5.5", "Outcome-first: a nova filosofia de prompts da OpenAI (substitui o GPT-5.1)", página "100 Prompts Essenciais", "Certificação" em cada nível |
| Paradigma | os "4 ingredientes" (o quê, sobre o quê, como, para quem), técnicas manuais de raciocínio (CoT, Skeleton of Thought, Tree of Thoughts), frameworks de persona (24 Dimensões, EXPERT, "Prompt Supremo"), parâmetros de modelo (temperature, top_p), RAG com código (embeddings, vector DB, chunking), agentes como tópico de masterclass |

**Posicionamento em relação ao FEP → AGI (publicado hoje):** aquele é o *mapa* das cinco eras para público 40+ leigo, apontando para os cursos do catálogo. Este é o **próprio FEP**, reescrito para o público original (quem quer dominar a técnica de pedir e delegar à IA, do iniciante ao técnico), tópico a tópico. Os dois não se sobrepõem: um diz "em que era você está"; este diz "o que exatamente fazer diferente com cada técnica que você aprendeu".

---

## 2. Triagem em quatro baldes

Critério único para cada técnica do FEP: **ela descreve o que eu quero (destino) ou compensa uma fraqueza do modelo de 2024–2025 (muleta)?** Destino continua. Muleta morre, ou vira condicional quando a fraqueza ainda aparece em algum caso.

### 2.1 MORREU — não serve mais (sai do curso ou vira nota histórica de uma linha)

| Técnica do FEP | Onde estava | Por que morreu |
|---|---|---|
| **Chain-of-Thought manual** ("pense passo a passo", "raciocine antes") | m2-cot, Iniciante cap. 3, 20 arquivos citam | Os modelos atuais raciocinam antes de responder por padrão e escolhem o nível de esforço. A instrução não acrescenta e às vezes piora (força verbosidade). O que sobra é *escolher o esforço* (ver NOVO) |
| **Skeleton of Thought, Tree of Thoughts, Self-consistency** como técnicas de prompt | m2-skeleton-of-thought, Masterclass | Eram jeitos de simular planejamento em modelos que não planejavam. Hoje o modelo planeja; o usuário define fronteiras e critério de pronto |
| **Frameworks de persona: 24 Dimensões de Persona, EXPERT Framework, "Prompt Supremo"** | m2-24-dimensoes-persona (908 palavras), m2-empoderamento (1.302), m2-engenheiro-interativo (1.480) | Eram templates de 20–30 linhas para "programar" uma persona. Com modelo forte, papel-como-título ("você é um especialista premiado") não muda o resultado; o que muda é dizer *de que perspectiva e com que critério* julgar (isso vai para CONDICIONAL) |
| **Instruções negativas como lista longa** ("O Poder do NÃO", 2.301 palavras) | m3-negative | Listas de "não faça" competem entre si e enchem a janela. Sobrevive só a **fronteira** (o que nunca pode acontecer no seu negócio), que é destino, não muleta |
| **Temperature / top_p como técnica de prompt** | m3-parameters (2.412 palavras), Técnico | Não existe no chat que 95% do público usa; na API, os modelos atuais recomendam deixar o padrão. Vira uma nota para quem programa |
| **Output prefilling** | m3-prefilling | Recurso de API de 2024 para forçar formato; hoje resolvido com pedir o formato ou usar saída estruturada nativa |
| **Prompt chaining manual de 4–5 prompts** (pesquisa → outline → escrita → SEO) | m3-chaining (2.221), Técnico | O agente encadeia sozinho quando recebe destino e skill. Chaining só volta como CONDICIONAL quando há aprovação humana entre etapas |
| **RAG com código: embeddings, vector DB, chunking de 512 tokens, LangChain/LlamaIndex** | m5-embeddings, m5-vectordb, m5-rag, Técnico mód. 3 | Para o público do FEP, projetos com arquivos, busca em documentos nativa e memória substituem 90% dos casos. Montar RAG é curso de engenharia, não de prompt. Fica uma seção conceitual: "quando a sua base não cabe no projeto" |
| **"Fazer múltiplas perguntas de uma vez é erro"** (Erro #3 do Iniciante) | Iniciante cap. 5 | Modelos atuais lidam com pedidos compostos; o erro real hoje é *não dizer o critério de bom*, não a quantidade de perguntas |
| **Humanização de texto gerado por IA** (1.586 palavras) | m2-humanizacao | Era truque para disfarçar texto de 2024. Modelos atuais escrevem no tom pedido; sobrevive só "dê contexto de voz" (ficha de contexto) |
| **Biblioteca "100 Prompts Essenciais"** | 100-prompts.html | Receitas prontas são a era 1 em estado puro. Substituída por um **kit de 12 briefings** (destino + fronteiras + pronto quando), cada um adaptável |
| **Guia GPT-5.5 / "Outcome-first substitui o GPT-5.1"** | index.html, recursos | Datado por construção. Vira uma seção "como ler o guia de prompting de qualquer modelo novo em 10 minutos" |
| **Certificação por nível, "Desafio Final", "Certificado de Conclusão"** | fim de cada nível | Gamificação sem avaliação real. Substituída por *auto-avaliação com evidência* (ver NOVO) |
| **Voice AI & Multimodal Agents** (2.021 palavras) | m7-voice | Fora do escopo de um curso de prompt; virou produto pronto. Sai |

### 2.2 SÓ QUANDO SERVE — condicional (fica, com a condição escrita)

| Técnica | Use quando | Não use quando |
|---|---|---|
| **Few-shot (exemplos)** | o padrão de formato ou estilo é difícil de descrever em palavras (um anúncio no tom da casa, uma classificação com rótulos próprios) | o que você quer cabe numa frase de critério; exemplos demais prendem o modelo ao passado e enchem a janela |
| **Role prompting (papel)** | o papel define **perspectiva e critério de julgamento** ("avalie como um auditor que procura o que falta") | o papel é só título de prestígio ("você é o melhor redator do mundo"); não muda nada |
| **Saída estruturada (JSON/XML)** | o resultado vai para outro programa, planilha ou sistema (integração, API) | você vai ler o resultado; peça tabela ou lista e pronto |
| **Chaining (etapas encadeadas)** | há **aprovação humana** entre etapas, ou etapas rodam em ferramentas diferentes | as etapas são só o seu jeito de pensar; entregue o destino e deixe o agente encadear |
| **Decomposição de tarefas** | o problema tem partes com donos, prazos ou riscos diferentes, e você quer ver cada parte | a decomposição é apenas a sua lista de passos; vira muleta |
| **Instrução negativa** | é **fronteira** do negócio: "nunca cite o nome do médico", "não prometa prazo" | é lista de estilo ("não use adjetivos", "não seja prolixo"); descreva o positivo |
| **Multimodal (imagem, áudio, documento)** | a entrada real é uma foto, uma planta, um áudio de reunião | o texto já existe; anexar imagem do texto só piora |
| **Gestão de janela longa** | conversa ou material muito grande: regra importante nas pontas, material só o necessário | a conversa é curta; não há o que gerir |
| **Refinamento iterativo** | iterar **o briefing** (destino, fronteira, critério), uma mudança por vez | iterar micro-instruções ("agora mais curto", "agora mais formal") sem mexer no destino |
| **Prompt injection e segurança** | **sempre que o agente lê conteúdo externo** (e-mail, site, PDF de terceiro). Ficou *mais* relevante, não menos | você só conversa no chat com material seu |
| **Escolha do modelo e do esforço** | tarefas com custo ou prazo relevante: esforço baixo para rotina, alto para decisão | não há diferença prática; deixe o padrão |
| **Testes e avaliação (evals)** | a tarefa se repete e o resultado importa: defina o critério e meça uma amostra por semana | pedido único e descartável |

### 2.3 CONTINUA — núcleo que não envelhece (reescrito, não copiado)

| Fundamento do FEP | Como fica em 2026 |
|---|---|
| **Clareza e especificidade** (m1-clareza, Erro #1 "ser vago") | continua, mas a clareza migra do *procedimento* para o *destino*: o que deve acontecer, o que importa, o que é um bom resultado |
| **Os 4 ingredientes** (o quê, sobre o quê, como, para quem) | viram **6 partes do briefing**: objetivo, o que importa, restrições, o que não pode acontecer, recursos disponíveis, critério de bom. "Como" (formato de entrega) continua; "como fazer" (passos) sai |
| **Contexto** (m2-contextualizacao, Erro #4 "falta de contexto") | sobe para o centro do curso: o que a IA precisa saber, em ficha de cinco linhas, **com casa própria** (projeto, instruções, memória) em vez de repetido no prompt |
| **Definir formato e tom de entrega** (Erros #2 e #5) | continua como *destino*: como você precisa receber, para quem vai |
| **Restrições** (Erro #6) | continua e ganha nome: **fronteiras**, o que nunca pode acontecer |
| **Refinar em vez de aceitar a primeira resposta** (Erro #7) | continua, no nível do briefing (ver condicional) |
| **Tokens e janela de contexto** (m1-tokens) | continua como conceito ("a mesa tem tamanho, o meio recebe menos atenção"), sem gestão manual |
| **O que é um LLM, como "pensa", limites** (m1-llm-basics, m1-ia-generativa) | continua, encurtado e atualizado: raciocínio nativo, ferramentas, memória, e o que **não** mudou (erra com confiança, não conhece o seu negócio, não responde pelo resultado) |
| **Ética e alinhamento** (m8-ethics) | continua como "responsabilidade": quem responde pelo que saiu é você |
| **Testing & A/B** (m4-testing) | continua e cresce: avaliação simples por amostra, critério observável |
| **Segurança e prompt injection** (m8-security) | continua e cresce, agora para agentes que leem conteúdo externo |

### 2.4 NOVO — não existia ou era rodapé de masterclass

| Novo | De onde vem | Por que entra |
|---|---|---|
| **Intenção e objetivo antes do prompt** (a hierarquia intenção → objetivo → prompt → skill) | Arquitetura de Intenção; FEP → AGI aula 5 | o FEP começava no nível do prompt; a maioria dos erros de hoje está nos dois níveis acima |
| **Skill como manual operacional reutilizável** | FEP Masterclass tinha "Claude Skills" só para dev (m7-skills) | passa para o núcleo, em linguagem de quem trabalha: quando usar, o que entrega, passos da casa, modelo, checklist |
| **Contexto com casa própria** (projetos, instruções, memória entre conversas) | Era 2 | tira do prompt o que nunca deveria ter morado nele |
| **Engenharia por subtração** | Arq. Intenção dia 4 | a habilidade nova: auditar um prompt antigo linha a linha e cortar o que o modelo de 2026 faz igual ou melhor sozinho |
| **Fronteiras em vez de passos; pronto com evidência** | Arq. Intenção dia 4 | o formato de pedido para modelos que operam na intenção: intenção, fronteiras, pronto-quando, registro |
| **Agente: ferramentas, memória, permissões, aprovação humana** | FEP Masterclass 2 (m6-tools, m6-memory, m6-mcp, m6-react) reescrito para não-dev | o FEP tratava como arquitetura de sistema; hoje é decisão de quem delega: que portas abrir, o que só com o seu sim |
| **Escolha de modelo e nível de esforço** | m4-optimization, m7-extended reescritos | substitui temperature/top_p e CoT manual: a alavanca hoje é *quanto esforço pedir* e *qual modelo para qual tarefa* |
| **Auto-avaliação com evidência** (substitui certificação) | — | ao fim de cada módulo, um artefato observável que o aluno consegue mostrar |
| **Kit de 12 briefings** (substitui 100 prompts) | — | um por classe de trabalho, no formato de quatro blocos |

---

## 3. De-para: cada tópico do FEP → balde → destino no curso novo

| Módulo FEP | Tópico | Balde | Destino no FEP 2026 |
|---|---|---|---|
| 1 | ia-generativa, llm-basics | CONTINUA | M1 (encurtado, atualizado com raciocínio nativo e agentes) |
| 1 | tokens | CONTINUA | M1 (conceito de janela) |
| 1 | clareza, anatomia (4 ingredientes) | CONTINUA | M2 (viram as 6 partes do briefing) |
| 2 | contextualizacao | CONTINUA | M3 (ficha de contexto com casa) |
| 2 | zero-shot | CONTINUA | M2 (é o padrão; deixa de ser "técnica") |
| 2 | few-shot | CONDICIONAL | M4 |
| 2 | role | CONDICIONAL | M4 (papel como perspectiva) |
| 2 | cot, skeleton-of-thought | MORREU | nota histórica em M1 + "esforço" em M6 |
| 2 | 24-dimensoes-persona, empoderamento (EXPERT), engenheiro-interativo (Prompt Supremo) | MORREU | sai; uma linha em M1 ("o que era programar persona") |
| 2 | humanizacao | MORREU | sai; "voz" entra na ficha de contexto (M3) |
| 2 | prompts-interativos | CONDICIONAL | M4 (pedir perguntas antes de executar, quando o destino é incerto) |
| 3 | decomposicao, chaining | CONDICIONAL | M4 (com aprovação humana entre etapas) e M5 |
| 3 | formatting | CONTINUA | M2 (formato de entrega) |
| 3 | negative | MORREU / CONDICIONAL | M2 (fronteiras) |
| 3 | parameters | MORREU | nota em M6 para quem usa API |
| 3 | prefilling | MORREU | sai |
| 3 | refinamento | CONTINUA | M2 e M6 (iterar o briefing) |
| 4 | longcontext | CONDICIONAL | M3 |
| 4 | multimodal | CONDICIONAL | M4 |
| 4 | optimization (model-specific) | NOVO (reescrito) | M6 (escolha de modelo e esforço; ler guia de modelo novo) |
| 4 | structured | CONDICIONAL | M4 |
| 4 | testing | CONTINUA | M6 |
| 5 | context-arch | CONTINUA | M3 |
| 5 | embeddings, vectordb, rag | MORREU (para este público) | M3, uma seção: "quando a base não cabe no projeto" |
| 6 | tools, mcp, memory, react, planning, error | NOVO (reescrito) | M5 (agente para quem delega) |
| 7 | extended | NOVO (reescrito) | M6 (esforço) |
| 7 | multiagent | NOVO (reescrito) | M5 (orquestrar, dois pontos humanos) — curto, aponta para agi-pratica |
| 7 | skills | NOVO (promovido) | M3 (skill como manual) |
| 7 | voice | MORREU | sai |
| 8 | security | CONTINUA (cresce) | M5 (prompt injection para agentes) |
| 8 | ethics | CONTINUA | M6 (responsabilidade) |
| 8 | observability, production | MORREU (para este público) | M6, uma seção: "medir uma amostra por semana" |
| — | 100 Prompts Essenciais | MORREU | Kit de 12 briefings (página própria) |
| — | Guia GPT-5.5 | MORREU | M6, seção "como ler o guia de qualquer modelo novo" |
| — | Certificação | MORREU | auto-avaliação com evidência ao fim de cada módulo |

---

## 4. Esqueleto do curso novo (consumível pela v2)

**Uma trilha, seis módulos, seis tópicos cada** (mínimo da v2). Público: quem já usa IA de chat no trabalho ou fez o FEP e quer saber o que mudou; sem código, sem terminal. Tom: simples e direto, uma técnica por seção, sempre com o par "antes (FEP 2025) / agora (2026)".

> **Tensão a resolver na invocação:** "simples e direto" é sobre o conteúdo. A v2 ainda exige 500–800 linhas por módulo, mapa da trilha, um SVG por módulo e camada de aprendizagem. O que encurta é a prosa e o número de módulos (6, não 8), não o contrato do formato.

| # | Módulo | Balde que alimenta | Tópicos (6) | Evidência de fim de módulo |
|---|---|---|---|---|
| **M1** | **O que mudou: do prompt-programa ao briefing** | Diagnóstico + MORREU | 1 o que a IA de 2026 faz sozinha · 2 o que ela ainda não faz (erra com confiança, não conhece o seu negócio, não responde) · 3 a tabela morreu/às vezes/continua · 4 por que CoT manual e persona-template morreram · 5 o teste da linha (destino ou muleta?) · 6 o que este curso não vai ensinar e por quê | o aluno marca D/M num prompt próprio |
| **M2** | **O que continua: as seis partes do briefing** | CONTINUA | 1 objetivo · 2 o que importa · 3 restrições e fronteiras (o "não" que fica) · 4 recursos · 5 critério de bom e formato de entrega · 6 iterar o briefing, não a micro-instrução | briefing de 6 linhas para uma tarefa real, testado |
| **M3** | **Contexto e skill: o que sai do prompt e ganha casa** | CONTINUA + NOVO | 1 contexto é matéria-prima · 2 a mesa tem tamanho (janela, pontas) · 3 ficha de cinco linhas · 4 onde mora: projetos, instruções, memória · 5 skill: o manual da casa em uma página · 6 quando a base não cabe (nota sobre busca em documentos) | ficha de contexto + esboço de skill |
| **M4** | **O que só serve às vezes** | CONDICIONAL | 1 few-shot · 2 papel como perspectiva · 3 saída estruturada · 4 etapas com aprovação humana (chaining) · 5 multimodal · 6 pedir perguntas antes (interativo) — cada um com "use quando / não use quando" e um exemplo certo e um errado | tabela pessoal "eu uso / não uso" |
| **M5** | **Do prompt ao agente: fronteiras, portas e aprovação** | NOVO | 1 o formato de quatro blocos (intenção, fronteiras, pronto-quando, registro) · 2 engenharia por subtração num prompt antigo · 3 ferramentas e memória (as portas) · 4 permissões: sozinho, avisa, só com o seu sim · 5 prompt injection: quando o agente lê o que não é seu · 6 vários agentes: dois pontos humanos (curto; aponta para Super-Agentes) | prompt antigo migrado + mapa de portas |
| **M6** | **Escolher, medir e responder** | NOVO + CONTINUA | 1 qual modelo para qual tarefa · 2 quanto esforço pedir (substitui temperature e CoT) · 3 como ler o guia de um modelo novo em 10 minutos · 4 avaliar por amostra: o critério e o número da sexta · 5 responsabilidade: quem responde pelo que saiu · 6 o kit de 12 briefings | kit iniciado com 3 briefings próprios |

**Páginas extras:** `kit-12-briefings.html` (substitui os 100 prompts) · `de-para.html` (a tabela da §3, para quem fez o FEP antigo saber o que fazer com o que aprendeu) · exercícios por módulo (v2).

**Kit de 12 briefings (uma classe de trabalho cada):** e-mail difícil · proposta comercial · relatório recorrente · resumo de reunião · pesquisa de concorrência · anúncio ou descrição de produto · resposta a reclamação · roteiro ou pauta · análise de planilha · plano de projeto · revisão de texto de terceiro · decisão entre alternativas. Cada um em quatro blocos, com o que trocar marcado.

---

## 5. O que fica explícito na primeira página do curso

1. **Se você fez o FEP, nada foi perdido**: a metade "destino" do que você aprendeu vale mais do que nunca; a metade "muleta" você vai aprender a cortar.
2. **Data de validade declarada**: este curso descreve os modelos de setembro de 2026. A seção "como ler o guia de um modelo novo" existe para o curso não envelhecer do mesmo jeito que o original.
3. **Sem hype**: o que não mudou está escrito no M1 antes do que mudou.

---

## 6. Próximos passos (execução)

1. Este plano fica no repo `FEP2026` (`PLANO-FEP2026.md`).
2. Construção no formato v2: `/formato-curso-v2` com este plano como fonte (a skill só responde por invocação direta do usuário).
3. Depois do curso: capa via `capa-inema`, GitHub Pages na raiz, publicação no portal via `atualiza-portal` (card novo "FEP 2026", com o card do FEP original mantido e apontando para este como "versão 2026").
