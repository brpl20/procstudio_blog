---
layout: page
title: Manual do Usuário para o ProcStudio
permalink: /user-manual/
---

<style>
.dev-info {
  background-color: #f0f0f0;
  border-left: 5px solid #007bff;
  padding: 10px;
  margin-bottom: 15px;
  font-family: monospace;
}
</style>

# Manual do Usuário - ProcStudio

## Índice

1. [Introdução](#introdução)
2. [Clientes](#cadastro-de-clientes)
3. [Trabalhos](#gestão-de-trabalhos)
4. [Documentos Legais](#documentos-legais)
5. [Usuários](#gestão-de-usuários)
6. [Escritórios](#gestão-de-escritórios)
7. [Tarefas](#tarefas)
8. [Atuação em Conjunto](#atuação-em-conjunto)

## Introdução

O ProcStudio é um sistema de gerenciamento de escritório de advocacia projetado para facilitar o gerenciamento de clientes, processos, documentos legais e tarefas diárias. O sistema também oferece funcionalidades de assinatura online, seguindo uma política de zero papel, e fornece aos clientes uma plataforma para acompanhamento processual.

<div class="dev-info">
Arquivos relacionados: 
<ul>
<li>README.md</li>
<li>config/application.rb</li>
</ul>

Monitoramento de alterações:
Implementar um webhook do GitHub para notificar sobre alterações nos arquivos principais.
</div>

## Cadastro de Clientes

### Tipos de Clientes
- Pessoa Física
- Pessoa Jurídica
- Contador

### Capacidade Civil
- Capaz
- Relativamente Incapaz
- Absolutamente Incapaz

### Funcionalidades
- Adicionar novo cliente
- Editar informações do cliente
- Associar representante legal (para clientes incapazes)
- Visualizar histórico do cliente

<div class="dev-info">
Arquivos relacionados:
<ul>
<li>app/models/client.rb</li>
<li>app/controllers/clients_controller.rb</li>
<li>app/views/clients/*</li>
</ul>

Monitoramento de alterações:
Criar um job que verifica diariamente as alterações nos modelos e controladores relacionados aos clientes.
</div>

## Gestão de Trabalhos

### Cadastro de Processos Jurídicos
- Informações do cliente
- Dados do processo
- Poderes concedidos
- Associação com o escritório de advocacia

### Parceiros
- Cadastro de parceiros
- Associação de parceiros a processos

<div class="dev-info">
Arquivos relacionados:
<ul>
<li>app/models/work.rb</li>
<li>app/controllers/works_controller.rb</li>
<li>app/views/works/*</li>
</ul>

Monitoramento de alterações:
Implementar um listener para alterações no modelo Work e seus relacionamentos.
</div>

## Documentos Legais

O sistema permite a geração dos seguintes documentos:

1. Procuração
2. Termo de Renúncia
3. Contrato de Honorários
4. Declaração de Carência

### Como Gerar Documentos
1. Selecione o cliente
2. Escolha o tipo de documento
3. Preencha as informações necessárias
4. Gere o documento

<div class="dev-info">
Arquivos relacionados:
<ul>
<li>app/services/generate_docs/*</li>
<li>app/models/document.rb</li>
<li>app/controllers/documents_controller.rb</li>
</ul>

Monitoramento de alterações:
Criar um sistema de versionamento para os templates de documentos e notificar quando houver atualizações.
</div>

## Gestão de Usuários

### Tipos de Usuários
- Advogado
- Paralegal
- Estagiário
- Secretário
- Contador
- Contador Externo

### Permissões de Acesso
- Advogado: Acesso total (CRUD completo)
- Paralegal: Acesso limitado (algumas restrições)
- Estagiário: Acesso de visualização
- Secretário: Acesso limitado (algumas restrições)
- Contador: Acesso específico para trabalhos tributários
- Contador Externo: Visualização limitada a clientes específicos

<div class="dev-info">
Arquivos relacionados:
<ul>
<li>app/models/admin.rb</li>
<li>app/models/profile_admin.rb</li>
<li>app/controllers/admins_controller.rb</li>
</ul>

Monitoramento de alterações:
Implementar testes automatizados para verificar as permissões de usuário e notificar em caso de falhas.
</div>

## Gestão de Escritórios

- Cadastro de escritórios
- Associação de advogados a escritórios
- Gerenciamento de filiais

<div class="dev-info">
Arquivos relacionados:
<ul>
<li>app/models/office.rb</li>
<li>app/controllers/offices_controller.rb</li>
<li>app/views/offices/*</li>
</ul>

Monitoramento de alterações:
Criar um job que verifica semanalmente as alterações na estrutura de escritórios e gera um relatório.
</div>

## Tarefas

### Tipos de Tarefas
- Relacionadas a um cliente
- Relacionadas a um trabalho (processo)
- Tarefas gerais do escritório

### Funcionalidades
- Criar nova tarefa
- Atribuir responsável
- Definir prazo
- Marcar como concluída

<div class="dev-info">
Arquivos relacionados:
<ul>
<li>app/models/job.rb</li>
<li>app/controllers/jobs_controller.rb</li>
<li>app/views/jobs/*</li>
</ul>

Monitoramento de alterações:
Implementar um sistema de log para registrar todas as alterações nas tarefas e notificar os usuários relevantes.
</div>

## Atuação em Conjunto

O sistema permite o registro e gerenciamento de atuações em conjunto com outros advogados ou escritórios.

### Como Registrar Atuação em Conjunto
1. Selecione o processo
2. Adicione os advogados ou escritórios parceiros
3. Defina as responsabilidades de cada parte

<div class="dev-info">
Arquivos relacionados:
<ul>
<li>app/models/job_work.rb</li>
<li>app/controllers/job_works_controller.rb</li>
<li>app/views/job_works/*</li>
</ul>

Monitoramento de alterações:
Criar um sistema de notificações para informar todos os envolvidos sobre alterações em atuações conjuntas.
</div>

## Suporte

Para mais informações ou suporte, entre em contato com nossa equipe de suporte através do e-mail suporte@procstudio.com ou pelo telefone (11) 1234-5678.

<div class="dev-info">
Arquivos relacionados:
<ul>
<li>app/mailers/support_mailer.rb</li>
<li>app/views/support/*</li>
</ul>

Monitoramento de alterações:
Implementar um sistema de feedback para usuários que acessam a seção de suporte e monitorar as principais dúvidas e problemas relatados.
</div>