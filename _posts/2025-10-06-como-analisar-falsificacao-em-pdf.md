---
layout: post
title: "Como analisar falsificação em PDFs"
description: "Aprenda a identificar falsificações em documentos PDF por meio da análise de metadados, checksums e assinaturas digitais. Um guia completo com exemplos reais e ferramentas gratuitas."
keywords: ["falsificação de PDF", "análise forense digital", "metadados PDF", "checksum", "assinatura digital", "prova digital", "autenticidade de documentos", "perícia em PDF"]
date: 2025-10-06
tags: [pdf, forensics, security, manipulation, falsification]
author: Bruno Pellizzetti
published: true
lang: pt-br
image: "/img/como-analisar-falsificacao-em-pdf.png"
og_image: "/img/como-analisar-falsificacao-em-pdf.png"
permalink: "/analisar-falsificacao-em-pdfs/"
categories: [Segurança Digital, Direito Digital]
---

![documento com alterações sendo investigado](/img/como-analisar-falsificacao-em-pdf.png)

# Como analisar falsificação em PDFs

PDFs são frequentemente considerados documentos "finais" e imutáveis, mas essa percepção é incorreta. Documentos PDF podem ser alterados após sua criação e até mesmo após assinatura digital. Este manual ensina como identificar quando um PDF foi manipulado ou falsificado, usando técnicas que qualquer pessoa pode aplicar.

## Caso Real: O Contrato Falsificado

Em um caso de investigação foi descoberto a alteração em um contrato de locação **após** ele ter sido assinado digitalmente, inserindo um adendo que não existia no documento original. A investigação revelou evidências irrefutáveis da falsificação através da análise de metadados e checksums - conceitos que são acessíveis a qualquer pessoa e que exploraremos neste manual.

## Conceitos Fundamentais

### O que são Metadados?

Metadados são "dados sobre dados" - informações ocultas dentro do arquivo PDF que registram:

- **Quando** o documento foi criado;
- **Quando** foi modificado pela última vez;
- **Quem** criou ou editou o documento;
- **Qual software** foi usado;
- **Quantas versões** existem do documento.

Pense nos metadados como o "DNA digital" de um documento - eles contam a história de sua vida.

### O que é um Checksum?

Um checksum (ou hash) é como uma "impressão digital" única de um arquivo. Se qualquer coisa no arquivo mudar - mesmo uma única vírgula - o checksum será completamente diferente. É matematicamente impossível falsificar um checksum, tornando-o uma prova definitiva de autenticidade.

**Exemplo prático:** No caso, o certificado de assinatura digital incluía um checksum do documento original. Quando o investigador calculou o checksum do PDF alterado, ele não correspondia ao certificado - prova irrefutável de que o documento havia sido modificado após a assinatura.

### IDs de Documento PDF

Todo PDF possui dois identificadores internos:

- **ID0:** Criado quando o documento é gerado pela primeira vez (certidão de nascimento).
- **ID1:** Muda sempre que o documento é modificado (histórico de alterações).

Quando ID0 e ID1 são idênticos, o documento nunca foi modificado. Quando são diferentes, houve alteração.

## Sinais de Alerta (Red Flags)

### Inconsistências Temporais

**O que procurar:**

- Data de modificação anterior à data de criação;
- Timestamps em fusos horários diferentes: Exemplo de uso de um serviço online para modificação por exemplo;
- Datas que não fazem sentido no contexto.

**Exemplo do caso real:** O documento original mostrava criação e modificação no mesmo momento em UTC. O documento falsificado mantinha a data de criação, mas tinha modificação dias depois em horário do Pacífico.

### Múltiplas Versões (EOFs)

PDFs modificados frequentemente contêm vestígios de versões anteriores. Cada vez que um PDF é salvo, ele adiciona um marcador "%%EOF" (End of File). Múltiplos EOFs indicam múltiplas edições.

### Evidências de Edição

**TouchUp_TextEdit:** Tag específica que aparece quando o Adobe Acrobat é usado para editar texto após o documento estar "finalizado".

**Fontes Renomeadas:** Quando uma página é editada, o software frequentemente renomeia todas as fontes daquela página de forma diferente do resto do documento.

## Ferramentas de Análise

### Ferramentas Gratuitas Essenciais

| Ferramenta     | O que faz                                 | Onde obter         |
|----------------|---------------------------------------------|--------------------|
| **PDFtk**       | Extrai metadados e informações estruturais  | pdflabs.com |
| **ExifTool**    | Analisa metadados detalhados                | exiftool.org |
| **PdfInfo**     | Mostra informações básicas do PDF           | Parte do Poppler |
| **Online MD5**  | Calcula checksums                           | onlinemd5.com |
| **PDF Analyzer**| Análise visual online                       | pdf-online.com |

## Análise Passo a Passo

### Investigação Básica

1. **Primeira inspeção visual**
- O documento parece uniforme?
- Há diferenças de formatação entre páginas?
- Algum texto parece "encaixado" de forma estranha?

2. **Verificação de metadados**
- As datas fazem sentido?
- O software usado é consistente?
- Há evidências de múltiplas edições?

3. **Análise de certificados**
- Se houver certificado digital, os checksums correspondem?
- A data do certificado bate com os metadados?

### Investigação Avançada

**Análise de Camadas:** PDFs podem ter texto "escondido" sob elementos visuais. Uma "redação" mal feita (tarjar texto com retângulo preto) ainda permite que o texto seja copiado.

**Verificação de Assinaturas Digitais:** Assinaturas digitais verdadeiras mostram um aviso quando o documento é modificado após a assinatura.

**Comparação de Versões:** Se você tem acesso a múltiplas versões, compare:
- Tamanho dos arquivos;
- Número de páginas;
- Checksums;
- Metadados.

## Assinaturas Digitais e Certificados
Utilize as próprias ferramentas oferecidas pelas empresas ou pelo Gov.br para fazer a verificação.

## Proteção e Prevenção

### Como Se Proteger

1. **Sempre salve uma cópia** imediatamente após assinar.
2. **Calcule e anote o checksum** de documentos importantes.
3. **Tire screenshots** de plataformas de assinatura online.
4. **Verifique certificados** antes de aceitar um documento como válido.
5. **Guarde emails** com links originais para documentos.
6. **Documentação adicional** salve conversas e mensagens relacionados ao negócio em si, isso pode ajudar a provar a intenção na formação do documento.

### Documentando Evidências

Ao encontrar suspeitas de falsificação:

1. **Não modifique** o arquivo suspeito;
2. **Faça múltiplas cópias** de segurança;
3. **Documente todos os metadados** com screenshots;
4. **Calcule e registre checksums** de todas as versões;
5. **Preserve a cadeia de custódia** dos arquivos.

## Valor Probatório
As evidências técnicas descritas neste manual são aceitas em tribunais e podem ser confirmadas como uma prova pericial, que chegará a mesma conclusão que você chegou se tudo foi feito corretamente.

## Conclusão
A aparente imutabilidade dos PDFs é uma ilusão. Como demonstrado no caso real, até mesmo documentos assinados digitalmente podem ser alterados de forma fraudulenta. No entanto, toda alteração deixa rastros digitais que podem ser detectados.

Com o conhecimento e ferramentas descritos neste manual, você está equipado para detectar a grande maioria das tentativas de falsificação de PDFs. Em casos de dúvida, procure um especialista em forense digital - mas agora você sabe o suficiente para identificar quando algo está errado.

---
## Recursos Adicionais

### Leitura Recomendada
- [PDF Reference Manual](https://www.adobe.com/devnet/pdf/pdf_reference.html) - Especificação técnica oficial.
- [Digital Forensics for Legal Professionals](https://www.sciencedirect.com/topics/computer-science/digital-forensics) - Aspectos legais.
- [NIST Guidelines on Digital Evidence](https://www.nist.gov/digital-evidence) - Padrões governamentais.

### Ferramentas Online
- [SmallPDF Metadata Viewer](https://smallpdf.com/pdf-tools) - Visualizador de metadados.
- [Online Hash Calculator](https://emn178.github.io/online-tools/sha256_checksum.html) - Cálculo de checksum.
- [PDF Candy Analyzer](https://pdfcandy.com/) - Análise geral de PDFs.

### Suporte Profissional

Para casos complexos ou com implicações legais significativas, considere contratar:

- Peritos em informática forense.
- Advogados especializados em crimes digitais.
- Empresas de auditoria digital.

Você confiaria em um contrato sem saber se ele foi alterado?

Compartilhe este guia e ajude a divulgar técnicas simples que qualquer pessoa pode usar para identificar falsificações em PDFs.

---
### Sobre o Autor

Bruno Pellizzetti, CEO da ProcStduio e ProcStudio IA, é um advogado previdenciário com mais de 15 anos de experiência no mundo jurídico e nos últimos anos tem se especializado em tecnologia e inteligência artificial. O responsável para implantação de soluções tecnológicas em processos jurídicos nas empresas com o objetivo de democratizar o acesso ao conhecimento jurídico para todos e aumentar a eficiência e precisão das equipes jurídicas.
