# Design System CAT — CLAUDE.md

Guida operativa per l'agente. Questo file è il punto d'ingresso: leggilo SEMPRE prima di scrivere HTML/CSS per papernest.it.

## Struttura cartella

```
work/design-system/
├── CLAUDE.md                  ← questo file (regole + quick reference)
├── DESIGN_SYSTEM_SPEC.md      ← 82KB raw extraction da Figma (reference dettagliato)
├── design_tokens.css          ← CSS custom properties pronte all'uso
├── SEO_GUIDELINES.md          ← Do's & Don'ts dal design team (da Notion)
└── FIGMA/                     ← 24 PNG export + asset ZIP
    ├── Design system - CAT.png       → [00] Palette completa (tutte le varianti colore)
    ├── Design system - CAT (1).png   → [01] Core Colors — scala Tailwind (Primary, Secondary, Destructive, Success, Warning, Stone)
    ├── Design system - CAT (2).png   → [02] Typography — scala HERO/HEADING/BODY con Avenir
    ├── Design system - CAT (3).png   → [03] Divider
    ├── Design system - CAT (4).png   → [04] Skeleton/Placeholder
    ├── Design system - CAT (5).png   → [05] Tag — varianti e specs (primary, positive, warning, negative, neutral)
    ├── Design system - CAT (6).png   → [06] Alert Banner — negative/positive, desktop/mobile, anatomy
    ├── Design system - CAT (7).png   → [07] Provider Card Grid — layout 1-4 colonne, desktop/mobile
    ├── Design system - CAT (8).png   → [08] Hero Section — heading + CTA + content area
    ├── Design system - CAT (9).png   → [09] Info Banner — feature highlight su bg viola chiaro
    ├── Design system - CAT (10).png  → [10] Accordion — collapsed/expanded, desktop/mobile
    ├── Design system - CAT (11).png  → [11] Alert Inline — info/success/error con left border
    ├── Design system - CAT (12).png  → [12] Checkbox — stati: default, hover, disabled, checked
    ├── Design system - CAT (13).png  → [13] Select/Combobox — dropdown, search, grouped items
    ├── Design system - CAT (14).png  → [14] Helper/Info Text — icon + testo
    ├── Design system - CAT (15).png  → [15] Input Field — stati validazione (default→error)
    ├── Design system - CAT (16).png  → [16] Progress Bar — barra orizzontale primary
    ├── Design system - CAT (17).png  → [17] Star Rating — 0-5 stelle, small/large
    ├── Design system - CAT (18).png  → [18] Native Select/Dropdown — con group titles
    ├── Design system - CAT (19).png  → [19] Slider/Range — thumb bianco su track nero
    ├── Design system - CAT (20).png  → [20] Textarea — stessi stati validazione di Input
    ├── Design system - CAT (21).png  → [21] Card/List semantica — info/success/destructive
    ├── Design system - CAT (22).png  → [22] Partner Offer Cards — grid 4-col desktop, stacked mobile
    └── Design system - CAT (23).png  → [23] Table — header navy, righe alternate bianco/viola chiaro
```

**Workflow**: per costruire un componente, leggi prima le regole qui sotto. Se hai bisogno di dettagli specifici su un componente, apri il PNG corrispondente dalla mappa sopra. Il `design_tokens.css` ha tutte le variabili CSS pronte.

---

## 1. Palette Colori

Il design system usa una scala Tailwind CSS (50→950) per ogni famiglia. I colori sotto sono quelli da usare — NON inventare varianti.

### Primary (Purple)
| Step | Hex | Uso |
|------|-----|-----|
| 50 | `#f6f5ff` | Background ultra-light, container bg |
| 100 | `#f1f0ff` | Background muted (tabelle, sezioni) |
| 200 | `#ceccff` | — |
| 300 | `#aca8ff` | — |
| 400 | `#8a85ff` | Hover light, secondary accent |
| **500** | **`#5a52ff`** | **Colore primario — bottoni, link, accenti** |
| 600 | `#443ec1` | — |
| 700 | `#3e38b2` | Hover/active su primary |
| 800 | `#2d297f` | Deep purple |
| 900 | `#1b194d` | — |
| 950 | `#110f32` | Darkest purple |

### Secondary (Teal)
| Step | Hex | Uso |
|------|-----|-----|
| 50 | `#f2fcfb` | Background light teal |
| 100 | `#e0f8f6` | — |
| 200 | `#b4eee7` | — |
| 300 | `#82e2d7` | — |
| 400 | `#4dd5c5` | Light teal |
| **500** | **`#02c5ae`** | **Teal — badge, input success alt, accenti** |
| 600 | `#029281` | — |
| 700 | `#018979` | Teal dark/hover |
| 800 | `#016559` | Deep teal |
| 900 | `#003c35` | — |

### Destructive (Red)
| Step | Hex | Uso |
|------|-----|-----|
| 50 | `#fff1f2` | Background error light |
| 100 | `#ffccd3` | — |
| 200 | `#ffa1ad` | — |
| 300 | `#ff637e` | Light red |
| 400 | `#ec003f` | — |
| **500** | **`#ff2056`** | **Errore, alert destructive, badge error** |
| 600 | `#c70036` | — |
| 700 | `#a50036` | Deep red |
| 800 | `#8b0836` | — |
| 900 | `#4d0218` | Darkest red |

### Success (Green)
| Step | Hex | Uso |
|------|-----|-----|
| 50 | `#ecfdf5` | Background success light |
| 100 | `#d0fae5` | — |
| 200 | `#a4f4cf` | — |
| 300 | `#5ee9b5` | — |
| 400 | `#00d492` | Light green |
| **500** | **`#00bc7d`** | **Success — validazione, conferme, CTA secondaria** |
| 600 | `#009966` | — |
| 700 | `#007a55` | — |
| 800 | `#006045` | — |
| 900 | `#004f3b` | Darkest green |

### Warning (Orange)
| Step | Hex | Uso |
|------|-----|-----|
| 50 | `#fffbeb` | Background warning light |
| 100 | `#fef3c6` | — |
| 200 | `#fee685` | — |
| 300 | `#ffba00` | — |
| 400 | `#e17100` | — |
| **500** | **`#fd9a00`** | **Warning — attenzione, input warning** |
| 600 | `#bb4d00` | — |
| 700 | `#973c00` | — |
| 800 | `#7b3306` | — |
| 900 | `#461901` | Darkest orange |

### Stone (Neutral/Gray)
| Step | Hex | Uso |
|------|-----|-----|
| 50 | `#fafaf9` | Surface bg (table, card) |
| 100 | `#f5f5f4` | Input bg, collapsible |
| 200 | `#e7e5e4` | Border default, divider |
| 300 | `#d6d3d1` | — |
| 400 | `#a6a09b` | Light icon/text |
| **500** | **`#79716b`** | **Text descriptions, border, icon** |
| 600 | `#57534d` | — |
| 700 | `#44403b` | — |
| 800 | `#292524` | — |
| 900 | `#1c1917` | Near-black |

### Colori Speciali
| Nome | Hex | Uso |
|------|-----|-----|
| Navy | `#212430` | Testo principale, header, dark bg |
| Navy Alt | `#212431` | Footer, cookie banner |
| Text Secondary | `#383c4c` | Testo secondario |
| Text Muted | `#63697f` | Label, placeholder |
| Text Subtle | `#81859a` | Caption, helper text |
| Trustpilot Green | `#00b67a` | Badge Trustpilot |
| Yellow/Stars | `#ffd230` | Rating stelle |
| Yellow Dark | `#ffb81d` | Accento giallo |
| Blue Info | `#0c68d3` | Tag/banner info |
| Blue Link | `#2563eb` | Link blu (TDB) |
| Blue Sky | `#20a8df` | Brand accent sky |
| Purple Banner | `#211430` | Banner dark bg |
| White | `#ffffff` | — |
| Black | `#000000` | — |

---

## 2. Typography

**Font principale**: Avenir (heading + body). Inter per UI/system. Exo per display/brand. Grand Hotel per decorativo.

### Scala HERO (titoli grandi)
| Nome | Size | Line Height | Weights |
|------|------|-------------|---------|
| 9xl | 128px | 128px | 400, 500, 800 |
| 8xl | 96px | 96px | 400, 500, 800 |
| 7xl | 72px | 72px | 400, 500, 800 |
| 6xl | 60px | 60px | 400, 500, 800 |
| 5xl | 48px | 48px | 400, 500, 800 |
| 4xl | 36px | 40px | 400, 500, 800 |

### Scala HEADING
| Nome | Size | Line Height | Weights |
|------|------|-------------|---------|
| xl | 20px | 28px | 500, 800 |
| lg | 18px | 24.6px | 400, 500, 800 |
| base | 16px | 21.9px | 400, 500, 800 |
| sm | 14px | 19.1px | 400, 500, 800 |

### Scala BODY
| Nome | Size | Line Height | Weights |
|------|------|-------------|---------|
| lg | 16px | 24px | 350, 400 |
| base | 14px | 33px | 350, 400 |
| sm | 12px | 16.4px | 300, 400, 500, 800 |
| xs | 10px | 16px | 350, 400 |

### Regole tipografia
- **Weight 800** = titoli/heading principali
- **Weight 500** = label, subtitle, emphasis
- **Weight 400** = body text, descrizioni
- **Weight 350** = body text leggero (Avenir Light)
- **Mai usare weight 900** per testo comune (riservato a accent specifici)
- **Line-height**: per HERO = uguale a font-size; per heading/body = maggiore

---

## 3. Spacing & Layout

**Griglia base**: 8px (design system). Lo storybook legacy usa 5px ma il DS preferisce 8px.

### Scala spacing
```
4px — 8px — 12px — 16px — 20px — 24px — 32px — 40px — 48px — 64px — 80px — 96px — 128px
```

### Pattern più comuni (gap + padding)
| Pattern | Quando usarlo |
|---------|--------------|
| `gap:8px pad:0` | Default flex gap |
| `gap:8px pad:8/16` | Buttons, badge, tag inline |
| `gap:8px pad:12/32` | Buttons grandi, CTA |
| `gap:16px pad:0` | Liste, stack verticale |
| `gap:24px pad:0` | Sezioni separate |
| `gap:64px pad:0` | Tra sezioni principali della pagina |
| `pad:4/4` | Spacing minimo (icon wrapper) |

### Regola dal Design Team
> **Non modificare padding e gap dei componenti** fino al redesign del design team. I valori sono scelti secondo l'8px grid e i principi della teoria Gestalt per gerarchia visiva.

---

## 4. Border Radius

### Scala pratica
```
2px — 4px — 6px — 8px — 12px — 16px — 24px — 32px — 9999px (pill/full)
```

### Regole
- **Modifiche consentite in intervalli di 5px** (dal design team)
- **ppn-shape**: eccezione con 18px su top-left e bottom-right (identità brand)
- I raggi più comuni: `8px` (card, container), `6px` (input, tag), `9999px` (pill button)

---

## 5. Shadows

### Scala semantica
| Nome | Valore | Uso |
|------|--------|-----|
| xs | `0 1px 2px rgba(0,0,0,0.05)` | Sottile, divider |
| sm | `0 1px 3px rgba(0,0,0,0.10), 0 1px 2px rgba(0,0,0,0.06)` | Card default |
| md | `0 4px 6px rgba(0,0,0,0.10), 0 2px 4px rgba(0,0,0,0.06)` | Card hover |
| lg | `0 10px 15px rgba(0,0,0,0.10), 0 4px 6px rgba(0,0,0,0.05)` | Modal, popover |
| xl | `0 20px 25px rgba(0,0,0,0.10), 0 10px 10px rgba(0,0,0,0.04)` | Dialog |
| 2xl | `0 25px 50px rgba(0,0,0,0.25)` | Overlay |
| primary | `0 2px 8px rgba(90,82,255,0.40)` | Focus ring primary |
| teal | `0 2px 4px rgba(24,215,210,0.42)` | Focus ring teal |
| card | `0 2px 12px 1px rgba(127,131,152,0.20)` | Card elevata (deal, offer) |

### Focus Ring (input validation)
| Stato | Shadow |
|-------|--------|
| Focus (primary) | `0 0 0 2px rgba(90,82,255,0.25)` |
| Warning | `0 0 0 2px rgba(234,88,12,0.25)` |
| Error | `0 0 0 2px rgba(220,38,38,0.25)` |

---

## 6. Icone

- **Libreria**: Lucide (lucide.dev)
- **Solo outline** — la libreria Lucide NON ha varianti filled
- **Sizes**: 16px (small), 24px (default), 32px (large), 48px (hero)
- **Colori**: seguono il contesto (primary, muted, semantic)

---

## 7. Componenti — Quick Reference

Ogni componente ha un PNG di riferimento nella cartella `FIGMA/`. Aprire il file per vedere anatomia, varianti e spacing.

### Form Components
| Componente | Ref | Varianti chiave |
|-----------|-----|----------------|
| Input | [15] | default, focus (purple border), success (teal), valid (green), warning (orange), error (red/pink), disabled |
| Textarea | [20] | stesse varianti di Input |
| Checkbox | [12] | unchecked, hover, disabled, checked (primary fill + white check) |
| Select | [13] | default, open dropdown, search, grouped items, multi-size |
| Native Select | [18] | trigger piccolo, dropdown con group titles |
| Slider/Range | [19] | thumb bianco, track nero |
| Star Rating | [17] | 0-5 stelle gialle (#ffd230), small/large |
| Progress Bar | [16] | barra primary purple |

### Feedback Components
| Componente | Ref | Varianti chiave |
|-----------|-----|----------------|
| Alert Banner | [06] | negative (red bg), positive (green bg), desktop/mobile, dismissible |
| Alert Inline | [11] | info (purple border), success (green border), error (red border) + title/description |
| Tag | [05] | primary, positive, warning, negative, neutral; sizes small/medium |
| Helper Text | [14] | icon + testo, icon left/right |
| Card Semantica | [21] | info (purple), success (green), destructive (red) con bullet list |

### Layout Components
| Componente | Ref | Varianti chiave |
|-----------|-----|----------------|
| Hero Section | [08] | heading purple + subtitle + CTA button + content placeholder |
| Info Banner | [09] | bg viola chiaro, heading purple con icon, body text |
| Accordion | [10] | collapsed/expanded, desktop/mobile |
| Divider | [03] | linea sottile per separare contenuti |
| Table | [23] | header navy (#212430, testo bianco), righe alternate bianco/viola chiaro |
| Skeleton | [04] | placeholder wireframe |

### Business Components
| Componente | Ref | Varianti chiave |
|-----------|-----|----------------|
| Provider Card Grid | [07] | 1-4 colonne, logo + nome + stelle + CTA, desktop/mobile |
| Partner Offer Cards | [22] | grid 4-col desktop/stacked mobile, logo + nome + desc + CTA phone |

---

## 8. Do's & Don'ts (dal Design Team)

Regole ufficiali dal design team per il SEO team. Vedi `SEO_GUIDELINES.md` per il documento completo.

### Colori
- **DO**: usare SOLO colori dalla palette Papernest (sezione 1 sopra)
- **DON'T**: inventare colori custom — rischiano di rompere la coesione visiva

### Typography
- **DO**: seguire la gerarchia tipografica (HERO > HEADING > BODY)
- **DO**: puoi cambiare size/weight/color entro la scala definita
- **DON'T**: usare font diversi da quelli del DS

### Icone
- **DO**: usare solo icone dalla libreria Lucide
- **DON'T**: usare icone filled — Lucide ha solo outline

### Shape & Radius
- **DO**: mantenere i radius dei componenti come da HTML originale
- **DO**: se modifichi, usa intervalli di 5px
- **DON'T**: dimenticare il ppn-shape (18px TL+BR)

### Spacing
- **DO**: seguire la scala 8px grid
- **DON'T**: modificare padding/gap dei componenti senza approvazione design team
- I valori seguono i principi Gestalt per gerarchia visiva e leggibilità

---

## 9. PPN Components (Storybook redesigned)

Componenti storybook ridisegnati con il nuovo design system:
- **Buttons** / **Button group**
- **ppn-block-double**
- **ppn-deals-list**
- **ppn-callout**
- **ppn-cta-block-single** (Lugia + Kamino)
- **ppn-cta-fullwidth**

## 10. Custom HTML Components

Componenti HTML custom usati dal SEO team:
- Navigation buttons, CTA promotion, HTML callout
- Main steps, Expert card, Comparation cards, Step by step
- HTML deal list, Multiple cards, Main providers, Color block
- Related news module, Related articles without images
- 3 time sections, Our service, Reviews
- HTML card, Card offer v1/v2, Offer table, Podiums

---

## 11. Logo & Brand

Lo ZIP `Design system - CAT.zip` contiene loghi per tutti i mercati:
- **FR** — Fournisseur-energie (principale)
- **NL** — ElektriciteitsTarief
- **IN** — Switcheroo
- **BR** — Compara e poupa
- **PT** — Comparaplanos
- **AR** — Tuplanbarrato
- **BE** — SuperPower
- **MX** — Holahorro

Varianti logo: `color=white|blue|black`, `icon=true|false`

---

## 12. Gradienti (principali)

| Uso | Tipo | Valori |
|-----|------|--------|
| CTA Lugia/Kamino | RADIAL | `#8a85ff → #5a52ff → #3e38b2` |
| CTA Teal | RADIAL | `#4dd5c5 → #02c5ae → #018979` |
| Brand logo | LINEAR | `#5a52ff → #918cff` |
| Trustpilot | LINEAR | `#00b67a → #e7e5e4` |

---

## Come usare questo file

1. **Sempre**: leggi sezioni 1-6 (palette, typo, spacing, radius, shadow, icon) prima di scrivere CSS
2. **Per un componente specifico**: cerca nella sezione 7, poi apri il PNG corrispondente per i dettagli visivi
3. **Regole**: segui sezione 8 (Do's & Don'ts) — sono regole ufficiali del design team
4. **Dettagli granulari**: consulta `DESIGN_SYSTEM_SPEC.md` (82KB, raw Figma export con tutti i valori)
5. **CSS ready**: importa `design_tokens.css` per tutte le variabili CSS

### Figma source
File ID: `3t2bjqWp5FPMk7IcOknP88` — [Design system - CAT](https://www.figma.com/design/3t2bjqWp5FPMk7IcOknP88/Design-system---CAT)
