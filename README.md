# 📊 Sistema Multi-Agente para Diagnóstico de Carteira de Investimentos

Este projeto implementa uma arquitetura robusta baseada em múltiplos agentes de Inteligência Artificial para realizar a coleta, análise de risco e diagnóstico educacional de carteiras de investimentos. 

Construído com foco avançado em **estratégia de dados e IA**, o sistema orquestra modelos de linguagem para simular etapas fundamentais de *suitability* e alocação de ativos. O fluxo de informações é projetado para ser seguro, ordenado e aderente aos altos padrões exigidos no mercado financeiro, evitando vieses e garantindo respostas fundamentadas.

## 🚀 Tecnologias Utilizadas

*   **[n8n](https://n8n.io/):** Orquestração do fluxo de trabalho e roteamento lógico dos agentes.
*   **[Ollama](https://ollama.com/):** Execução de LLMs na infraestrutura para processamento das análises cognitivas e manutenção da privacidade de dados.
*   **Integrações Externas:** Triggers de Chat, nós de envio de E-mail (Gmail) e Memória de Contexto.

## 🧠 Arquitetura do Sistema

O fluxo foi desenhado utilizando o padrão de **Supervisor Worker**, onde um agente central gerencia o estado da conversa e delega tarefas específicas para agentes especialistas, além de passar por rigorosas barreiras de segurança (Guardrails).

### 🛡️ Camadas de Segurança (Guardrails)
1.  **Input Guardrails:** Antes de qualquer processamento, a entrada do usuário é validada para garantir que o prompt não contém violações ou requisições fora do escopo financeiro.
2.  **Output Guardrails:** Após a formulação do diagnóstico, a resposta passa por uma última validação de segurança antes de ser enviada ao usuário por E-mail e no Chat.

---

### 🤖 Os Agentes Especialistas

O sistema é composto por um Supervisor e três agentes estritamente isolados por domínio de atuação:

#### 👑 Agente Supervisor (Orquestrador)
Responsável exclusivamente por gerenciar a ordem de execução. Ele não realiza análises financeiras próprias, apenas garante que os dados fluam corretamente pela esteira de agentes e consolida o resultado final sem inventar suposições (alucinações).

#### 🕵️ Agente 1: Coleta e Triagem
Mapeia o perfil do usuário a partir de 7 eixos principais:
*   Ativos atuais e valores investidos.
*   Objetivo principal e horizonte de tempo (prazo).
*   Preferência de risco vs. retorno.
*   Necessidade de liquidez.

O Agente 1 estrutura essas respostas não estruturadas em dados organizados para a próxima etapa.

#### ⚖️ Agente 2: Análise de Risco e Desbalanceamento
Atua com base *exclusiva* nos dados triados pelo Agente 1. Suas funções incluem:
*   Avaliar o nível de risco aparente e concentração de ativos.
*   Identificar incompatibilidades entre o risco assumido, o prazo e o objetivo declarado.
*   Detectar sinais de desbalanceamento ou problemas de liquidez.

#### 💡 Agente 3: Diagnóstico e Recomendações
Recebe o dossiê completo (dados do Agente 1 + análise do Agente 2) para gerar recomendações educacionais.
*   Foca em ajustes de diversificação e rebalanceamento.
*   Mantém um tom informativo e alinhado ao perfil de risco declarado.
*   Sinaliza explicitamente quando há ausência de dados para uma recomendação segura.

## ⚙️ Como Funciona o Fluxo (Passo a Passo)

1.  O usuário envia uma mensagem detalhando sua situação financeira no Chat.
2.  O **Guardrail de Entrada** aprova o conteúdo.
3.  O **Supervisor** aciona o **Agente 1** para extrair os parâmetros-chave.
4.  Com os dados estruturados, o **Supervisor** aciona o **Agente 2** para encontrar furos, riscos e concentrações na carteira.
5.  Com a análise de risco pronta, o **Supervisor** aciona o **Agente 3** para redigir o diagnóstico final.
6.  O **Supervisor** consolida tudo.
7.  O **Guardrail de Saída** revisa o texto.
8.  O diagnóstico é enviado para o e-mail do usuário e exibido na interface de chat.

## ⚠️ Aviso Legal (Disclaimer)
Este sistema tem finalidade **estritamente educacional**. O diagnóstico gerado reflete uma análise preliminar baseada em inteligência artificial e não substitui a avaliação individualizada e profissional de um especialista ou consultor de investimentos certificado. Nenhuma recomendação gerada aqui constitui garantia de rentabilidade ou indicação formal de compra/venda de ativos.
