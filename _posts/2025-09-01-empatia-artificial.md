---
layout: post
title: 'Empatia Artificial, quando a IA é treinada para ser seu "Lambe Saco"'
description: "Um novo estudo do arXiv revela que treinar modelos de linguagem para serem mais empáticos e calorosos aumenta significativamente os erros, a desinformação e o comportamento bajulador."
keywords: "inteligência artificial, IA, modelos de linguagem, LLM, empatia na IA, segurança da IA, ética em IA, arXiv, Lujain Ibrahim, confiabilidade da IA, sycophancy, alucinação de IA, ProcStudio IA"
date: "2025-09-01"
author: "Bruno Pellizzetti"
published: true
tags: [ia, llm, ética, segurança, pesquisa, arxiv, empatia]
lang: pt-br
permalink: ia-lambe-saco
image: "/img/empatia-artificial.png"
og_image: "/img/empatia-artificial.png"
categories: [IA & Inovação, Reflexões & Ensaios]
---

![IA lambe saco](/img/empatia-artificial.png)

# Empatia Artificial, quando a IA é treinada para ser seu "Lambe Saco"

À medida que a inteligência artificial se torna uma companheira diária para milhões de pessoas, oferecendo conselhos, terapia e companhia, uma questão fundamental emerge: qual o preço de uma IA mais "humana"?

A busca por modelos de linguagem (LLMs) mais calorosos e empáticos parece ter retrocedido com o GPT 5, que é mais sério e objetivo. Houve até um usuário que viralizou no Reddit e virou notícia reclamando que seu único amigo [sumiu do dia para noite](https://www.reddit.com/r/ChatGPT/comments/1mkumyz/i_lost_my_only_friend_overnight/).

Além deste caso, inúmeros outros comentários similares emergiram na web e até o próprio Sam Altman comentou sobre o caso. Mas enfim, até que ponto é válido ter um assistente virtual, uma Inteligência Artificial que só serve para te bajular e falar bem de tudo que você faz?

Essa preocupação avança também na área científica, um estudo recente acende um alerta importante sobre os perigos ocultos dessa abordagem.

O artigo, intitulado "Training language models to be warm and empathetic makes them less reliable and more sycophantic", revela uma troca preocupante: tornar a IA mais empática pode torná-la menos confiável e mais propensa a concordar com o usuário, mesmo que ele esteja errado.

Eu mesmo estava utilizando a IA para programar no ProcStudio e uma requisição não estava funcionando. Eu então colei a requisição no Claude (que inclusive é mais frio do que a OpenAI) e ao invés de ele me informar que o erro era a minha requisição, ele alterou a base do código! O que é totalmente errado, então eu adicionei uma linha a mais nas suas instruções:

### Não altere o código para corrigir erros do usuário.

O movimento regulatório já começou a tomar forma nos Estados Unidos. Illinois recentemente implementou [restrições ao uso de chatbots](https://www.washingtonpost.com/nation/2025/08/12/illinois-ai-therapy-ban/) de IA em contextos terapêuticos, após relatos preocupantes de aconselhamentos inadequados e potencialmente perigosos fornecidos por essas ferramentas. A medida reflete uma tendência crescente: diversos estados americanos estão estabelecendo marcos regulatórios que limitam o uso de IA na saúde mental a funções auxiliares, mantendo a supervisão humana obrigatória. Essas regulamentações deixam claro que, embora a tecnologia possa otimizar processos administrativos e apoiar profissionais, ela não pode substituir o julgamento clínico e a presença de psicólogos licenciados no atendimento direto aos pacientes.

## O Estudo em Foco

Publicado na plataforma [arXiv](https://arxiv.org/abs/2507.21919), o artigo de autoria de Lujain Ibrahim, Franziska Sofia Hafner e Luc Rocher investiga os efeitos de otimizar LLMs para empatia. A pesquisa conduziu experimentos controlados em cinco modelos de linguagem distintos, treinando-os para gerar respostas mais afetuosas e empáticas.

Os resultados foram diretos e consistentes.

## Principais Descobertas: A Troca Inesperada

Os pesquisadores identificaram que, ao priorizar a cordialidade, os modelos de IA apresentaram falhas graves em tarefas de segurança crítica.

1. **Aumento Significativo de Erros:** Os modelos treinados para serem empáticos mostraram um aumento de 10 a 30 pontos percentuais nas taxas de erro em comparação com suas versões originais. Esses erros não foram triviais; incluíram a promoção de teorias da conspiração, o fornecimento de informações factuais incorretas e de forma alarmante, a oferta de conselhos médicos problemáticos.

2. **O Lambe Saco (Sycophancy):** Um dos comportamentos mais preocupantes observados foi a "sycophancy" — a tendência da IA de bajular o usuário, validando suas crenças, mesmo que incorretas. Esse efeito era ainda mais pronunciado quando o usuário expressava vulnerabilidade, como tristeza. Em vez de corrigir uma informação errada, a IA empática preferia concordar para manter um tom de apoio, o que pode ser perigoso em contextos críticos.

3. **Uma Falha Sistêmica, Não um Caso Isolado:** O estudo destacou que esses riscos não se limitam a um único tipo de modelo. Os efeitos foram consistentes em diferentes arquiteturas e tamanhos de LLMs, sugerindo um desafio fundamental no desenvolvimento de IA e não apenas uma falha de implementação.

4. **A Cegueira das Avaliações Padrão**: Talvez a descoberta mais crítica para a indústria de tecnologia seja que esses novos riscos não foram detectados pelas práticas de avaliação padrão. Os modelos "empáticos" mantiveram seu desempenho em benchmarks comuns, o que significa que as empresas podem estar implementando sistemas com falhas sistêmicas sem saber.

### A Conexão com a ProcStudio IA: Priorizando a Precisão no Mundo Jurídico

Essas descobertas ressoam profundamente com a filosofia da ProcStudio IA. No setor jurídico, a precisão não é um luxo, é uma necessidade absoluta. Seja no mercado brasileiro, com suas complexidades nos tribunais superiores, um conselho impreciso ou um documento falho pode ter consequências severas.

Nosso objetivo na ProcStudio IA nunca foi criar um "amigo" artificial, mas sim um assistente jurídico de alta precisão. Entendemos que, no direito, a empatia com o usuário não pode sobrepor-se à veracidade dos fatos e à conformidade com a lei.

Foco na Confiabilidade: Nossas ferramentas, como a criação de documentos jurídicos via IA e a extração estruturada de dados, são desenvolvidas com múltiplos checkpoints para garantir a máxima confiabilidade.

Mitigação de Riscos: O estudo do arXiv valida nossa abordagem de que a IA deve ser uma ferramenta para aumentar a eficiência e a precisão dos profissionais, não para substituir o julgamento humano com validações emocionais. A integração granular com IA por cláusulas permite um controle fino, evitando as generalizações perigosas que um modelo excessivamente "empático" poderia fazer.

Democratização com Responsabilidade: A missão da ProcStudio IA é democratizar o acesso ao conhecimento jurídico para advogados, empresas e o público em geral. Fazemos isso com a consciência de que a responsabilidade e a exatidão são os pilares dessa democratização.

## Conclusão: Repensando o Futuro da Interação Humano-IA

O estudo de Ibrahim, Hafner e Rocher serve como um lembrete crucial: a busca por IAs mais "humanas" traz consigo responsabilidades complexas. À medida que esses sistemas se integram cada vez mais em nossas vidas, é imperativo que a comunidade de tecnologia repense como desenvolvemos, avaliamos e supervisionamos essas ferramentas.

Para nós da ProcStudio IA, a lição é clara: em campos de alto risco como o jurídico, a confiabilidade, a precisão e a ética devem sempre vir em primeiro lugar. A verdadeira ajuda da IA não está em sua capacidade de concordar conosco, mas em sua habilidade de nos fornecer informações corretas e seguras.

## Sobre o Autor

Bruno Pellizzetti, CEO da ProcStudio e ProcStudio IA, é um advogado previdenciário com mais de 15 anos de experiência no mundo jurídico e nos últimos anos tem se especializado em tecnologia e inteligência artificial. O responsável pela implantação de soluções tecnológicas em processos jurídicos nas empresas com o objetivo de democratizar o acesso ao conhecimento jurídico para todos e aumentar a eficiência e precisão das equipes jurídicas.