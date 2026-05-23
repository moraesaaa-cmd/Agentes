# Mockups Textuais — Features Prioritárias

Wireframes em texto para as 5 features de maior ROI. Cada uma com fluxo, campos, regras de negócio e snippet de implementação.

---

## 1. Calculadora de Rescisão CLT

URL: `/calculadoras/rescisao-trabalhista`

### Layout (mobile-first)

```
┌─────────────────────────────────────────┐
│  AdvAqui  [diretório] [blog] [planos]  │
├─────────────────────────────────────────┤
│                                         │
│   📊 Calculadora de Rescisão CLT       │
│      Valor exato. Sem cadastro.        │
│                                         │
│   ┌───────────────────────────────┐    │
│   │ Data de admissão              │    │
│   │ [   /   /     ]               │    │
│   ├───────────────────────────────┤    │
│   │ Data de saída                 │    │
│   │ [   /   /     ]               │    │
│   ├───────────────────────────────┤    │
│   │ Motivo da saída               │    │
│   │ [ Demissão sem justa causa ▾ ]│    │
│   ├───────────────────────────────┤    │
│   │ Último salário                │    │
│   │ R$ [ 2.500,00 ]               │    │
│   ├───────────────────────────────┤    │
│   │ Aviso prévio                  │    │
│   │ ◉ Trabalhado  ○ Indenizado    │    │
│   ├───────────────────────────────┤    │
│   │ Férias vencidas?              │    │
│   │ ○ Sim  ◉ Não                  │    │
│   ├───────────────────────────────┤    │
│   │ Saldo aproximado de FGTS      │    │
│   │ R$ [ opcional ]               │    │
│   └───────────────────────────────┘    │
│                                         │
│   [  🧮 Calcular agora  ]              │
│                                         │
└─────────────────────────────────────────┘

         ↓ (após calcular)

┌─────────────────────────────────────────┐
│   ✅ Resultado                          │
│                                         │
│   Total líquido SEM FGTS                │
│   R$ 10.147,60                         │
│                                         │
│   Total líquido COM FGTS + multa 40%   │
│   R$ 18.420,80                         │
│                                         │
│   ▼ Ver memória de cálculo             │
│   ├─ Saldo de salário        R$ 1.250  │
│   ├─ Aviso prévio indeniz.   R$ 2.500  │
│   ├─ 13º proporcional        R$   208  │
│   ├─ Férias + 1/3            R$ 1.111  │
│   ├─ INSS (-)                R$  -275  │
│   ├─ IRRF (-)                R$     0  │
│   └─ FGTS + multa 40%        R$ 8.273  │
│                                         │
│   [ 📤 Enviar p/ WhatsApp ]            │
│   [ 📄 Baixar PDF ]                    │
│   [ ✉️  Receber por email ]             │
│                                         │
│   ───────────────────────────────────   │
│                                         │
│   💼 Quer validar com um advogado?     │
│   [ Ver advogados em São Paulo →]      │
│   (detectado por geoIP, sem cadastro)  │
│                                         │
└─────────────────────────────────────────┘
```

### Regras de negócio

- Cálculo client-side (JS) — zero latência, sem servidor.
- "Baixar PDF" e "Receber por email" exigem opt-in (LGPD double opt-in).
- Geolocalização opcional via API HTML5 ou IP (sem pedir permissão dura).
- Estado "calcular novamente" preserva inputs no localStorage.

### Conteúdo SEO ao redor (mín. 2.500 palavras abaixo da calc)

- H2: "Como funciona a calculadora"
- H2: "O que entra no cálculo da rescisão"
- H2: "Direitos por tipo de demissão" (tabela)
- H2: "Tabela INSS e IRRF 2026"
- H2: "Quando procurar um advogado trabalhista"
- H2: FAQ (10 perguntas) — schema FAQPage
- H2: "Casos reais" (3 mini-exemplos numéricos)

### Schemas

- WebApplication (the calculator)
- FAQPage
- BreadcrumbList
- HowTo (passo-a-passo de uso)

### KPIs específicos

- Sessões/mês na URL
- % usuários que clicam "calcular"
- % que clicam "ver advogado"
- Emails capturados via "receber por email"
- Compartilhamentos WhatsApp

---

## 2. "Pergunte a um Advogado" (Q&A Público)

URL: `/perguntas` (listagem) + `/perguntas/[slug]` (detalhe)

### Fluxo do leigo

```
1. /perguntas → vê barra "Faça sua pergunta" + ranking de mais visualizadas
2. Clica "Fazer pergunta" → modal
   ┌────────────────────────────────┐
   │ Sua dúvida em poucas palavras │
   │ [ ex: posso pedir demissão... ]│
   ├────────────────────────────────┤
   │ Área                          │
   │ [ Trabalhista ▾ ]             │
   ├────────────────────────────────┤
   │ Detalhes (opcional)           │
   │ [ texto livre, 500 chars max ]│
   ├────────────────────────────────┤
   │ Cidade                        │
   │ [ São Paulo - SP ]            │
   ├────────────────────────────────┤
   │ ✉️ Seu email (recebe avisos)   │
   │ [ ___________ ]               │
   └────────────────────────────────┘
   [ Publicar pergunta ]

3. Moderação automática (anti-spam, PII removal) → publicação
4. Notificação por email a TODOS advogados Premium da área + cidade
5. Pergunta vira URL: /perguntas/posso-pedir-demissao-em-ferias-2026-04812
```

### Fluxo do advogado Premium

```
- Recebe push/email "nova pergunta na sua área em SP"
- Clica → vê detalhe → responde no editor
- Limite: 3 respostas por pergunta (evita spam)
- Resposta exibida com nome, OAB, foto, link perfil
- Cliente recebe email "Dr. X respondeu sua pergunta"
- Botão "Quero falar com o Dr. X via WhatsApp"
```

### Regras anti-abuso e ética OAB

- Resposta **não pode** "garantir resultado".
- Resposta **não pode** ofertar honorários direto.
- Templates banidos via regex.
- Reviewer humano amostral (10%).
- Sistema de denúncia 1-clique.
- Disclaimer fixo: "Resposta orientativa, não substitui consulta."

### Por que gera SEO infinito

- 1.000 perguntas/mês = 12.000 URLs novas/ano.
- Long-tail: ranqueia para "posso pedir demissão estando em férias 2026" sem nenhuma campanha.
- Cada URL é uma página em escala — modelo Jusbrasil aplicado.

### Schemas obrigatórios

- **QAPage** (Schema.org/QAPage) — rich snippet específico de Q&A.
- **Question** + **Answer** com `upvoteCount`, `dateCreated`, `author`.

---

## 3. Lead Magnet — "Kit Demissão Sem Justa Causa"

### Estrutura da landing page

URL: `/kits/demissao-sem-justa-causa`

```
┌──────────────────────────────────────────┐
│  📥 Kit Demissão Sem Justa Causa         │
│      Tudo que você precisa em 1 download │
│                                          │
│  Você vai receber:                      │
│  ✅ Checklist de verbas (PDF, 4 págs)   │
│  ✅ Planilha calculadora (Excel/Sheets) │
│  ✅ Modelo notificação para empresa     │
│  ✅ Modelo recibo quitação parcial      │
│  ✅ Modelo declaração horas extras      │
│                                          │
│  [ Seu email ___________ ]              │
│  [ ✅ Concordo com a política LGPD ]    │
│  [   📩 Receber gratuitamente   ]       │
│                                          │
│  🔒 Sem spam. Cancele quando quiser.   │
│                                          │
│  ─────────────────────────────────────  │
│                                          │
│  Mais de 2.400 pessoas já baixaram      │
│  ⭐⭐⭐⭐⭐ 4.9/5 (312 avaliações)        │
│                                          │
│  "Recuperei R$ 8.400 que a empresa     │
│   não tinha pago" — Carlos, SP         │
│                                          │
└──────────────────────────────────────────┘
```

### Sequência de email (drip)

| # | Quando | Assunto | Conteúdo |
|---|---|---|---|
| 1 | Imediato | "Aqui está seu Kit Demissão" | Links download + dica #1 |
| 2 | D+3 | "5 erros caros após demissão" | Mini-guia + CTA artigo |
| 3 | D+7 | "Você sabe quanto vale sua rescisão?" | Link calculadora |
| 4 | D+14 | "Quer falar com advogado em [cidade]?" | Link diretório segmentado |
| 5 | D+30 | "Direito trabalhista da semana" | Início newsletter regular |

### Plataforma sugerida

**Brevo** ou **Mailerlite** (gratuitos até 1k contatos). Webhook para alimentar CRM próprio.

### Conformidade LGPD

- Double opt-in obrigatório.
- Checkbox não pré-marcado.
- Link de descadastro em todo email.
- DPO designado (a Advaqui já precisa ter um por receber dados de advogados).
- Política de privacidade linkada.

---

## 4. Perfil Expandido do Advogado (Premium)

URL: `/advogados/[uf]/[cidade]/[nome-slug]`

```
┌────────────────────────────────────────────┐
│  Dra. Ana Souza                  ⭐ 4.9   │
│  OAB/SP 123.456  ✅ verificada  (47 reviews)│
│                                            │
│  [Foto profissional]    📍 São Paulo - SP │
│                         💼 12 anos OAB    │
│                                            │
│  🟢 [ Falar no WhatsApp ]                 │
│  ☎️ [ Ligar agora ]                       │
│  📧 [ Enviar email ]                      │
│                                            │
│  Especialidades:                          │
│  [Trabalhista] [Família] [Consumidor]    │
│                                            │
│  Horário de atendimento:                  │
│  Seg-Sex 9h-18h · Sáb 9h-12h             │
│                                            │
├────────────────────────────────────────────┤
│  Sobre                                    │
│  Texto livre 500-1500 caracteres...      │
│                                            │
├────────────────────────────────────────────┤
│  Formação                                 │
│  • USP, Bacharel em Direito (2012)       │
│  • PUC-SP, Pós-graduação Trabalhista     │
│                                            │
├────────────────────────────────────────────┤
│  Áreas atendidas                          │
│  São Paulo capital + Guarulhos +          │
│  Osasco + 6 cidades próximas              │
│                                            │
├────────────────────────────────────────────┤
│  Artigos publicados (3)                  │
│  • Reforma trabalhista: o que mudou      │
│  • Como pedir rescisão indireta          │
│  • Banco de horas é abusivo?             │
│                                            │
├────────────────────────────────────────────┤
│  Avaliações de clientes (47)             │
│  ⭐⭐⭐⭐⭐ "Resolveu meu caso..."  - João │
│  ⭐⭐⭐⭐⭐ "Muito atenciosa..."     - Ana  │
│  [Ver todas as 47 avaliações]            │
│                                            │
├────────────────────────────────────────────┤
│  Localização                              │
│  [ Mapa Google Maps embedded ]            │
│                                            │
└────────────────────────────────────────────┘
```

### Schemas no perfil

- `LegalService` (com endereço, telefone, abertura)
- `Person` (advogado individual)
- `AggregateRating` (estrelas + n reviews)
- `Review` (cada review)
- `BreadcrumbList`

### Diferencial competitivo

Botão **WhatsApp** com mensagem pré-preenchida:
> "Olá Dra. Ana, vim pela AdvAqui. Tenho uma dúvida sobre [especialidade]."

Tracking via UTM no link `?utm_source=advaqui&utm_medium=whatsapp&utm_advogado=ana-souza`.

### Reviews — fluxo

```
1. Advogado registra contato como "fechado" no painel (sem auditoria, baseia confiança)
2. Sistema dispara email para o cliente 7 dias depois:
   "A Dra. Ana Souza atendeu você semana passada? Avalie em 30s →"
3. Cliente clica → modal de 5 estrelas + comentário opcional
4. Sistema valida (telefone/email diferente do advogado, 1 review por contato)
5. Publica
```

---

## 5. Conta Gratuita do Leigo

URL: `/minha-conta` (após login)

### Funcionalidades

```
┌─────────────────────────────────────┐
│  👤 Minha Conta                     │
│                                     │
│  🔖 Advogados favoritos (3)         │
│  📚 Artigos salvos (8)              │
│  🧮 Meus cálculos (2)               │
│  📬 Newsletters ativas (Trabalhista)│
│  🔔 Alertas de jurisprudência (2)   │
│  📥 Kits baixados (4)               │
│  ❓ Minhas perguntas no Q&A (1)     │
│                                     │
│  ⚙️ Configurações | Sair             │
└─────────────────────────────────────┘
```

### Onboarding

- Cadastro em 30 segundos: email + senha (ou Google OAuth).
- Wizard de 3 passos:
  1. "Em qual área você tem dúvida hoje?" → segmenta newsletter
  2. "Qual sua cidade?" → personaliza diretório
  3. "Quer alertas de jurisprudência?" → opt-in granular

### Loop de retorno

- Push web (notificação navegador) quando novo artigo da área.
- Email com peça da semana (decisão STJ explicada).
- Notificação "Dra. X respondeu sua pergunta".

### Por que importa para SEO

- Usuário logado tem sessões mais longas (sinal de qualidade).
- Engaged user → menor bounce rate → ranqueamento melhor.
- Email/push gera "tráfego direto" (sinal positivo no algoritmo).

---

## 6. Stack Técnica Sugerida (referência)

| Camada | Stack |
|---|---|
| Frontend | Next.js 15 (App Router) + React Server Components |
| Estilização | Tailwind + shadcn/ui |
| Backend API | Next.js API routes ou Node/Express dedicado |
| DB | PostgreSQL + Prisma |
| Search | Meilisearch ou Algolia (busca de advogados/jurisprudência) |
| Email | Brevo / Mailerlite + Postmark transacional |
| Auth | Auth.js (Google + email) |
| Storage | Cloudflare R2 ou S3 (PDFs dos kits) |
| Imagens OG | Vercel Edge OG ou Cloudinary |
| Analytics | Plausible + GA4 |
| Erro tracking | Sentry |
| Calcs client-side | Web Workers para cálculos complexos |
| Schema validation | Schema.org Validator + Search Console manual |
| CMS | Sanity / Strapi para artigos editoriais |

---

## 7. Roadmap de Construção (12 semanas)

| Sprint | Entregável |
|---|---|
| S1 | Schema markup + OG tags + datas/autoria em todo site |
| S2 | Lead magnet #1 ("Kit Demissão") + integração Brevo |
| S3 | Calculadora Rescisão (MVP client-side) + página SEO ao redor |
| S4 | Lead magnet #2-3 ("Kit Divórcio", "Kit INSS") |
| S5 | Conta gratuita do leigo (auth + wizard) |
| S6 | Calculadora Pensão Alimentícia |
| S7 | Perfil expandido de advogado + reviews (admin + flow) |
| S8 | Q&A público — schema + listagem + form de pergunta |
| S9 | Q&A — fluxo de resposta + moderação + notificações |
| S10 | Calculadora FGTS + página-pilar Trabalhista |
| S11 | Página-pilar Família + Consumidor |
| S12 | Newsletter automation + push web + métricas dashboard |
