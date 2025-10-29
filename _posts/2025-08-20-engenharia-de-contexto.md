---
layout: post
title: "A Nova Habilidade em IA não é Prompting, é Engenharia de Contexto"
date: 2025-08-20
permalink: /blog/engenharia-de-contexto
published: true
description: "Engenharia de Contexto é um novo termo ganhando força na IA: o foco sai do 'prompt perfeito' e vai para um sistema que monta e entrega o contexto ideal ao LLM."
author: "Bruno Pellizzetti"
image: /img/engenharia-de-contexto.png
og_image: /img/engenharia-de-contexto.png
categories: [IA & Inovação]
tags: [engenharia de contexto, prompting, RAG, agentes]
---

![Engenharia de contexto](/img/engenharia-de-contexto.png) 

# A Nova Habilidade em IA não é Prompting, é Engenharia de Contexto

Engenharia de Contexto é um novo termo que está ganhando força no mundo da IA. A conversa está mudando de "engenharia de prompts" para um conceito mais amplo e poderoso: Engenharia de Contexto. Tobi Lutke a descreve como "a arte de fornecer todo o contexto para que a tarefa seja plausivelmente solucionável pelo LLM", e ele está certo.

Com o surgimento dos Agentes, torna-se mais importante quais informações carregamos na "memória de trabalho limitada". Estamos vendo que o princ4ipal fator que determina se um Agente tem sucesso ou falha é a qualidade do contexto que você fornece. A maioria das falhas dos agentes não são mais falhas do modelo, são falhas de contexto.

## O que é o Contexto?

Para entender a engenharia de contexto, primeiro devemos expandir nossa definição de "contexto". Não é apenas o prompt único que você envia para um LLM. Pense nele como tudo o que o modelo vê antes de gerar uma resposta.

### Contexto

- **Instruções / Prompt do Sistema:** Um conjunto inicial de instruções que definem o comportamento do modelo durante uma conversa, pode/deve incluir exemplos, regras...

- **Prompt do Usuário:** Tarefa imediata ou pergunta do usuário.

- **Estado / Histórico (Memória de curto prazo):** A conversa atual, incluindo respostas do usuário e do modelo que levaram a este momento.

- **Memória de Longo Prazo:** Base de conhecimento persistente, reunida ao longo de muitas conversas anteriores, contendo preferências aprendidas do usuário, resumos de projetos passados ou fatos que foi solicitado a lembrar para uso futuro.

- **Informações Recuperadas (RAG):** Conhecimento externo e atualizado, informações relevantes de documentos, bancos de dados ou APIs para responder a perguntas específicas.

- **Ferramentas Disponíveis:** Definições de todas as funções ou ferramentas integradas que pode chamar (por exemplo: check_inventory, send_email).

- **Saída Estruturada:** Definições sobre o formato da resposta do modelo, por exemplo, um objeto JSON.

## Por Que Isso Importa: De Demo Barata a Produto Mágico

O segredo para construir agentes de IA realmente eficazes tem menos a ver com a complexidade do código que você escreve e tudo a ver com a qualidade do contexto que você fornece.

Construir Agentes é menos sobre o código que você escreve ou o framework que você usa. A diferença entre uma demo barata e um agente "mágico" está na qualidade do contexto que você fornece. Imagine que um assistente de IA seja solicitado a agendar uma reunião com base em um email simples:

>"Ei, só verificando se você está disponível para uma sincronização rápida amanhã."

O Agente "Demo Barata" tem contexto pobre. Ele vê apenas a solicitação do usuário e nada mais. Seu código pode ser perfeitamente funcional — ele chama um LLM e obtém uma resposta — mas a saída é inútil e robótica:

>"Obrigado por sua mensagem. Amanhã funciona para mim. Posso perguntar que horas você tinha em mente?"

O Agente "Mágico" é alimentado por um contexto rico. O trabalho principal do código não é descobrir como responder, mas reunir as informações que o LLM precisa para cumprir seu objetivo. Antes de chamar o LLM, você estenderia o contexto para incluir:

- Suas informações de calendário (que mostram que você está totalmente ocupado).

- Seus e-mails anteriores com essa pessoa (para determinar o tom informal apropriado).

- Sua lista de contatos (para identificá-los como um parceiro-chave).
Ferramentas para send_invite ou send_email.

Então você pode gerar uma resposta:

>"Ei Jim! Amanhã está lotado para mim, reuniões o dia todo. Quinta de manhã estou livre, se funcionar para você? Enviei um convite, me avise se funciona."

A mágica não está em um modelo mais inteligente ou em um algoritmo mais esperto. Está em fornecer o contexto certo para a tarefa certa. É por isso que a engenharia de contexto importará. As falhas dos agentes não são apenas falhas do modelo; são falhas de contexto.

## De Prompt para Engenharia de Contexto

O que é engenharia de contexto? Enquanto a "engenharia de prompts" se concentra em elaborar o conjunto perfeito de instruções em uma única string de texto, a engenharia de contexto é muito mais ampla. Vamos colocar de forma simples:

**Engenharia de Contexto** é a disciplina de projetar e construir sistemas dinâmicos que fornecem as informações e ferramentas certas, no formato certo, no momento certo, para dar a um LLM tudo o que ele precisa para realizar uma tarefa.

A Engenharia de Contexto é:

- **Um Sistema, Não uma String:** Contexto não é apenas um modelo de prompt estático. É a saída de um sistema que roda antes da chamada principal do LLM.

- **Dinâmica:** Criada na hora, adaptada à tarefa imediata. Para uma solicitação, podem ser os dados do calendário, para outra, os e-mails ou uma pesquisa na web.

- **Sobre as informações certas, ferramentas no momento certo:** O trabalho principal é garantir que o modelo não esteja faltando detalhes cruciais ("Lixo Entra, Lixo Sai"). Isso significa fornecer tanto conhecimento (informações) quanto capacidades (ferramentas) apenas quando necessário e útil.

- **Onde o formato importa:** Como você apresenta as informações importa. Um resumo conciso é melhor do que um despejo de dados brutos. Um esquema de ferramenta claro é melhor do que uma instrução vaga.

## Conclusão

Construir Agentes de IA poderosos e confiáveis está se tornando menos sobre encontrar um prompt mágico ou atualizações de modelo. É sobre a engenharia de contexto e fornecer as informações e ferramentas certas, no formato certo, no momento certo. É um desafio multifuncional que envolve entender seu caso de uso de negócios, definir suas saídas e estruturar todas as informações necessárias para que um LLM possa "realizar a tarefa".

---

Artigo baseado em: [A nova habilidade em IA não é a indução, mas sim a engenharia de contexto](https://www.philschmid.de/context-engineering).