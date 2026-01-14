# Simulação de uma Clínica Médica — ATP 2025/2026

Licenciatura em Engenharia Biomédica

Algoritmos e Técnicas de Programação

Projeto desenvolvido por: Catarina Peixoto, Joana Sousa, Mafalda Sequeira

Docentes: José Carlos Ramalho e Luís Filipe Cunha
_____________________________________________________________________________________________________________________________
## Objetivo do Projeto

Este projeto consiste no desenvolvimento de uma aplicação em Python para simular o funcionamento de uma **clínica médica** com múltiplos agentes: pacientes, enfermeiros e médicos. A simulação é baseada em eventos discretos, com chegadas probabilísticas, triagem, filas com prioridade e atendimento por especialidade.

A aplicação inclui também uma interface gráfica (simpleGUI) com visualização de logs, estatísticas e gráficos.
______________________________________________________________________________________________________________________________
## Setup
### Requisitos
- Python

#### Bibliotecas utilizadas:

- matplotlib

- simpleGUI (fornecida pela disciplina)

- json

- random

- statistics

- tkinter

### Ficheiros necessários

- pessoas.json – lista de pacientes simulados.

- clinic_alunos.py – código base fornecido pelos docentes.

- Ficheiros Python desenvolvidos pelos autores (simulação completa + GUI).
_____________________________________________________________________________________________________________________________
## Modelo de Simulação

O funcionamento do simulador baseia-se em três fases principais: chegada, triagem e consulta. Todos os eventos são organizados numa fila cronológica que controla o fluxo da simulação.

### Chegadas

As chegadas de pacientes seguem uma distribuição de Poisson, típica de sistemas reais de espera. Cada chegada gera um evento que tenta alocar um enfermeiro disponível; se nenhum estiver livre, o paciente entra na fila de triagem.

### Triagem

- Durante a triagem, o paciente recebe:
- Uma pulseira com prioridade (70% verde, 20% amarela, 10% vermelha)
- Uma especialidade médica (Geral, Ortopedia, Gastroenterologia, Cardiologia, Neurologia ou Psiquiatria), atribuída segundo probabilidades definidas

A seguir, o sistema tenta atribuir um médico da especialidade correta; se não existir um disponível, o paciente entra numa fila específica de médicos, ordenada por prioridade.

### Consultas

O tempo de consulta é determinado por uma das três distribuições configuráveis:

- Exponencial

- Normal

- Uniforme

Os médicos só atendem pacientes da sua especialidade e a seleção do próximo paciente é feita com base em:

- Especialidade compatível

- Prioridade da pulseira

- Tempo de chegada

_________________
## Funcionalidades 
### Simulação Clínica
A aplicação executa automaticamente:
- geração e processamento de eventos
- triagem e atendimento
- gestão equilibrada da carga dos enfermeiros
- sistema de prioridades na fila dos médicos
- recolha de métricas gerais e individuais

As estruturas de dados do sistema (filas, dicionários, listas de profissionais) garantem eficiência, clareza e estabilidade da simulação.

### Visualização Gráfica
A interface gráfica apresenta vários elementos essenciais:

- Gráfico da evolução das filas (triagem e médicos)

- Gráfico da ocupação dos enfermeiros

- Gráfico da ocupação dos médicos

- Gráfico da fila média de espera em função da evolução da fila
  
Estes gráficos são atualizados a cada simulação, com mecanismos que evitam sobreposição de figuras de execuções anteriores.

### Logs e Estatísticas

O separador de Logs apresenta um registo cronológico completo dos eventos: chegadas, início e fim de triagem, entrada em consulta e saída.
Nas estatísticas, é possível visualizar:

- tempo médio de espera
- tempo médio de consulta
- tempo média na clínica
- tamanho da fila de espera (máximo e média)
- quantidade de doentes atendidos
- tempo total de ocupação de cada enfermeiro
- ocupação de cada médico juntamente com a respetiva especialidade

Estas métricas permitem identificar gargalos e avaliar o dimensionamento dos recursos clínicos.

### Gestão da Equipa

Os médicos têm especialidades distribuídas de forma probabilística, mas garantindo sempre que existe pelo menos um médico de cada área.
Os enfermeiros são atribuídos com base num algoritmo que seleciona sempre o profissional com menor tempo acumulado de ocupação, evitando sobrecarga desigual.
____________________________________
## Interface Gráfica
Para tornar esta simulação acessível e visualmente intuitiva, foi desenvolvida uma interface gráfica utilizando simpleGUI. A interface permite configurar os seguintes parâmetros: 

- Número de enfermeiros:	Inteiro ≥ 1
- Número de médicos:	Inteiro ≥ 1
- Taxa de chegada:	Pacientes por hora
- Tempo médio de triagem:	Minutos
- Tempo médio de consulta:	Minutos
- Duração total:	Minutos de simulação
- Distribuição das consultas:	Exponencial, Normal ou Uniforme

Dispõe também de um mecanismo de Tabs com 3 separadores:
- Logs – registo cronológico de eventos
- Estatísticas – tabelas com ocupação dos recursos
- Gráficos – evolução das filas e ocupações ao longo do tempo

Inclui ainda botões para Executar Simulação e Sair, com validações de input robustas (deteção de texto, decimais indevidos e mensagens de erro informativas).
___________________________________________________________________________________________________________________________
## Exemplo de Simulação
Numa execução típica, por exemplo, com 5 enfermeiros, 8 médicos, taxa de chegada de 10 pacientes por hora, triagem média de 5 minutos e consultas de 15 minutos distribuídas exponencialmente ao longo de 480 minutos, observou-se um comportamento harmonioso do sistema. As taxas de ocupação dos enfermeiros mostraram-se equilibradas, validando o algoritmo de distribuição de carga. As ocupações dos médicos foram mais variáveis, refletindo a desigual procura por especialidades, o que é coerente com o modelo probabilístico implementado. A fila de triagem manteve-se curta e estável, enquanto a fila dos médicos variou ao longo do tempo, atingindo picos e descendo progressivamente consoante os períodos de maior procura.

__________________________________________________________________________________________________________________________
## Conclusão

Este projeto permitiu consolidar competências importantes na área da modelação computacional, simulação de sistemas reais, estruturação de dados, programação probabilística e criação de interfaces gráficas interativas. Para além disso, proporcionou uma visão prática sobre como gerir recursos clínicos e como pequenas alterações nos parâmetros podem provocar mudanças significativas no comportamento global do sistema. O trabalho cumpriu todos os objetivos propostos e constitui uma base sólida para extensões futuras, como a introdução de novos tipos de recursos, melhorias no sistema de prioridades, integração com bases de dados ou aumento do realismo clínico do modelo.
