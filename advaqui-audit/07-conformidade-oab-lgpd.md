# Conformidade OAB e LGPD — Guarda-Corpos Legais

Todas as recomendações deste audit precisam respeitar dois pilares:
1. **Código de Ética e Disciplina da OAB** (Provimento 205/2021 — Publicidade na Advocacia).
2. **LGPD** (Lei 13.709/2018).

Este documento é o checklist regulatório para implementação segura.

---

## 1. OAB — O que pode, o que não pode

### 1.1 Pode (conteúdo informativo)

- Informar sobre direitos, prazos, procedimentos (jurídico explicado).
- Citar áreas de atuação, formação, OAB, idiomas.
- Compartilhar artigos, vídeos, posts educativos.
- Publicar bio profissional sóbria.
- Listar serviços (sem precificar agressivamente).
- Citar publicações próprias, livros, palestras.
- Receber e responder Q&A em linguagem orientativa.

### 1.2 Não pode

- ❌ **Captação de clientela** (procurar pessoas com problema jurídico para oferecer serviço).
- ❌ **Mercantilização** ("o melhor advogado de", "ganhe sua causa", "100% garantido").
- ❌ **Comparações desabonadoras** com colegas.
- ❌ **Promoção em mídia de massa** com tom comercial (Outdoor "fui demitido? Ligue 0800").
- ❌ **Divulgação de valor de causas ganhas** específicas.
- ❌ **Pagar lead ao site** condicionado a contato/contrato (= captação por intermediário).
- ❌ **Anúncios pagos por clique** com promessa de resultado.

### 1.3 Como a Advaqui se posiciona corretamente

| Feature | Risco | Salvaguarda |
|---|---|---|
| Diretório de advogados | Nenhum (perfil profissional é permitido) | Manter sóbrio, sem rankings tipo "melhor" |
| WhatsApp direto | Nenhum (canal legítimo) | Mensagem pré-preenchida é orientativa, não comercial |
| Plano Premium R$ 59,90 | Nenhum (assinatura por destaque, sem comissão) | **Diferencial — não é "lead por venda"**, é mídia paga |
| Reviews de clientes | Médio | Texto livre, sem incentivo a hipérbole; auditoria amostral; sem "antes/depois de processo" |
| Q&A público | Médio | Respostas **orientativas**, não consultoria; disclaimer fixo; moderação de promessas |
| Calculadoras | Baixo | "Cálculo aproximado, consulte advogado para validar" |
| Lead magnets / email capture | Baixo | É conteúdo educativo, não captação de cliente — não está vinculado a contratação |
| Reviews com estrelas no schema | Médio | Critérios públicos, número real, sem manipulação |

### 1.4 Disclaimer-padrão sugerido (rodapé de toda peça)

> "Este conteúdo tem caráter exclusivamente informativo e não substitui consulta jurídica individual. AdvAqui é uma plataforma de informação e diretório profissional, não presta serviços jurídicos. Todos os profissionais listados são responsáveis pelo conteúdo de seus perfis e pela observância do Código de Ética da OAB."

---

## 2. LGPD — Mapeamento de Dados Tratados

### 2.1 Categorias de titulares

| Titular | Dados típicos | Bases legais |
|---|---|---|
| **Leigo (visitante)** | Email (opt-in), IP, navegação | Consentimento, legítimo interesse (analytics) |
| **Leigo (cadastrado)** | Nome, email, cidade, histórico | Consentimento + execução de contrato |
| **Leigo (Q&A)** | Pergunta pública + email | Consentimento + execução de contrato |
| **Advogado Free** | Dados profissionais, OAB | Execução de contrato |
| **Advogado Premium** | + pagamento, faturamento | Execução de contrato + obrigação legal (fiscal) |
| **Cliente que avalia advogado** | Email/telefone, review | Consentimento expresso |

### 2.2 Dados sensíveis? Sim, mas indiretamente

Q&A público pode revelar:
- Situação de saúde (auxílio-doença)
- Origem étnica (caso de discriminação)
- Filiação sindical
- Vida sexual (divórcio com adultério)

Salvaguarda:
- Moderação automática + humana antes de publicar.
- Anonimização de detalhes pessoais.
- Botão "remover esta pergunta" 1-clique disponível ao autor.
- Disclaimer pré-publicação: "não inclua nomes, CPF, datas exatas".

### 2.3 Checklist LGPD para implementação

#### Bases legais documentadas
- [ ] Mapeamento RoPA (Record of Processing Activities) completo.
- [ ] Cada formulário com base legal explícita.

#### Consentimento
- [ ] Double opt-in para email marketing (clique no link no email).
- [ ] Checkbox **não pré-marcado** para consentimento.
- [ ] Texto do checkbox claro: "Concordo em receber emails sobre [tema] e que meus dados sejam tratados conforme a Política de Privacidade."
- [ ] Granularidade: opt-in separado para newsletter, alerta, marketing.

#### Direitos do titular
- [ ] Endpoint `/minha-conta/privacidade` com botões:
  - "Baixar meus dados" (export JSON/CSV)
  - "Solicitar exclusão" (anonimização em até 15 dias)
  - "Revogar consentimento"
  - "Corrigir dados"
- [ ] Email DPO visível: `dpo@advaqui.com.br`.
- [ ] Resposta em até 15 dias (Art. 19 LGPD).

#### Segurança
- [ ] HTTPS obrigatório (HSTS).
- [ ] Senhas com bcrypt/argon2.
- [ ] Logs de acesso a dados pessoais (audit trail).
- [ ] Backup criptografado.
- [ ] Pen test anual ou após mudança maior.
- [ ] Plano de resposta a incidentes (notificar ANPD em até 2 dias úteis se vazamento).

#### Cookies
- [ ] Banner de consentimento granular (essenciais / analytics / marketing).
- [ ] Sem carregar Google Analytics/Pixel antes do consentimento.
- [ ] Política de cookies linkada.

#### Compartilhamento com terceiros
- [ ] Lista pública de operadores (Brevo, Cloudflare, Stripe, etc.).
- [ ] Contratos DPA assinados com cada operador.
- [ ] Cláusulas de transferência internacional (EUA — Mailerlite/Brevo).

#### Q&A público — específico
- [ ] Aviso pré-publicação destacado.
- [ ] Moderação automática (regex anti-PII) + humana.
- [ ] Botão "remover" do autor.
- [ ] Histórico de revisões guardado por 90 dias (rollback).

#### Reviews — específico
- [ ] Cliente que avalia consente explicitamente em ter review publicado.
- [ ] Pode editar/remover em 30 dias.
- [ ] Advogado pode contestar (resposta pública).
- [ ] Sem manipulação (sem "compre reviews", sem advogado avaliar a si mesmo).

---

## 3. Termos de Uso e Política de Privacidade — Estrutura

### Termos de Uso

Seções obrigatórias:
1. Objeto da plataforma (diretório + conteúdo informativo)
2. Cadastro de advogado (verificação OAB, responsabilidade pelo perfil)
3. Cadastro do leigo (uso lícito, idade mínima 18)
4. Q&A público — regras de conduta, moderação, propriedade
5. Reviews — quem pode, como funciona
6. Pagamento Premium — período, cancelamento, reembolso
7. Limitações — não presta serviço jurídico, não garante resultado
8. Propriedade intelectual — conteúdo do site, modelos, calculadoras
9. Suspensão/cancelamento por violação
10. Foro e legislação aplicável

### Política de Privacidade

Seções obrigatórias (modelo ANPD):
1. Identificação do controlador (AdvAqui CNPJ, endereço)
2. DPO — nome e contato
3. Dados coletados, por categoria de titular
4. Finalidades de cada tratamento
5. Bases legais
6. Compartilhamento com operadores (lista)
7. Transferência internacional
8. Cookies e tecnologias
9. Direitos do titular (com botões/canais)
10. Retenção (quanto tempo guarda)
11. Crianças/adolescentes (proibido <18)
12. Alterações na política (com aviso)
13. Atualizada em [data]

---

## 4. Acessibilidade (WCAG 2.1 AA — bônus regulatório)

Não é obrigatório (ainda) por lei brasileira específica para sites privados, mas:
- Lei Brasileira de Inclusão (LBI 13.146/2015) **exige acessibilidade em serviços públicos e de relevância pública**.
- Direito é considerado de relevância pública em alguns precedentes do MPF.

Recomendado implementar:
- Contraste mínimo AA (4.5:1)
- Navegação por teclado completa
- Labels em todos os formulários
- Alt text em imagens
- Legendas em vídeos
- Reader-friendly markup
- Ajuste de fonte/contraste no site (botão A+/A-)

Ganho colateral: melhora SEO (Google valoriza).

---

## 5. Checklist Pré-Lançamento (todas as novas features)

Antes de pôr no ar qualquer item deste audit, validar:

- [ ] Não fere Código de Ética OAB (Provimento 205/2021)
- [ ] Tem base legal LGPD documentada
- [ ] Tem opt-in adequado se coleta dado pessoal
- [ ] Tem disclaimer "não substitui consulta jurídica"
- [ ] Schema markup correto e validado (Search Console)
- [ ] Acessível por teclado e screen reader
- [ ] Funciona em mobile sem fricção
- [ ] Tem fluxo de "remover meus dados" se aplicável
- [ ] Auditado por advogado interno parceiro (responsável técnico)
- [ ] Inclui termo de revisão técnica visível ("Revisado por OAB/__ ___")

---

## 6. Risco Reputacional — Lições do Jusbrasil

O Jusbrasil sofreu múltiplas decisões do TED/OAB e ações cíveis por:
- Captação ativa de clientes via SEO agressivo
- Leilão de leads (quebra do art. 7º Provimento 205)
- Reviews manipuladas
- Anúncios pagos com tom comercial

A Advaqui pode (e deve) capitalizar nesses tropeços com posicionamento:

> "Não cobramos comissão. Não leiloamos leads. Não prometemos resultado. Somos um diretório profissional ético — alinhado ao Provimento 205 da OAB."

Essa diferenciação é monetizável (advogados de prestígio migram do Jusbrasil), defensável (não atrai ações OAB), e ranqueável (Google valoriza E-E-A-T de site sóbrio).

---

## Fontes

- Provimento 205/2021 OAB (Publicidade na Advocacia)
- Lei 13.709/2018 (LGPD)
- Lei 13.146/2015 (LBI)
- WCAG 2.1 (W3C)
- Diretrizes ANPD para sites e apps
