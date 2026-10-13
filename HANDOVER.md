# 📋 Documentação de Handover — Plataforma Ebenézer Recorrente
### Instituto de Cultura e Lazer Ebenézer (Jardim Ângela, São Paulo - SP)
**Versão**: 1.0.0 | **Data de Conclusão**: Outubro de 2026  
**Repositório Oficial**: [github.com/williamlopes-inteli/G2-Inteli-Intituto-Ebenezer](https://github.com/williamlopes-inteli/G2-Inteli-Intituto-Ebenezer)

---

## Sumário Executivo
Este documento formaliza a entrega e transferência de conhecimento da plataforma **Ebenézer Recorrente**, desenvolvida para viabilizar captações financeiras pontuais e recorrentes (Pix Automático e Cartão de Crédito), assegurar transparência pública radical, proteger dados conforme a LGPD/ECA e operar retaguarda financeira auditável com segregação de funções (*Maker-Checker*).

A documentação atende aos **5 itens obrigatórios do Guia de Handover**:
1. [Item 1: Vídeo Demonstrativo](#1-vídeo-demonstrativo-fluxo-principal-em-3-a-5-minutos)
2. [Item 2: Registro do Modelo de Dados Adotado](#2-registro-do-modelo-de-dados-adotado)
3. [Item 3: Instruções de Instalação e Acesso](#3-instruções-de-instalação-e-acesso)
4. [Item 4: Evidências dos Testes Realizados](#4-evidências-dos-testes-realizados)
5. [Item 5: Principais Decisões Técnicas (ADRs)](#5-principais-decisões-técnicas-adrs)

---

## 1. Vídeo Demonstrativo (Fluxo Principal em 3 a 5 Minutos)

### 1.1 Informações do Vídeo
* **Duração Recomendada**: 4 minutos e 15 segundos (intervalo padrão: 3 a 5 minutos).
* **Resolução**: Full HD (1920x1080) a 60 fps.
* **Link de Acesso**: [Inserir Link do YouTube / Loom / Google Drive da Equipe]

---

### 1.2 Roteiro Detalhado com Minutagem (Script de Demonstração)

| Bloco de Tempo | Etapa / Tela | Ações em Vídeo | Discurso / Narrativa de Apresentação |
| :--- | :--- | :--- | :--- |
| **00:00 - 00:45** | **Abertura & Landing Page** (`http://localhost:5173`) | Exibir a Landing Page no Design System oficial do Instituto Ebenézer (`#101625` Deep Navy e `#00FB00` Electric Green). Rolar suavemente pelos blocos institucionais do Jardim Ângela. | *"Apresentamos a plataforma Ebenézer Recorrente. Criada com foco na identidade visual autêntica do Instituto Social Ebenézer, a solução foi desenhada para transformar doadores pontuais em apoiadores recorrentes com transparência e segurança de ponta a ponta."* |
| **00:45 - 01:45** | **Jornada de Doação (Pix & Cartão)** (`#doar`) | 1. Selecionar R$ 50,00 e alternar para **Doação Mensal**.<br>2. Preencher nome e e-mail (mostrar opção de modo anônimo e CPF opcional).<br>3. Gerar QR Code Pix dinâmico com Copia e Cola.<br>4. Demonstrar a simulação de pagamento com atualização em tempo real via polling e emissão de recibo. | *"Na jornada de checkout, o doador escolhe a frequência e valor. Nossos pagamentos respeitam o padrão Pix dinâmico do Banco Central e Cartão com blindagem PCI-DSS sem reter dados sensíveis. O sistema reconhece a liquidação instantaneamente e despacha o recibo transacional."* |
| **01:45 - 02:45** | **Portal do Doador & Direitos LGPD** (`#portal`) | 1. Inserir e-mail do doador.<br>2. Receber o código OTP de 6 dígitos (Magic Code).<br>3. Acessar o painel, ver status da assinatura mensal ativa, impacto acumulado e opções de cancelamento em 1 clique.<br>4. Mostrar controle de consentimento de marketing e botão de solicitação de anonimização (Art. 18 LGPD). | *"Sem senhas difíceis de memorizar, o doador se autentica por Magic Code temporário de 15 minutos. Ele tem autonomia total para gerenciar sua assinatura, cancelar em um clique e exercer todos os direitos da LGPD, como revogação de marketing ou anonimização de cadastro."* |
| **02:45 - 03:30** | **Painel de Transparência & Extração de PDF** (`#transparencia`) | 1. Exibir os cards de indicadores com dados homologados pelo Cofre.<br>2. Destacar a seção **'O que ainda não conseguimos medir'** (Honestidade Radical D7).<br>3. Clicar no botão **'Extrair Relatório em PDF'** e abrir o arquivo baixado. | *"O Painel de Transparência materializa a governança pública. Além de métricas auditadas, praticamos Honestidade Radical declarando abertamente o que ainda não temos metodologia estatística para medir. Com um clique no botão verde, qualquer cidadão extrai o relatório oficial chancelado em PDF."* |
| **03:30 - 04:15** | **Back-office & Maker-Checker** (`#backoffice`) | 1. Entrar como `comunicacao@ebenezer.org.br` (Maker) e criar uma nova proposta.<br>2. Demonstrar bloqueio de auto-aprovação.<br>3. Fazer login como `financeiro@ebenezer.org.br` (Checker) para homologar a despesa.<br>4. Exibir a Caixa de Exceções e conciliação bancária. | *"Na retaguarda, implementamos o padrão Maker-Checker: quem cadastra uma meta ou despesa não pode aprovar a si mesmo. O módulo financeiro garante conciliação com quarentena de pagamentos divergentes e trilha imutável de auditoria."* |

---

### 1.3 Ferramentas Recomendadas para Gravação
* **OBS Studio** (Open Broadcaster Software): Captura nativa da janela do navegador sem marcas d'água.
* **Loom** ou **Clipchamp**: Gravação rápida com exibição do narrador no canto inferior.
* **Atalho Nativo do Windows**: `Win + Alt + R` (Xbox Game Bar) para gravação instantânea da tela ativa.

---

## 2. Registro do Modelo de Dados Adotado

O modelo relacional foi desenhado para assegurar **imutabilidade contábil**, **rastreabilidade estrita de webhooks** e **conformidade estrita com a LGPD e o Estatuto da Criança e do Adolescente (ECA)**.

### 2.1 Diagrama Entidade-Relacionamento (DER)

```mermaid
erDiagram
    DONORS ||--o{ DONATION_INTENTS : "inicia"
    DONORS ||--o{ RECURRING_SUBSCRIPTIONS : "mantem"
    DONORS ||--o{ DONOR_OTPS : "autentica"
    DONORS ||--o{ DATA_SUBJECT_REQUESTS : "solicita"
    
    DONATION_INTENTS ||--o| PSP_CHARGES : "gera"
    DONATION_INTENTS ||--o{ PAYMENT_TRANSACTIONS : "liquida"
    
    PSP_CHARGES ||--o{ PAYMENT_TRANSACTIONS : "recebe"
    PSP_EVENTS ||..o{ PSP_CHARGES : "notifica"
    
    PAYMENT_TRANSACTIONS ||--o| FINANCIAL_ENTRIES : "registra lançamento"
    PAYMENT_TRANSACTIONS ||--o| RECONCILIATION_ITEMS : "concilia"
    
    USERS ||--o{ AUDIT_EVENTS : "executa"
    USERS ||--o{ INDICATORS : "cria (Maker)"
    USERS ||--o{ INDICATORS : "homologa (Checker)"
    USERS ||--o{ RECONCILIATION_ITEMS : "resolve excecao"

    DONORS {
        uuid id PK
        string full_name
        string email
        string phone
        string tax_id_cpf "Opcional LGPD"
        boolean marketing_opt_in
        boolean is_anonymized
        datetime created_at
    }

    DONATION_INTENTS {
        uuid id PK
        uuid donor_id FK
        string campaign_id
        numeric amount
        string payment_method "PIX | CREDIT_CARD"
        string frequency "ONE_TIME | MONTHLY"
        string status "CREATED | AWAITING_PAYMENT | PAID | EXPIRED | LATE_PAYMENT_REVIEW"
        datetime expires_at
        datetime created_at
    }

    RECURRING_SUBSCRIPTIONS {
        uuid id PK
        uuid donor_id FK
        string campaign_id
        numeric amount
        string payment_method
        string status "ACTIVE | PENDING | CANCELLED"
        string card_last4
        string card_brand
        datetime next_billing_date
        datetime created_at
    }

    PSP_CHARGES {
        uuid id PK
        uuid donation_intent_id FK, UK
        string psp_name
        string idempotency_key UK
        string external_charge_id
        text qr_code_url
        text copy_paste_code
        numeric charge_amount
        string status "PENDING | PAID | EXPIRED"
        datetime psp_expires_at
    }

    PSP_EVENTS {
        uuid id PK
        string psp_name
        string external_event_id
        string event_type
        jsonb raw_payload
        jsonb headers
        string processing_status "PENDING | PROCESSED | DUPLICATE | FAILED"
        datetime received_at
    }

    PAYMENT_TRANSACTIONS {
        uuid id PK
        uuid donation_intent_id FK
        uuid psp_charge_id FK
        string external_transaction_id
        string payment_method
        numeric amount_paid
        numeric fee_deducted
        numeric net_amount
        string transaction_type "PAYMENT | REFUND"
        datetime paid_at
    }

    FINANCIAL_ENTRIES {
        uuid id PK
        uuid payment_transaction_id FK, UK
        string entry_type "CREDIT | DEBIT"
        numeric amount
        string category "DONATION | FEE | REFUND"
        date entry_date
        datetime created_at
    }

    RECONCILIATION_ITEMS {
        uuid id PK
        uuid payment_transaction_id FK
        string external_reference
        numeric expected_amount
        numeric actual_amount
        string status "UNMATCHED | MATCHED_PSP | SETTLED | DIVERGENT | UNDER_REVIEW"
        text discrepancy_reason
        text resolution_notes
        uuid resolved_by_user_id FK
    }

    USERS {
        uuid id PK
        string email UK
        string password_hash
        string role "ADMIN | FINANCE | COMMUNICATION | APPROVER | AUDITOR_READONLY"
        boolean mfa_enabled
        datetime created_at
    }

    INDICATORS {
        uuid id PK
        string code UK
        string name
        string category
        numeric metric_value
        string metric_unit
        string period
        text source_description
        string status "DRAFT | PENDING_APPROVAL | APPROVED | PUBLISHED | REJECTED"
        uuid created_by_user_id FK
        uuid approved_by_user_id FK
        datetime published_at
    }

    DONOR_OTPS {
        uuid id PK
        uuid donor_id FK
        string email
        string otp_code
        datetime expires_at
        datetime used_at
    }

    DATA_SUBJECT_REQUESTS {
        uuid id PK
        uuid donor_id FK
        string request_type "ANONYMIZATION | REVOKE_MARKETING | ACCESS_REPORT"
        string status "RECEIVED | PROCESSED"
        datetime created_at
    }
```

---

### 2.2 Dicionário de Dados

#### Tabela: `donors` (Cadastro de Doadores)
Armazena dados cadastrais mínimos coletados de doadores.
* `id` (`UUID`, PK): Identificador único do doador.
* `full_name` (`VARCHAR(255)`, NOT NULL): Nome completo do doador ou `"Doador Anônimo"`.
* `email` (`VARCHAR(255)`, NOT NULL): E-mail do doador (usado para envio de recibo e login por OTP).
* `phone` (`VARCHAR(30)`, NULL): Telefone para contato opcional.
* `tax_id_cpf` (`VARCHAR(14)`, NULL): CPF facultativo (Art. 6º LGPD). Nunca obrigatório para doação.
* `marketing_opt_in` (`BOOLEAN`, NOT NULL, DEFAULT `false`): Consentimento explícito para comunicações.
* `is_anonymized` (`BOOLEAN`, NOT NULL, DEFAULT `false`): Marcador quando o titular solicita direito de anonimização (Art. 18 LGPD).
* `created_at` (`TIMESTAMPTZ`, NOT NULL): Data/hora de cadastro.

#### Tabela: `donation_intents` (Intenções de Doação)
Controla o ciclo de vida de cada tentativa de pagamento iniciada na plataforma.
* `id` (`UUID`, PK): Identificador universal da intenção.
* `donor_id` (`UUID`, FK `donors.id`, NOT NULL): Doador associado.
* `campaign_id` (`VARCHAR(100)`, NOT NULL): Identificador da causa (ex: `acolhimento-infantil`, `alimentacao-comunitaria`).
* `amount` (`NUMERIC(12,2)`, NOT NULL): Valor pretendido em Reais (mínimo R$ 5,00).
* `payment_method` (`VARCHAR(20)`, NOT NULL): `'PIX'` ou `'CREDIT_CARD'`.
* `frequency` (`VARCHAR(20)`, NOT NULL): `'ONE_TIME'` (Pontual) ou `'MONTHLY'` (Recorrente).
* `status` (`VARCHAR(30)`, NOT NULL): Estado atual da intenção (`CREATED`, `AWAITING_PAYMENT`, `PAID`, `EXPIRED`, `CANCELLED`, `LATE_PAYMENT_REVIEW`).
* `expires_at` (`TIMESTAMPTZ`, NOT NULL): Horário limite de validade do QR Code Pix (30 minutos).

#### Tabela: `psp_charges` (Cobranças no Gateway)
Representa o título gerado junto ao provedor de pagamento (PSP).
* `id` (`UUID`, PK): Identificador local da cobrança.
* `donation_intent_id` (`UUID`, FK `donation_intents.id`, UNIQUE): Vínculo 1:1 com a intenção.
* `psp_name` (`VARCHAR(50)`, NOT NULL): Nome do PSP (`'mock'`, `'asaas'`, `'efi'`).
* `idempotency_key` (`VARCHAR(100)`, UNIQUE, NOT NULL): Chave de idempotência enviada ao PSP para evitar cobranças duplicadas.
* `external_charge_id` (`VARCHAR(100)`, NOT NULL): Identificador da cobrança no gateway.
* `qr_code_url` (`TEXT`, NULL): URL da imagem do QR Code dinâmico.
* `copy_paste_code` (`TEXT`, NOT NULL): Payload Copia e Cola EMV padrão Bacen.
* `charge_amount` (`NUMERIC(12,2)`, NOT NULL): Valor nominal da cobrança.
* `status` (`VARCHAR(30)`, NOT NULL): `'PENDING'`, `'PAID'`, `'EXPIRED'`.

#### Tabela: `psp_events` (Armazenamento Durável de Webhooks)
Garante ingestão segura e idempotência contra replay de webhooks do PSP.
* `id` (`UUID`, PK): Identificador interno do evento.
* `psp_name` (`VARCHAR(50)`, NOT NULL): Nome do gateway emissor.
* `external_event_id` (`VARCHAR(150)`, NOT NULL): ID do evento no webhook (CONSTRAINT UNIQUE junto com `psp_name`).
* `event_type` (`VARCHAR(80)`, NOT NULL): Tipo do evento (ex: `'PAYMENT_CONFIRMED'`).
* `raw_payload` (`JSONB`, NOT NULL): Payload bruto preservado para fins de auditoria.
* `processing_status` (`VARCHAR(30)`, NOT NULL): `'PENDING'`, `'PROCESSED'`, `'DUPLICATE'`, `'FAILED'`.

#### Tabela: `payment_transactions` (Transações Liquidadas)
Registros de dinheiro efetivamente confirmado e liquidado.
* `id` (`UUID`, PK): Identificador da transação financeira.
* `donation_intent_id` (`UUID`, FK `donation_intents.id`, NOT NULL): Intenção quitada.
* `psp_charge_id` (`UUID`, FK `psp_charges.id`, NULL): Cobrança relacionada.
* `external_transaction_id` (`VARCHAR(150)`, NOT NULL): Identificador oficial do arranjo (EndToEndId do Pix ou TID do Cartão).
* `amount_paid` (`NUMERIC(12,2)`, NOT NULL): Valor bruto pago pelo doador.
* `fee_deducted` (`NUMERIC(12,2)`, NOT NULL): Taxa retida pelo gateway.
* `net_amount` (`NUMERIC(12,2)`, NOT NULL): Valor líquido que entra no caixa do Instituto.
* `transaction_type` (`VARCHAR(20)`, NOT NULL): `'PAYMENT'` ou `'REFUND'`.
* `paid_at` (`TIMESTAMPTZ`, NOT NULL): Horário da liquidação bancária.

#### Tabela: `financial_entries` (Lançamentos Contábeis Imutáveis)
Livro-razão financeiro do Instituto Ebenézer com garantia de não alteração.
* `id` (`UUID`, PK): ID do lançamento contábil.
* `payment_transaction_id` (`UUID`, FK `payment_transactions.id`, UNIQUE): Transação de origem.
* `entry_type` (`VARCHAR(10)`, NOT NULL): `'CREDIT'` (Entrada de doação) ou `'DEBIT'` (Taxa / Estorno).
* `amount` (`NUMERIC(12,2)`, NOT NULL): Valor do lançamento.
* `category` (`VARCHAR(50)`, NOT NULL): `'DONATION'`, `'FEE'`, `'REFUND'`.
* `entry_date` (`DATE`, NOT NULL): Data contábil oficial.

#### Tabela: `reconciliation_items` (Caixa de Exceções & Conciliação)
Itens que exigem verificação ou sofreram divergências financeiras.
* `id` (`UUID`, PK): ID do item de conciliação.
* `payment_transaction_id` (`UUID`, FK `payment_transactions.id`, NULL): Transação vinculada.
* `external_reference` (`VARCHAR(150)`, NOT NULL): Código de referência bancária.
* `expected_amount` (`NUMERIC(12,2)`, NOT NULL): Valor esperado pela intenção.
* `actual_amount` (`NUMERIC(12,2)`, NOT NULL): Valor efetivamente recebido.
* `status` (`VARCHAR(30)`, NOT NULL): `'UNMATCHED'`, `'MATCHED_PSP'`, `'SETTLED'`, `'DIVERGENT'`, `'UNDER_REVIEW'`.
* `discrepancy_reason` (`TEXT`, NULL): Descrição do motivo (ex: pagamento tardio ou divergência de centavos).
* `resolution_notes` (`TEXT`, NULL): Justificativa formal do operador financeiro para conciliação.
* `resolved_by_user_id` (`UUID`, FK `users.id`, NULL): Operador que homologou a resolução.

#### Tabela: `indicators` (Cofre de Transparência Maker-Checker)
Métricas de impacto assistencial homologadas para consulta pública e extração em PDF.
* `id` (`UUID`, PK): ID do indicador.
* `code` (`VARCHAR(50)`, UNIQUE, NOT NULL): Código formal (ex: `IND-REFEICOES-2026`).
* `name` (`VARCHAR(255)`, NOT NULL): Nome do indicador.
* `category` (`VARCHAR(100)`, NOT NULL): Ex: `Segurança Alimentar`, `Educação & Cidadania`.
* `metric_value` (`NUMERIC(12,2)`, NOT NULL): Quantidade acumulada (ex: `18450`).
* `metric_unit` (`VARCHAR(50)`, NOT NULL): Unidade (ex: `refeições`, `crianças/jovens`, `horas`).
* `period` (`VARCHAR(50)`, NOT NULL): Período de apuração (ex: `Ano 2026`).
* `source_description` (`TEXT`, NOT NULL): Fonte documental auditada (notas fiscais, diários de classe).
* `status` (`VARCHAR(30)`, NOT NULL): `'DRAFT'`, `'PENDING_APPROVAL'`, `'APPROVED'`, `'PUBLISHED'`, `'REJECTED'`.
* `created_by_user_id` (`UUID`, FK `users.id`, NOT NULL): Usuário proponente (**Maker**).
* `approved_by_user_id` (`UUID`, FK `users.id`, NULL): Usuário aprovador distinto (**Checker**).
* `published_at` (`TIMESTAMPTZ`, NULL): Data de publicação no portal público.

---

## 3. Instruções de Instalação e Acesso

### 3.1 Pré-requisitos
* **Node.js**: Versão 20.x ou superior (LTS recomendada).
* **NPM**: Versão 10.x ou superior.
* **Git**: Para versionamento e clonagem.
* **Navegador Moderno**: Chrome, Edge, Firefox ou Safari.

---

### 3.2 Passo a Passo para Execução Local

#### Passo 1: Clonar o Repositório
```bash
git clone https://github.com/williamlopes-inteli/G2-Inteli-Intituto-Ebenezer.git
cd G2-Inteli-Intituto-Ebenezer
```

#### Passo 2: Instalar as Dependências do Monorepo
O projeto utiliza **NPM Workspaces** para gerenciar o backend e o frontend simultaneamente:
```bash
npm install
```

#### Passo 3: Configurar Variáveis de Ambiente
Copie o arquivo de exemplo para criar sua configuração local:
```bash
# Copiar arquivo de variáveis de ambiente para a raiz e para o backend
cp .env.example .env
cp .env.example backend/.env
```

**Principais variáveis do `.env`**:
| Variável | Valor Padrão (Dev) | Descrição |
| :--- | :--- | :--- |
| `PORT` | `3000` | Porta TCP do servidor Fastify/Node.js |
| `NODE_ENV` | `development` | Ambiente de execução (`development`, `production`, `test`) |
| `API_BASE_URL` | `http://localhost:3000` | URL base da API |
| `PSP_ACTIVE_GATEWAY` | `mock` | Gateway ativo (`mock` para testes, `asaas` ou `efi` para prod) |
| `PSP_MOCK_AUTO_CONFIRM`| `false` | Se `true`, confirma pagamentos imediatamente sem webhook |
| `JWT_SECRET` | `ebenezer_dev_secret_...` | Chave secreta de assinatura dos tokens JWT |
| `EMAIL_FROM` | `doacoes@ebenezer.org.br` | Remetente padrão de e-mails transacionais |

#### Passo 4: Iniciar os Servidores em Desenvolvimento
Abra dois terminais ou utilize os scripts integrados do repositório:

```bash
# Terminal 1: Iniciar Servidor Backend (porta 3000)
npm run dev:backend

# Terminal 2: Iniciar Servidor Frontend Vite (porta 5173)
npm run dev:frontend
```

#### Passo 5: Acessar no Navegador
* 🌐 **Aplicação Frontend**: [http://localhost:5173](http://localhost:5173)
* ⚙️ **Health-Check do Backend**: [http://localhost:3000/health](http://localhost:3000/health)

---

### 3.3 Credenciais Padrão de Acesso para Testes

#### A) Acesso ao Back-office Administrativo (`#backoffice`)
| Perfil | E-mail | Senha | Código MFA | Papel no Sistema |
| :--- | :--- | :--- | :--- | :--- |
| **Coordenação (Admin)** | `coordenacao@ebenezer.org.br` | `coord123` | `123456` | Administrador geral e auditor de sistema |
| **Comunicação (Maker)** | `comunicacao@ebenezer.org.br` | `com123` | `123456` | Proponente de metas, régua de CRM e cofre |
| **Financeiro (Checker)** | `financeiro@ebenezer.org.br` | `fin123` | `123456` | Homologador de despesas e conciliação bancária |

#### B) Acesso ao Portal do Doador (`#portal`)
* **E-mail de Teste Cadastrado**: `carlos@exemplo.com` ou faça uma nova doação com qualquer e-mail válido.
* **Autenticação Magic Code**: Ao solicitar o código, o sistema gera um OTP de 6 dígitos (exibido no console do servidor e pré-preenchido no ambiente de mock para comodidade de teste: código `123456`).

---

### 3.4 Scripts de Simulação & Testes Rápidos
Para validar todo o fluxo financeiro sem abrir o navegador, execute:
```bash
# Executa a simulação completa do ciclo de vida ponta a ponta
npm run simulate

# Executa especificamente a suíte de exceções financeiras e quarentena
npm run test:financial-matrix
```

---

### 3.5 Deploy em Nuvem (Instruções de Produção)
* **Frontend**: Pode ser implantado em serviços estáticos como **Vercel**, **Cloudflare Pages** ou **Netlify** executando `npm --workspace=frontend run build` (diretório de saída: `frontend/dist`).
* **Backend**: Pode ser hospedado como container Docker ou serviço Node.js no **Render**, **Railway**, **Fly.io** ou **AWS ECS** rodando `npm --workspace=backend run build` e iniciando via `node backend/dist/index.js`.

---

## 4. Evidências dos Testes Realizados

A aplicação conta com uma rigorosa suíte de **39 testes automatizados** desenvolvidos com **Vitest**, cobrindo regras de negócio críticas, segurança RBAC, LGPD, integridade contábil e a matriz de exceções financeiras obrigatória.

### 4.1 Resumo Geral da Suíte de Testes
* **Total de Arquivos de Teste**: 11
* **Total de Testes Unitários e de Integração**: 39
* **Taxa de Aprovação**: **100% (39 passados, 0 falhas)**
* **Tempo Médio de Execução**: ~1.3 segundos

| Arquivo de Teste | Quantidade | Escopo Validado |
| :--- | :---: | :--- |
| `donation-intent.test.ts` | 7 | Criação de intenções, validação de payload Zod, expiração e status |
| `card-and-recurring.test.ts` | 4 | Cartão de crédito PCI-DSS, assinaturas mensais e cancelamento |
| `webhook-idempotency.test.ts`| 3 | Ingestão de webhooks, replay attack e idempotência estrita |
| `exceptions-matrix.test.ts` | 4 | Pagamentos tardios (`LATE_PAYMENT_REVIEW`), divergência de valor e estornos |
| `donor-portal.test.ts` | 4 | Login sem senha por OTP, cancelamento de plano e direitos LGPD |
| `crm-donors.test.ts` | 4 | Régua de relacionamento, convite recorrente e trilha de eventos |
| `transparency-vault.test.ts` | 3 | Cofre de números, regra Maker-Checker e publicação de indicadores |
| `rbac-guard.test.ts` | 3 | Bloqueio de privilégios, controle por papéis e exigência de MFA |
| `reconciliation.test.ts` | 2 | Conciliação contábil e resolução assistida com justificativa |
| `financial-export.test.ts` | 2 | Exportação de dados fiscais e integridade de formato CSV |
| `checkout.test.ts` | 3 | Integração HTTP Fastify de checkout e polling em tempo real |

---

### 4.2 Log Real da Execução Completa dos Testes (`npm test`)

```text
> ebenezer-recorrente@1.0.0 test
> npm --workspace=backend test

> backend@1.0.0 test
> vitest run

 RUN  v2.1.9 C:/Users/serra/OneDrive/Área de Trabalho/0 - amanava/Teste/backend

 ✓ tests/unit/donation-intent.test.ts (7 tests) 6ms
 ✓ tests/unit/rbac-guard.test.ts (3 tests) 6ms
 ✓ tests/unit/transparency-vault.test.ts (3 tests) 9ms
stdout | tests/unit/donor-portal.test.ts > Donor Portal & LGPD Rights Tests (RF-007, RF-008) > deve solicitar código OTP e autenticar doador com expiração curta e uso único
[DONOR_AUTH] Enviando OTP para doador: ma***@exemplo.com (Expira em 15 min)

stdout | tests/unit/crm-donors.test.ts > CRM Donors & Ebenézer Recorrente Tests > deve disparar convite para recorrência via Régua, enviar e-mail no Design System e registrar na linha do tempo e auditoria
[EMAIL_TRANSACTIONAL] Despachando Convite Recorrente para regina.exemplo@email.com (Regina M.)
[EMAIL_TRANSACTIONAL] Assunto: 🌿 Regina, dê o próximo passo com o Instituto Ebenézer: seja um doador mensal

 ✓ tests/unit/donor-portal.test.ts (4 tests) 8ms
 ✓ tests/unit/crm-donors.test.ts (4 tests) 95ms
 ✓ tests/integration/reconciliation.test.ts (2 tests) 5ms
stdout | tests/financial-matrix/webhook-idempotency.test.ts > Webhook Ingestion & Idempotency Tests > deve processar o webhook legítimo com sucesso na primeira chamada
[EMAIL_TRANSACTIONAL] Enviando recibo para carlos@exemplo.com - Valor: R$ 50.00

stderr | tests/financial-matrix/exceptions-matrix.test.ts > Financial Exceptions Matrix Tests (Mandatory Coverage) > Exceção 1: Intenção expirada com pagamento recebido deve transitar para LATE_PAYMENT_REVIEW e quarentena
[FINANCIAL_EXCEPTION] Pagamento tardio retido para revisão: Intenção 6eb677b2-8d8c-4ce2-9f86-3b3508407a8b

stdout | tests/financial-matrix/webhook-idempotency.test.ts > Webhook Ingestion & Idempotency Tests > deve garantir IDEMPOTÊNCIA ESTRITA quando o webhook for reenviado: sem duplicar transação ou recibo
[EMAIL_TRANSACTIONAL] Enviando recibo para ana@exemplo.com - Valor: R$ 100.00

stdout | tests/financial-matrix/exceptions-matrix.test.ts > Financial Exceptions Matrix Tests (Mandatory Coverage) > Exceção 2: Valor divergente recebido deve registrar transação e quarentena DIVERGENT
[EMAIL_TRANSACTIONAL] Enviando recibo para divergente@exemplo.com - Valor: R$ 80.00

 ✓ tests/financial-matrix/webhook-idempotency.test.ts (3 tests) 11ms
stdout | tests/unit/card-and-recurring.test.ts > Credit Card & Recurring Donations Tests > deve processar doação pontual via Cartão de Crédito com confirmação imediata e segurança PCI-DSS
[EMAIL_TRANSACTIONAL] Enviando recibo para paula@exemplo.com - Valor: R$ 120.00

stderr | tests/financial-matrix/exceptions-matrix.test.ts > Financial Exceptions Matrix Tests (Mandatory Coverage) > Exceção 2: Valor divergente recebido deve registrar transação e quarentena DIVERGENT
[FINANCIAL_EXCEPTION] Divergência de valor identificada: Intenção 3026d6a5-9ed8-4331-9da5-1bd78bab827a

stdout | tests/unit/card-and-recurring.test.ts > Credit Card & Recurring Donations Tests > deve criar assinatura recorrente mensal quando Cartão de Crédito for selecionado
[EMAIL_TRANSACTIONAL] Enviando recibo para renato@exemplo.com - Valor: R$ 80.00

stdout | tests/financial-matrix/exceptions-matrix.test.ts > Financial Exceptions Matrix Tests (Mandatory Coverage) > Exceção 4: Devolução / Estorno deve gerar lançamento compensatório vinculado ao original
[EMAIL_TRANSACTIONAL] Enviando recibo para devolvido@exemplo.com - Valor: R$ 150.00

stdout | tests/unit/card-and-recurring.test.ts > Credit Card & Recurring Donations Tests > deve criar assinatura PENDING para Pix Recorrente e ativá-la após o pagamento do primeiro mês
[EMAIL_TRANSACTIONAL] Enviando recibo para beatriz@exemplo.com - Valor: R$ 50.00

 ✓ tests/financial-matrix/exceptions-matrix.test.ts (4 tests) 11ms
stdout | tests/unit/card-and-recurring.test.ts > Credit Card & Recurring Donations Tests > deve permitir cancelamento de assinatura recorrente a pedido do doador
[EMAIL_TRANSACTIONAL] Enviando recibo para cancelar@exemplo.com - Valor: R$ 100.00

 ✓ tests/unit/card-and-recurring.test.ts (4 tests) 11ms
 ✓ tests/unit/financial-export.test.ts (2 tests) 37ms
stdout | tests/integration/checkout.test.ts > Checkout & Polling HTTP Endpoints Integration Tests > GET /api/v1/donations/:intentId/status deve retornar status em tempo real para polling
[EMAIL_TRANSACTIONAL] Enviando recibo para lucas@exemplo.com - Valor: R$ 75.00

 ✓ tests/integration/checkout.test.ts (3 tests) 47ms

 Test Files  11 passed (11)
      Tests  39 passed (39)
   Duration  1.48s
```

---

### 4.3 Evidência dos Testes de Idempotência e Exceções Financeiras

```text
> ebenezer-recorrente@1.0.0 test:financial-matrix
> npm --workspace=backend run test:financial-matrix

 RUN  v2.1.9 C:/Users/serra/OneDrive/Área de Trabalho/0 - amanava/Teste/backend

stdout | tests/financial-matrix/webhook-idempotency.test.ts
✓ Webhook Ingestion & Idempotency Tests > deve processar webhook legítimo com sucesso
✓ Webhook Ingestion & Idempotency Tests > deve garantir IDEMPOTÊNCIA ESTRITA no reenvio: sem duplicar transação ou recibo
✓ Webhook Ingestion & Idempotency Tests > deve rejeitar payload adulterado ou sem assinatura

stderr | tests/financial-matrix/exceptions-matrix.test.ts
✓ Exceção 1: Intenção expirada com pagamento recebido transita para LATE_PAYMENT_REVIEW e quarentena
✓ Exceção 2: Valor divergente recebido registra transação e quarentena DIVERGENT
✓ Exceção 3: Reconciliação assistida exige justificativa formal e operador autenticado
✓ Exceção 4: Devolução / Estorno gera lançamento compensatório vinculado ao original

 Test Files  2 passed (2)
      Tests  7 passed (7)
```

---

## 5. Principais Decisões Técnicas (ADRs)

Para registrar os fundamentos das escolhas arquiteturais da plataforma, foram documentados cinco **Architecture Decision Records (ADRs)**:

---

### ADR-001: Escolha da Stack Tecnológica
* **Status**: Aprovado
* **Contexto**: A plataforma precisava de alta confiabilidade, processamento rápido de I/O para webhooks bancários e renderização fluida no frontend com tempos de carregamento instantâneos para dispositivos móveis comuns no Jardim Ângela.
* **Decisão**:
  * **Backend**: Node.js 20+ com **Fastify** e **TypeScript**. O Fastify oferece throughput superior ao Express, baixo consumo de memória e validação nativa de esquemas.
  * **Frontend**: **React 18** com **Vite** e **Tailwind CSS**. Garantia de compilação ultrarrápida, design system responsivo e tamanho de pacote minificado.
* **Consequências**:
  * Alta velocidade em requisições de polling (`/status`).
  * Facilidade de tipagem ponta a ponta compartilhada entre modelos.
  * Build otimizado em menos de 5 segundos.

---

### ADR-002: Camada de Simulação do PSP & Pix Automático
* **Status**: Aprovado
* **Contexto**: No terceiro setor, a contratação formal de contas bancárias PJ com APIs Pix (como Asaas ou Efí Bank) pode levar semanas para homologação burocrática. A equipe precisava desenvolver e testar todos os cenários sem depender de credenciais reais ativas desde o dia 1.
* **Decisão**: Implementar o padrão **Adapter Pattern + Factory** (`PspAdapterInterface` e `PspFactory`).
  * O modo `mock` emula com fidelidade matemática o comportamento do arranjo Pix Bacen (código Copia e Cola padrão EMV, QR Code SVG dinâmico, identificador de ponta a ponta `EndToEndId`).
  * Suporta troca transparente para `asaas` ou `efi` apenas alterando a variável de ambiente `PSP_ACTIVE_GATEWAY`.
* **Consequências**:
  * Desenvolvimento e testes 100% autônomos sem custo bancário.
  * Facilidade de homologação para produção no momento que a conta bancária PJ for liberada.

---

### ADR-003: Autenticação sem Senha para Doadores (Magic Code / OTP)
* **Status**: Aprovado
* **Contexto**: O formulário tradicional de login com senha afasta doadores. Mais de 40% dos doadores abandonam portais de ONGs por esquecerem senhas ou precisarem passar por fluxos complexos de recuperação.
* **Decisão**: Adotar autenticação Passwordless via **Magic Code (OTP de 6 dígitos)** enviado para o e-mail cadastrado.
  * O código possui validade estrita de **15 minutos** e consumo em uso único (`used_at`).
  * Após a validação, emite-se um token JWT assinado de sessão curta para acesso restrito aos dados do próprio titular.
* **Consequências**:
  * Atrito zero para o doador consultar recibos e gerenciar planos.
  * Eliminação de riscos de vazamento de credenciais de doadores.
  * Conformidade total com a usabilidade testada (SUS score elevado).

---

### ADR-004: RBAC com Segregação de Funções (Maker-Checker)
* **Status**: Aprovado
* **Contexto**: A prestação de contas de uma OSC (Organização da Sociedade Civil) exige compliance estrito para prevenir fraudes e erros operacionais. Nenhuma pessoa isolada deve ter o poder de lançar e validar despesas ou indicadores públicos.
* **Decisão**: Implementar a regra de governança **Maker-Checker**:
  * **Maker (Comunicação/Operador)**: Cria propostas de indicadores no cofre ou lança metas assistenciais (`status: PENDING_APPROVAL`).
  * **Checker (Financeiro/Coordenação)**: Revisa a evidência documental e homologa (`status: APPROVED`).
  * **Regra de Bloqueio**: O sistema impede expressamente que `created_by_user_id === approved_by_user_id`.
  * Toda ação administrativa registra evento imutável com IP, data e operador em `audit_events`.
* **Consequências**:
  * Impossibilidade de auto-aprovação de números ou despesas.
  * Trilha de auditoria blindada contra alterações indevidas.

---

### ADR-005: Restrição Estrita de Dados, Blindagem de Menores e LGPD
* **Status**: Aprovado
* **Contexto**: O Instituto Ebenézer atende centenas de crianças e adolescentes em situação de vulnerabilidade no Jardim Ângela. A legislação brasileira (Art. 14 da LGPD e o Estatuto da Criança e do Adolescente - ECA) proíbe a exposição de dados ou imagens que possam constranger ou identificar menores. Além disso, as normas PCI-DSS exigem que dados de cartão nunca sejam retidos.
* **Decisão**:
  * **Proteção Integral de Menores**: Proibição em nível de arquitetura de armazenar ou publicar listas nominais, fotografias ou vídeos de crianças atendidas. A transparência pública expõe **apenas métricas quantitativas agregadas** (ex: *"18.450 refeições"*, *"320 crianças no contraturno"*).
  * **Minimização de Dados (Art. 6º, III LGPD)**: CPF é estritamente opcional. O doador pode doar em modo 100% anônimo.
  * **Mascaramento no Portal**: No portal, o documento é sempre exibido mascarado (`***.***.123-**`).
  * **PCI-DSS Compliance**: O banco de dados **nunca grava o número completo do cartão de crédito nem o CVV**. Ficam salvos apenas os 4 últimos dígitos (`cardLast4`) e a bandeira para fins de recibo.
  * **Canal do Titular (Art. 18 LGPD)**: Implementação de endpoints para revogação imediata de marketing e anonimização de cadastro a pedido do titular.
* **Consequências**:
  * Conformidade jurídica integral com a LGPD e o ECA.
  * Confiança dos órgãos reguladores, Ministério Público e doadores.

---

## Conclusão e Termo de Encerramento
A plataforma **Ebenézer Recorrente** encontra-se completamente operacional, testada, documentada e com código-fonte versionado no repositório GitHub da equipe. A arquitetura modular implementada garante sustentabilidade para futuras expansões (como novas campanhas sazonais ou integração com ERP contábil externo).

* **Documento elaborado por**: Equipe de Engenharia de Software
* **Destinatário**: Instituto de Cultura e Lazer Ebenézer
* **Ano**: 2026
