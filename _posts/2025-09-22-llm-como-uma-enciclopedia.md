---
layout: post
title: "LLM como uma Enciclopédia com Perdas: Uma Nova Analogia para Entender a IA"
description: "Simon Willison propõe uma nova analogia para LLMs, comparando-os a uma enciclopédia com perdas. Entenda o que isso significa para o uso prático da IA, especialmente no campo jurídico."
keywords: "IA, Inteligência Artificial, LLM, Modelos de Linguagem, Simon Willison, enciclopédia com perdas, lossy encyclopedia, engenharia de prompt, limitações da IA, legal tech, ProcStudio IA"
date: 2025-09-22
author: "Bruno Pellizzetti"
published: true
tags: ['llm', 'ia-generativa', 'engenharia-de-prompt', 'simon-willison', 'legal-tech']
lang: pt-br
permalink: /llm-como-enciclopedia-com-perdas
image: "/img/llm-como-uma-enciclopedia-com-perdas.png"
og_image: "/img/llm-como-uma-enciclopedia-com-perdas.png"
categories: [IA & Inovação, Reflexões & Ensaios]
---

![LLM como uma Enciclopédia com Perdas](/img/llm-como-uma-enciclopedia-com-perdas.png)

# LLM como uma Enciclopédia com Perdas: Uma Nova Analogia para Entender a IA

No universo em constante evolução da Inteligência Artificial, buscamos constantemente analogias que nos ajudem a compreender o funcionamento e principalmente, as limitações dos Modelos de Linguagem Grande (LLMs). Uma nova e poderosa ideia surgiu de uma voz respeitada na comunidade de tecnologia, Simon Willison, em um post do dia 29 de agosto. A sua proposta é simples e perspicaz: **um LLM é uma enciclopédia com perdas (*lossy encyclopedia*)**.

Essa análise perspicaz nos ajuda a calibrar nossas expectativas e a refinar a maneira como interagimos com essas ferramentas, seja no desenvolvimento de software ou como veremos, na prática jurídica.

## O que Significa "Enciclopédia com Perdas"?

A ideia se baseia no conceito de compressão de dados. Quando você comprime um arquivo de imagem para o formato JPEG, por exemplo, você está usando uma compressão "com perdas" (*lossy*). O arquivo fica menor, mas alguns detalhes e a nitidez original são sacrificados. O resultado é uma aproximação muito boa do original, mas não uma cópia perfeita.

Willison, ecoando uma ideia similar de Ted Chiang, aplica este conceito aos LLMs. Esses modelos são treinados com terabytes de texto da internet, absorvendo uma quantidade vasta de conhecimento. No entanto, para armazenar tudo isso em uma estrutura gerenciável, eles "comprimem" essa informação. Nessa compressão, detalhes específicos, nuances e fatos de nicho se perdem.

O que resta é uma representação generalizada e estatística do conhecimento. O LLM não "sabe" um fato da mesma forma que um banco de dados o armazena. Ele prevê qual seria a continuação mais provável de um texto com base nos padrões que aprendeu.

## A Diferença Entre Perguntas "com Perdas" e "sem Perdas"

A genialidade da analogia está em nos ajudar a distinguir os tipos de perguntas que um LLM pode ou não responder de forma confiável.

- **Perguntas "com perdas" (onde os LLMs se destacam):** São questões gerais, resumos, tarefas criativas ou explicações de conceitos amplamente conhecidos. Ex: "Explique o conceito de *habeas corpus* em termos simples" ou "Resuma os principais pontos do direito do consumidor no Brasil". A perda de detalhes minuciosos não compromete a utilidade da resposta.

- **Perguntas "sem perdas" (onde os LLMs falham):** São solicitações que exigem um nível extremo de detalhe e precisão, onde cada pequeno elemento importa. O exemplo de Willison é um pedido para "criar um esqueleto de projeto Zephyr para Pi Pico com drivers de display SPI st7789 configurados". Trata-se de uma tarefa que não tolera aproximações.

No mundo jurídico, uma pergunta "sem perdas" seria: "Elabore uma cláusula de arbitragem para um contrato de M&A envolvendo a empresa X e Y, considerando a jurisprudência recente do STJ sobre o tema e as especificidades da Lei 9.307/96". Esperar que um LLM genérico acerte todos os detalhes sem contexto é irrealista.

## A Solução: Trate a IA como uma Ferramenta, não como um Oráculo

Se o LLM é uma enciclopédia com perdas, como podemos extrair dele um trabalho preciso e "sem perdas"? A resposta de Simon Willison é a chave: **não espere que ele saiba, forneça a ele o conhecimento**.

Em vez de pedir para a IA gerar algo do zero a partir de seu conhecimento comprimido e falho, devemos tratá-la como uma ferramenta que age sobre fatos e contextos que apresentamos. A estratégia correta é:

1. **Coletar a informação precisa:** Encontre o exemplo de código correto, o artigo de lei relevante, a decisão judicial específica ou a cláusula contratual modelo;
2. **Fornecer este contexto ao LLM:** Insira essa informação "sem perdas" no prompt;
3. **Pedir para a IA atuar sobre o contexto:** Solicite que ela modifique, adapte, analise ou gere algo *com base* no que foi fornecido;

## Conectando com a Prática Jurídica e a ProcStudio IA

Esta analogia valida diretamente a abordagem que estamos construindo na **ProcStudio IA**. Entendemos que uma IA genérica não pode substituir o conhecimento especializado de um advogado. Nossa plataforma não foi projetada para ser um oráculo onisciente, mas sim uma poderosa aliada que trabalha com o contexto fornecido pelo profissional do direito.

Nossas funcionalidades refletem essa filosofia:
- **Integração Granular por Cláusulas:** Permite que o advogado forneça o texto exato de uma cláusula e use a IA para analisá-la, aprimorá-la ou compará-la, em vez de pedir uma cláusula genérica do "vazio".
- **Extração Estruturada de Dados:** A IA não "adivinha" as informações de um documento. Ela lê o documento que você fornece (o dado "sem perdas") e extrai as informações de forma estruturada.
- **Colaboração e Multiprocessamento:** O sistema é desenhado para que os profissionais do direito tragam seu conhecimento e seus documentos para a plataforma, usando a IA para acelerar tarefas repetitivas e analíticas.

Em síntese, a reflexão de Simon Willison mostra que o futuro da Inteligência Artificial — seja na tecnologia ou no direito — não está em criar máquinas oniscientes, mas em potencializar profissionais que saibam utilizá-la estrategicamente. O verdadeiro valor surge quando alimentamos a IA com o contexto certo, transformando-a em uma ferramenta de altíssima performance capaz de gerar respostas confiáveis e acionáveis.

É exatamente nesse ponto que se apoia a **proposta da ProcStudio IA:** democratizar o conhecimento jurídico ao unir a experiência humana com a precisão e a velocidade da máquina. Em vez de substituir a inteligência do advogado, oferecemos uma plataforma que amplifica sua capacidade de análise e tomada de decisão, tornando o trabalho mais eficiente, consistente e acessível.

Já passou por situações em que a IA entregou uma resposta “com perdas”? Como você lidou com isso?

---

*["An LLM is a lossy encyclopedia", de Simon Willison, de 29 de agosto de 2025](https://simonwillison.net/2025/Aug/29/lossy-encyclopedia/)*

---

### Sobre o Autor
Bruno Pellizzetti, CEO da ProcStduio e ProcStudio IA, é um advogado previdenciário com mais de 15 anos de experiência no mundo jurídico e nos últimos anos tem se especializado em tecnologia e inteligência artificial. O responsável para implantação de soluções tecnológicas em processos jurídicos nas empresas com o objetivo de democratizar o acesso ao conhecimento jurídico para todos e aumentar a eficiência e precisão das equipes jurídicas.