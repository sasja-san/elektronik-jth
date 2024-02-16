# elektronik-jth

Laborationer mm. för Introduktion till elektronik på JTH.

`.qmd` är "Quarto MarkDown", en dialekt av Pandocs MarkDown.
`quarto` är ett program för att generera/typsätta dokument skrivna i md.
Verktyget är mycket kapabelt och kan t.ex. generera grafer m.h.a. `numpyplot` och sedan stoppa in dessa som figurer i ens dokument.

För detta projekt så används Quarto för det snygga med MarkDown, men för att slippa det tråkigaste med LaTeX.


## Komma igång

  1. Gå till denna adress och antingen installera pre-release-versionen (under "more downloads") eller ladda ner och kör git-versionen: <https://quarto.org/docs/get-started/>

  2. Installera VS Code och när det är inne, sök på quarto bland Extensions och installera det du hittar.

  3. Skapa ett litet dummy-dokument, typ detta:

```qmd
---
title: I am dummy
author: John Doe
format:
    pdf:
      documentclass: scrartcl
      papersize: a4
---

# Chapter 1

How I Learned to Stop Worrying and Love the Bomb....

>
> -- Hey Vasquez, have you ever been mistaken for a man?
>
> -- No. Have you?
>

# Chapter 2

Lorem ipsum pälö pälö pälööööö....

```

  4. Om allt stämmer så bör du kunna klicka på Preview-knappen uppe till höger i VS Code. Om du *inte* har något om "format" i YAML-headern (som sedd ovan) så ska du få en HTML rätt snabbt och den visas i VS Code.

  5. När du försöker göra en preview på en PDF så kommer terminalen i VS Code klaga. Kör det den vill, förmodligen `quarto install tinytex`

Nu borde du ha allt som behövs för att kunna bygga dessa dokument.
Öppna en av laborationernas `.qmd` filer och testa preview.
Första gången så har den dynamiska TeX-installeraren ingenting av vad du behöver, så bli inte förvånad om det tar rätt lång tid att ladda ner allt.


## Filerna

### .quarto/

Detta är en mapp lägger man typsnitt och lite smått och gott som Quarto kan behöva. Filen `before-body.tex` *skulle* nog kunna ligga här, men eftersom den kan komma att redigeras så skippar vi det.

### before-body.tex

Eftersom denna nämns i `_quarto.yml` så ersätter den "standard"-framsidan för dokumentet.
Den layout som finns på framsidan med `$title$`, `$subtitle$`, `$author$` osv. defineras här.
Den kommer med i dokumenten p.g.a. `\maketitle`.


### `_quarto.yml`

Detta är den YAML-header som håller inställningarna för de olika laborationerna.
Här defineras pappersstorlek, typsnitt osv.
Viktigast här är kanske att varje år fixa med "author"-blocket så att rätt namn står i de genererade filerna.

Har även en lång lista med LaTeX-grejer som är relevanta för projektet.
Om du försöker förstå dig på de olika sakerna som används i filerna, titta igenom alla `\newcommand` här först.

### imgX

En mapp per labb.
Om "bilderna" är kretsar som ser snygga ut så är de ritade med `circuitikz` och importeras från ren LaTeX in i qmd-filen.

### gammalt

Mapp med tidigare års grejer, källmaterial som all text ursprungligen kom från.


### tex-doc

Dokumentation för alla de olika bibliotek som labbarna använder.
Vanligast att läsa är nog `easytable.pdf` för att fatta hur man gör med `TAB`-miljön i LaTeX när man vill dimensionera ens rutor rätt.


# qmd-filerna

Längst upp ska de ha sin "title" och "subtitle" deklarerade.
Dessa används i `before-body.tex` så att framsidan blir snygg.

Notationen med `:::` öppnar/stänger en "div" i quarto.
Den vanligaste att öppna är `{.column-margin}` vilket betyder "lägg det som kommer innan jag stänger denna div i marginalen".
Det är inte ovanligt att dessa innehåller en "callout"-ruta.

Andra sätt att använda marginalen är via text som skrivs så här:

```qmd
Hej detta[Och detta är en marginalnotis som dyker upp på samma rad som ordet "detta" står. Det är *inte* en fotnot.]{.aside} är en text!
```

För att göra snygga linjer att skriva svar på så används två egendefinerade kommandon:
`\notes` och `\ansline`. Som tidigare nämnt så finns dess definitioner i `_quarto.yml` men i Lab1 så kan man se dem användas på lite olika sätt.
För att rada upp saker snyggt så används de (speciellt `\ansline`) tillsammans med `\tabto`.

För att hålla källdokumenten läsliga/navigerbara så tog jag och stoppade in c:a 10 tomma rader efter varje `{{< pagebreak >}}`.

Innehållet i marginalen var ibland rätt svårt att kontrollera.
Det knuffades runt en del, så för att trixa runt det så blev det ibland att det kommer en `{.column-margin}` som direkt inleds med en `\vspace{25mm}` bara för att lägga sakerna rätt.
Finns inget riktigt snyggt sätt att göra det bättre på.
Gör man inte detta så skriver de på samma yta.



