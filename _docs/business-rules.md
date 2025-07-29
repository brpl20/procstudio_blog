---
title: "Business Rules"
category: "Business"
date: 2025-07-29
author: "Bruno Pellizzetti"
tags: [business, models]
excerpt: "Business rules..."
breadcrumbs: ["Development", "API Reference"]
related_docs: ["getting-started", "authentication-guide"]
---

# ProcStudio Business Rules Model

## Table of Contents
- [Project Vision & Evolution](#project-vision--evolution)
- [System Architecture](#system-architecture)
- [Core Data Models](#core-data-models)
- [Business Logic Rules](#business-logic-rules)
- [Authorization & Security](#authorization--security)
- [Software Architecture Best Practices](#software-architecture-best-practices)
- [Testing Strategy](#testing-strategy)
- [Validation Framework](#validation-framework)
- [Bug Prevention & Resolution](#bug-prevention--resolution)

## Project Vision & Evolution

### Mission Statement
ProcStudio was conceived to revolutionize how lawyers generate legal documents, transforming a traditionally complex and time-consuming process into a streamlined, efficient workflow. The platform addresses the critical need for lawyers to produce both simple individual documents and mass document generation while maintaining legal accuracy and compliance.

Zero Paper =>

User First =>

OBS Player => Criar jornada do usuário : Excalidraw

Domínios/Registros =>

Traduzir =>

Trazer Disclamer Docx para cá =>


### Lembretes
- Arquivos compartilhados
- Compartilhar JSONS insominia
- Segurança de Dados e senhas
- Compartilhar design Figma
- Falar sobre planos de pagamentos, acabou ficando em outros lugares esparsos
- Hard Problems => Reduce PDF


### Development Phases

#### Phase 1: MVP - Lawyer-Customer Document Layer (Current)
**Objective**: Establish core document generation between lawyers and their cutomers

**Key Features**:
- Basic legal document templates (contracts -> contrato de honorários, power of attorney -> procuração, declarations -> declaração, termo de juizado)
- Customer relationship management
- Document creation and storage
- Digital signature integration
- Simple workflow management (jobs and works)

**Business Value**: Reduces document creation time by 50% and ensures consistency across all customer documents.

#### Phase 2-> X: Extended Legal Ecosystem Integration
**Objective**: Expand document generation to include justice system and broader legal contexts

**Planned Features**:
- Compliance checking
- Lawyers Partnerships
- AI Helpers
- AI-powered document template suggestions
- AI Extractors
- Mass Document Generation: Subs - regularoty + compliance
- Social Contract and updates
- Wiki
- Reports
- Improve Tasks
- Improve Works
- Improve Processes
- Finances
- Integration with external legal databases
- Time tracking for billing purposes
- Progress reporting to customers
- Approval workflows for task/jogs/docs/works(?) completion
- Finalizar contrato
- Ferramentas: Cálculos básicos
- Ferramentas: Cálculos avançados -- sistemas como planilha inteligente


**Business Value**: Transforms legal practices into highly efficient, data-driven operations capable of handling large-scale legal work.

## System Architecture

### Architectural Principles
- **Domain-Driven Design**: Models reflect real-world legal concepts
- **Service-Oriented Architecture**: Modular services for document generation, user management, and integrations
- **Event-Driven Patterns**: Document lifecycle events trigger automated workflows
- **SOLID Principles**: Maintainable, extensible codebase

### Technology Stack
- **Backend**: Ruby on Rails 7.0 --- Ruby 2.6.10
- **Database**: PostgreSQL
- **Authentication**: Devise with role-based access control
- **Document Processing**: Docx gem with custom legal template engine
- **Digital Signatures**: ZapSign API integration (OFFLINE :x:)
- **Cloud Infrastructure Storage**: AWS S3
- **Server**: Hostinger
- **Email Services**: MailJet Free
- **Monitoring**: Pending :x:
- **Testing**: Peinding :x:

#### Environments
- [Homologação Admins](https://admin_hml.procstudio.com.br)
- [Homologação Clientes](https://admin_hml.procstudio.com.br)
- [Produção](https://procstudio.com.br)
- [Blog](https://blog.procstudio.com.br/)
- [Docs](https://blog.procstudio.com.br/docs/)

#### Repositórios
- [API Central](https://github.com/brpl20/prc_api)
- [Client Frontend](https://github.com/brpl20/prc_client-fe)
- [Admin Frontend](https://github.com/brpl20/prc_admin-fe)
- [Blog-Docs](https://github.com/brpl20/procstudio_blog)
- [Tests](https://github.com/brpl20/procstudio_tests)
- [ProcStudio-OCR] *TD*
- [Legal_Data] *TD*


## Core Data Models

### Primary Entities

#### Admin Model
**Purpose**: Central platform users representing legal professionals

**Admin Model Journey**:

Possíveis jornadas do usuário:

1. Advogado iniciante começa a praticar o direito, geralmente sozinho e sem auxiliares;
2. Advogado se une com um colega para iniciar seu escritório de advocacia, porém sem grana para terem um CNPJ;
3. Advogado já intermediário tem um CNPJ e deseja melhorar seus processos internos;
4. Advogados abrem um CNPJ para economias fiscais, já estão em um estágio intermediário;
5. Advogados mais avançados possuem um CNPJ com vários advogados e funcionários;
6. Dois advogados abrem uma sociedade mas possuem um outro advogado parceiro no seu escritório que atua somente na pessoa física ainda;

Neste contexto teremos também mudanças nas sociedades e contratação de estagiários, secretárias, paralegais e outros advogados.

<< Vídeo do Youtube >>

Neste sentido precisamos observar que temos muitas lógicas e possibilidades dentro de uma sociedade, o que nós trás a uma ideia de encapsulamento do negócio dentro de uma figura abstrata de times, que abarcará essas lógicas e determinará os relacionamentos entre estes times e os customers dentro do negócio, com todos os detalhes e granularidade possível.

**Relationships**:
- `belongs_to :office` (optional - solo practitioners supported)

##### Accountants

**Business Context**: In Brazilian legal practice, accountants often work closely with lawyers, especially in tax law. The system accommodates this with specialized roles:
- **Counter**: Accountant with lawyer-like powers for tax cases
- **ExCounter**: External accountant with read-only access for customer monitoring


#### Customer Model
**Purpose**: Lawyer's customers with system access for case monitoring

**Business Rules**:
- Automatic account creation when added to system
- Email invitation with secure access credentials
- Subdomain access: `customer.procstudio.com.br`
- Data isolation per lawyer/office context
- Document download and case status monitoring

**Key Features**:
- Case timeline visibility
- Document library access
- Communication history with legal team
- Billing and payment tracking

#### Work Model
**Purpose**: Primary legal cases or projects for customers

**Business Context**: Represents comprehensive legal matters that may span months or years, containing multiple smaller tasks (jobs).

**Relationships**:
- `belongs_to :customer`
- `belongs_to :admin` -> Provavelmente mudaremos para `team`

#### Job Model
**Purpose**: Granular tasks within works or standalone customer services

**Business Value**: Enables precise task delegation and progress tracking, essential for law firm efficiency.

**Types of Jobs**:
- **Pre-Work Jobs**: Initial consultations, research, document review
- **Work-Related Jobs**: Specific tasks within larger cases
- **Administrative Jobs**: Filing, correspondence, scheduling
- **Research Jobs**: Legal precedent research, case law analysis

**Delegation Rules**:
- Jobs can be assigned to any qualified team member


#### JobWork Model
**Purpose**: Many-to-many relationship enabling job-work associations

**Business Logic**: Allows complex case management where jobs can belong to multiple works or exist independently.

#### Document Model
**Purpose**: Generated legal documents with version control and digital signatures

**Document Lifecycle**:
1. **Template Selection**: Choose from predefined legal templates
2. **Data Population**: Automatic filling from customer/work data
3. **Review Process**: Internal approval workflows
4. **Customer Review**: Customer access for review and feedback
5. **Digital Signature**: ZapSign integration for legally binding signatures
6. **Archive**: Secure storage with audit trail

**Document Types**:
- Power of Attorney (Procuração)
- Legal Contracts (Contratos)
- Poverty Declarations (Declaração de Carência)
- Waiver Terms (Termo de Renúncia)
- Court Filings (Petições)

#### Power Model
**Purpose**: Legal representation authorities assigned to specific works

**Brazilian Legal Context**: Powers define the scope of lawyer's authority to act on behalf of customers in various legal contexts.

**Power Categories**:
- General representation powers
- Specific court representation
- Administrative procedure powers
- Tax and fiscal representation
- Corporate representation powers

#### Honorary Model
**Purpose**: Fee structure management for legal services

**Fee Types**:
- **Work (Fixed)**: Predetermined amount for specific services
- **Success**: Percentage of monetary gains achieved
- **Both**: Combination of fixed fee plus success percentage
- **Bonus (Pro Bono)**: Free legal services
- **Previdenciary Special**: Custom fee structures for social security cases

#### Office Model
**Purpose**: Law firm or legal office entity

**Business Rules**:
- Optional association (supports solo practitioners)
- Multiple lawyers per office supported
- Shared customer and case management within office
- Separate billing and administrative controls

#### Profiles (ProfileAdmin, ProfileCustomer, ProfileWork)
**Purpose**: Extended attribute storage for core entities

**Design Pattern**: Profile pattern prevents core model bloat while maintaining clean database structure.

**ProfileAdmin**: Professional credentials, certifications, specializations
**ProfileCustomer**: Personal details, legal status, contact preferences
**ProfileWork**: Case-specific metadata, custom fields, external references

#### Supporting Models

**Represent Model**: Handles legal representation for incapacitated individuals or corporate entities requiring individual representation.

**Recommendation Model**: Referral system tracking where customers originate and managing referral fee payments.

**PendingDocument Model**: Checklist system for documents required from customers, with future notification capabilities.

**Address/Bank/Email/Phone Models**: Normalized contact and financial information with validation for Brazilian standards.

## Business Logic Rules

### BR001 - Document Generation Workflow
**Automatic Generation Triggers**:
- Customer profile creation → Simple power of attorney
- Work registration → Comprehensive power of attorney + related documents
- Job completion → Progress reports and billing documents

**Template Management**:
- Master templates stored on AWS S3
- Customer-specific customizations supported
- Version control for template changes
- Fallback mechanisms for template failures

### BR002 - User Access Control Matrix

| Role | Customers | Works | Jobs | Documents | Admin Management |
|------|-----------|-------|------|-----------|------------------|
| Lawyer (Full) | Full CRUD | Full CRUD | Full CRUD | Full CRUD | Full CRUD |
| Lawyer (L1) | Full CRUD | Full CRUD | Full CRUD | Full CRUD | Read Only |
| Paralegal | CRU + Supervised D | Full CRUD* | Full CRUD* | Full CRUD* | None |
| Trainee | CR (limited) | UD (own only) | UD (own only) | UD (own only) | None |
| Secretary | CR (no bank) | UD (own only) | UD (own only) | UD (own only) | None |
| Counter | CRU | CRU (tax only) | CRU (tax related) | CRU (tax docs) | None |
| ExCounter | R (assigned only) | R (assigned only) | R (assigned only) | R (assigned only) | None |

*With approval workflow for entities created by others

### BR003 - Data Integrity Rules
- TD

### BR004 - Workflow State Management
**Work States**: `draft → active → [pending] → completed/cancelled → archived`
**Document States**: `draft → review → approved → signed → archived`
**Job States**: `assigned → in_progress → review → completed/cancelled`

**State Transition Rules**:
- TD: Revisar estes `states`:
  - Only assigned users can change states
  - Approval workflows for critical transitions
  - Audit logging for all state changes
  - Rollback capabilities for administrative corrections

## Authorization & Security
- TD

### BR006 - Data Isolation Rules
- TD - Revisar:
  - Customer data partitioned by lawyer/office
  - Document access requires explicit permissions
  - Cross-office data sharing requires administrative approval
  - Audit trails for all data access attempts

### BR007 - External Integration Security
- ZapSign API calls use OAuth 2.0 with token refresh
- MailJet integration with encrypted templates
- AWS S3 access with signed URLs and expiration
- All external API failures gracefully handled

## Software Architecture Best Practices

### Design Patterns Implementation

#### 1. Service Objects Pattern
```ruby
# Document generation service
class DocumentGenerationService
  def initialize(work, template_type)
    @work = work
    @template_type = template_type
  end

  def call
    validate_inputs
    load_template
    populate_data
    generate_document
    store_securely
    notify_stakeholders
  rescue StandardError => e
    handle_generation_error(e)
  end

  private

  def validate_inputs
    raise InvalidWorkError unless @work.valid?
    raise TemplateNotFoundError unless template_exists?
  end
end
```

#### 2. Repository Pattern
```ruby
class CustomerRepository
  def find_by_lawyer(lawyer_id)
    Customer.includes(:profile_customer, :works)
           .where(admin_id: lawyer_id)
           .active
  end

  def find_with_pending_documents(lawyer_id)
    find_by_lawyer(lawyer_id)
      .joins(:pending_documents)
      .where(pending_documents: { status: 'pending' })
  end
end
```

#### 3. Decorator Pattern for Document Templates
```ruby
class DocumentDecorator < SimpleDelegator
  def initialize(document, context = {})
    super(document)
    @context = context
  end

  def formatted_legal_text
    apply_legal_formatting(content)
  end

  def customer_safe_content
    remove_internal_notes(content)
  end
end
```

#### 4. Observer Pattern for Audit Logging
```ruby
class AuditObserver
  def self.document_created(document)
    AuditLog.create(
      action: 'document_created',
      entity: document,
      user: Current.user,
      metadata: document.audit_metadata
    )
  end
end
```

### Code Organization Best Practices

#### 1. Domain-Driven Directory Structure
```
app/
├── models/
│   ├── concerns/
│   │   ├── auditable.rb
│   │   ├── brazilian_validations.rb
│   │   └── role_permissions.rb
│   ├── legal/
│   │   ├── document.rb
│   │   ├── power.rb
│   │   └── work.rb
│   └── users/
│       ├── admin.rb
│       └── customer.rb
├── services/
│   ├── document_generation/
│   ├── user_management/
│   └── integration/
├── policies/
├── decorators/
└── repositories/
```

#### 2. Configuration Management
```ruby
# config/business_rules.yml
document_generation:
  max_template_size: 10MB
  supported_formats: ['.docx', '.pdf']
  signature_timeout: 30.days

user_permissions:
  trainee:
    max_customers: 50
    requires_approval: true
  paralegal:
    max_customers: 200
    can_delete_own: true
```

#### 3. Error Handling Strategy
```ruby
class ApplicationService
  include ErrorHandling

  private

  def handle_errors
    yield
  rescue ValidationError => e
    Result.failure(:validation_failed, e.message)
  rescue ExternalServiceError => e
    Result.failure(:external_service_failed, e.message)
  rescue StandardError => e
    notify_error_tracking(e)
    Result.failure(:internal_error, "An unexpected error occurred")
  end
end
```

## Testing Strategy

### 1. Test Pyramid Implementation

#### Unit Tests (70% of test suite)
```ruby
# spec/models/work_spec.rb
RSpec.describe Work, type: :model do
  describe 'validations' do
    it 'requires customer association' do
      work = build(:work, customer: nil)
      expect(work).not_to be_valid
      expect(work.errors[:customer]).to include("must exist")
    end
  end

  describe 'state transitions' do
    it 'transitions from draft to active when approved' do
      work = create(:work, :draft)
      work.approve!
      expect(work).to be_active
    end
  end

  describe 'business rules' do
    it 'calculates total fees correctly for success-based honorary' do
      work = create(:work, :with_success_honorary)
      expect(work.calculate_total_fees(10000)).to eq(3000) # 30% of 10000
    end
  end
end
```

#### Integration Tests (20% of test suite)
```ruby
# spec/services/document_generation_service_spec.rb
RSpec.describe DocumentGenerationService do
  describe '#call' do
    let(:work) { create(:work, :with_customer) }
    let(:service) { described_class.new(work, 'power_of_attorney') }

    it 'generates document successfully' do
      expect { service.call }.to change(Document, :count).by(1)
    end

    it 'handles template not found error' do
      allow(service).to receive(:template_exists?).and_return(false)
      result = service.call
      expect(result).to be_failure
      expect(result.error).to eq(:template_not_found)
    end
  end
end
```

#### End-to-End Tests (10% of test suite)
```ruby
# spec/features/document_workflow_spec.rb
RSpec.describe 'Document Workflow', type: :feature do
  scenario 'Lawyer creates work and generates documents' do
    lawyer = login_as_lawyer
    customer = create(:customer, admin: lawyer)

    visit new_work_path
    fill_in_work_details(customer)
    click_button 'Create Work'

    expect(page).to have_content('Work created successfully')
    expect(Document.count).to eq(1) # Auto-generated power of attorney
    expect(page).to have_link('Download Power of Attorney')
  end
end
```

### 2. Test Data Management
```ruby
# spec/factories/works.rb
FactoryBot.define do
  factory :work do
    association :customer
    association :admin
    title { Faker::Lorem.sentence }
    description { Faker::Lorem.paragraph }
    status { :draft }

    trait :with_honorary do
      association :honorary, :fixed_rate
    end

    trait :tax_case do
      case_type { 'tributario_pis_cofins' }
      association :admin, :counter
    end
  end
end
```

### 3. Test Coverage Requirements
- **Models**: 95% line coverage
- **Services**: 90% line coverage
- **Controllers**: 85% line coverage
- **Integration**: 80% path coverage

### 4. Performance Testing
```ruby
# spec/performance/document_generation_spec.rb
RSpec.describe 'Document Generation Performance' do
  it 'generates documents within acceptable time limits' do
    work = create(:work)

    expect {
      DocumentGenerationService.new(work, 'contract').call
    }.to perform_under(2.seconds)
  end

  it 'handles bulk document generation efficiently' do
    works = create_list(:work, 100)

    expect {
      BulkDocumentGenerationService.new(works).call
    }.to perform_under(30.seconds)
  end
end
```

## Validation Framework

### 1. Model-Level Validations
```ruby
class Customer < ApplicationRecord
  # Brazilian-specific validations
  validates :cpf_cnpj, presence: true,
                       format: { with: CPF_CNPJ_REGEX },
                       uniqueness: { scope: :admin_id }

  validates :email, presence: true,
                    format: { with: URI::MailTo::EMAIL_REGEXP },
                    uniqueness: { case_sensitive: false }

  # Business rule validations
  validate :customer_limit_per_lawyer
  validate :active_status_requirements

  private

  def customer_limit_per_lawyer
    return unless admin&.trainee?

    if admin.customers.active.count >= 50
      errors.add(:admin, 'Trainees cannot manage more than 50 customers')
    end
  end
end
```

### 2. Service-Level Validations
```ruby
class WorkCreationService
  include ActiveModel::Validations

  attr_accessor :customer, :admin, :work_params

  validates :customer, presence: true
  validates :admin, presence: true
  validate :admin_can_create_work_for_customer
  validate :work_type_allowed_for_admin_role

  def call
    return failure_result unless valid?

    Work.transaction do
      create_work
      generate_initial_documents
      notify_stakeholders
    end
  rescue StandardError => e
    failure_result(e.message)
  end

  private

  def admin_can_create_work_for_customer
    unless admin.can_manage?(customer)
      errors.add(:admin, 'Cannot create work for this customer')
    end
  end
end
```

### 3. Input Sanitization
```ruby
module InputSanitizer
  extend ActiveSupport::Concern

  included do
    before_save :sanitize_text_fields
  end

  private

  def sanitize_text_fields
    self.class.text_attributes.each do |attr|
      value = send(attr)
      next unless value.is_a?(String)

      send("#{attr}=", sanitize_legal_text(value))
    end
  end

  def sanitize_legal_text(text)
    # Remove potentially dangerous content while preserving legal formatting
    ActionController::Base.helpers.sanitize(
      text,
      tags: %w[p br strong em u],
      attributes: []
    )
  end
end
```

### 4. API Input Validation
```ruby
class WorksController < ApplicationController
  def create
    @work = WorkCreationService.new(work_creation_params)

    if @work.call.success?
      render json: { work: @work.result }, status: :created
    else
      render json: { errors: @work.errors }, status: :unprocessable_entity
    end
  end

  private

  def work_creation_params
    params.require(:work).permit(:title, :description, :customer_id, :case_type)
          .merge(admin: current_admin)
  end
end
```

## Bug Prevention & Resolution

### 1. Static Code Analysis
```ruby
# .rubocop.yml
AllCops:
  TargetRubyVersion: 3.0
  NewCops: enable
  Exclude:
    - 'db/schema.rb'
    - 'bin/**/*'

# Custom rules for legal domain
Metrics/MethodLength:
  Max: 15
  Exclude:
    - 'app/services/document_generation/**/*' # Complex legal logic allowed

Layout/LineLength:
  Max: 120

Style/Documentation:
  Enabled: true # Mandatory for legal compliance
```

### 2. Pre-commit Hooks
```bash
#!/bin/sh
# .git/hooks/pre-commit

# Run security audit
bundle exec bundle-audit check --update

# Run code quality checks
bundle exec rubocop

# Run critical tests
bundle exec rspec spec/models/ spec/services/

# Check for sensitive data
git diff --cached --name-only | xargs grep -l "password\|secret\|key" && {
  echo "Potential sensitive data found"
  exit 1
}
```

### 3. Error Monitoring & Alerting
```ruby
class ApplicationController < ActionController::API
  rescue_from StandardError, with: :handle_unexpected_error
  rescue_from ActiveRecord::RecordNotFound, with: :handle_not_found
  rescue_from Pundit::NotAuthorizedError, with: :handle_unauthorized

  private

  def handle_unexpected_error(exception)
    # Log error with context
    ErrorTracker.capture_exception(exception, {
      user_id: current_user&.id,
      request_id: request.uuid,
      params: sanitized_params
    })

    # Alert for critical errors
    if critical_error?(exception)
      AlertingService.notify_on_call_engineer(exception)
    end

    render json: { error: 'Internal server error' }, status: 500
  end

  def critical_error?(exception)
    exception.is_a?(DocumentGenerationError) ||
    exception.is_a?(PaymentProcessingError) ||
    exception.is_a?(DataCorruptionError)
  end
end
```

### 4. Database Migration Safety
```ruby
class AddIndexToCustomersEmail < ActiveRecord::Migration[7.0]
  disable_ddl_transaction! # Required for concurrent index creation

  def up
    # Create index concurrently to avoid locking
    add_index :customers, :email, algorithm: :concurrently

    # Add constraint after index is created
    add_foreign_key :customers, :admins, validate: false
    validate_foreign_key :customers, :admins
  end

  def down
    remove_foreign_key :customers, :admins
    remove_index :customers, :email
  end
end
```

### 5. Monitoring & Health Checks
```ruby
class HealthChecksController < ApplicationController
  def show
    checks = {
      database: database_healthy?,
      redis: redis_healthy?,
      s3: s3_healthy?,
      zapsign: zapsign_healthy?,
      document_generation: document_generation_healthy?
    }

    status = checks.values.all? ? :ok : :service_unavailable

    render json: {
      status: status,
      checks: checks,
      timestamp: Time.current
    }, status: status
  end

  private

  def database_healthy?
    ActiveRecord::Base.connection.execute('SELECT 1')
    true
  rescue StandardError
    false
  end

  def document_generation_healthy?
    # Test document generation with dummy data
    service = DocumentGenerationService.new(
      build(:work),
      'test_template'
    )
    service.test_mode = true
    service.call.success?
  rescue StandardError
    false
  end
end
```

### 6. Bug Triage Process

#### Severity Levels
- **P0 (Critical)**: System down, data loss, security breach
- **P1 (High)**: Core functionality broken, customer-facing errors
- **P2 (Medium)**: Feature partially broken, workaround available
- **P3 (Low)**: Minor issues, cosmetic problems

#### Resolution Workflow
```ruby
class BugReport
  include AASM

  aasm column: :status do
    state :reported, initial: true
    state :triaged
    state :assigned
    state :in_progress
    state :resolved
    state :verified
    state :closed

    event :triage do
      transitions from: :reported, to: :triaged
      after do
        assign_priority
        notify_relevant_team
      end
    end

    event :assign do
      transitions from: :triaged, to: :assigned
      after do
        create_development_task
        set_deadline_based_on_priority
      end
    end
  end
end
```

### 7. Post-Incident Review Process
```markdown
## Incident Report Template

### Incident Summary
- **Incident ID**: INC-2024-001
- **Date/Time**: 2024-01-15 14:30 UTC
- **Duration**: 45 minutes
- **Severity**: P1
- **Services Affected**: Document Generation, Customer Portal

### Root Cause Analysis
1. **Immediate Cause**: AWS S3 bucket policy misconfiguration
2. **Contributing Factors**:
   - Inadequate testing of policy changes
   - Missing monitoring for S3 access errors
3. **Root Cause**: Deployment process lacks infrastructure validation

### Resolution Steps
1. Reverted S3 bucket policy to previous version
2. Validated document access functionality
3. Notified affected customers

### Prevention Measures
- [ ] Add S3 access validation to deployment pipeline
- [ ] Implement monitoring for document generation errors
- [ ] Create runbook for S3-related incidents
- [ ] Schedule infrastructure review meeting
```

---

*This comprehensive business rules model serves as the authoritative guide for ProcStudio development, ensuring legal compliance, system reliability, and maintainable code architecture.*

**Last Updated**:
**Version**: 2.0
**Next Review**: March 28, 2025
