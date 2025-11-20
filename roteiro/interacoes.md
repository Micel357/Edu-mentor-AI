# Roteiro textual das interações

## Visão geral
Eventual passo-a-passo, de como o orquestrador conduziu a equipe.


# Projeto de Agentes de IA: EduMentor AI

Este repositório contém a documentação e os arquivos de configuração para o sistema de agentes de IA **EduMentor AI**, baseado no roteiro de história fornecido. O sistema simula um processo de aprendizado personalizado para um aluno, coordenado por um Orquestrador e executado por uma equipe de agentes especializados.

## Estrutura do Repositório

A organização dos arquivos foi pensada para facilitar a implementação e a compreensão do fluxo de trabalho:

| Arquivo | Conteúdo | Propósito |
| :--- | :--- | :--- |
| `AGENTS_CONFIG.json` | Configuração técnica de todos os agentes em formato JSON. | Importação direta em frameworks de agentes (ex: Autogen, CrewAI). |
| `AGENTS_PROMPTS.md` | Lista detalhada dos System Prompts e objetivos de cada agente. | Referência rápida para o comportamento de cada agente. |
| `WORKFLOW_OVERVIEW.md` | Passo a passo de como o Orquestrador (Luis) conduz o fluxo. | Visão de alto nível da lógica de coordenação. |
| `CONVERSATION_SIMULATION.md` | Roteiro textual completo das interações entre o aluno e os agentes. | Exemplo prático e teste de validação do fluxo. |

## Agentes Principais

O sistema é composto por 8 agentes, coordenados por Luis:

| Agente | Função | Foco |
| :--- | :--- | :--- |
| **Luis** | Coordenador Pedagógico (Orquestrador) | Gestão de Fluxo e Roteamento |
| **Thiago** | Tutor de Conteúdo | Explicação e Exercícios Iniciais |
| **Erika** | Agente de Diagnóstico | Avaliação de Desempenho e Identificação de Falhas |
| **Mikael** | Agente Motivacional | Apoio Emocional e Reforço Positivo |
| **Sena** | Agente de Exercícios | Criação de Atividades Personalizadas |
| **Julio** | Agente de Avaliação | Medição Formal de Progresso |
| **Pedro** | Agente de Estratégias de Estudo | Organização de Rotina e Cronograma |
| **Jonathan** | Agente de Relatório de Progresso | Consolidação de Dados e Parecer Final |
