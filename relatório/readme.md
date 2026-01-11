\documentclass[12pt,a4paper]{article} %fonte da letra e tamanho do documento
\usepackage[utf8]{inputenc} % possibilita utilizar códigos directos para alguns caracteres específicos
\usepackage{natbib} %auxiliar nas citações/referências
\usepackage[portuges]{babel} %garantir que os acentos da língua portuguesa são "lidos"
\usepackage{fancyhdr} %permitir acrescentar cabeçalhos e rodapés
\usepackage{graphicx} %possibilita adicionar gráficos, figuras
\usepackage{float} %não permite que uma imagem/tabela seja dividida em duas páginas \usepackage{wrapfig} %permite que haja texto à volta de imagens/tabelas
\usepackage{indentfirst} %indentação da primeira linha do parágrafo
\usepackage[left=2.5 cm,top=3cm,right=2.5cm,bottom=2.5cm,bindingoffset=0.5cm]{geometry} 
%Medidas poderão ser alteradas conforme as normas/requerimento do docente/empresa, bindingoffset acrescebta espaço extra na margem esquerda para encadernação
\usepackage{multirow} %permite criar tabelas com várias linhas e colunas
\usepackage[table,xcdraw]{xcolor} %usar outras cores na tabela
\usepackage{amsmath} %permite usar símbolos matemáticos
\usepackage[pdftex]{hyperref} %permite criar hiperligações
\usepackage{subfigure} %usar várias imagens em simultâneo
\usepackage{fancyheadings}
 %usar estilo fancy para os cabeçalhos e rodapés
\usepackage{adjustbox}
\renewcommand{\baselinestretch}{1.5} %parágrafos com espaçamento de 1.5
\usepackage{booktabs} %estilo de tabela
\usepackage{caption}
\usepackage{placeins}
\usepackage[T1]{fontenc} %nclui todos os caracteres acentuados do alfabeto ocidental
\usepackage{hyperref}
\usepackage{xcolor}
\usepackage{titlesec}

% Cor usada nos títulos (podes alterar)
\definecolor{chaptercolor}{RGB}{90,120,140}

% Estilo do número grande
\titleformat{\chapter}[display]
  {\normalfont\bfseries\huge\color{chaptercolor}}
  {\fontsize{60}{60}\selectfont\thechapter\ \textcolor{chaptercolor}{|}}
  {1ex}
  {\Huge}



% **************************************************************************************************************
\pagestyle{fancy} %usado para o estilo do cabeçalho e rodapé

\rhead{ATP} %cabeçalho do lado direito
\lhead{LEBIOM} %cabeçalho do lado esquerdo
%\chead{\includegraphics[scale=0.1]{./Imagens/EEUMLOGO.png}} %podem ser adicionadas imagens ao cabeçalho também (centro)

\begin{document}
%**********************************************CAPA*************************************************

\begin{titlepage} % pagina não numerada 

\begin{figure}[h]
\centering
\includegraphics[scale=0.4]{./Imagens/EEUMLOGO.png}    
\end{figure}


\begin{center} 
    
  \vspace{1cm}

  \begin{large}  
  \bfseries {\Huge{Relatório do Projeto}} 
  \vspace{2cm}
  
  \upshape {{Licenciatura em Engenharia Biomédica}} 
  \vspace{1 cm}
  
  \bfseries {Algoritmos e Técnicas de Programação\\ 
  Ano Letivo 2025/2026}
    \vspace{1,5 cm}
    \end{large}  
  
  {Catarina Peixoto, A112402\\
  Joana Sousa, A111697\\
  Mafalda Sequeira, A112113} 
  \vspace{2 cm}

{{Docentes: José Carlos Ramalho e Luís Filipe Cunha
}
  \vspace{1.5 cm}
  
  {7 de janeiro de 2025}
  }
  \end{center}

\thispagestyle{empty} %forçar o documento a não ter mais nada para além daquilo que eu escrevo no titlepage
\end{titlepage}

\pagenumbering{roman} %inicio da numeração romana
\cfoot{\thepage} %estilo da paginação

%INDICE NORMAL
\newpage  %cria nova página
\renewcommand*\contentsname{Índice} %renomeia a página de contents como indice
\tableofcontents %permite adicionar conteudo ao indice automaticamente




\newpage
\renewcommand*\contentsname{Índice de Figuras}
\listoffigures%permite adicionar conteudo ao indice automaticamente

\newpage
\pagenumbering {arabic} %fim da numeração romana e quero numeração numérica

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
\newpage
\section{Introdução}

No âmbito da Unidade Curricular de Algoritmos e Técnicas de Programação, foi solicitado o desenvolvimento de uma aplicação em Python para simular o atendimento de doentes numa clínica médica. Este projeto laboratorial, intitulado "Simulação de uma Clínica Médica", tem como objetivo principal a modelação de sistemas do mundo real através de processos probabilísticos, implementando uma simulação de eventos discretos que replica o fluxo de pacientes num ambiente clínico.

A aplicação desenvolvida permite simular a chegada aleatória de doentes segundo uma distribuição de Poisson, o seu atendimento por um conjunto de médicos cujo tempo de consulta segue distribuições probabilísticas (exponencial, normal ou uniforme), e a gestão de uma fila de espera quando todos os médicos se encontram ocupados. Durante a simulação, são registados diversos parâmetros de desempenho, incluindo tempos de espera, tamanhos das filas e percentagem de ocupação dos médicos.

Para além da simulação base, o sistema oferece funcionalidades de análise que permitem estudar o comportamento da clínica sob diferentes condições operacionais, como a variação da taxa de chegada de pacientes ou a alteração dos parâmetros de duração das consultas. A aplicação inclui uma interface gráfica desenvolvida com o módulo simpleGUI, onde é possível configurar parâmetros, executar simulações e visualizar resultados através de gráficos informativos.

O projeto exige ainda a consideração e tratamento de casos específicos do sistema de saúde simulado, o desenvolvimento de uma interface intuitiva, e a capacidade de gerar análises estatísticas relevantes para a gestão de recursos médicos. Através desta implementação, os alunos aplicam conceitos fundamentais de programação, análise de dados e modelação de sistemas, consolidando competências técnicas essenciais para a Engenharia Biomédica.

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%\section{Análise e Especificação}
\newpage
\section{Análise e Especificação}
\subsection{Descrição informal do problema}
O sistema a desenvolver deve simular o funcionamento de uma clínica médica na qual os pacientes chegam de forma aleatória, seguindo uma distribuição de Poisson. Logo a seguir, são triados por enfermeiros, que atribuem pulseiras, também de forma aleatória (verde, amarela, vermelha) indicando a sua prioridade. De seguida, são encaminhados para especialidades médicas específicas onde aguardam em fila de espera até um médico da especialidade estar disponível. Quando este se encontra disponível, os pacientes são atendidos e, no final da consulta, saem da clínica.

O sistema deve registar estatísticas importantes como tempos de espera, tamanhos das filas, taxa de ocupação de médicos e enfermeiros e número de pacientes atendidos. Estes dados seguem distribuições aleatórias, tornando cada simulação diferente e mais próxima da realidade. No final da simulação, o objetivo é analisar estes resultados e perceber como diferentes configurações afetam o desempenho da clínica.

%_______________________________________________________________
\subsection{Especificação de requesitos}
\subsubsection{Dados}

Para a realização deste projeto, foi-nos fornecido um ficheiro JSON (pessoas.json) contendo informações de pessoas simuladas que serão utilizadas como pacientes em formato de dicionário. Cada pessoa possui:
\begin{itemize}
\item Id: identificador único (formato "p1", "p2", etc.)
\item Nome: nome completo do paciente
\item Idade: idade do paciente
\item Sexo: sexo do paciente
\item Informações adicionais conforme necessário
\end{itemize}

Para além disso, foi também fornecido pelos docentes um código base em Python (\texttt{clinic\_alunos.py}) que implementa uma versão simplificada da simulação, servindo como ponto de partida para o desenvolvimento do projeto completo.

O código base implementa um cenário mais simlpes onde os pacientes chegam aleatoriamente à clínica segundo uma distribuição de Poisson; são atendidos por médicos disponíveis em regime de "primeiro a chegar, primeiro a ser atendido"; se não há médico disponível, aguardam numa fila de espera; o tempo de consulta varia de acordo com uma distribuição configurável (exponencial, normal ou uniforme); e após a consulta, o paciente sai e o médico fica disponível para atender o próximo da fila.

Após a análise cuidadosa deste código, fomos capazes de colocá-lo noutro patamar, implementando mais funções que vão ser descritas já de seguida.

\subsubsection{Pedidos}
Como vimos antes, são pedidas diversas funções na formulação do sistema, em seguida enumeramos o que é pedido para cada uma das funções requesitadas.

\subsubsection*{Parâmetros de configuração}

Portanto, deve haver no trabalho, parâmetros configuráveis como:
\begin{itemize}
\item Número de enfermeiros na clínica
\item Número de médicos disponíveis
\item Taxa de chegada de pacientes (pacientes/hora)
\item Tempo médio de triagem (minutos)
\item Tempo médio de consulta (minutos)
\item Duração total da simulação (minutos)
\item Tipo de distribuição (exponential, normal,
uniform)
\end{itemize}

\newpage

\subsubsection*{Resultados esperados}

Tal como qualquer trabalho, é esperado atingirmos resultados específicos, neste caso é fundamental reconhecer:
\begin{itemize}
    \item Tempo médio de espera para os doentes
    \item Tempo médio de consulta
    \item Quanto tempo em média esteve cada doente na clínica
    \item Tamanho da fila de espera (média e máximo)
    \item Percentagem de tempo em que os médicos estão ocupados
    \item Número total de doentes atendidos
\end{itemize}

\subsubsection*{Interface gráfica}

Deverá ter uma interface gráfica desenvolvida com o módulo simpleGUI na qual deverá ser possivel:

\begin{enumerate}
    \item \textbf{Executar uma simulação} - Processar eventos de chegada, triagem e saída.
    \item \textbf{Alterar os parametros da simulação} - Permitir ao utilizador definir todos os parâmetros antes de executar a simulação.
    \item \textbf{Visualizar  resultados} - Tabela de Log que mostra cronologicamente todos os eventos da simulação.
    \item \textbf{Visualização de gráficos} -  a fila de espera e ocupação dos médicos.
\end{enumerate}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%\section{Conceção da Resolução}
\newpage
\section{Conceção da Resolução}

\subsection{Estrutura de dados}

Para a realização deste projeto, foi necessário definir cuidadosamente as estruturas de dados que suportariam toda a lógica da simulação. A escolha adequada destas estruturas foi crucial para garantir eficiência, clareza do código e facilidade de manutenção.

\subsubsection*{Fila de Eventos}

A simulação baseia-se no conceito de eventos discretos, organizados numa lista cronológica denominada \texttt{queueEventos}. Cada evento é representado por um tuplo de três elementos: o tempo de ocorrência (valor decimal em minutos), o tipo de evento (\texttt{"chegada", "fim\_triagem" ou "saída"}) e o id do paciente envolvido.

Para garantir o funcionamento correto, a lista deve manter sempre a ordem temporal. Assim, ao criar um novo evento, é preciso inseri-lo na posição adequada. Para isso existem três funções: uma que encontra a posição de inserção, outra que adiciona o evento (\texttt{enqueue}) e uma terceira que remove o próximo evento a processar (\texttt{dequeue}).

\subsubsection*{Fila de espera}

O sistema possui duas filas de espera distintas, cada uma servindo um propósito específico no fluxo de atendimento.

A primeira é a fila de triagem (\texttt{fila\_triagem}), onde aguardam os pacientes que chegaram à clínica mas ainda não foram atendidos por um enfermeiro. Cada elemento desta fila é um tuplo contendo o id do paciente e o momento em que chegou à clínica.

A segunda é a fila de médicos (\texttt{queue}), significativamente mais complexa que a anterior. Aqui aguardam os pacientes que já foram triados e estão à espera de serem atendidos por um médico da especialidade apropriada. Esta fila não funciona num simples regime de "primeiro a chegar, primeiro a ser atendido" - em vez disso, implementa um sistema de prioridades baseado na cor da pulseira atribuída durante a triagem. Quando um médico fica disponível, o sistema procura na fila o paciente com maior prioridade (pulseira vermelha > amarela > verde) que necessita daquela especialidade específica. Em caso de empate na prioridade, prevalece quem chegou primeiro.

\subsubsection*{Dicionário do Paciente}\label{subsubsec: Dicionário do Paciente}

Toda a informação sobre cada paciente é armazenada num dicionário Python \texttt{(doentes)}, onde a chave é o id único do paciente e o valor é outro dicionário contendo todos os seus dados. Estes dados incluem as informações originais carregadas do ficheiro JSON (como nome e ID), bem como atributos atribuídos dinamicamente durante a simulação que seguem a seguinte distribuição:

\textbf{Cor da pulseira:}
\begin{itemize}
    \item Verde: 70\% dos casos (baixa prioridade)
    \item Amarela: 20\% dos casos (prioridade média)
    \item Vermelha: 10\% dos casos (alta prioridade)
\end{itemize}

\textbf{Especialidade médica:}
\begin{itemize}
    \item Medicina Geral: 35\%
    \item Ortopedia: 20\%
    \item Gastroenterologia: 15\%
    \item Cardiologia: 15\%
    \item Neurologia: 10\%
    \item Psiquiatria: 5\%
\end{itemize}

\subsubsection*{Lista de Enfermeiros}

Os enfermeiros são representados numa lista \texttt{(enfermeiros)}, onde cada enfermeiro é outra lista contendo cinco elementos: identificador (string no formato "e1", "e2", etc.), estado de ocupação (booleano indicando se está a atender alguém), identificador do paciente atual (None se estiver livre), tempo total acumulado em que esteve ocupado (para calcular estatísticas) e o momento em que iniciou a triagem atual.

Esta estrutura permite não apenas saber quem está disponível, mas também calcular a taxa de ocupação de cada enfermeiro ao longo da simulação. Para equilibrar a carga de trabalho, implementamos um algoritmo que, ao procurar um enfermeiro disponível, seleciona aquele que tem o menor tempo total de ocupação acumulado.

\subsubsection*{Lista de médicos}

Semelhante aos enfermeiros, os médicos são representados numa lista \texttt{(medicos)}, mas com um elemento adicional: a especialidade. Cada médico é uma lista com seis elementos: identificador, estado de ocupação, paciente atual, tempo total ocupado, momento de início da consulta atual e especialidade médica. 

A atribuição de especialidades aos médicos é feita durante a inicialização da simulação, seguindo uma distribuição específica:
\begin{itemize}
    \item Medicina Geral: 30\%
    \item Ortopedia: 20\%
    \item Gastroenterologia: 15\%
    \item Cardiologia: 20\%
    \item Neurologia: 10\%
    \item Psiquiatria: 5\%
\end{itemize}

Os primeiros médicos criados recebem automaticamente as seis especialidades principais (garantindo que há pelo menos um médico de cada especialidade), e os restantes recebem especialidades de forma probabilística, com maior peso para Medicina Geral e Cardiologia.

\subsubsection*{Estruturas para visualização gráfica}

Para permitir a criação dos gráficos analíticos, implementamos cinco listas paralelas que registam a evolução do sistema ao longo do tempo:
\begin{itemize}
    \item \texttt{h\_t}: regista cada momento de tempo em que ocorreu um evento
    \item \texttt{h\_f\_tri}: regista o tamanho da fila de triagem em cada momento
    \item \texttt{h\_f\_med}: regista o tamanho da fila de médicos em cada momento
    \item \texttt{h\_oc\_med}: regista a percentagem de médicos ocupados em cada momento
    \item \texttt{h\_oc\_enf}: regista a percentagem de enfermeiros ocupados em cada momento
\end{itemize}

Estas listas são atualizadas a cada evento processado, criando um histórico completo que alimenta os gráficos apresentados na interface.
%_______________________________________________________________

\subsection{Modelação do sistema}

A modelação do sistema foi concebida para replicar de forma realista o funcionamento de uma clínica médica, capturando a complexidade das interações entre pacientes, enfermeiros e médicos.

\subsubsection*{Fluxo do atendimento}
O ciclo de vida de um paciente na clínica passa por três fases principais.

Na primeira fase, um paciente chega à clínica. Este momento é um evento de tipo \texttt{"chegada"}  gerado antes do início da simulação, seguindo uma distribuição de Poisson que modela chegadas aleatórias mas com uma taxa média definida. Quando este evento é processado, o sistema carrega os dados do paciente tenta atribuí-lo a um enfermeiro disponível. Se existe um enfermeiro livre (especificamente, aquele que tem o menor tempo acumulado de trabalho), a triagem inicia imediatamente e é agendado um evento de \texttt{"fim\_triagem"} para o futuro. Caso contrário, o paciente entra na fila de triagem e aguarda.

A segunda fase inicia quando ocorre um evento de \texttt{"fim\_triagem"}. Neste momento, o enfermeiro que realizou a triagem fica disponível novamente e, se há pacientes na fila de triagem, o próximo é imediatamente chamado. O paciente triado recebe então dois atributos cruciais: uma cor de pulseira e uma especialidade médica necessária (determinadas aleatoriamente de acordo com as distribuições mencionadas em ~\ref{subsubsec: Dicionário do Paciente}). Logo a seguir, o sistema procura um médico disponível da especialidade correta e, se encontrado, a consulta inicia e agenda-se um evento de \texttt{"saída"}. Se não, o paciente entra na fila de médicos.

A terceira e última fase ocorre com o evento de \texttt{"saída"}, quando a consulta termina. O médico fica livre e incrementa-se o contador de pacientes atendidos. Crucialmente, se existe uma fila de espera, não é simplesmente chamado o próximo paciente, em vez disso, executa-se um algoritmo de priorização que percorre toda a fila procurando o paciente prioritário que necessita daquela especialidade específica.


\subsubsection*{Sistema de prioridades}
O sistema de priorização implementado é sofisticado e multi-critério. Quando um médico de uma determinada especialidade fica disponível, o algoritmo percorre a fila de espera considerando três critérios hierárquicos:
\begin{enumerate}
    \item Considera apenas pacientes que necessitam daquela especialidade específica (exemplo: um paciente que precisa de Ortopedia nunca será atendido por um cardiologista, independentemente da sua prioridade).
    \item Entre os pacientes da especialidade correta, dá preferência absoluta à cor da pulseira: vermelha (valor 1) é atendida antes de amarela (valor 2), que é atendida antes de verde (valor 3).
    \item Em caso de empate na cor da pulseira, prevalece quem chegou primeiro (FIFO - First In, First Out).
\end{enumerate}

\subsubsection*{Distribuições Probabilísticas}

A simulação utiliza três distribuições probabilísticas diferentes, cada uma modelando um aspeto específico do sistema:
\begin{itemize}
    \item \textbf{Distribuição de Poisson} governa as chegadas de pacientes. Esta é uma escolha clássica em teoria das filas porque modela bem eventos aleatórios que ocorrem de forma independente a uma taxa média constante.
    \item \textbf{Distribuição Exponencial} é usada por defeito para os tempos de triagem e pode também ser usada para os tempos de consulta.
    \item \textbf{Distribuição normal} para os tempos de consulta, o que gera valores concentrados em torno da média com menor variabilidade, ou uma distribuição uniforme, onde qualquer valor entre metade e uma vez e meia da média é igualmente provável.
\end{itemize}

\newpage
\subsection{Interface gráfica}
A interface gráfica foi desenvolvida com o objetivo de tornar a simulação acessível, intuitiva e visualmente informativa, permitindo que utilizadores sem conhecimentos de programação possam explorar diferentes cenários.

\subsubsection{Estrutura geral da Interface}
A janela principal foi organizada seguindo princípios de design de interfaces (\ref{fig:interface}). No topo, um título em destaque identifica a aplicação. Abaixo, encontra-se a secção de configurações, onde todos os parâmetros da simulação podem ser ajustados através de campos de entrada numéricos simples. Esta secção inclui:

\begin{itemize}
    \item Número de enfermeiros (valor inteiro)
    \item Número de médicos (valor inteiro)
    \item Taxa de chegada de pacientes em pacientes por hora (valor inteiro)
    \item Duração total da simulação em minutos (valor inteiro)
    \item Tempo médio de triagem em minutos (valor decimal)
    \item Tempo médio de consulta em minutos (valor decimal)
    \item Tipo de distribuição para tempos de consulta (menu de seleção)
\end{itemize}

\begin{figure}[h]
    \centering
    \includegraphics[width=0.4\linewidth]{./Imagens/image1.png}
    \caption{Interface}
    \label{fig:interface}
\end{figure}


\subsubsection{Botões de controlo}
Dois botões principais controlam a aplicação, o botão "Executar Simulação" e o botão Sair.

Um aspeto importante do design foi garantir que a simulação pode ser executada múltiplas vezes sem fechar a aplicação. Cada execução limpa os resultados anteriores e processa uma nova simulação independente, permitindo comparações rápidas entre diferentes configurações.

\subsubsection*{Botão Executar Simulação}

O botão "Executar Simulação" (\ref{fig:executar}), destacado visualmente com cor de fundo amarela clara, inicia todo o processo de simulação com os parâmetros atualmente configurados.

\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\linewidth]{Imagens/image2.png}
    \caption{Botão Executar simulação}
    \label{fig:executar}
\end{figure}

\subsubsection*{Botão Sair}

O botão "SAIR" (\ref{fig:sair}) permite fechar a aplicação de forma limpa.

\begin{figure}[h]
    \centering
    \includegraphics[width=0.3\linewidth]{Imagens/image3.png}
    \caption{Botão Sair}
    \label{fig:sair}
\end{figure}

\subsubsection{Estrutura de Tabs para resultados}

Os resultados são apresentados através de um sistema de tabs (separadores) que organiza a informação em três categorias distintas:

\newpage
\subsubsection*{Tab de Log}

A Tab de Log (\ref{fig:log}) apresenta um registo cronológico completo de todos os eventos da simulação. Cada linha mostra o tipo de evento (Chegada, Triagem, Fim Triagem, Atendido, Espera, Saída), o tempo em que ocorreu, o id do paciente envolvido e detalhes adicionais contextuais. Por exemplo, ao ver "Triado", são mostradas a cor da pulseira atribuída e a especialidade. Este log é apresentado numa caixa de texto de múltiplas linhas, não editável mas com scroll automático.

\begin{figure}[h]
    \centering
    \includegraphics[width=0.8\linewidth]{Imagens/image4.png}
    \caption{Tab de Log}
    \label{fig:log}
\end{figure}


\subsubsection*{Tab de Estatistica}

A Tab de Estatísticas apresenta métricas calculadas sobre o desempenho do sistema. Para cada enfermeiro, mostra o seu identificador e a percentagem de tempo que passou ocupado durante toda a simulação (\ref{fig:estatenfer}). Para cada médico, mostra adicionalmente a sua especialidade entre parênteses. Estas estatísticas permitem identificar rapidamente se há recursos subutilizados (baixa ocupação) ou sobrecarregados (ocupação próxima de 100\%)(\ref{fig:estatmedic}).

\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\linewidth]{Imagens/image5.png}
    \caption{Tab de Estatística - Enfermeiros}
    \label{fig:estatenfer}
\end{figure}

\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\linewidth]{Imagens/image6.png}
    \caption{Tab de Estatística - Médicos}
    \label{fig:estatmedic}
\end{figure}


\newpage
\subsubsection*{Tab de Gráficos}

A Tab de Gráficos é a mais complexa visualmente. Apresenta três gráficos de linha empilhados verticalmente, cada um mostrando a evolução temporal de métricas diferentes:
\begin{itemize}
    \item O primeiro gráfico mostra simultaneamente duas linhas: o tamanho da fila de triagem (azul turquesa) e o tamanho da fila de médicos (rosa choque), permitindo comparar visualmente como as duas filas evoluem (\ref{fig:evolfilas})
\end{itemize}

\begin{figure}[h]
    \centering
    \includegraphics[width=0.6\linewidth]{Imagens/image7.png}
    \caption{Gráfico - Evolução das Filas}
    \label{fig:evolfilas}
\end{figure}

\newpage
\begin{itemize}
    \item O segundo gráfico mostra a taxa de ocupação dos enfermeiros ao longo do tempo, em percentagem (\ref{fig:ocupeferm})
\end{itemize}
\begin{figure}[h]
    \centering
    \includegraphics[width=0.6\linewidth]{Imagens/image8.png}
    \caption{Gráfico - Ocupação dos Enfermeiros}
    \label{fig:ocupeferm}
\end{figure}

\begin{itemize}
    \item O terceiro gráfico mostra a taxa de ocupação dos médicos ao longo do tempo, também em percentagem (\ref{fig:ocupmed})
\end{itemize}

\begin{figure}[h]
    \centering
    \includegraphics[width=0.6\linewidth]{Imagens/image9.png}
    \caption{Gráfico - Ocupação dos Médicos}
    \label{fig:ocupmed}
\end{figure}


Esta secção foi implementada como uma coluna com scroll vertical, permitindo que o utilizador visualize confortavelmente os três gráficos mesmo em ecrãs mais pequenos.

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%\section{Codificação e Testes}
\newpage
\section{Codificação e Testes}

\subsection{Alternativas, Decisões e Problemas de Implementação}

Durante o desenvolvimento deste projeto, foram encontrados diversos desafios técnicos que exigiram análise cuidadosa, pesquisa de soluções e, em alguns casos, refatorização significativa do código. Esta secção documenta os principais problemas enfrentados e as soluções implementadas.


\subsubsection{Problemas e Implementação}

\subsubsection*{Validação de Inputs Numéricos}

Um dos primeiros problemas identificados relacionou-se com a entrada de dados por parte do utilizador. Como a interface permite configurar diversos parâmetros numéricos, era essencial garantir que apenas valores válidos fossem aceites.

A solução implementada envolveu uma validação em duas etapas. Primeiro, todos os valores são convertidos para decimais (float) dentro de um bloco try-except, capturando qualquer tentativa de inserir texto não numérico. Se esta conversão for bem-sucedida, verifica-se então quais campos devem ser especificamente inteiros (número de enfermeiros, número de médicos, taxa de chegada e duração da simulação). Apenas se ambas as validações passarem é que os valores são aceites e a simulação pode prosseguir.

Esta abordagem permite dar feedback específico ao utilizador: se inserir texto, recebe uma mensagem a indicar que deve introduzir apenas números (\ref{fig:erro1}); se inserir um decimal num campo que requer inteiro, recebe uma mensagem diferente explicando que aqueles campos específicos devem ser números inteiros (\ref{fig:erro2}).

\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\linewidth]{Imagens/image10.png}
    \caption{Mensagem se inserir texto}
    \label{fig:erro1}
\end{figure}

\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\linewidth]{Imagens/image11.png}
    \caption{Mensagem se inserir números decimais}
    \label{fig:erro2}
\end{figure}

\subsubsection*{Gestão de múltiplos Gráficos}

A visualização gráfica apresentou um problema particular: quando a simulação era executada múltiplas vezes, os novos gráficos sobrepunham-se aos anteriores em vez de os substituir, criando uma interface confusa e consumindo memória progressivamente.

A solução implementada verifica, antes de criar novos gráficos, se já existem canvas anteriores. Se existirem, os seus widgets Tkinter são explicitamente destruídos. Este processo é repetido para os três canvas (fila de espera, ocupação de enfermeiros e ocupação de médicos). Apenas após garantir que todos os canvas anteriores foram destruídos é que se criam as novas figuras matplotlib e se desenham os novos gráficos.


\subsubsection*{Balanço de carga entre Enfermeiros}

Durante os testes iniciais, observou-se um padrão não desejado: o primeiro enfermeiro da lista tinha consistentemente uma taxa de ocupação muito superior aos restantes. A análise do código revelou que a função de procura de enfermeiro livre simplesmente retornava o primeiro que encontrasse disponível, sem qualquer critério de balanceamento.

Para resolver este problema, foi implementado um algoritmo que, em vez de retornar o primeiro enfermeiro livre, percorre todos os enfermeiros disponíveis e seleciona aquele que tem o menor tempo total acumulado de ocupação. Isto distribui a carga de trabalho equitativamente.
\newpage
\subsubsection*{Sistema de prioridades na fila de Médicos}

A implementação do sistema de prioridades foi um dos pontos mais difíceis, porque não bastava ordenar a fila por cor da pulseira: era preciso considerar especialidade, prioridade e tempo de chegada ao mesmo tempo.

O algoritmo faz uma procura linear, mantendo o melhor candidato encontrado até então. Para isso, começa com valores sentinela: índice = -1, prioridade = 999 e tempo de chegada = 999999.

Depois percorre toda a fila. Para cada paciente, verifica primeiro se a especialidade necessária coincide com a do médico livre; se não coincidir, ignora-o. Se coincidir, obtém a prioridade numérica da pulseira (vermelha=1, amarela=2, verde=3).

Um paciente passa a ser o novo “melhor” se tiver prioridade superior (número menor) ou, em caso de empate, se tiver chegado mais cedo.

No fim, se o índice encontrado não for -1, remove-se esse paciente da fila, mesmo que não esteja na primeira posição, e inicia-se o seu atendimento.

\subsection{Exemplo de Execução}

Para demonstrar o funcionamento do sistema, apresentamos um cenário de teste que ilustra o funcionamento equilibrado da simulação, onde os recursos são dimensionados adequadamente para a demanda esperada (\ref{fig:configurações}). Os parâmetros utilizados foram:
\begin{itemize}
    \item Enfermeiros: 5
    \item Médicos: 8
    \item Taxa de Chegada: 10 pacientes/hora
    \item Tempo Médio de Triagem: 5 minutos
    \item Tempo Médio de Consulta: 15 minutos
    \item Duração da Simulação: 480 minutos (8 horas de funcionamento)
    \item Distribuição dos Tempos de Consulta: Exponencial
\end{itemize}

\newpage
\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\linewidth]{Imagens/image13.png}
    \caption{Configurações}
    \label{fig:configurações}
\end{figure}

Ao executar a simulação com estes parâmetros, o sistema primeiro apresentou no terminal a tabela de especialidades atribuídas aos médicos. Esta distribuição é feita automaticamente pelo sistema, garantindo que todas as seis especialidades têm pelo menos um médico:

\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\linewidth]{Imagens/image12.png}
    \caption{Médicos gerados e as suas especialidades}
    \label{fig:medicosgerados}
\end{figure}

O log gerado apresentou cronologicamente todos os eventos da simulação (\ref{fig:iniciolog}).
\begin{figure}[h]
    \centering
    \includegraphics[width=0.7\linewidth]{Imagens/image14.png}
    \caption{Início do Log de simulação}
    \label{fig:iniciolog}
\end{figure}

As estatísticas calculadas ao final da simulação mostraram um sistema bem balanceado. Para os enfermeiros, as taxas de ocupação foram:
\newpage
\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\linewidth]{Imagens/image15.png}
    \caption{Taxa de Ocupação dos Enfermeiros}
    \label{fig:enfermeiros}
\end{figure}

A proximidade destes valores confirma que o algoritmo de balanceamento de carga está a funcionar corretamente. Nenhum enfermeiro ficou significativamente mais sobrecarregado do que que os restantes.

Para os médicos, as taxas de ocupação variaram mais significativamente devido à variação das diferentes probabilidades de cada especialidade:

\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\linewidth]{Imagens/image16.png}
    \caption{Taxa de Ocupação dos Médicos}
    \label{fig:medicos}
\end{figure}

O primeiro gráfico, (\ref{fig:grafico1}) que mostra a evolução das filas, revelou padrões interessantes. A fila de triagem manteve-se uma linha reta, revelando que 5 enfermeiros chega perfeitamente para a taxa de chegada configurada.

A fila de médicos, em contraste, apresentou um comportamento mais irregular. Iniciou próxima de zero, cresceu gradualmente nas primeiras 2 horas até um pico de cerca de 14 pacientes por volta dos 300 minutos, depois foi diminuindo até ao fim da simulação.
\newpage
\begin{figure}[h]
    \centering
    \includegraphics[width=0.7\linewidth]{Imagens/image17.png}
    \caption{Gráfico Filas de Espera}
    \label{fig:grafico1}
\end{figure}

O segundo gráfico (\ref{fig:grafico2})mostrou a taxa de ocupação dos enfermeiros oscilando entre 20\% e 80\%. Os períodos de 100\% correspondiam a momentos onde todos os enfermeiros estavam simultaneamente ocupados. A média visual situou-se em torno de 20\%, consistente com as estatísticas calculadas.

\begin{figure}[h]
    \centering
    \includegraphics[width=0.7\linewidth]{Imagens/image18.png}
    \caption{Simulação - Taxa de Ocupação dos Enfermeiros}
    \label{fig:grafico2}
\end{figure}

O terceiro gráfico (\ref{fig:grafico3}), de ocupação dos médicos, apresentou maior variabilidade. A taxa oscilou entre 20\% e 80\%, refletindo a heterogeneidade das especialidades. Períodos de alta ocupação (>90\%) indicavam momentos onde quase todos os médicos estavam ocupados, o que, neste caso, acabou por não acontecer.  Enquanto os períodos de menor ocupação refletiam desbalanceamentos temporários entre oferta e demanda de especialidades específicas.

\begin{figure}
    \centering
    \includegraphics[width=0.7\linewidth]{Imagens/image19.png}
    \caption{Simulação - Taxa de Ocupação dos Médicos}
    \label{fig:grafico3}
\end{figure}

\clearpage

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%section{Conclusão}
\newpage
\section{Conclusão}

O desenvolvimento deste projeto revelou-se extremamente enriquecedor. A complexidade de coordenar múltiplos recursos (enfermeiros e médicos), gerir filas com diferentes prioridades e simular comportamentos estocásticos exigiu raciocínio lógico avançado e atenção aos detalhes.

Em suma, o projeto cumpriu os objetivos propostos e proporcionou uma sólida base de conhecimentos em simulação de sistemas, programação Python e análise de dados, competências essenciais para a Engenharia Biomédica.

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%\section{Referências Bibliográficas}
\newpage
\section{Referências}

\bibliographystyle{unsrt}
Ficheiros fornecidos pelos docentes para realização do projeto\\
\url{https://epl.di.uminho.pt/~jcr/AULAS/ATP2025/aulas2025.html}\\
\url{https://pythontutor.com/}\\


\end{document}


