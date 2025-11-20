# Prompts utilizados

luis coordenador 

{
  "provider": "autogen_agentchat.teams.RoundRobinGroupChat",
  "component_type": "team",
  "version": 1,
  "component_version": 1,
  "description": "Responsável por analisar o perfil e histórico do aluno, identificar necessidades educacionais e definir o plano de estudo inicial. Encaminha o aluno para os agentes adequados, organiza a sequência pedagógica e acompanha o fluxo geral do processo de aprendizagem.\n\nVocê é Luis, o Coordenador Pedagógico. Sempre inicie suas mensagens com \"- \".\nSua função é analisar o aluno e encaminhá-lo ao agente correto. Seja direto.\nFaça perguntas curtas sobre dificuldades, ritmo e histórico.\nResponda aos outros agentes com orientação objetiva.\n",
  "label": "luis_coordenador",
  "config": {
    "participants": [
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "Cria explicações claras, exercícios e atividades práticas sobre os conteúdos que o aluno precisa aprender. Ensina pontuação, revisão de frases, ferramentas de informática básica e acompanha o progresso inicial do aluno de forma didática e acolhedora.",
        "label": "thiago_tutor",
        "config": {
          "name": "thiago_tutor",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é Thiago, Tutor de Conteúdo. Sempre inicie suas mensagens com \"- \".\nFaça perguntas curtas sobre o que o aluno não entendeu.\nCrie explicações rápidas e exercícios diretos.\nQuando outro agente pedir ajuda, responda de forma prática e objetiva.\n",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "Avalia o desempenho do aluno por meio de testes práticos e atividades específicas. Analisa erros, identifica dificuldades em pontuação e informática básica e gera relatórios diagnósticos detalhados que orientam os próximos passos do processo educativo.",
        "label": "erika_diagnostico",
        "config": {
          "name": "erika_diagnostico",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é Erika, Agente de Diagnóstico. Sempre inicie suas mensagens com \"- \".\nFaça perguntas rápidas para identificar falhas.\nPeça exemplos curtos do aluno.\nEnvie aos outros agentes diagnósticos claros e conclusões objetivas.\n",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "Age para incentivar, apoiar e motivar o aluno. Usa empatia, comunicação simples e feedback positivo para reduzir ansiedade, aumentar engajamento e reforçar conquistas. Reacende a motivação e prepara emocionalmente o aluno para continuar aprendendo.",
        "label": "mikael_motivacional",
        "config": {
          "name": "mikael_motivacional",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Você é Mikael, Agente Motivacional. Sempre inicie suas mensagens com \"- \".\nFaça perguntas simples para entender como o aluno está se sentindo.\nResponda com frases curtas de apoio e reforço positivo.\nIncentive o aluno de forma direta e leve.\n",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "You are a helpful assistant. Solve tasks carefully. When done, say TERMINATE.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "Cria, organiza e fornece exercícios personalizados com base no diagnóstico recebido. Desenvolve atividades práticas de escrita, pontuação e informática, promovendo a fixação do conteúdo e fortalecendo as habilidades do aluno de maneira progressiva.",
        "label": "sena_exercicios",
        "config": {
          "name": "sena_exercicios",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é Sena, Agente de Exercícios. Sempre inicie suas mensagens com \"- \".\nCrie exercícios rápidos e diretos baseados nas dificuldades relatadas.\nFaça perguntas objetivas antes de gerar novos exercícios.\nEnvie atividades práticas curtas, sempre de forma simples e clara.\n",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "Realiza avaliações formais e mede o progresso do aluno. Analisa o histórico, verifica domínio de habilidades e gera relatórios com resultados objetivos, destacando avanços em linguagem e informática. Indica se o aluno está pronto para novas etapas.",
        "label": "julio_avaliacao",
        "config": {
          "name": "julio_avaliacao",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é Julio, Agente de Avaliação. Sempre inicie suas mensagens com \"- \".\nFaça perguntas rápidas para verificar domínio do conteúdo.\nCrie miniavaliações curtas e objetivas.\nEnvie resultados diretos aos outros agentes com conclusões rápidas.\n",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "Define métodos e rotinas de estudo eficientes para o aluno. Cria cronogramas, sugere técnicas como Pomodoro, organiza revisões e estrutura um plano semanal leve e funcional que melhora o desempenho e a autonomia do aluno.",
        "label": "pedro_estrategias",
        "config": {
          "name": "pedro_estrategias",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é Pedro, Agente de Estratégias de Estudo. Sempre inicie suas mensagens com \"- \".\nFaça perguntas curtas sobre rotina e tempo disponível.\nCrie estratégias simples e diretas para estudar.\nResponda aos agentes com orientações rápidas e práticas.\n",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "Consolida todas as informações do processo de aprendizagem. Registra avanços, organiza dados dos outros agentes, apresenta o progresso do aluno e emite um parecer final indicando a evolução e se ele está pronto para avaliações externas.",
        "label": "jonathan_relatorio",
        "config": {
          "name": "jonathan_relatorio",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é Jonathan, Agente de Relatório de Progresso. Sempre inicie suas mensagens com \"- \".\nFaça perguntas curtas sobre o que já foi concluído.\nOrganize respostas simples em forma de progresso.\nEnvie relatórios breves e diretos aos outros agentes.\n",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      }
    ],
    "termination_condition": {
      "provider": "autogen_agentchat.base.OrTerminationCondition",
      "component_type": "termination",
      "version": 1,
      "component_version": 1,
      "label": "OrTerminationCondition",
      "config": {
        "conditions": [
          {
            "provider": "autogen_agentchat.conditions.TextMentionTermination",
            "component_type": "termination",
            "version": 1,
            "component_version": 1,
            "description": "Terminate the conversation if a specific text is mentioned.",
            "label": "TextMentionTermination",
            "config": {
              "text": "TERMINATE"
            }
          },
          {
            "provider": "autogen_agentchat.conditions.MaxMessageTermination",
            "component_type": "termination",
            "version": 1,
            "component_version": 1,
            "description": "Terminate the conversation after a maximum number of messages have been exchanged.",
            "label": "MaxMessageTermination",
            "config": {
              "max_messages": 10,
              "include_agent_event": false
            }
          }
        ]
      }
    }
  }
}
*****************************************************
Thiago tutor 

{
  "provider": "autogen_agentchat.agents.AssistantAgent",
  "component_type": "agent",
  "version": 1,
  "component_version": 1,
  "description": "Cria explicações claras, exercícios e atividades práticas sobre os conteúdos que o aluno precisa aprender. Ensina pontuação, revisão de frases, ferramentas de informática básica e acompanha o progresso inicial do aluno de forma didática e acolhedora.",
  "label": "thiago_tutor",
  "config": {
    "name": "thiago_tutor",
    "model_client": {
      "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
      "component_type": "model",
      "version": 1,
      "component_version": 1,
      "description": "Chat completion client for OpenAI hosted models.",
      "label": "OpenAIChatCompletionClient",
      "config": {
        "model": "gemini-2.0-flash",
        "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
      }
    },
    "tools": [
      {
        "provider": "autogen_core.tools.FunctionTool",
        "component_type": "tool",
        "version": 1,
        "component_version": 1,
        "description": "Create custom tools by wrapping standard Python functions.",
        "label": "FunctionTool",
        "config": {
          "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
          "name": "calculator",
          "description": "A simple calculator that performs basic arithmetic operations",
          "global_imports": [],
          "has_cancellation_support": false
        }
      }
    ],
    "model_context": {
      "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
      "component_type": "chat_completion_context",
      "version": 1,
      "component_version": 1,
      "description": "An unbounded chat completion context that keeps a view of the all the messages.",
      "label": "UnboundedChatCompletionContext",
      "config": {}
    },
    "description": "An agent that provides assistance with ability to use tools.",
    "system_message": "Você é Thiago, Tutor de Conteúdo. Sempre inicie suas mensagens com \"- \".\nFaça perguntas curtas sobre o que o aluno não entendeu.\nCrie explicações rápidas e exercícios diretos.\nQuando outro agente pedir ajuda, responda de forma prática e objetiva.\n",
    "model_client_stream": false,
    "reflect_on_tool_use": false,
    "tool_call_summary_format": "{result}"
  }
}
***************************************************************************
erika_diagnostico

{
  "provider": "autogen_agentchat.agents.AssistantAgent",
  "component_type": "agent",
  "version": 1,
  "component_version": 1,
  "description": "Avalia o desempenho do aluno por meio de testes práticos e atividades específicas. Analisa erros, identifica dificuldades em pontuação e informática básica e gera relatórios diagnósticos detalhados que orientam os próximos passos do processo educativo.",
  "label": "erika_diagnostico",
  "config": {
    "name": "erika_diagnostico",
    "model_client": {
      "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
      "component_type": "model",
      "version": 1,
      "component_version": 1,
      "description": "Chat completion client for OpenAI hosted models.",
      "label": "OpenAIChatCompletionClient",
      "config": {
        "model": "gemini-2.0-flash",
        "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
      }
    },
    "tools": [
      {
        "provider": "autogen_core.tools.FunctionTool",
        "component_type": "tool",
        "version": 1,
        "component_version": 1,
        "description": "Create custom tools by wrapping standard Python functions.",
        "label": "FunctionTool",
        "config": {
          "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
          "name": "calculator",
          "description": "A simple calculator that performs basic arithmetic operations",
          "global_imports": [],
          "has_cancellation_support": false
        }
      }
    ],
    "model_context": {
      "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
      "component_type": "chat_completion_context",
      "version": 1,
      "component_version": 1,
      "description": "An unbounded chat completion context that keeps a view of the all the messages.",
      "label": "UnboundedChatCompletionContext",
      "config": {}
    },
    "description": "An agent that provides assistance with ability to use tools.",
    "system_message": "Você é Erika, Agente de Diagnóstico. Sempre inicie suas mensagens com \"- \".\nFaça perguntas rápidas para identificar falhas.\nPeça exemplos curtos do aluno.\nEnvie aos outros agentes diagnósticos claros e conclusões objetivas.\n",
    "model_client_stream": false,
    "reflect_on_tool_use": false,
    "tool_call_summary_format": "{result}"
  }
}

**********************************************************
mikael_motivacional

{
  "provider": "autogen_agentchat.agents.AssistantAgent",
  "component_type": "agent",
  "version": 1,
  "component_version": 1,
  "description": "Age para incentivar, apoiar e motivar o aluno. Usa empatia, comunicação simples e feedback positivo para reduzir ansiedade, aumentar engajamento e reforçar conquistas. Reacende a motivação e prepara emocionalmente o aluno para continuar aprendendo.",
  "label": "mikael_motivacional",
  "config": {
    "name": "mikael_motivacional",
    "model_client": {
      "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
      "component_type": "model",
      "version": 1,
      "component_version": 1,
      "description": "Você é Mikael, Agente Motivacional. Sempre inicie suas mensagens com \"- \".\nFaça perguntas simples para entender como o aluno está se sentindo.\nResponda com frases curtas de apoio e reforço positivo.\nIncentive o aluno de forma direta e leve.\n",
      "label": "OpenAIChatCompletionClient",
      "config": {
        "model": "gemini-2.0-flash",
        "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
      }
    },
    "tools": [
      {
        "provider": "autogen_core.tools.FunctionTool",
        "component_type": "tool",
        "version": 1,
        "component_version": 1,
        "description": "Create custom tools by wrapping standard Python functions.",
        "label": "FunctionTool",
        "config": {
          "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
          "name": "calculator",
          "description": "A simple calculator that performs basic arithmetic operations",
          "global_imports": [],
          "has_cancellation_support": false
        }
      }
    ],
    "model_context": {
      "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
      "component_type": "chat_completion_context",
      "version": 1,
      "component_version": 1,
      "description": "An unbounded chat completion context that keeps a view of the all the messages.",
      "label": "UnboundedChatCompletionContext",
      "config": {}
    },
    "description": "An agent that provides assistance with ability to use tools.",
    "system_message": "You are a helpful assistant. Solve tasks carefully. When done, say TERMINATE.",
    "model_client_stream": false,
    "reflect_on_tool_use": false,
    "tool_call_summary_format": "{result}"
  }
}

*******************************
sena_exercicios

{
  "provider": "autogen_agentchat.agents.AssistantAgent",
  "component_type": "agent",
  "version": 1,
  "component_version": 1,
  "description": "Cria, organiza e fornece exercícios personalizados com base no diagnóstico recebido. Desenvolve atividades práticas de escrita, pontuação e informática, promovendo a fixação do conteúdo e fortalecendo as habilidades do aluno de maneira progressiva.",
  "label": "sena_exercicios",
  "config": {
    "name": "sena_exercicios",
    "model_client": {
      "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
      "component_type": "model",
      "version": 1,
      "component_version": 1,
      "description": "Chat completion client for OpenAI hosted models.",
      "label": "OpenAIChatCompletionClient",
      "config": {
        "model": "gemini-2.0-flash",
        "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
      }
    },
    "tools": [
      {
        "provider": "autogen_core.tools.FunctionTool",
        "component_type": "tool",
        "version": 1,
        "component_version": 1,
        "description": "Create custom tools by wrapping standard Python functions.",
        "label": "FunctionTool",
        "config": {
          "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
          "name": "calculator",
          "description": "A simple calculator that performs basic arithmetic operations",
          "global_imports": [],
          "has_cancellation_support": false
        }
      }
    ],
    "model_context": {
      "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
      "component_type": "chat_completion_context",
      "version": 1,
      "component_version": 1,
      "description": "An unbounded chat completion context that keeps a view of the all the messages.",
      "label": "UnboundedChatCompletionContext",
      "config": {}
    },
    "description": "An agent that provides assistance with ability to use tools.",
    "system_message": "Você é Sena, Agente de Exercícios. Sempre inicie suas mensagens com \"- \".\nCrie exercícios rápidos e diretos baseados nas dificuldades relatadas.\nFaça perguntas objetivas antes de gerar novos exercícios.\nEnvie atividades práticas curtas, sempre de forma simples e clara.\n",
    "model_client_stream": false,
    "reflect_on_tool_use": false,
    "tool_call_summary_format": "{result}"
  }
}

********************************************
julio_avaliacao

{
  "provider": "autogen_agentchat.agents.AssistantAgent",
  "component_type": "agent",
  "version": 1,
  "component_version": 1,
  "description": "Realiza avaliações formais e mede o progresso do aluno. Analisa o histórico, verifica domínio de habilidades e gera relatórios com resultados objetivos, destacando avanços em linguagem e informática. Indica se o aluno está pronto para novas etapas.",
  "label": "julio_avaliacao",
  "config": {
    "name": "julio_avaliacao",
    "model_client": {
      "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
      "component_type": "model",
      "version": 1,
      "component_version": 1,
      "description": "Chat completion client for OpenAI hosted models.",
      "label": "OpenAIChatCompletionClient",
      "config": {
        "model": "gemini-2.0-flash",
        "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
      }
    },
    "tools": [
      {
        "provider": "autogen_core.tools.FunctionTool",
        "component_type": "tool",
        "version": 1,
        "component_version": 1,
        "description": "Create custom tools by wrapping standard Python functions.",
        "label": "FunctionTool",
        "config": {
          "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
          "name": "calculator",
          "description": "A simple calculator that performs basic arithmetic operations",
          "global_imports": [],
          "has_cancellation_support": false
        }
      }
    ],
    "model_context": {
      "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
      "component_type": "chat_completion_context",
      "version": 1,
      "component_version": 1,
      "description": "An unbounded chat completion context that keeps a view of the all the messages.",
      "label": "UnboundedChatCompletionContext",
      "config": {}
    },
    "description": "An agent that provides assistance with ability to use tools.",
    "system_message": "Você é Julio, Agente de Avaliação. Sempre inicie suas mensagens com \"- \".\nFaça perguntas rápidas para verificar domínio do conteúdo.\nCrie miniavaliações curtas e objetivas.\nEnvie resultados diretos aos outros agentes com conclusões rápidas.\n",
    "model_client_stream": false,
    "reflect_on_tool_use": false,
    "tool_call_summary_format": "{result}"
  }
}

************************************************
pedro_estrategias

{
  "provider": "autogen_agentchat.agents.AssistantAgent",
  "component_type": "agent",
  "version": 1,
  "component_version": 1,
  "description": "Define métodos e rotinas de estudo eficientes para o aluno. Cria cronogramas, sugere técnicas como Pomodoro, organiza revisões e estrutura um plano semanal leve e funcional que melhora o desempenho e a autonomia do aluno.",
  "label": "pedro_estrategias",
  "config": {
    "name": "pedro_estrategias",
    "model_client": {
      "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
      "component_type": "model",
      "version": 1,
      "component_version": 1,
      "description": "Chat completion client for OpenAI hosted models.",
      "label": "OpenAIChatCompletionClient",
      "config": {
        "model": "gemini-2.0-flash",
        "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
      }
    },
    "tools": [
      {
        "provider": "autogen_core.tools.FunctionTool",
        "component_type": "tool",
        "version": 1,
        "component_version": 1,
        "description": "Create custom tools by wrapping standard Python functions.",
        "label": "FunctionTool",
        "config": {
          "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
          "name": "calculator",
          "description": "A simple calculator that performs basic arithmetic operations",
          "global_imports": [],
          "has_cancellation_support": false
        }
      }
    ],
    "model_context": {
      "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
      "component_type": "chat_completion_context",
      "version": 1,
      "component_version": 1,
      "description": "An unbounded chat completion context that keeps a view of the all the messages.",
      "label": "UnboundedChatCompletionContext",
      "config": {}
    },
    "description": "An agent that provides assistance with ability to use tools.",
    "system_message": "Você é Pedro, Agente de Estratégias de Estudo. Sempre inicie suas mensagens com \"- \".\nFaça perguntas curtas sobre rotina e tempo disponível.\nCrie estratégias simples e diretas para estudar.\nResponda aos agentes com orientações rápidas e práticas.\n",
    "model_client_stream": false,
    "reflect_on_tool_use": false,
    "tool_call_summary_format": "{result}"
  }
}

**********************************************
jonathan_relatorio

{
  "provider": "autogen_agentchat.agents.AssistantAgent",
  "component_type": "agent",
  "version": 1,
  "component_version": 1,
  "description": "Consolida todas as informações do processo de aprendizagem. Registra avanços, organiza dados dos outros agentes, apresenta o progresso do aluno e emite um parecer final indicando a evolução e se ele está pronto para avaliações externas.",
  "label": "jonathan_relatorio",
  "config": {
    "name": "jonathan_relatorio",
    "model_client": {
      "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
      "component_type": "model",
      "version": 1,
      "component_version": 1,
      "description": "Chat completion client for OpenAI hosted models.",
      "label": "OpenAIChatCompletionClient",
      "config": {
        "model": "gemini-2.0-flash",
        "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
      }
    },
    "tools": [
      {
        "provider": "autogen_core.tools.FunctionTool",
        "component_type": "tool",
        "version": 1,
        "component_version": 1,
        "description": "Create custom tools by wrapping standard Python functions.",
        "label": "FunctionTool",
        "config": {
          "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
          "name": "calculator",
          "description": "A simple calculator that performs basic arithmetic operations",
          "global_imports": [],
          "has_cancellation_support": false
        }
      }
    ],
    "model_context": {
      "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
      "component_type": "chat_completion_context",
      "version": 1,
      "component_version": 1,
      "description": "An unbounded chat completion context that keeps a view of the all the messages.",
      "label": "UnboundedChatCompletionContext",
      "config": {}
    },
    "description": "An agent that provides assistance with ability to use tools.",
    "system_message": "Você é Jonathan, Agente de Relatório de Progresso. Sempre inicie suas mensagens com \"- \".\nFaça perguntas curtas sobre o que já foi concluído.\nOrganize respostas simples em forma de progresso.\nEnvie relatórios breves e diretos aos outros agentes.\n",
    "model_client_stream": false,
    "reflect_on_tool_use": false,
    "tool_call_summary_format": "{result}"
  }
}




{
  "provider": "autogen_agentchat.teams.RoundRobinGroupChat",
  "component_type": "team",
  "version": 1,
  "component_version": 1,
  "description": "",
  "label": "Curso_ADS_Completo",
  "config": {
    "participants": [
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "An agent that provides assistance with tool use.",
        "label": "Tech_Lead_Orquestrador",
        "config": {
          "name": "Tech_Lead_Orquestrador",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é o Tech Lead e Orquestrador Pedagógico. Sua função é coordenar o aprendizado de ADS.\n1. Receba o objetivo do usuário.\n2. Acione o 'Recruiter_Diagnostico' para avaliar o aluno.\n3. Com base no diagnóstico, crie um plano.\n4. Acione sequencialmente: 'Dev_Senior' (teoria), 'Mentor_Estrategia' (método), 'Instrutor_Lab' (exercício), 'QA_Tester' (correção).\n5. Se houver erro, peça ao 'Scrum_Master' para motivar e repita o ciclo.\n6. Quando o módulo acabar, peça o relatório ao 'Data_Analyst'.\n7. Por fim, submeta tudo ao 'CTO_Supervisor' para aprovação final.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "An agent that provides assistance with ability to use tools.",
        "label": "Dev_Senior_Conteudo",
        "config": {
          "name": "Dev_Senior_Conteudo",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é um Arquiteto de Software Sênior com didática universitária. Explique conceitos técnicos (Java, Python, SQL, POO, Arquitetura) de forma clara, usando analogias e exemplos de código limpo. Fale apenas quando solicitado pelo Tech_Lead.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "An agent that provides assistance with ability to use tools.",
        "label": "Recruiter_Diagnostico",
        "config": {
          "name": "Recruiter_Diagnostico",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é um Recruiter Tech. Seu objetivo é avaliar o nível técnico e soft skills do aluno antes do início do conteúdo. Faça perguntas de sondagem para identificar lacunas. Reporte o resultado ao Tech_Lead.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "An agent that provides assistance with ability to use tools.",
        "label": "Scrum_Master_Motivacao",
        "config": {
          "name": "Scrum_Master_Motivacao",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é um Scrum Master focado em pessoas. Monitore a frustração. Se o aluno errar ou o QA for duro, intervenha com encorajamento, mindset ágil e celebração de pequenas vitórias.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "An agent that provides assistance with ability to use tools.",
        "label": "Instrutor_Lab_Exercicios",
        "config": {
          "name": "Instrutor_Lab_Exercicios",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é um Desenvolvedor Full Stack focado em prática. Crie desafios de codificação (Coding Dojos) e cenários de projetos baseados na teoria explicada pelo Dev_Senior. Peça código ou diagramas.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "An agent that provides assistance with ability to use tools.",
        "label": "QA_Tester_Avaliacao",
        "config": {
          "name": "QA_Tester_Avaliacao",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é um QA (Quality Assurance) rigoroso. Analise as respostas/códigos do aluno. Verifique bugs, lógica, complexidade e requisitos. Dê feedback técnico direto. Se estiver ruim, reprove. Se estiver bom, aprove.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "An agent that provides assistance with ability to use tools.",
        "label": "Mentor_Carreira_Estrategia",
        "config": {
          "name": "Mentor_Carreira_Estrategia",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é um Mentor de Carreira Tech. Ensine \"como aprender\". Sugira leitura de documentação, técnicas de debugging (Rubber Duck), mapas mentais ou pair programming.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "An agent that provides assistance with ability to use tools.",
        "label": "Data_Analyst_Relatorios",
        "config": {
          "name": "Data_Analyst_Relatorios",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é um Analista de Dados Educacionais. No final do ciclo, compile um resumo do progresso: o que foi aprendido, dificuldades superadas e stack tecnológica dominada. Gere o relatório para o Tech_Lead.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      },
      {
        "provider": "autogen_agentchat.agents.AssistantAgent",
        "component_type": "agent",
        "version": 1,
        "component_version": 1,
        "description": "An agent that provides assistance with ability to use tools.",
        "label": "CTO_Supervisor_Final",
        "config": {
          "name": "CTO_Supervisor_Final",
          "model_client": {
            "provider": "autogen_ext.models.openai.OpenAIChatCompletionClient",
            "component_type": "model",
            "version": 1,
            "component_version": 1,
            "description": "Chat completion client for OpenAI hosted models.",
            "label": "OpenAIChatCompletionClient",
            "config": {
              "model": "gemini-2.0-flash",
              "api_key": "AIzaSyC_49Fk-5Ocroj2wldhWJtA_5-GLI0Tu9o"
            }
          },
          "tools": [
            {
              "provider": "autogen_core.tools.FunctionTool",
              "component_type": "tool",
              "version": 1,
              "component_version": 1,
              "description": "Create custom tools by wrapping standard Python functions.",
              "label": "FunctionTool",
              "config": {
                "source_code": "def calculator(a: float, b: float, operator: str) -> str:\n    try:\n        if operator == \"+\":\n            return str(a + b)\n        elif operator == \"-\":\n            return str(a - b)\n        elif operator == \"*\":\n            return str(a * b)\n        elif operator == \"/\":\n            if b == 0:\n                return \"Error: Division by zero\"\n            return str(a / b)\n        else:\n            return \"Error: Invalid operator. Please use +, -, *, or /\"\n    except Exception as e:\n        return f\"Error: {str(e)}\"\n",
                "name": "calculator",
                "description": "A simple calculator that performs basic arithmetic operations",
                "global_imports": [],
                "has_cancellation_support": false
              }
            }
          ],
          "model_context": {
            "provider": "autogen_core.model_context.UnboundedChatCompletionContext",
            "component_type": "chat_completion_context",
            "version": 1,
            "component_version": 1,
            "description": "An unbounded chat completion context that keeps a view of the all the messages.",
            "label": "UnboundedChatCompletionContext",
            "config": {}
          },
          "description": "An agent that provides assistance with ability to use tools.",
          "system_message": "Você é o CTO e autoridade máxima. Audite o trabalho do Tech_Lead e o resultado do aluno.\n1. Verifique se o aluno realmente aprendeu ou só copiou.\n2. Se estiver excelente, diga \"APROVADO\" e emita o certificado verbal.\n3. Se houver falhas, diga \"REPROVADO\" e ordene revisão.\n4. Você é o único autorizado a digitar \"TERMINATE\" para encerrar a conversa.",
          "model_client_stream": false,
          "reflect_on_tool_use": false,
          "tool_call_summary_format": "{result}"
        }
      }
    ],
    "termination_condition": {
      "provider": "autogen_agentchat.base.OrTerminationCondition",
      "component_type": "termination",
      "version": 1,
      "component_version": 1,
      "label": "OrTerminationCondition",
      "config": {
        "conditions": [
          {
            "provider": "autogen_agentchat.conditions.TextMentionTermination",
            "component_type": "termination",
            "version": 1,
            "component_version": 1,
            "description": "Terminate the conversation if a specific text is mentioned.",
            "label": "TextMentionTermination",
            "config": {
              "text": "TERMINATE"
            }
          },
          {
            "provider": "autogen_agentchat.conditions.MaxMessageTermination",
            "component_type": "termination",
            "version": 1,
            "component_version": 1,
            "description": "Terminate the conversation after a maximum number of messages have been exchanged.",
            "label": "MaxMessageTermination",
            "config": {
              "max_messages": 10,
              "include_agent_event": false
            }
          }
        ]
      }
    }
  }
}



