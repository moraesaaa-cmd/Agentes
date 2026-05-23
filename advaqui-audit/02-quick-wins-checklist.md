# Quick Wins — Checklist Acionável (0–30 dias)

Itens prontos para implementação imediata, alto impacto, baixo esforço.

---

## 🏷️ Schema Markup (1–3 dias dev)

### Em toda página do blog
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "{{ titulo }}",
  "image": ["{{ og_image_1200x630 }}"],
  "datePublished": "{{ data_publicacao }}",
  "dateModified": "{{ data_atualizacao }}",
  "author": {
    "@type": "Person",
    "name": "{{ autor_nome }}",
    "url": "/autores/{{ autor_slug }}",
    "jobTitle": "Advogado(a) OAB/{{ uf }} {{ numero }}"
  },
  "publisher": {
    "@type": "Organization",
    "name": "AdvAqui",
    "logo": { "@type": "ImageObject", "url": "https://advaqui.com/logo.png" }
  },
  "mainEntityOfPage": "{{ canonical_url }}"
}
</script>
```

### FAQ (já tem conteúdo no fim de cada artigo)
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Tenho direito a seguro-desemprego?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Sim, se cumpridos requisitos de carência..."
      }
    }
  ]
}
</script>
```

### LocalBusiness em cada perfil de advogado
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LegalService",
  "name": "{{ nome_advogado }}",
  "image": "{{ foto }}",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "{{ cidade }}",
    "addressRegion": "{{ uf }}",
    "addressCountry": "BR"
  },
  "telephone": "{{ telefone }}",
  "areaServed": "{{ cidade }}",
  "knowsAbout": ["{{ especialidade_1 }}", "{{ especialidade_2 }}"],
  "aggregateRating": { ... quando houver reviews }
}
</script>
```

### BreadcrumbList em todas as páginas internas

---

## 🌐 Open Graph + Twitter Cards (4h)

```html
<meta property="og:title" content="{{ titulo }}">
<meta property="og:description" content="{{ descricao_155_caracteres }}">
<meta property="og:image" content="https://advaqui.com/og/{{ slug }}.jpg">
<meta property="og:url" content="{{ canonical_url }}">
<meta property="og:type" content="article">
<meta property="og:locale" content="pt_BR">
<meta name="twitter:card" content="summary_large_image">
```

Gerar `og/<slug>.jpg` automaticamente (template Cloudinary ou edge function) com:
- Título grande
- Logo AdvAqui
- Cor por categoria (azul=trabalhista, verde=família, etc.)

---

## 📅 Datas + Autor Visíveis (1 dia)

No header de cada artigo:
```
🏷️ Trabalhista · ✍️ Dra. Ana Souza, OAB/SP 123.456
📅 Publicado em 10/05/2026 · 🔄 Atualizado em 18/05/2026 · ⏱️ 9 min
```

Box no fim do artigo:
```
┌────────────────────────────────────────┐
│ 🧑‍⚖️ Dra. Ana Souza                      │
│ Advogada trabalhista, OAB/SP 123.456   │
│ 12 anos atuando em São Paulo           │
│ [Ver outros artigos] [LinkedIn]        │
└────────────────────────────────────────┘
```

---

## 📤 Compartilhamento Social (2h)

Sidebar floating (desktop) + bottom (mobile):
- 🟢 WhatsApp ← **prioridade máxima no Brasil**
- ✈️ Telegram
- 𝕏 X
- 📘 Facebook
- 💼 LinkedIn
- 🔗 Copiar link

Link WhatsApp: `https://wa.me/?text={{ titulo }}%20{{ url_encoded }}`

---

## 📨 Captura de Email — 3 Lead Magnets Piloto (1 semana)

### Kit Demissão Sem Justa Causa
Conteúdo:
- PDF: "Checklist de verbas rescisórias 2026" (já existe no artigo, repaginar)
- Planilha Excel/Google Sheets: Calculadora de rescisão
- 3 modelos editáveis (.docx): Notificação para empresa, recibo de quitação parcial, declaração de horas extras

### Kit Divórcio Consensual
- Checklist de documentos
- Modelo de petição extrajudicial em cartório
- Tabela de custas por estado

### Kit Recurso INSS
- Modelo de recurso administrativo
- Tabela de prazos
- Checklist de provas

### Implementação
- Caixa inline a 60% do artigo + sticky footer mobile.
- Mailerlite ou Brevo (gratuito até 1k contatos / 9k emails/mês).
- Double opt-in obrigatório (LGPD).
- Tag automática por interesse (segmentação).
- E-mail #1: entregar kit.
- E-mail #2 (3 dias): "veja também esses 5 erros comuns".
- E-mail #3 (7 dias): "precisa de orientação? veja advogados em [cidade do user]".

---

## 🗂️ Robots, Sitemap, Performance (1 dia)

- Confirmar `robots.txt` libera tudo exceto admin/staging.
- `sitemap.xml` segmentado: `/sitemap-blog.xml`, `/sitemap-advogados.xml`, `/sitemap-jurisprudencia.xml`.
- Submeter no Google Search Console e Bing Webmaster.
- Confirmar HTTPS, HSTS, HTTP/2.
- Lazy-load de imagens (`loading="lazy"`).
- WebP em todas as imagens.
- Pré-carregar fontes críticas (`<link rel="preload" as="font">`).

---

## 🎯 Métricas para Validar Quick Wins (em 30 dias)

| Indicador | Como medir |
|---|---|
| Rich snippets aparecendo | Google Search Console → Performance → Aparência da pesquisa |
| CTR no SERP | GSC → Performance → CTR médio (deve subir 10-25%) |
| Compartilhamentos via WhatsApp | UTM `?utm_source=share&utm_medium=whatsapp` |
| Emails capturados | Dashboard Mailerlite/Brevo |
| Tempo médio no blog | GA4 → Engagement → Pages |
| Posição média keywords-alvo | GSC → Performance → Average position |
