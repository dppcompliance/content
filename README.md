# DPP Compliance – treści

Repozytorium trzyma treści redakcyjne wspólne dla aplikacji `app.dppcompliance.pl` (repo
`dashboard`) i portalu `dppcompliance.pl` (repo `ui-app`). Dzięki temu regulamin i polityka
prywatności mają jedno źródło prawdy i nie wymagają wdrożenia aplikacji przy każdej korekcie.

## Struktura

```
legal/
  privacy-policy.md    # Polityka Prywatności
  terms-of-service.md  # Regulamin Świadczenia Usług
```

## Format

Każdy dokument to Markdown z nagłówkiem YAML:

```yaml
---
title: Polityka Prywatności
slug: privacy-policy
updated: sierpień 2025
description: Krótkie streszczenie dokumentu.
---
```

- `title` – nagłówek renderowany nad treścią oraz tytuł strony (`<title>`).
- `slug` – identyfikator dokumentu w API aplikacji (`/api/legal/{slug}`).
- `updated` – data ostatniej aktualizacji, pokazywana pod tytułem. Wolny tekst, żeby nie
  udawać precyzji dziennej tam, gdzie dokument jej nie ma.
- `description` – używane w meta description strony.

Obsługiwany jest świadomie wąski podzbiór Markdown: nagłówki `##`/`###`, akapity, listy
numerowane i punktowane, tabele GFM, `---`, `**pogrubienie**`, `` `kod` `` oraz linki
`[tekst](url)`. Surowy HTML jest escapowany, a nie renderowany — konsument treści traktuje ten
plik jako dane, nie jako szablon.

## Jak treść trafia do aplikacji

`dashboard` pobiera pliki po HTTP z gałęzi `main` tego repozytorium
(`https://raw.githubusercontent.com/dppcompliance/content/main/...`) i trzyma je w pamięci
podręcznej. Po zmerge'owaniu zmiany do `main` aplikacja podchwyci ją po wygaśnięciu cache
(domyślnie 15 minut) — bez ponownego wdrożenia.

Zmiany merdżujemy do `main` przez pull request: to jest wersja, którą widzą użytkownicy.
