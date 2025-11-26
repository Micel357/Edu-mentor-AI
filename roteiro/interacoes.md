 Documentação do Sistema de Agentes de IA: EduMentor AI

 Roteiro Textual das Interações

Visão Geral

Este repositório contém a documentação e os arquivos de configuração para o sistema de agentes de IA EduMentor AI. Baseado no roteiro de história fornecido, o sistema simula um processo de aprendizado personalizado para um aluno, coordenado por um Orquestrador e executado por uma equipe de agentes especializados.

Eventual Passo-a-Passo (Visão do Orquestrador)

O fluxo de trabalho é conduzido pelo Orquestrador (Luis) de forma sequencial e rigorosa. O fluxo principal para os temas de Português/Informática é:

1.
Análise Inicial: Luis recebe a demanda do aluno, analisa o perfil e define o plano de estudo inicial.

2.
Explicação de Conteúdo: Luis chama Thiago (Tutor de Conteúdo).

3.
Diagnóstico de Falhas: Luis chama Erika (Agente de Diagnóstico) para identificar o ponto de dificuldade.

4.
Apoio Emocional: Luis chama Mikael (Agente Motivacional) para reduzir a ansiedade e incentivar o aluno.

5.
Fixação Prática: Luis chama Sena (Agente de Exercícios) para criar atividades curtas e focadas.

6.
Avaliação de Domínio: Luis chama Julio (Agente de Avaliação) para corrigir o exercício e dar o veredito.

7.
Estratégia de Estudo: Luis chama Daniel (Agente de Estratégias) para sugerir um método de organização do tempo ou revisão.

8.
Parecer Final: Luis chama Jose (Agente de Relatório) para consolidar o processo e emitir o parecer final, encerrando o ciclo.




📂 Estrutura do Repositório

A organização dos arquivos foi pensada para facilitar a implementação e a compreensão do fluxo de trabalho:

Arquivo
Conteúdo
Propósito
AGENTS_CONFIG.json
Configuração técnica de todos os agentes em formato JSON.
Importação direta em frameworks de agentes (ex: Autogen, CrewAI).
AGENTS_PROMPTS.md
Lista detalhada dos System Prompts e objetivos de cada agente.
Referência rápida para o comportamento de cada agente.
WORKFLOW_OVERVIEW.md
Passo a passo de como o Orquestrador (Luis) conduz o fluxo.
Visão de alto nível da lógica de coordenação.
CONVERSATION_SIMULATION.md
Roteiro textual completo das interações entre o aluno e os agentes.
Exemplo prático e teste de validação do fluxo.





 Agentes Principais do Sistema

O sistema é composto por 7 agentes especializados, coordenados por Luis, o Orquestrador.

Agente
Função
Foco Principal (Extraído do JSON)
Luis
Coordenador Pedagógico (Orquestrador)
Gestão de Fluxo e Roteamento (Decidir sempre o próximo passo e manter a ordem de chamada).
Thiago
Tutor de Conteúdo
Explicação da matéria, tirar dúvidas e fornecer conceitos (Ser didático, objetivo e prático).
Erika
Agente de Diagnóstico
Identificar exatamente ONDE e POR QUE o aluno errou ou tem dificuldade (Entregar um diagnóstico claro).
Mikael
Agente Motivacional
Dar apoio emocional, reduzir a ansiedade e incentivar o aluno (Usar linguagem leve, empática e frases curtas de reforço).
Sena
Agente de Exercícios
Criar atividades práticas para fixar o conteúdo explicado (Criar 1 ou 2 exercícios curtos focados na dificuldade diagnosticada).
Julio
Agente de Avaliação
Corrigir o exercício do Sena ou verificar se o aluno dominou o tópico (Ser binário e direto na avaliação: "Correto" ou "Incorreto").
Daniel
Agente de Estratégias de Estudo
Sugerir como o aluno deve organizar o tempo ou revisar esse conteúdo específico (Foco em "como estudar", não "o que estudar").
Jose
Agente de Relatório de Progresso
Analisar todo o histórico da conversa para gerar um Parecer Final estruturado (Consolidar o processo e emitir o parecer final).





