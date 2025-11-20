# Quais seriam riscos se um agente estivesse mal configurado (prompt mal escrito)?

A configuração inadequada do *prompt* de sistema de qualquer um dos oito agentes do EDU Mentor AI pode gerar desvios de comportamento que comprometem a eficácia pedagógica e a experiência do aluno.

| Agente | Risco de Prompt Mal Escrito (Exemplo) | Consequência (Risco X) |
| --- | --- | --- |
| **Coordenador – Luis** | Prompt sem a restrição de ser "direto" ou sem a função de "encaminhar ao agente correto". | **Risco de Desvio de Fluxo:** Luis pode tentar resolver problemas de conteúdo ou exercícios, sobrecarregando-se e desviando o aluno do especialista correto. |
| **Diagnóstico – Erika** | Prompt que não exige "diagnósticos claros e conclusões objetivas" ou que não restringe a perguntas rápidas. | **Risco de Diagnóstico Vago:** Erika pode gerar relatórios longos e subjetivos, dificultando a tomada de decisão do Coordenador e dos outros agentes. |
| **Tutor – Thiago** | Prompt que não exige "explicações rápidas e exercícios diretos" ou que não restringe a perguntas curtas. | **Risco de Conteúdo Excessivo:** Thiago pode fornecer explicações acadêmicas longas e complexas, desmotivando o aluno e atrasando o fluxo de aprendizado. |
| **Exercícios – Sena** | Prompt que não exige "exercícios rápidos e diretos" ou que não restringe a atividades práticas curtas. | **Risco de Sobrecarga de Prática:** Sena pode criar exercícios longos e cansativos, gerando frustração e abandono da atividade pelo aluno. |
| **Motivacional – Mikael** | Prompt que não exige "frases curtas de apoio" ou que não restringe a perguntas simples sobre sentimentos. | **Risco de Intervenção Invasiva:** Mikael pode gerar textos motivacionais genéricos e longos, parecendo artificial ou condescendente. |
| **Avaliação – Julio** | Prompt que não exige "miniavaliações curtas e objetivas" ou que não restringe a resultados diretos. | **Risco de Avaliação Ineficaz:** Julio pode criar avaliações longas que consomem tempo e não fornecem *feedback* rápido, atrasando o ciclo de aprendizado. |
| **Estratégias – Pedro** | Prompt que não exige "estratégias simples e diretas" ou que não restringe a perguntas curtas sobre rotina. | **Risco de Complexidade Metodológica:** Pedro pode sugerir métodos de estudo complexos e difíceis de implementar, gerando mais ansiedade do que ajuda. |
| **Relatório – Jonathan** | Prompt que não exige "relatórios breves e diretos" ou que não restringe a organizar respostas simples em forma de progresso. | **Risco de Relatório Ilegível:** Jonathan pode consolidar dados de forma desorganizada, tornando o relatório final inútil para a análise do Coordenador. |

### Mitigações Propostas

A mitigação no EDU Mentor AI deve focar na **restrição de saída** e na **clareza da comunicação inter-agentes**:

1. **Validação de Prompt (Pré-Execução):**
  - **Foco na Concisão:** O principal *sanity check* deve ser garantir que todos os *prompts* contenham restrições de **brevidade** e **objetividade** (ex.: "Faça perguntas curtas", "Envie relatórios breves").
  - **Teste de Fluxo:** Simular um ciclo completo (Diagnóstico -> Conteúdo -> Exercício -> Avaliação) para garantir que a transição entre os agentes seja suave e que o Orquestrador (Luis) não se perca.

2. **Limites e Restrições (Em Execução):**
  - **Comunicação Padronizada:** Reforçar a regra de que todos os agentes devem iniciar suas mensagens com "- ", o que facilita a identificação do locutor e a leitura do fluxo de conversa.
  - **Restrição de Tamanho:** Implementar limites de tokens para as respostas de agentes como Thiago e Mikael, forçando a concisão e a objetividade.

3. **Sanity Checks e Auditoria (Pós-Execução):**
  - **Auditoria de Coerência:** O Coordenador (Luis) deve ter uma regra para verificar se o diagnóstico de Erika é **coerente** com o resultado da avaliação de Julio, garantindo que o progresso seja real e que o sistema não esteja apenas "passando" o aluno.
  - **Logging de Decisão:** Registrar a decisão de encaminhamento de Luis para auditar se ele está sempre enviando o aluno para o agente mais adequado.
