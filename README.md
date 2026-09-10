# 📊 Sistema Multi-Agente para Diagnóstico de Carteira de Investimentos

Este projeto implementa uma arquitetura robusta baseada em múltiplos agentes de Inteligência Artificial para realizar a coleta, análise de risco e diagnóstico educacional de carteiras de investimentos. 

Construído com foco avançado em **estratégia de dados e IA**, o sistema orquestra modelos de linguagem para simular etapas fundamentais de *suitability* e alocação de ativos. O fluxo de informações é projetado para ser seguro, ordenado e aderente aos altos padrões exigidos no mercado financeiro, evitando vieses e garantindo respostas fundamentadas.

## 🚀 Tecnologias Utilizadas

*   **[n8n](https://n8n.io/):** Orquestração do fluxo de trabalho e roteamento lógico dos agentes.
*   **[Ollama](https://ollama.com/):** Execução de LLMs na infraestrutura para processamento das análises cognitivas e manutenção da privacidade de dados.
*   **Integrações Externas:** Triggers de Chat, nós de envio de E-mail (Gmail) e Memória de Contexto.
*   **Instruções de importação do workflow no n8n no final deste README.

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

## 🚀 Como importar o workflow no n8n

Este repositório contém um workflow em formato JSON que pode ser importado diretamente no n8n
.

Siga o passo a passo abaixo para configurar o workflow.

1. Copie o código JSON

No repositório, localize o arquivo .json que contém o workflow.

Abra o arquivo e clique em Raw para visualizar o código JSON completo.

Depois:

Selecione todo o conteúdo do arquivo (Ctrl + A no Windows/Linux ou Cmd + A no Mac).
Copie o código (Ctrl + C ou Cmd + C).

⚠️ Certifique-se de copiar todo o conteúdo do JSON, desde o primeiro { até o último }.

2. Abra o n8n

Acesse sua instalação do n8n
 e entre no seu workspace.

Você pode utilizar o n8n hospedado na nuvem ou uma instalação própria.

3. Crie um novo workflow

Dentro do n8n:

Clique em Create Workflow ou New Workflow.
Abra o editor de workflows.
Com o workflow aberto, utilize a opção de importação de workflow.
4. Importe o JSON

No n8n, procure a opção:

Import from Clipboard

Cole o código JSON que você copiou do GitHub.

Depois, confirme a importação.

O n8n irá interpretar o arquivo e recriar automaticamente os nodes, conexões e configurações que estão presentes no workflow.

5. Verifique os nodes

Depois da importação, confira se todos os nodes foram carregados corretamente e se as conexões entre eles estão funcionando.

Dependendo do workflow, alguns nodes podem exigir configurações adicionais, como:

🔑 Credenciais de APIs
🌐 URLs ou endpoints
📋 Variáveis
🗄️ Banco de dados
🔐 Tokens de autenticação
⚙️ Configurações específicas do seu ambiente
6. Configure suas credenciais

Caso algum node apresente um aviso de credencial ausente, abra o node e selecione ou configure a credencial correspondente.

Importante: o JSON do workflow não deve conter senhas, tokens ou chaves privadas.

Se o workflow depender de alguma API ou serviço externo, configure suas próprias credenciais dentro do n8n.

7. Teste o workflow

Antes de ativar o workflow, execute um teste manual.

Clique em Execute Workflow e acompanhe a execução dos nodes.

Verifique se:

Todos os nodes executam corretamente;
Não existem erros de autenticação;
As informações estão sendo recebidas corretamente;
As conexões entre os nodes estão funcionando;
Os resultados estão de acordo com o esperado.
8. Ative o workflow

Depois de confirmar que tudo está funcionando corretamente, você pode ativar o workflow.

A partir desse momento, ele poderá ser executado automaticamente de acordo com o trigger configurado no workflow.

📌 Resumo rápido

Se você já está familiarizado com o n8n, o processo é simples:

GitHub → Abrir arquivo JSON → Raw → Copiar JSON → n8n → Import from Clipboard → Colar → Importar → Configurar credenciais → Testar → Ativar

💡 Dica: sempre revise as credenciais e configurações após importar um workflow de terceiros. O JSON recria a estrutura do workflow, mas algumas configurações precisam ser adaptadas ao seu ambiente.

🛠️ Requisitos

Antes de importar o workflow, certifique-se de ter:

Uma conta ou instalação do n8n;
Acesso às ferramentas e APIs utilizadas pelo workflow;
As credenciais necessárias para os serviços utilizados;
As permissões necessárias para executar as integrações.

