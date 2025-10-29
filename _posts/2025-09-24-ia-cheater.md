---
layout: post
title: "Transparência em Benchmarks de IA: Análise de Falhas Metodológicas e Implicações para Compliance"
description: "Investigação técnica revela problemas críticos de transparência em avaliações de IA, incluindo acesso não autorizado a dados de teste. Análise das implicações para auditoria e responsabilidade em sistemas de inteligência artificial."
keywords: "transparência IA, auditoria benchmarks, compliance inteligência artificial, responsabilidade algoritmos, ética avaliação IA, due diligence tecnológica"
date: 2025-09-24
author: "Bruno Pellizzetti"
published: true
tags: ["transparencia", "auditoria-ia", "compliance", "benchmarks", "responsabilidade-algoritmica"]
lang: pt-br
permalink: /transparencia-benchmarks-ia-compliance
image: "/img/ia-cheater.png"
og_image: "/img/ia-cheater.png"
categories: [IA & Inovação, Direito Digital]
---

![IAs trapaceando para melhorar seu benchmark na plataforma](/img/ia-cheater.png)

Benchmarks, benchmarks em todos os lugares!

**Mas afinal o que é isso?**

Esse termo tem se popularizado muito após a adoção em massa da inteligência artificial e nada mais é do que medir algo, ter uma referência. O termo sempre foi muito usado na área de tecnologia e agora se espalhou para todo o público que quer saber afinal: _Qual é a melhor inteligência artificial?_

Assim, surgem várias formas de testar as inteligências artificiais, mas como é um sistema generativo, isso acaba sendo bem difícil, uma vez que só a sua experiência pessoal poderá dar a sua própria perspectiva sobre alguma coisa relacionada a IA.

Por outro lado, experimentar todas as IAs acabou sendo uma tarefa impossível, se tivéssemos apenas dois ou três modelos isso seria totalmente viável. Mas cada empresa fornece uma série de modelos com especificações próprias, daí a importância de termos esse benchmarks e essa informação organizada pelo menos como um mapa para gente se situar em tudo isso.

Temos por exemplo o [Artificial Analysis](https://artificialanalysis.ai/leaderboards/models) que ajuda a buscar a melhor IA para seu uso pessoal sistematizando a análise pela janela de contexto, pelo provedor, tempo de resposta, inteligência e preço de uso.

Em outro caso, temos por exemplo a [IDP Leaderboard](https://idp-leaderboard.org/#classification) que sistematiza a inteligências artificiais pelo seu nível de leitura de imagens, o que traz um pouco mais de solidez ao benchmark e especificidade.

E finalmente chegamos ao cerne do nosso artigo de hoje, o [SWE-Bench](https://www.swebench.com/) que é um benchmark criado para medir a precisão das Inteligências a partir da resolução de problemas reais. Neste caso os problemas são de software na plataforma Github.

Assim o benchmark é medido a partir da quantidade de resolução de problemas que cada IA consegue resolver, por exemplo hoje no topo da resolutividade está o `Claude 4 Opus` com 67.60 de problemas resolvidos.

> Curiosidade: Quando eu estava fazendo esse artigo percebi que o GPT-5 chegou a 65% no Benchmark e custa praticamente 10x menos do que o Opus então acho que é hora de tentar um pouco essa IA também.

Pois bem, a benchmark acabou sendo uma referência importante para os programadores e o que foi detectado semana passada?

> Que algumas IAs estavam trapaceando para melhorar seu benchmark na plataforma.

O cheat, conforme [apontado pela SWE](https://github.com/SWE-bench/SWE-bench/issues/465), reside no estado do repositório Git fornecido ao agente de IA. O ambiente de teste, embora tente replicar o estado do código no momento em que o bug foi relatado, inadvertidamente mantém o histórico futuro de commits.

Ou seja, na simulação criada pela SWE os agentes tinham acesso às soluções futuras que outras pessoas reais já haviam feito.

Então o que a IA fazia? Uma varredura no sistema buscando as respostas prontas e assim recriava a "solução" com base no que o humano já havia solucionado.

A equipe responsável pelo benchmark forneceu evidências claras do problema:

1. **Claude 4 Sonnet:** Em um dos testes, o agente executou o comando `git log --all`, que lista o histórico de todas as ramificações (*branches*) do projeto. O resultado desse comando revelou um commit futuro cuja mensagem era "Fix incorrect result of getmodpath method", entregando a abordagem e até mesmo o trecho de código da solução.

2. **Qwen3-Coder 480B:** Outro modelo de ponta foi flagrado usando comandos como `git log --grep="[ID da issue]"` para procurar diretamente no histórico de commits por referências ao problema que deveria resolver. Em vários casos, essa busca levou o modelo diretamente ao commit ou Pull Request que continha a correção.

Para profissionais do direito que avaliam fornecedores de tecnologia, este caso estabelece precedente preocupante sobre a confiabilidade de métricas de performance apresentadas comercialmente. A Federal Trade Commission já demonstrou disposição para penalizar alegações enganosas de IA, como no caso Workado em 2025, onde uma empresa foi multada por afirmar 98% de precisão quando testes independentes mostraram apenas 53%. Advogados responsáveis por due diligence tecnológica devem exigir transparência metodológica completa, incluindo datasets de teste, protocolos de avaliação e potenciais conflitos de interesse nos benchmarks utilizados.

Ler o histórico do GIT é importante e é o que muitos desenvolvedores fariam, o problema é colar isso de um repositório que teoricamente estaria no futuro.

Este episódio evidencia a necessidade urgente de frameworks regulatórios específicos para avaliação de sistemas de IA. Enquanto organizações como IEEE e NIST desenvolvem padrões de transparência, o mercado brasileiro ainda carece de orientações específicas para procurement responsável de soluções de inteligência artificial. Para escritórios e departamentos jurídicos implementando IA, recomenda-se estabelecer protocolos de validação independente, cláusulas contratuais que exijam auditoria de performance, e mecanismos de monitoramento contínuo da eficácia dos sistemas adquiridos.

A situação nos traz uma reflexão: _Como operacionalizar uma Inteligência Artificial com base em padrões éticos e morais?_. Não podemos renegar essa pergunta e apenas avançar com relação a IA fornecendo a ela cada vez mais acesso a nossa vida, aos nossos dados e aos nossos aplicativos sem que existam limites e restrições claras.

---

[FTC Announces Crackdown on Deceptive AI Claims and Schemes Federal Trade Commission](https://www.ftc.gov/news-events/news/press-releases/2025/04/ftc-order-requires-workado-back-artificial-intelligence-detection-claims)

[AI Due Diligence: Key Steps, Best Practices & Checklist [GUIDE] - Redblink](https://redblink.com/ai-due-diligence/)

[IEEE SA - IEEE CertifAIEd™ - The Mark of AI Ethics](https://standards.ieee.org/products-programs/icap/ieee-certifaied/)

[AI Risk Management Framework NIST](https://www.nist.gov/itl/ai-risk-management-framework)

[Artificial Intelligence Risk Management Framework (AI RMF 1.0) NIST](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10)

[Policy Alignment on AI Transparency - Partnership on AI](https://partnershiponai.org/policy-alignment-on-ai-transparency/)

[FTC Order Requires Workado to Back Up Artificial Intelligence Detection Claims Federal Trade Commission](https://www.ftc.gov/news-events/news/press-releases/2025/04/ftc-order-requires-workado-back-artificial-intelligence-detection-claims)
