# Lua Case Study: Frontend Development (Shopify)

Willkommen zur Case Study! Wir möchten sehen, wie du dich in ein bestehendes Shopify-Theme einarbeitest, wie du Anforderungen in eine Lösung übersetzt und welche Entscheidungen du dabei triffst.

Grundlage ist **Horizon**, das aktuelle Standard-Theme von Shopify. Du findest es in diesem Repository.

Die Aufgaben sind bewusst offen formuliert. Wir beschreiben das Problem und das gewünschte Ergebnis. Den Weg dorthin, die technische Umsetzung und die Detailentscheidungen überlassen wir dir. Wenn etwas unklar ist, triff eine sinnvolle Annahme und schreib sie in deinen PR.

**Zeitrahmen:** maximal **3 Stunden**, die Einrichtung eingeschlossen. **Bitte halte dich unbedingt an dieses Zeitlimit.** Wie du die Zeit aufteilst, entscheidest du.

**Es ist absolut kein Problem, wenn du nicht alle Aufgaben schaffst.** Wir erwarten nicht, dass alles perfekt oder vollständig ist. Uns ist eine saubere, durchdachte Teillösung lieber als eine vollständige, aber wackelige. Setz deine Prioritäten selbst und dokumentiere, was du mit mehr Zeit noch machen würdest.

**Überblick:**

- Teil 0: Setup
- Teil 1: Produktinformationen auf der Produktseite
- Teil 2: Fortschritt zum kostenlosen Versand im Cart Drawer
- Teil 3: A/B-Test-Variante auf der Produktseite
- Teil 4: Abgabe

---

## Teil 0: Setup

Bevor du loslegen kannst, brauchst du eine lauffähige Entwicklungsumgebung. Am Ende muss Folgendes stehen:

1. Ein **Fork** dieses Repositorys (`<REPO-URL>`) in deinem GitHub-Account, lokal geklont.
2. Ein **Shopify-Partner-Account** mit einem **Development Store**. Testprodukte musst du nicht von Hand anlegen, Shopify kann den Shop beim Erstellen mit Testdaten befüllen.
3. Die **Shopify CLI**, mit der du das Theme aus deinem Fork lokal gegen deinen Entwicklungsshop entwickelst und deine Änderungen direkt in einer Vorschau siehst.

### Einstiegspunkte

- Shopify Partners: <https://www.shopify.com/partners>
- Shopify CLI für Themes: <https://shopify.dev/docs/storefronts/themes/tools/cli>
- Theme-Architektur: <https://shopify.dev/docs/storefronts/themes/architecture>

> Wenn du beim Setup hängen bleibst, melde dich bei uns. Das Setup ist nicht der Kern der Aufgabe, und niemand soll daran scheitern.

---

## Teil 1: Produktinformationen auf der Produktseite

### Ausgangslage

Zu unseren Produkten gibt es Zusatzinformationen, die nicht in den Fließtext der Produktbeschreibung gehören:

- **Material**
- **Pflegehinweise**
- **Herkunft**
- **Highlights** (mehrere kurze Stichpunkte pro Produkt)

Viele Produkte teilen sich dasselbe Material und damit auch dieselben Pflegehinweise. Wenn sich ein Pflegehinweis ändert, wollen wir das nicht bei jedem Produkt einzeln nachpflegen.

Diese Informationen wollen wir strukturiert über **Shopifys Custom Data** pflegen. Auf der Produktseite sollen sie übersichtlich und einheitlich dargestellt werden.

### Aufgabe

1. Lege in deinem Entwicklungsshop ein **passendes Datenmodell** für diese Informationen an. Ob du Metafelder, Metaobjects oder eine Kombination nutzt und wie du sie strukturierst, entscheidest du.
2. Pflege die Daten bei einigen Testprodukten ein. Denk dabei auch an Produkte, bei denen nicht alles gepflegt ist.
3. Setze die Darstellung auf der Produktseite im Theme um.

### Anforderungen

- Händler können die Darstellung **selbst im Theme Editor** auf der Produktseite platzieren und anpassen.
- Die Darstellung bleibt auch dann sauber, wenn bei einem Produkt einzelne oder alle Informationen fehlen.
- Sie fügt sich optisch und technisch in Horizon ein.

Begründe im PR kurz, wie du das Datenmodell aufgebaut hast und welche Einstellmöglichkeiten du Händlern gibst und warum.

---

## Teil 2: Fortschritt zum kostenlosen Versand im Cart Drawer

### Ausgangslage

Ab einem bestimmten Bestellwert versenden wir kostenlos. Kundinnen und Kunden sollen im Warenkorb jederzeit sehen, wie weit sie davon noch entfernt sind. Das soll sie motivieren, noch etwas dazuzulegen.

### Aufgabe

Ergänze den **Cart Drawer** um einen Hinweis mit Fortschrittsanzeige, z. B.:

> Noch **12,50 €** bis zum kostenlosen Versand
> `[██████████░░░░░]`

Ist die Schwelle erreicht, soll das für Kundinnen und Kunden klar erkennbar sein.

### Anforderungen

- Die Schwelle lässt sich ohne Code-Änderung anpassen.
- Die Anzeige stimmt jederzeit mit dem aktuellen Warenkorb überein, auch wenn er sich ändert, während der Drawer offen ist.
- Beträge werden korrekt dargestellt.
- **Rabattcodes müssen berücksichtigt werden.** Wird ein Rabattcode im Warenkorb eingelöst oder entfernt, muss die Anzeige stimmen.

Alles darüber hinaus, also Randfälle, weitere Einstellungen und weitere Einsatzorte, liegt in deinem Ermessen. Schreib im PR, was du bewusst berücksichtigt oder weggelassen hast.

---

## Teil 3: A/B-Test-Variante

### Ausgangslage

A/B-Tests laufen bei uns über ein Testing-Tool, das zur Laufzeit JavaScript auf der Seite ausführt. Für Testvarianten wird das Theme selbst also **nicht angefasst**.

Unsere Hypothese: Wenn der Preis direkt im Kaufen-Button steht, steigt die Add-to-Cart-Rate.

### Aufgabe

Schreib die **Variante B** als reines JavaScript. Auf der Produktseite zeigt der Kaufen-Button zusätzlich den Preis der aktuell gewählten Variante:

> **In den Warenkorb · 49,00 €**

### Anforderungen

- Die Variante ist **ein eigenständiges Skript**, das einfach in der **Browser-Konsole** auf der Produktseite ausgeführt wird. Es ändert keine Theme-Dateien.
- Der Preis im Button stimmt immer mit der gewählten Variante überein.
- Wenn das Skript etwas nicht findet, was es erwartet, darf die Seite dadurch nicht kaputtgehen.

---

## Teil 4: Abgabe

Gib **Teil 1 und Teil 2 jeweils als eigenen Pull Request** von deinem Fork gegen den `main`-Branch des **Original-Repositorys** ab:

- **PR 1:** Produktinformationen auf der Produktseite (Teil 1)
- **PR 2:** Fortschritt zum kostenlosen Versand (Teil 2)

Die beiden PRs dürfen nicht voneinander abhängen. Jeder muss sich für sich allein reviewen und mergen lassen.

Für die **A/B-Test-Variante (Teil 3)** brauchst du keinen PR. Bring das Skript einfach zum Gespräch mit.

Schick uns außerdem einen **Vorschau-Link** deines Themes im Entwicklungsshop, inklusive Passwort, falls der Shop geschützt ist.

### Rahmenbedingungen

- Keine zusätzlichen Frameworks, Libraries oder Build-Tools.

### KI-Tools

Wir ermutigen dich ausdrücklich, KI-Tools zu nutzen, so wie du es auch im Arbeitsalltag tun würdest. Im Gespräch möchten wir dann sehen:

- **wie** du KI eingesetzt hast, z. B. mit welchen Tools und Prompts,
- **an welchen Stellen** sie dir geholfen hat und wo du selbst eingreifen oder korrigieren musstest.

Wichtig dabei: Wir erwarten, dass du **jede Zeile deines Codes verstehst** und erklären kannst, warum sie so ist, wie sie ist. Egal, ob du sie selbst geschrieben hast oder nicht.

---

## Worauf wir achten

- **Lösung:** Funktioniert sie, auch über den Idealfall hinaus?
- **Einarbeitung:** Wie gut verstehst du das bestehende Theme, und wie fügt sich deine Lösung darin ein?
- **Händler- und Kundensicht:** Ist das Ergebnis für beide Seiten sinnvoll und gut nutzbar?
- **Codequalität:** Lesbarkeit, Struktur und Wartbarkeit.
- **Eigenständigkeit & Kommunikation:** Wie du Lücken füllst, Prioritäten setzt und deine Entscheidungen begründest.

Viel Erfolg, wir freuen uns auf deine Lösung! 🚀
