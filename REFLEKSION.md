# Refleksion – Figma til kode

**Gruppemedlemmer:**
Katrine Bruhn og Vanest Jalal

## Eksempel 1: Push, pull og merge conflicts

### Hvor og hvorfor?

Vi oplevede problemer med push, pull og merge conflicts, når vi arbejdede sammen i det samme GitHub-repository. Det skete især, hvis vi begge havde lavet ændringer i den samme fil, for eksempel Header.astro.

For at holde vores lokale versioner opdaterede og sende ændringer til GitHub arbejdede vi blandt andet med:
git add .
git commit -m "beskrivelse af ændringer"
git push
git pull

Vi lærte, at det er vigtigt at lave git pull, inden man begynder at arbejde eller pusher sine egne ændringer. På den måde mindsker man risikoen for konflikter mellem forskellige versioner af de samme filer.

### Relevant kode

Et eksempel på vores normale workflow var:
git add .
git commit -m "responsive header"
git pull
git push

Hvis vi begge havde ændret de samme linjer, kunne Git ikke automatisk vælge, hvilken version der skulle bruges. Vi måtte derfor gennemgå merge conflicten og vælge de ændringer, vi ønskede at beholde.

### Afprøvning og ændringer

- **Vi testede:** At pushe og pulle ændringer mellem vores lokale projekter og det fælles repository.
- **Vi observerede:** At der kunne opstå merge conflicts, hvis vi begge havde ændret samme del af en fil.
- **Vi ændrede eller mangler:** Vi blev mere opmærksomme på at pulle de nyeste ændringer og kommunikere om, hvilke filer vi arbejdede i.

## Eksempel 2: Astro og komponenter

Det var en udfordring at arbejde med Astro og forstå, hvordan komponenterne arbejder sammen. Projektet var opdelt i flere komponenter, blandt andet header, cards og team-medlemmer.

Vi oplevede især problemer med styling, bredder og spacing, fordi komponenter kunne have deres egne max-width, margin og padding. Derfor skulle vi finde ud af, om et stylingproblem kom fra selve komponenten eller fra den sektion, komponenten blev brugt i.

Vi har placeret generel styling, som bruges flere steder på siden, i vores globale CSS, mens styling, der kun gælder for en bestemt komponent, ligger i den enkelte Astro-komponent. Det gjorde det nemmere at finde og ændre stylingen uden at påvirke resten af siden.

### Fallback / progressive enhancement

Vi har brugt CSS Grid til flere layouts på siden. Når browseren understøtter Grid, vises elementerne i det ønskede kolonnelayout. Hvis Grid ikke understøttes, vil indholdet stadig være tilgængeligt, men layoutet vil ikke blive vist på samme måde.

Vi har testet siden i Google Chrome på desktop og gennem Chromes responsive visning.

### Relevant kode

Vi brugte blandt andet komponenter til vores cards, så den samme struktur kunne genbruges flere steder:
<ServiceCard
  title="Creative Ideas"
  text="..."
  icon="..."
/>
På den måde behøvede vi ikke skrive den samme HTML-struktur for hvert card. I stedet kunne vi ændre indholdet gennem props og styre den fælles styling i komponenten.

Vi brugte også data til vores team-medlemmer og viste kun de første medlemmer på siden:
{employees.slice(0, 2).map((employee) => (
<TeamMember employee={employee} />
))}
Det gjorde løsningen mere dynamisk, fordi team-medlemmerne ikke skulle skrives manuelt direkte i HTML'en.

- **Vi testede:** Komponenterne på forskellige sider og med forskelligt indhold.
- **Vi observerede:** At styling i en komponent kunne påvirke layoutet anderledes end forventet, især i forhold til bredde og spacing.
- **Vi ændrede eller mangler:** Vi justerede blandt andet max-width, padding, margin og grid-layouts og blev mere opmærksomme på, hvor stylingen skulle placeres.

## Eksempel 3: Responsivitet

Vi oplevede udfordringer med at gøre siden responsiv. Det gjaldt blandt andet navigationen, hero-sektionen, billeder, tekst, bredder på sektioner, spacing og cards.

Layoutet fungerede på desktop, men nogle elementer fik for lidt plads eller stod forkert på mindre skærme. Derfor brugte vi media queries til at ændre layoutet ved mindre skærmbredder.

Et eksempel er vores header:

```css
@media (max-width: 700px) {
  .header-inner {
    grid-template-columns: 1fr auto;
  }
}
```

Her ændrer vi grid-layoutet, når skærmen bliver mindre end 700px, så headeren bedre kan tilpasse sig mobilvisningen.

Vi brugte samme princip andre steder på siden, hvor layouts med flere kolonner blev ændret til én kolonne på mindre skærme.

- **Vi testede:** Siden i forskellige skærmstørrelser gennem browserens responsive visning.
- **Vi observerede:** At nogle sektioner, cards, billeder og tekster ikke automatisk tilpassede sig mindre skærme.
- **Vi ændrede eller mangler:** Vi brugte media queries til blandt andet at ændre antal kolonner, bredder og spacing. På mobil lod vi flere sektioner gå fra flere kolonner til én kolonne.

## Brug af AI og andre hjælpemidler

Vi brugte MDN til dokumentation af CSS Grid og brugte ellers AI som hjælp. Vi testede løsningen i Google Chrome på desktop og gennem Chromes responsive visning.

Vi har brugt AI som hjælp under udviklingen, blandt andet når vi havde problemer med Astro, CSS, responsivitet og Git.

Vi brugte ikke altid løsningerne direkte, men tilpassede dem til vores egen kode og design. Vi kontrollerede ændringerne ved at køre projektet lokalt og teste, om resultatet fungerede og stemte overens med vores Figma-design.

AI hjalp os især med at forstå fejl og finde mulige løsninger. Vi lærte samtidig, at det er vigtigt at forstå den kode, vi indsætter, og teste den i vores eget projekt frem for bare at kopiere et svar.
