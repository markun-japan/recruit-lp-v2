# FINAL_AUDIT.md

Date: 2026-07-15
Agent: tsuki / Grok 4.5 field supervisor
Scope: grok / fugu / sol / terra / luna index.html
Root index.html: NOT modified

## Static audit summary

| lane | issues | call contract | line contract | meta | deps |
|---|---|---|---|---|---|
| grok | 0 | pass | pass | lang/viewport/noindex/slot ok | none |
| fugu | 0 | pass | pass | lang/viewport/noindex/slot ok | none |
| sol | 0 | pass | pass | lang/viewport/noindex/slot ok | none |
| terra | 0 | pass | pass | lang/viewport/noindex/slot ok | none |
| luna | 0 | pass | pass | lang/viewport/noindex/slot ok | none |

## Measured table (Playwright remeasure)

| lane | vp | noHScroll | imgOk | maxCallW | topOverlap | bottomOverlap |
|---|---|---|---|---:|---|---|
| grok | mobile390 | true | true | 358 | false | false |
| grok | mobile375 | true | true | 343 | false | false |
| grok | desktop1440 | true | true | 408 | false | false |
| fugu | mobile390 | true | true | 322 | false | false |
| fugu | mobile375 | true | true | 307 | false | false |
| fugu | desktop1440 | true | true | 520 | false | false |
| sol | mobile390 | true | true | 370 | false | false |
| sol | mobile375 | true | true | 355 | false | false |
| sol | desktop1440 | true | true | 520 | false | false |
| terra | mobile390 | true | true | 350 | false | false |
| terra | mobile375 | true | true | 335 | false | false |
| terra | desktop1440 | true | true | 520 | false | false |
| luna | mobile390 | true | true | 354 | false | false |
| luna | mobile375 | true | true | 339 | false | false |
| luna | desktop1440 | true | true | 520 | false | false |

## NG / P1
- All lanes clean (必ず/絶対/日本一/No.1/祝い金 none)
- Luna P1 phrases removed

## CTA contract
- call: https://micro-tube-pace-tuning.trycloudflare.com/?src={lane} + data-cta=call + same tab
- line: https://lin.ee/XEVQvbw + data-cta=line + target=_blank rel=noopener
- ANALYTICS_SLOT before </body>

## Remaining blockers
- Final photography beyond current 4 assets
- Permanent call URL (trycloudflare provisional)
- GA4 / post-funnel measurement into ANALYTICS_SLOT
