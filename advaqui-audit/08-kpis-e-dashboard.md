# KPIs, Métricas e Dashboard de Acompanhamento

Conjunto de indicadores para medir o sucesso de cada iniciativa do audit. Norte-Norte: **mais leigo engajado → mais valor para o advogado pagante → mais Premium → mais receita.**

---

## 1. North-Star Metric

**MAU (Monthly Active Users) do leigo** — pessoas únicas que visitam ≥1x no mês e cumprem ≥1 ação engajada (calculadora, kit, Q&A, conta criada).

| Hoje (estimado) | 3m | 6m | 12m |
|---|---|---|---|
| ? | 50k | 250k | 1M |

Por que essa métrica: tráfego cru pode crescer com adwords ou ataque de SEO superficial. **MAU engajado** garante que estamos construindo audiência real e proteção contra atualizações Google.

---

## 2. KPIs por Camada do Funil

### Aquisição

| KPI | Como medir | Frequência | Meta 6m |
|---|---|---|---|
| Sessões orgânicas/mês | GA4 + GSC | Semanal | 500k+ |
| Páginas indexadas | GSC | Mensal | 200k+ |
| Posição média keywords-alvo (top 50) | GSC + RankMath | Semanal | Top 10 em 60% |
| CTR médio no SERP | GSC | Semanal | 5.5%+ |
| Rich snippets aparecendo | GSC > Aparência | Mensal | 40% das URLs |
| Tráfego direto/marca | GA4 (sem ref) | Mensal | 25% do total |
| Backlinks ganhos/mês | Ahrefs/SEMrush | Mensal | +50 RD/mês |

### Ativação (primeira ação engajada)

| KPI | Como medir | Meta 6m |
|---|---|---|
| % sessões com ≥1 evento | GA4 | 60%+ |
| % sessões com calculadora usada | GA4 evento `calc_run` | 8%+ |
| % sessões com kit baixado | GA4 evento `kit_download` | 4%+ |
| % sessões com Q&A aberta | GA4 | 3%+ |
| Conta criada (leigo) / sessão | GA4 | 1.5%+ |

### Retenção

| KPI | Como medir | Meta 6m |
|---|---|---|
| Returning visitors | GA4 | 35%+ |
| Sessões/usuário (mensal) | GA4 | 1.8+ |
| Subscribers email ativos | Brevo dashboard | 15k+ |
| Open rate newsletter | Brevo | 28%+ |
| Click rate newsletter | Brevo | 5%+ |
| Push web inscritos | OneSignal | 8k+ |
| Push click rate | OneSignal | 4%+ |

### Conversão (leigo → ação de valor)

| KPI | Como medir | Meta 6m |
|---|---|---|
| Cliques em WhatsApp do advogado | UTM track | 30k/mês |
| Cliques em telefone do advogado | UTM track | 10k/mês |
| Perguntas postadas no Q&A | DB count | 1.2k/mês |
| Respostas postadas | DB count | 3.6k/mês (3× pergunta) |
| Reviews coletadas | DB count | 800/mês |
| Estrelas média por advogado | DB avg | 4.5+ |

### Receita (lado advogado pagante)

| KPI | Como medir | Meta 6m |
|---|---|---|
| MRR (Monthly Recurring Revenue) | Stripe/Pagarme | R$ 80k+ |
| ARPU mensal | MRR / clientes | R$ 59,90 |
| Free → Premium conversion | Cohort 30d | 4-6% |
| Churn mensal | Stripe | <5% |
| LTV (Lifetime Value) | MRR ÷ Churn | R$ 1.200+ |
| CAC (Custo Aquisição Cliente) | Marketing $ ÷ novos pagos | <R$ 150 |
| LTV/CAC | Razão | >8x |

---

## 3. Dashboard Operacional — Mockup

Painel sugerido (Metabase ou Looker Studio sobre PostgreSQL):

```
┌──────────────────────────────────────────────────────────────┐
│  ADVAQUI — DASHBOARD SEMANAL                  [Data: 20/jul] │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  🎯 NORTH STAR: MAU Leigo                                    │
│     ▓▓▓▓▓▓▓▓▓░ 47.832  (+18% vs sem. passada) ✅            │
│                                                              │
├──────────────────────────────────────────────────────────────┤
│ AQUISIÇÃO                                                    │
│  Sessões orgânicas       127.430  ▲ 12%                     │
│  Páginas indexadas         8.420  ▲  3%                     │
│  Top 10 keywords             34/50 ▲  2                     │
│  Backlinks ganhos             18   →                        │
├──────────────────────────────────────────────────────────────┤
│ ATIVAÇÃO                                                     │
│  Calc usadas              4.821   ▲ 22%                     │
│  Kits baixados            1.730   ▲ 31%                     │
│  Contas criadas             645   ▲ 18%                     │
│  Q&A perguntas              112   ▲  8%                     │
├──────────────────────────────────────────────────────────────┤
│ ENGAJAMENTO ADVOGADO                                         │
│  WhatsApp cliques        3.421   ▲ 14%                      │
│  Telefone cliques        1.107   ▲  6%                      │
│  Reviews coletadas         87    ▲ 21%                      │
├──────────────────────────────────────────────────────────────┤
│ RECEITA                                                      │
│  MRR                R$ 62.380   ▲  9%                       │
│  Novos Premium             47    ▲  3                       │
│  Churn                      8    ▼  2 (bom)                 │
│  LTV/CAC                  6.4x   ▲ 0.3                      │
├──────────────────────────────────────────────────────────────┤
│ ALERTAS                                                      │
│  🟡 Calc Pensão Aliment. sem evento "calc_run" há 3 dias   │
│  🔴 Página /modelos com erro 500 detectado às 14:30        │
│  🟢 Schema FAQ validado em 12 novos artigos                │
└──────────────────────────────────────────────────────────────┘
```

---

## 4. Eventos GA4 (taxonomia)

Padrão de naming sugerido:

| Evento | Quando dispara | Parâmetros |
|---|---|---|
| `calc_run` | Usuário clica calcular | `calc_type` (rescisao/pensao/...), `result_value` |
| `calc_share` | Compartilha resultado | `calc_type`, `share_via` (whatsapp/email/pdf) |
| `kit_view` | Vê landing do kit | `kit_slug` |
| `kit_submit` | Envia email | `kit_slug` |
| `kit_confirmed` | Double opt-in confirmado | `kit_slug` |
| `qa_view` | Lê uma pergunta | `qa_id`, `qa_area` |
| `qa_ask` | Posta pergunta | `qa_area`, `qa_city` |
| `qa_answer` | Advogado responde | `qa_id`, `lawyer_id` |
| `lawyer_view` | Abre perfil | `lawyer_id`, `lawyer_city`, `lawyer_area` |
| `lawyer_whatsapp` | Clica botão WhatsApp | `lawyer_id` |
| `lawyer_phone` | Clica botão telefone | `lawyer_id` |
| `lawyer_review` | Submete review | `lawyer_id`, `rating` |
| `signup_lay` | Leigo cria conta | `source_page` |
| `signup_lawyer` | Advogado cria conta | `plan` |
| `subscribe_premium` | Ativa Premium | `lawyer_id`, `mrr_delta` |
| `cancel_premium` | Cancela | `lawyer_id`, `reason` |
| `newsletter_signup` | Inscreve newsletter | `topic` |
| `share` | Compartilha artigo | `slug`, `channel` |

---

## 5. Cohorts e Análises Críticas

### Cohort de retenção do leigo

Tabela semana após semana:

| Coorte de signup | W1 | W2 | W4 | W8 | W12 |
|---|---|---|---|---|---|
| Jul/06 | 100% | 42% | 28% | 19% | 14% |
| Jul/13 | 100% | 45% | 31% | 22% | — |
| Jul/20 | 100% | 47% | 33% | — | — |

Meta: W4 retention ≥30% (sinal de produto sticky).

### Conversão Free → Premium do advogado

Tempo médio até upgrade, por trigger:

| Trigger | Tempo médio | Taxa conversão |
|---|---|---|
| Cadastro free + onboarding completo | 12 dias | 6.8% |
| Premium oferecido após 5 visualizações de perfil | 4 dias | 12.3% |
| Premium oferecido após 1 cliente WhatsApp | 2 dias | 18.5% |
| Premium oferecido em campanha email D+7 | 8 dias | 3.2% |

Insight para otimizar: **gatilho "1 cliente WhatsApp" tem maior CR — investir em fazer free advogados receberem ao menos 1 contato rápido.**

### Funil de conversão crítico

```
1.000.000 sessões/mês (alvo)
  → 600.000 com evento engajado (60%)
  → 80.000 com calc usada (8%)
  → 40.000 com kit download ou Q&A (4%)
  → 15.000 contas criadas leigo (1.5%)
  → 300.000 cliques em advogado (vários eventos somados)
  → 30.000 cliques WhatsApp (10% do clique em perfil)
  → 1.000 advogados free ativos (escala)
  → 50 premium novos / mês (5% free→premium)
  → R$ 3.000 MRR delta / mês
```

---

## 6. Rituais de Análise

### Semanal (segundas, 30 min)

- Conferir dashboard
- Identificar 3 movimentos relevantes (positivos e negativos)
- Plano de ação 1-3 itens

### Quinzenal (60 min)

- Revisão de SEO: novas keywords ranqueando, URLs perdendo posição
- Backlog editorial — ajustes
- Análise de uma feature específica (rotativo)

### Mensal (2h)

- Cohort retention
- Funil de conversão completo
- Revisão de OKRs do trimestre
- Decisão de double-down ou kill de experimentos

### Trimestral (meio-dia)

- Definir OKRs do próximo Q
- Revisar roadmap macro
- Auditoria SEO técnica
- Auditoria de conformidade OAB+LGPD

---

## 7. Stack de Medição Sugerido

| Camada | Ferramenta | Custo |
|---|---|---|
| Web analytics | Plausible (privacy-first) + GA4 | $9/mês + grátis |
| SEO técnico | Google Search Console + Bing Webmaster | Grátis |
| Keyword tracking | Serpwatch / SEMrush Lite | $30-100/mês |
| Backlinks | Ahrefs lite / SE Ranking | $80-200/mês |
| Email | Brevo / Mailerlite | Grátis até 1k |
| Erro tracking | Sentry | Grátis até 5k events |
| Uptime | UptimeRobot | Grátis |
| Heatmaps / replays | Microsoft Clarity | Grátis |
| Dashboard | Metabase self-hosted | Grátis |
| A/B testing | GrowthBook (open-source) | Grátis |

Total estimado: ~R$ 800-1.500/mês para infra de medição madura.

---

## 8. OKRs Sugeridos — Q3 2026

### Objective 1: Tornar a AdvAqui o destino #1 para o leigo resolver dúvidas jurídicas
- **KR1:** Atingir 250k sessões orgânicas/mês até 30/set
- **KR2:** 5 calculadoras lançadas com ≥1k execuções/mês cada
- **KR3:** 50.000 emails capturados via lead magnets
- **KR4:** Q&A público com 500+ perguntas e 1.500+ respostas

### Objective 2: Aumentar valor entregue ao advogado Premium
- **KR1:** Crescer MRR de R$ X para R$ X×1.8
- **KR2:** Free → Premium conversion de baseline para 6%
- **KR3:** Avg reviews por advogado Premium = 8+
- **KR4:** Churn mensal abaixo de 4%

### Objective 3: Construir autoridade YMYL no Google
- **KR1:** DR (Ahrefs) saltar para 30+
- **KR2:** 100+ domínios referenciadores novos
- **KR3:** 5+ menções em mídia top-tier (Folha/Estadão/UOL/Exame)
- **KR4:** Schema validado em 100% das URLs principais

---

## 9. Anti-Métricas (Vanity Metrics a Ignorar)

- ❌ Pageviews totais sem contexto de engajamento.
- ❌ Tempo médio em segundos (use bounce + scroll depth).
- ❌ Curtidas em redes sociais sem clicks.
- ❌ "Impressões" no Search Console sem CTR.
- ❌ Domínios referenciadores totais sem qualidade (DR ponderado importa).
- ❌ MRR sem churn (negócio assinatura vive do net).
- ❌ Cadastros free sem ativação.
