---
layout: post
title: "RAG juridico: como estruturar documentacao que a IA entende (Parte 2)"
description: "Parte 2 tecnica sobre RAG juridico: chunking, metadados, taxonomia, versao de documentos e testes de recuperacao para aumentar a precisao da IA."
keywords: "RAG juridico, documentacao para IA, chunking, metadados, taxonomia juridica, base de conhecimento, recuperacao de informacao"
date: 2026-01-20
author: "Bruno Pellizzetti"
published: true
tags: [IA, RAG, Documentacao, Advocacia Digital]
lang: pt-br
permalink: /rag-juridico-documentacao-ia-parte-2/
image: "/img/rag-juridico-parte-2.png"
og_image: "/img/rag-juridico-parte-2.png"
categories: [IA & Inovacao]
---

![RAG juridico](/img/rag-juridico-parte-2.png)

# RAG juridico: como estruturar documentacao que a IA entende (Parte 2)

A Parte 1 mostrou os fundamentos. Agora o foco e tecnico: como organizar a base documental para melhorar recuperacao de informacao e reduzir respostas imprecisas.

RAG funciona bem quando a documentacao e consistente, segmentada e rastreavel. Abaixo estao as praticas que mais impactam a qualidade.

## 1) Chunking baseado em significado

Chunking e a divisao dos documentos em partes menores. O erro comum e cortar por tamanho fixo. O ideal e cortar por significado:

- Cada chunk deve conter uma unidade completa de informacao.
- Evite separar definicoes do contexto imediato.
- Agrupe regra + excecao no mesmo chunk.

**Exemplo pratico:**

- Ruim: separar prazos e requisitos em blocos distintos.
- Bom: prazo + requisito + excecao no mesmo bloco.

## 2) Metadados juridicos essenciais

Metadados ajudam o sistema a filtrar o que e relevante. Um conjunto minimo:

- Area (previdenciario, trabalhista, civil)
- Tipo (modelo, orientacao, jurisprudencia)
- Data e versao
- Jurisdicao (STJ, STF, TJ)
- Status (vigente, revogado, em revisao)

Sem metadados, a IA pode responder com regras antigas ou fora de contexto.

## 3) Taxonomia e vocabulario controlado

Crie um vocabulario padrao para termos juridicos do escritorio. Isso melhora a busca semantica e reduz ambiguidades.

**Exemplo:**

- Use "peticao inicial" como termo principal.
- Registre sinonimos apenas como referencia.

Esse padrao ajuda tanto humanos quanto a IA.

## 4) Versionamento de documentos

Documentos juridicos mudam com frequencia. Sem controle de versao, a IA pode recuperar conteudo desatualizado.

Boas praticas:

- Inclua numero de versao no front matter.
- Registre data de atualizacao.
- Marque documentos antigos como "revogado".

## 5) Estrutura recomendada por tipo

**Modelo de documento procedural:**

- Objetivo
- Base legal
- Passo a passo
- Excecoes
- Documentos exigidos
- Checklist final

**Modelo de jurisprudencia:**

- Ementa
- Tese aplicavel
- Relacao com casos internos
- Link oficial

## 6) Testes de recuperacao

Teste o RAG com perguntas reais. O objetivo e verificar se o sistema recupera o chunk correto.

**Checklist de teste:**

- A resposta citou a fonte correta?
- O trecho recuperado e atual?
- O contexto esta completo?

Se a resposta usa fonte errada, ajuste metadados ou reorganize o chunk.

## 7) Indicadores de qualidade em RAG

Algumas metricas praticas:

- **Precision@k:** quantas fontes relevantes aparecem no top k.
- **Recall:** quantas fontes relevantes foram recuperadas.
- **Taxa de citacao correta:** percentual de respostas com referencia valida.

Mesmo metricas simples ja mostram onde a base precisa de ajustes.

## 8) Exemplo de template de documento

```
---
titulo: "Prazo de recurso ordinario"
area: "trabalhista"
tipo: "orientacao"
versao: "1.2"
status: "vigente"
ultima_atualizacao: "2025-12-10"
---

Objetivo: orientar sobre prazo e requisitos do recurso ordinario.

Base legal: CLT, art. 895.

Prazo: 8 dias uteis contados da intimacao.

Excecoes: casos com Fazenda Publica.
```

## FAQ

**Qual o tamanho ideal de chunk?**
Depende do conteudo, mas em geral entre 300 e 800 palavras por unidade coerente.

**Preciso de metadados para tudo?**
Sim. Metadados sao o filtro principal para reduzir erros.

**RAG elimina alucinacoes?**
Nao. Ele reduz, mas nao substitui revisao humana.

---

Com essa base, o escritorio ganha respostas mais consistentes e rastreaveis. O proximo tema e como avaliar modelos com benchmarks reais.
