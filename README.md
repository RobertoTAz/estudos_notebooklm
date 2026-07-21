# estudos_notebooklm

# Miniguia de Estudos: Tableau para Análise Estatística e Big Data utilizando o NotebookLM

## 1. Contexto e Objetivos
Este repositório contém um caderno temático desenvolvido no NotebookLM focado no uso do Tableau como ferramenta de Análise Visual Exploratória (EVA) e modelagem estatística em cenários de Big Data.
O objetivo principal deste estudo é compreender como o Tableau gerencia bilhões de registros com alta performance através do motor Hyper e como analistas podem aplicar funções de modelagem preditiva e clustering para extrair insights sem dependência imediata de programação externa.

## 2. Curadoria de Fontes
- Characterizing Exploratory Visual Analysis (Battle & Heer) https://homes.cs.washington.edu/~leibatt/static/papers/battle_eurovis2019_cr_04_11_2019.pdf
- Find Clusters in Data - Tableau Help https://help.tableau.com/current/pro/desktop/en-us/clustering.htm
- Predictive Modeling Functions - Tableau Help https://help.tableau.com/current/pro/desktop/en-us/functions_functions_predictivemodeling.htm
- Extract Your Data (Motor Hyper e Extratos) - Tableau Help https://help.tableau.com/current/pro/desktop/en-us/extracting_data.htm
- How to build advanced analytics applications with TabPy - Tableau https://www.tableau.com/blog/building-advanced-analytics-applications-tabpy

## 3. Engenharia de Prompts e "Cicatrizes"
Nesta seção, documento a jornada de refinamento das perguntas feitas à IA para extrair o máximo de profundidade técnica das 21 fontes analisadas. O foco foi ir além do básico, buscando detalhes de arquitetura e aplicação estatística.

### 1. Entendendo as limitações do plano gratuito
Prompt: "Quais são os recursos disponíveis para o plano gratuito do Tableau?"
Raciocínio: O objetivo foi identificar se a ferramenta possui flexibilidade e aplicabilidade no ambiente corporativo mesmo em sua capacidade gratuita.
**Resposta obtida:** 
O principal recurso gratuito oferecido é o Tableau Public, uma plataforma voltada para a criação e compartilhamento de visualizações de dados com a comunidade. Embora seja uma versão sem custos, ela inclui funcionalidades analíticas avançadas e restrições específicas de privacidade.
Abaixo estão os recursos e limitações detalhados nas fontes:

#### 1. Funcionalidades Analíticas e de Dados
Capacidades Estatísticas: O plano gratuito permite o uso de recursos avançados, como a análise de agrupamento (Clustering) baseada no algoritmo k-means.
Modelagem Preditiva: Estão disponíveis as funções de modelagem preditiva nativas, como MODEL_QUANTILE e MODEL_PERCENTILE, permitindo gerar previsões diretamente na ferramenta.
Motor Hyper: O Tableau Public é alimentado pela tecnologia Hyper, o motor de dados em memória otimizado para consultas rápidas em grandes conjuntos de dados.
#### 2. Restrições de Privacidade e Armazenamento
Hospedagem Pública: Uma restrição crítica da versão gratuita é que todos os painéis de análise e seus respectivos conjuntos de dados subjacentes devem ser hospedados publicamente na nuvem.
Sem Salvamento Local: A ferramenta impede o salvamento de arquivos de forma segura e local na máquina do usuário.
Uso Corporativo: Devido à natureza pública do armazenamento, o Tableau Public é considerado inadequado para projetos que envolvam dados sensíveis ou informações corporativas confidenciais.
#### 3. Outras Formas de Acesso Gratuito
Programas Acadêmicos: O Tableau oferece programas acadêmicos que podem fornecer acesso gratuito para estudantes e professores.
Treinamento: Estão disponíveis vídeos de treinamento gratuitos e recursos de aprendizado para auxiliar usuários novos a utilizarem a plataforma.
Avaliação Gratuita (Trial): Existe a opção de iniciar uma avaliação gratuita das versões completas (como o Tableau Desktop) por um período limitado antes da compra.

### 2. Mergulho na Arquitetura (O motor Hyper)
Prompt: "Como o motor Hyper otimiza a performance em Big Data?"
Cicatriz (Troubleshooting): Respostas iniciais de IAs costumam ser genéricas ("é mais rápido"). Refinei o prompt exigindo detalhes sobre hardware e processamento de consultas.
**Resposta completa:** 
O motor Hyper é a tecnologia de motor de dados em memória do Tableau, projetada especificamente para acelerar a ingestão de dados e o processamento de consultas analíticas em conjuntos de dados grandes ou complexos.

A otimização de performance em Big Data ocorre através de diversas frentes tecnológicas e arquiteturais:
#### 1. Inovações na Arquitetura de Processamento
- Compilação JIT (Just-In-Time) via LLVM: O Hyper não interpreta consultas SQL de forma sequencial; em vez disso, ele as compila diretamente em código de máquina nativo para o processador no momento da execução. Isso extrai o rendimento máximo do hardware moderno e minimiza os ciclos de instrução da CPU.
- Paralelização Baseada em Morsels: O motor divide os blocos de dados em pequenas frações de trabalho ("morsels") que são distribuídas dinamicamente entre todos os núcleos de CPU disponíveis. Isso permite que a velocidade de execução das consultas escale de forma quase linear com o número de núcleos da máquina.

#### 2. Gestão Eficiente de Recursos (Memória e CPU)
- Otimização de Memória RAM e Spooling: O Hyper prioriza o processamento em memória para garantir tempos de resposta rápidos. Caso o volume de dados exceda a RAM disponível (geralmente acima de 80% de uso), ele utiliza um mecanismo de transbordamento (spooling) adaptativo para SSDs, carregando apenas as colunas específicas exigidas pela visualização ativa.
- Uso Intensivo da CPU: Ele é projetado para maximizar o uso de cada núcleo, podendo utilizar, por padrão, até 75% da CPU por hora durante o processamento de consultas para garantir a maior rapidez possível.

#### 3. Melhorias no Ciclo de Vida dos Dados
- Ingestão Acelerada (Extratos): Com o Hyper, os extratos são gerados quase tão rápido quanto o sistema de origem consegue entregar os dados, eliminando etapas de pós-processamento como a ordenação (sorting), que eram necessárias em versões anteriores.
- Suporte a Volumes Massivos: A tecnologia permite lidar com extratos que chegam a bilhões de linhas, superando limitações de motores antigos e permitindo que mais dados sejam consolidados em um único arquivo .hyper.

#### 4. Técnicas Avançadas de Consulta
O motor utiliza uma série de otimizações internas para tornar as buscas mais velozes, incluindo:
- Materialização de valores mínimos e máximos para cada coluna.
- Mini-índices para otimizar os intervalos de busca.
- Dicionários granulares ao nível de bloco de dados.
- Lógica avançada para otimização de junções (joins) e subconsultas.
Essas características combinadas permitem que o Tableau realize análises exploratórias fluidas ("na velocidade do pensamento") mesmo quando o analista interage com volumes massivos de informação.

### 3. Visuais para Estatística em Larga Escala
Prompt: "Quais são os visuais mais utilizados no dia a dia de um profissional que usa Tableau para Análise Estatística em Big Data?"
Raciocínio: Buscar a aplicação prática da EVA (Análise Visual Exploratória).
Resposta completa: Os visuais essenciais incluem:
Histogramas e Box Plots: Para distribuição e identificação automática de outliers via Intervalo Interquartil (IQR).
Gráficos de Dispersão com Clustering: Para visualização de agrupamentos k-means.
Marcas de Densidade (Heatmaps): Cruciais em Big Data para evitar o overplotting em milhões de registros.
Eixos Duplos Sincronizados: Para comparar dados reais com previsões de modelos MODEL_QUANTILE.

### 4. Análise de Decisão: Tableau vs. Python
Prompt: "Faça um paralelo entre vantagens e desvantagens do Tableau versus Python com a finalidade de análise exploratória e estatística em Big Data."
Raciocínio: Entender o posicionamento da ferramenta no mercado (Buy vs. Build).
**Resposta completa:** 
Ao analisar o Tableau em comparação com o Python para análise exploratória e estatística em cenários de Big Data, observam-se distinções claras em termos de acessibilidade, profundidade estatística e performance.

#### 1. Curva de Aprendizado e Democratização
Tableau: Possui uma curva de aprendizado baixa a média, sendo projetado para ser amigável a profissionais não técnicos através de sua interface de arrastar e soltar. Ele funciona como uma ferramenta de democratização analítica, permitindo que diversos setores da empresa acessem e entendam os dados.
Python: Exige um nível de conhecimento alto, demandando domínio de lógica de programação e métodos de ciência de dados.

#### 2. Performance e Aderência ao Big Data
Tableau: Demonstra excelente aderência ao Big Data devido ao motor Hyper, que utiliza compressão colunar, compilação JIT (Just-In-Time) e paralelização para processar bilhões de linhas com alta velocidade.
Python: Para lidar com volumes massivos, o Python é frequentemente dependente de bibliotecas externas de processamento distribuído, como Spark ou Dask, não possuindo a mesma otimização "nativa" para exploração visual instantânea que o motor Hyper oferece.

#### 3. Profundidade Estatística e Customização
Tableau: Oferece recursos estatísticos nativos e automáticos, como Clustering (k-means) e funções preditivas (MODEL_QUANTILE), que facilitam a exploração rápida. Contudo, possui limitações severas em análises formais, carecendo de testes de hipótese clássicos (como t-Student ou Qui-Quadrado) e validações de premissas de modelos diretamente na interface.
Python: Oferece controle absoluto e customização total. Através de bibliotecas como scikit-learn e statsmodels, permite a aplicação de qualquer técnica estatística ou modelo de machine learning complexo, como redes neurais e processamento de linguagem natural.

#### 4. Custos e Integração
Tableau: Apresenta um custo de licenciamento elevado, baseado em perfis funcionais (Creator, Explorer, Viewer), o que pode ser uma barreira para equipes menores.
Python: É um ecossistema gratuito e open-source, com uma comunidade acadêmica vasta e suporte amplo a bases NoSQL e manipulação de JSON, áreas onde o Tableau ainda é limitado.

#### 5. Sinergia (O melhor dos dois mundos)
É importante notar que as ferramentas não são mutuamente exclusivas. O Tableau pode ser estendido via TabPy, permitindo que scripts Python sejam executados dentro de campos calculados do Tableau. Isso permite que a potência estatística do Python seja entregue através da interface visual intuitiva do Tableau, embora exija cuidados com a latência de rede em visualizações com muitas marcas.

### 5. Integração e Extensibilidade (TabPy)
Prompt: "Como funciona a integração do Tableau com Python?"
Cicatriz (Troubleshooting): Precisei entender como evitar que o Tableau ficasse lento ao chamar o Python.
**Resposta completa:**
A integração do Tableau com Python funciona principalmente através de um componente chamado TabPy (Tableau Python Server), que permite a execução de scripts Python diretamente em campos calculados do Tableau e o uso de modelos de machine learning em tempo real.
Abaixo estão os detalhes de como essa integração é estruturada e operada:

#### 1. Arquitetura e Conectividade
Servidor TabPy: O TabPy atua como um serviço que recebe requisições do Tableau, executa o código Python e devolve os resultados. Ele pode ser instalado localmente ou hospedado em infraestruturas de nuvem, como a AWS (em instâncias EC2), utilizando conexões HTTPS criptografadas para garantir a segurança dos dados.
Funções de Passagem (Pass-Through): A integração ocorre dentro de campos calculados do Tableau usando funções específicas, como SCRIPT_REAL, SCRIPT_STR, SCRIPT_INT e SCRIPT_BOOL. Esses comandos enviam os dados do Tableau para o Python como parâmetros estruturados.

#### 2. Formas de Execução
Existem duas maneiras principais de utilizar o Python com o Tableau:
Scripts Ad-hoc: O desenvolvedor escreve o código Python diretamente dentro de um cálculo no Tableau. Isso é útil para explorações rápidas ou transformações de dados simples.
Funções Publicadas: É possível treinar um modelo de machine learning (como uma Floresta Aleatória ou Redes Neurais) no Python e publicá-lo como uma função no servidor TabPy. O Tableau então chama essa função pelo nome, passando novos dados para obter predições, o que facilita o gerenciamento e a governança dos modelos.

#### 3. Casos de Uso em Big Data e Estatística
A integração permite aplicar bibliotecas avançadas como scikit-learn e statsmodels para tarefas que o Tableau não realiza nativamente:
Agrupamento Avançado: Uso de algoritmos como DBSCAN para identificar hotspots geográficos ou padrões complexos em grandes volumes de dados.
Predição e Classificação: Criação de modelos para prever rotatividade de funcionários (attrition), pontuação de leads de vendas ou diagnósticos médicos (ex: detecção de câncer) com alta precisão.

#### 4. Otimização de Performance
Um desafio crítico é a latência de rede. Se o Tableau estiver configurado para enviar dados "marca por marca", ele fará uma chamada HTTP individual para cada ponto no gráfico, o que degrada o desempenho.
Chamadas em Lote (Batching): Recomenda-se ajustar os cálculos de tabela para que todas as dimensões sejam enviadas em um único lote vetorial (single batch call). Isso garante que o modelo Python receba a matriz de dados completa de uma vez, reduzindo drasticamente o tempo de resposta.

#### 5. Outras Integrações via APIs
Além do TabPy para análise em tempo real, o Python é amplamente utilizado para automação de dados através de outras APIs:
- Hyper API: Permite que scripts Python criem, leiam e atualizem arquivos de extrato .hyper diretamente, facilitando a ingestão de bilhões de linhas vindas de fontes externas.
- Tableau Server Client (TSC): Biblioteca Python que utiliza a REST API para automatizar tarefas administrativas, como a publicação de fontes de dados e o agendamento de atualizações.
- Pantab: Uma biblioteca de código aberto que simplifica a conversão de DataFrames do Pandas para o formato Hyper do Tableau.

## 4. Miniguia de Estudo (Entrega Final)
Este estudo detalha como o Tableau atua como uma plataforma de Análise Visual Exploratória (EVA) de alta performance para ambientes de Big Data.
Abaixo, os pontos fundamentais de forma sintetizada:
- O Conceito de EVA: A análise visual exploratória baseia-se em um ciclo interativo de perguntas e inspeção visual que permite aos analistas atingirem uma precisão superior a 80% em tarefas complexas.
- Arquitetura Hyper: Para processar bilhões de registros, o motor Hyper utiliza compilação JIT (Just-In-Time) e paralelização baseada em morsels, escalando a performance de forma quase linear com os núcleos da CPU.
- Gestão de Dados: O uso de Extratos (.hyper) é a estratégia recomendada para Big Data, pois otimiza consultas e permite o transbordamento (spooling) para SSDs quando a memória RAM é insuficiente.
- Estatística e IA: A ferramenta oferece clustering k-means determinístico e funções preditivas nativas (MODEL_QUANTILE), além do Explain Data, que utiliza modelos estatísticos automáticos para justificar anomalias e outliers.
- Integração com Python: Através do TabPy, é possível estender o Tableau com modelos complexos de machine learning, sendo essencial o uso de chamadas em lote (batching) para evitar latência em grandes volumes de dados.
- Comportamento do Analista: Pesquisas mostram que o ritmo da exploração é mais lento do que o assumido por desenvolvedores de sistemas (14-15 segundos de "tempo de reflexão"), o que permite a aplicação de otimizações de sistema durante essas pausas

**Glossário de Conceitos**
- Hyper: Motor de dados em memória do Tableau otimizado para consultas analíticas rápidas.
- VizQL: Tecnologia que converte interações visuais em queries de banco de dados.
- Morsel-Driven Parallelization: Técnica que divide blocos de dados em pequenas frações de trabalho para distribuição entre núcleos de CPU.
- Spooling: Processo de mover dados da RAM para o disco (SSD) quando a memória física é insuficiente, evitando falhas em queries pesadas.
- TabPy: Servidor que permite integrar scripts Python diretamente em campos calculados do Tableau.

**Prompts Reutilizáveis para Revisão**
"Resuma o funcionamento do algoritmo k-means no Tableau e como ele decide o número ideal de clusters."
"Quais as melhores práticas de engenharia de dados para otimizar extratos .hyper com bilhões de linhas?"
"Explique a diferença entre os modelos de regressão linear regularizada e processos gaussianos nas funções de modelagem preditiva."
