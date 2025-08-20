---
layout: post
title: "CloudFare Vs Perplexity: uma briga das novas gigantes da web"
description: "CloudFare expõe Perplexity por constantemente modificar seu agente de usuário e mudando IPs e ASNs para ocultar sua atividade de rastreamento, em conflito direto com as preferências de não rastreamento expressas pelos sites." 
keywords: "Perplexity, Rastreadores não-declarados, Evasão de No-crawl, Inteligência Artificial, Segurança, CloudFare"
date: 2025-08-24
author: "Bruno Pellizzetti"
published: true
categories: Inteligência Artificial, Segurança Cibernética
tags: Perplexity, Rastreamento, Evasão, No-crawl, Inteligência Artificial
lang: pt
permalink: /blog/cloufare-expoe-perplexity-usa-rastreadores-ocultos-nao-declarados
image: /img/cloudfare-vs-perplexity.png
og_image: /img/cloudfare-vs-perplexity.png
---

![CloudFare Vs Perplexity](/img/cloudfare-vs-perplexity.png) 

# CloudFare Vs Perplexity: uma briga das novas gigantes da web

A Cloudfare (talvez o maior expoente de segurança da Web hoje) faz uma exposição alarmante, a Perplexity que se tornou um líder em buscadores de informações baseados em IA, tem feito [rastreamento furtivo da web](https://blog.cloudflare.com/perplexity-is-using-stealth-undeclared-crawlers-to-evade-website-no-crawl-directives/). 

Embora a Perplexity inicialmente rastreie de seu agente de usuário declarado, quando eles se deparam com um bloqueio de rede, parece que tentam obscurecer sua identidade de rastreamento em uma tentativa de contornar as preferências do site.

Conforme observado no post original de Gabriel Corral, Vaibhav Singhal, Brian Mitchell e Reid Tatoris, Perplexity está constantemente modificando seu agente de usuário e alterando seus ASNs (sistema de mapeamento) de origem para ocultar sua atividade de rastreamento. O que também é preocupante, é a indisposição da Perplexity em respeitar - ou até mesmo buscar- os arquivos robots.txt.

A internet, como conhecemos há três décadas, está mudando rapidamente, mas uma coisa permanece constante: ela é baseada em confiança. Existem preferências claras para que os rastreadores sejam transparentes, sirvam a um propósito claro, realizem uma atividade específica e, o mais importante, sigam as diretrizes e preferências dos sites.

Com base no comportamento observado da Perplexity, que é incompatível com essas preferências, a CloudFare deslistou eles como bots verificados e adicionamos heurísticas às nossas regras gerenciadas que bloqueiam esse rastreamento furtivo.

Há um desejo expresso pela internet de como bons bots devem se comportar. Todos os bots bem-intencionados que agem de boa fé devem: ser transparentes, identificarem-se honestamente, não inundarem sites com tráfego excessivo, não rasparem dados sensíveis e não usarem táticas furtivas para tentar driblar a detecção.

A CloudFare atesta que OpenAI é um exemplo de uma empresa líder em IA que segue essas melhores práticas de crawling. Eles claramente descrevem seus bots e fornecem explicações detalhadas para cada propósito do bot. Eles respeitam robots.txt e não tentam evadir uma diretiva robots.txt ou um bloqueio de nível de rede.

Além de banir a Perplexity da whitelist a Cloudfare aponta toda atividade de rastreamento não declarada da empresa para passar por um desafio adicional, bloqueando os bots indesejados.

---

# Sobre o Autor
Bruno Pellizzetti, é CEO da ProcStudio IA e ProcStudio, dois pioneiros no mundo jurídico da tecnologia. Especialista em Direito Previdenciário com mais de 15 anos no mercado jurídico, Bruno tem se