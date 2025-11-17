---
layout: post
title: "Como Programar com IA"
description: "Um guia prático e reflexivo sobre como usar Inteligência Artificial no desenvolvimento de software — incluindo ferramentas como Claude Code, GPT-5, Zed e estratégias reais de produtividade com IA."
keywords: IA para programadores, programar com inteligência artificial, Claude Code, GPT-5, IA no desenvolvimento, melhores práticas com IA, automatização de código, ferramentas de IA para devs
date: 2025-11-07
author: "Bruno Pellizzetti"
published: true
tags: [IA, Direito, Legal Tech, Advocacia Digital]
lang: pt-BR
permalink: /como-programar-com-ia/
image: "/img/como-programar-com-ia.png"
og_image: "/img/como-programar-com-ia.png"
categories: [IA & Inovação]
---

![Como programar com IA](/img/como-programar-com-ia.png)

# Como programar com IA

Já faz tempo que eu não posto nada aqui sobre tecnologia justamente porque eu tenho andado ocupado programando a maior parte do meu tempo o meu sistema, o ProcStudio.

O que tem me ajudado muito são as ferramentas de Inteligência Artificial, especialmente o Claude Code. Algumas dessas estratégias eu aprendi sozinho e outras eu acabei copiando de algum programador mais experiente, então vamos lá.

Primeiramente você precisa entender que eu não sou um programador profissional, tenho um conhecimento de bootcamp e autodidata, estou longe de um conhecimento profissional, mas às vezes, justamente o que você precisa é de um conhecimento menos "enviesado".

No decorrer deste texto vou adicionar alguns artigos que podem te ajudar nesta jornada, o primeiro é deste desenvolvedor não profissional assim como eu:

- [https://efitz-thoughts.blogspot.com/2025/08/my-experience-creating-software-with_22.html](https://efitz-thoughts.blogspot.com/2025/08/my-experience-creating-software-with_22.html)

Outro é um veterano tentando o 'vibe coding':

- [https://levelup.gitconnected.com/vibe-coding-as-a-coding-veteran-cd370fe2be50](https://levelup.gitconnected.com/vibe-coding-as-a-coding-veteran-cd370fe2be50)

Um expoente do IA na programação é o Simon Willisons, muitos insights deste texto foram retirados aos poucos do seu [blog](https://simonwillison.net/):

- [E este post também é muito bom](https://simonwillison.net/2025/Mar/11/using-llms-for-code/)

## Setup

Geralmente eu divido meu setup entre dois terminais, um com 5 abas do repositório: `API, Frontend, Backend, Testes, Docs` e no outro rodando com 3 abas: `Rails Server, Rails Console, Vite Server - Svelte` para debugar o que está acontecendo. Nestes terminais eu rodo o Claude Code, no máximo em duas frentes para não gerar confusão.

Além disso, eu uso o GPT-5 no Zed para dúvidas rápidas, um navegador para o Claude e DeepSeek para questões mais simples como comandos da AWS, e se precisar abrindo um Claude Code no terminal do Zed também ganha produtividade. Se você não tem o Zed disponível ou não gostou (ainda faltam muitas extensões), use o VSCode com o RooCode que é uma excelente ferramenta.

Confira a SWE Bench para ver os melhores modelos com base em resolução de issues: [https://github.com/SWE-bench](https://github.com/SWE-bench)

Como eu falei, não gosto de usar múltiplas instâncias do Claude porque não consigo acompanhar o desenvolvimento propriamente, mas se você é um programador experiente isso é perfeitamente possível utilizando git trees e outras ferramentas. Veja este artigo que é de um programador mais experiente:

- [https://zachwills.net/i-managed-a-swarm-of-20-ai-agents-for-a-week-here-are-the-8-rules-i-learned/](https://zachwills.net/i-managed-a-swarm-of-20-ai-agents-for-a-week-here-are-the-8-rules-i-learned/)
- [https://zachwills.net/how-to-use-claude-code-subagents-to-parallelize-development/](https://zachwills.net/how-to-use-claude-code-subagents-to-parallelize-development/)

**1. Faça prompts simples:** Pequenos e de melhorias incrementais. No início eu pedia para a IA refatorar uma grande quantidade de código ou mesmo criar uma funcionalidade complexa. O resultado: algumas linhas úteis, porém a maioria acabava se perdendo e uma infinidade de erros acontecia. Depois que eu li um artigo do pessoal da Repomirror, consegui aprender algo muito valioso. O melhor são pequenos prompts (eles chegaram ao benchmark de 103 palavras - que é bem aceitável) de tarefas únicas. Se você concatenar tarefas, tenha certeza de que sejam simples e que suas instruções sejam bem organizadas. Neste projeto específico eles deixaram a IA em looping até copiar efetivamente um repositório específico em outra linguagem. Não se frustre com pequenos ganhos incrementais ou a diminuição de prompts. A IA já está te dando um ganho de produtividade imenso. Você não precisa resolver tudo com um único prompt como se a LLM fosse fazer mágica:

- [https://github.com/repomirrorhq/repomirror/blob/main/repomirror.md](https://github.com/repomirrorhq/repomirror/blob/main/repomirror.md)

**2. Fique atento ao modelo que está sendo utilizado:** Mesmo que você tenha um plano abrangente com o Claude Code você vai ter limites de uso de modelos. Estes limites são diários e semanais. Portanto utilize os modelos mais avançados com cuidado. Para ações simples sempre utilize modelos mais simples ou até mesmo outra ferramenta. Aliás, sobre isso, o maior aprendizado é aprender a utilizar a ferramenta, assim como precisamos aprender a extrair o melhor do nosso editor de textos, do terminal, do aprendizado de Rails e Svelte. Aprenda a utilizar a ferramenta lendo a documentação e acompanhando as notícias da Anthropic, iniciando com essa leitura básica: 

- [https://www.anthropic.com/engineering/claude-code-best-practices](https://www.anthropic.com/engineering/claude-code-best-practices)

**3. Utilize a IA para melhorar a IA:** Planeje muito antes de iniciar a execução do código, entenda as possíveis falhas e pontos que você precisa cobrir, utilize modelos mais complexos para te ajudar no planejamento de novas features, dúvidas difíceis de resolver, especialmente de arquitetura. Crie abstrações e questionamentos diversos, enfim, crie um longo chat sobre arquitetura. Utilize o bom e velho chat do navegador mesmo, sem nenhuma ferramenta e somente depois passe para o prompt que o agente executará isso bem mais facilmente. Finalmente, salve o chat e compartilhe com a equipe através do Linear ou outra ferramenta, isso vai evitar novos e novos chats e retrabalho. Veja o exemplo:

> As a software architect what is the best way to create a system for reporting system throught all my Models, please note we have specific methods already implemented but are hard to mantain and we need an migration strategy.

> Help me build a reporting system.

**Mais sobre arquitetura de software:**
- [97 Things Every Software Architect Should Know](https://yoshi389111.github.io/kinokobooks/soft_en/index.html)
- [Renato Augusto](https://www.youtube.com/@RenatoAugustoTech)

**4. Não fuja do padrão:** Muitos programadores experientes têm relatado que as IAs funcionam bem para aquilo que já foi escrito e reescrito um milhão de vezes. Como um simples sistema de CRUD, por exemplo. Porém a IA não vai te responder bem em coisas que nunca foram criadas ou que são usadas em poucos projetos. Um dos exemplos é atalho de teclado no navegador (não achei a referência para essa informação, mas quando me deparar com algo neste sentido eu colocarei aqui). Portanto, nestas tecnologias você vai precisar estudar o que você precisa fazer de fato e somente depois alimentar a IA utilizando o seu modelo. Um exemplo é o React que tem muitos exemplos pela internet contra o Svelte que tem menos usabilidade. Então o Svelte não seria o melhor candidato para programar com a IA, especialmente por causa do Svelte 5. Mas foi a opção escolhida por ser um framework rápido e responsivo e até para não ficarmos preguiçosos pedindo tudo para a IA.

**5. Sobre modelos, é importante sempre alimentar a IA com um código base:** A equipe da Cloudflare fez isso com muito sucesso no projeto de criação do OAuth e o que existe no seu repositório importa muito, porque é onde a IA vai buscar inspirações para o código. Se o seu código atual é ruim, a IA vai continuar reproduzindo código ruim.

- [https://github.com/cloudflare/workers-oauth-provider/?tab=readme-ov-file#written-using-claude](https://github.com/cloudflare/workers-oauth-provider/?tab=readme-ov-file#written-using-claude)

> In all seriousness, two months ago (January 2025), I (@kentonv) would have agreed. I was an AI skeptic. I thought LLMs were glorified Markov chain generators that didn't actually understand code and couldn't produce anything novel. I started this project on a lark, fully expecting the AI to produce terrible code for me to laugh at. And then, uh... the code actually looked pretty good. Not perfect, but I just told the AI to fix things, and it did. I was shocked.

> To emphasize, this is not "vibe coded". Every line was thoroughly reviewed and cross-referenced with relevant RFCs, by security experts with previous experience with those RFCs. I was trying to validate my skepticism. I ended up proving myself wrong.


**6. A IA não se importa tanto com organização e legibilidade do código:** De forma que cabe a você quebrar os componentes e o código de uma forma fácil e legível para o seu colega humano ou para você mesmo depois de certo tempo.

**7. Saiba suas limitações:** No texto já citado no início deste documento de Zack Will, ele ensina de forma incrível como utilizar a IA em múltiplos terminais para executar várias tarefas ao mesmo tempo. Ele, como um profissional experiente, mostrou que isso é perfeitamente possível. Porém, isso para mim é impossível, porque meu limitado conhecimento não permite que eu acompanhe todas essas telas e todo esse código com uma velocidade razoável. Geralmente eu demoro uma semana para revisar o que a IA fez em uma sessão.

**8. Acompanhe a IA e interrompa-a se estiver indo no caminho errado:** Seguindo a recomendação de Zack, ele também informa que você deve interromper a IA no primeiro momento em que ela estiver desviando do direcionamento que você deu no prompt. Não adianta ter esperança de "ver até onde isso vai dar", em todas as vezes ela vai continuar ou piorar outro erro.

**9. Checkpoints ou commits frequentes:** Alguns editores de texto já têm o sistema de checkpoint embarcado no chat da IA, o que permite o retorno rápido do estado anterior do sistema em caso de erros desastrosos. Se você não tiver esse sistema, apenas faça commits mais frequentes no seu código. Nunca peça para a IA remover o que ela criou anteriormente (excluir algum arquivo, por exemplo) porque ela vai esquecer alguma coisa e seu código vai quebrar e você vai gastar tokens na reversão: *Resete o git e dê um /clean no contexto*.

**10. Revisão:** Tenha seu próprio prompt para revisão e use o modelo mais poderoso para isso. O meu é o seguinte:

> Act as a senior QA / code especialist and check my last commit for flaws, broken features, code mantaibility, DRY and good practices.

**11. Tecnologia nova:** Trabalhar com novas bibliotecas e novas tecnologias é problemático. Já gerei muito código deprecado de ImageMagick, Mongo e Svelte 4, por exemplo. Lembre-se que as IAs dependem de muito aprendizado por reforço, o que faz com que elas fiquem 'viciadas' em padrões de códigos antigos. Introdução de novos códigos demoram muito e o melhor é estudá-los do modo antigo. Antes de iniciar a sessão, injete a tecnologia nova na IA e depois revise com cuidado redobrado. Adicione regras estáticas para ser um failsafe contra códigos deprecados.

**12. Frustração:** Um dos grandes insights que eu tive foi lendo o blog do Simon Willison, que em algum momento falou: Não fique frustrado com os erros da IA. Basta você reformular e refatorar tudo de novo. Ela não cansa, então você não tem praticamente qualquer limite de refatoração: Então eu sempre carrego esse modelo mental. Eu não posso me frustrar com a IA, ela está aqui para me ajudar e não vai me julgar pelos meus erros e minhas pequenas bobagens. A única pessoa que pode cansar e se frustrar sou eu e eu não vou fazer isso.

**13. Domine o MCP (Model Context Protocol):** O uso dos MCPs permite uma agilidade muito grande no desenvolvimento e ajuda a deixar a IA muito mais poderosa e livre para executar suas ferramentas, inclusive para ter acesso à documentação. Quando eu preciso de algo muito complexo, eu ativo o claude-swarm pré-configurado para o Rails, assim eu tenho um exército de agentes prontos para executarem as tarefas para mim. Atualmente estou usando o Claude-On-Rails que é um Framework muito bom, mas consome muito recurso de tokens _use com cuidado_:

- [https://www.youtube.com/watch?v=FLpS7OfD5-s](https://www.youtube.com/watch?v=FLpS7OfD5-s)
- [https://github.com/obie/claude-on-rails](https://github.com/obie/claude-on-rails)
- [https://khromov.se/how-and-why-i-built-an-mcp-server-for-svelte/](https://khromov.se/how-and-why-i-built-an-mcp-server-for-svelte/) (Cuidado que neste ele tem SvelteKit junto, o que pode confundir a IA)
- [https://modelcontextprotocol.io/docs/getting-started/intro](https://modelcontextprotocol.io/docs/getting-started/intro)

**14. Crie instruções práticas para a IA nos arquivos .md no seu repositório:** Isso vai dar um direcionamento muito melhor para a IA. Certifique-se de que ela faça a leitura do documento porque isso pode não acontecer:  _Lembre-se a IA é um dev júnior que não aprende_. Geralmente esse arquivo é salvo como `CLAUDE.md` ou `AGENTS.md`. Você também pode criar arquivos específicos, por exemplo, na minha pasta de testes eu tenho um `CLAUDE-e2e.md` e um `CLAUDE-api.md` que vão lidar cada um com uma responsabilidade específica.

- [https://www.sanity.io/blog/first-attempt-will-be-95-garbage](https://www.sanity.io/blog/first-attempt-will-be-95-garbage)

**15. Forneça ferramentas para a IA:** Por exemplo, na minha configuração eu tenho um sistema de autenticação pronto para a IA fazer alguns testes via API, assim eu não preciso ficar fornecendo instruções de como logar no sistema e testar e isso economiza muitos tokens e tempo evitando que ela decifre como logar no sistema todas as vezes.

**16. Docs:** Evite utilizar a IA para criar documentos. Ela irá inflar o documento com EMOJIS e informações genéricas e desnecessárias que ninguém vai querer ler e isso irá contaminar a cultura de código. Use apenas para criar um template básico e te ajudar em alguma dúvida pontual.

**17. Mantenha-se conectado à sua code base:** A partir do momento que você perde o toque do que está realmente acontecendo com o seu código, você precisa parar, ler, testar, visualizar e entender o que o seu código está fazendo e deixando de fazer. Você precisa ter o alinhamento mental. Se você fica muito tempo no prompt do Claude Code e pouco tempo no editor de textos, provavelmente é um sinal que isso irá acontecer mais cedo ou mais tarde: _Pare tudo e volte ao básico lendo e entendendo linha a linha_. Esse texto (aliás muito importante para entender como trabalhar com códigos em larga escala) fala muito sobre este alinhamento: Prioridades: Mental Alignment -> Correct Solution -> Design Discussion -> Find Bugs -> Style.

- [https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md)

> This is actually the most important part of research/plan/implement to us. A guaranteed side effect of everyone shipping way more code is that a much larger proportion of your codebase is going to be unfamiliar to any given engineer at any point in time.