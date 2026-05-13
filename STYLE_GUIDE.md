# Guia d'estil — Jornades Internacionals 2027

> Referència visual i de codi per al lloc web de les **I Jornades Internacionals d'Intercanvi d'Experiències de Millora en Polítiques i Serveis Públics** (Lima, 15–16 de juliol de 2027).
>
> Aquesta guia documenta l'estat actual de la maqueta (`index.html`) per garantir coherència en futures iteracions i en l'incorporació de noves pàgines o components.

---

## 1. Concepte i to visual

El registre és **editorial-institucional**: més a prop d'una revista acadèmica o d'un programa de congrés imprès que d'una landing tech. Les decisions de disseny haurien de reforçar aquesta lectura:

- Sobrietat per davant d'efectes vistosos.
- Contrastos cromàtics continguts: blau marí profund + dauradura sobre fons crema.
- Tipografia amb personalitat clàssica (serif d'editorial) combinada amb una sans-serif neta per al cos.
- Espai en blanc generós; densitat de la informació, mai de l'ornament.
- L'accent vermell només per a un element de senyalització, mai com a color decoratiu.

Si en el futur cal afegir components nous, la prova és: *quedaria bé imprès en un programa de paper de la conferència?* Si la resposta és no, probablement el component no encaixa.

---

## 2. Paleta de colors

Tots els colors es declaren com a variables CSS a `:root`. **No s'haurien d'introduir colors hardcoded** fora d'aquesta paleta sense afegir-los abans aquí.

| Variable | Valor | Ús previst |
|---|---|---|
| `--gold` | `#B8963E` | Color d'accent principal: logo, hover de navegació, botó primari, vores destacades |
| `--gold-light` | `#F5E8C8` | Fons de badges informatius, avisos (`.notice`) |
| `--gold-dark` | `#7A5E1F` | Text sobre fons clar quan es vol èmfasi daurat (preus, badges, hover invers) |
| `--ink` | `#1A1814` | Text principal i fons foscos (`.submit-box`, capçaleres de taula) |
| `--ink-mid` | `#4A4640` | Text de cos secundari (`.lead-text`) |
| `--ink-soft` | `#8A837A` | Text terciari, llegendes, etiquetes inactives |
| `--cream` | `#FAF7F2` | Fons general del lloc (`body`) |
| `--white` | `#FFFFFF` | Fons de targetes i blocs sobre el crema |
| `--red-peru` | `#C8102E` | **Reservat**: només per a l'etiqueta superior del hero |
| `--border` | `#E2DAD0` | Vores fines, separadors |

**Color de capçalera i peu:** `#1a3a5c` (blau marí). Actualment està hardcoded a `header`, `.hero` i `footer` — convindria promoure'l a variable (`--navy`) en una propera neteja.

### Regles d'ús del color

- El **vermell Perú** és exclusiu de l'etiqueta del hero. Si el necessitem en algun altre lloc (per exemple, una alerta crítica), cal repensar-ho com a sistema, no afegir-lo aleatòriament.
- El **daurat** és el fil conductor: vora esquerra de cards (`.topic-card`, `.notice`), vora superior de la caixa del premi, hover de navegació, accent en text dels titulars del hero (`.hero h1 em`).
- **No barrejar** `--gold` i `--gold-dark` al mateix component sense intenció clara: el daurat clar és per a fons, el daurat fosc per a text.

---

## 3. Tipografia

### Famílies

- **Display — `Playfair Display` (serif):** títols, números de preu, marca, valors de metadades. Pesos 400 i 600; cursiva 400 disponible.
- **Cos — `DM Sans` (sans-serif):** tot el text corregut, navegació, formularis, botons. Pesos 300, 400, 500.
- **Pes per defecte del cos: 300** (light). És deliberat — dona l'aire editorial. Si es passa a 400 globalment, es perd el to.

Càrrega via Google Fonts a `<head>`. Si s'afegeixen pesos, fer-ho a la URL d'importació, no com a `@import` dins del CSS.

### Escala (estat actual)

| Element | Família | Mida | Pes | Notes |
|---|---|---|---|---|
| `.hero h1` | Playfair | `clamp(1.6rem, 3vw, 2.6rem)` | 600 | Cursiva daurada per a la part destacada (`<em>`) |
| `.section-title` | Playfair | `1.9rem` | 600 | Subratllat amb `border-bottom` fi |
| `.day-header`, `.info-block h4`, `.topic-card h4` | Playfair | `1rem` | 600 | Títols de bloc |
| `.lead-text` | DM Sans | `1.05rem` | 300 | `line-height: 1.8`, `max-width: 740px` |
| Cos general | DM Sans | `0.85–0.95rem` | 300–400 | Variable segons component |
| Etiquetes / overlines | DM Sans | `0.7–0.78rem` | 500 | `text-transform: uppercase`, `letter-spacing: 0.08–0.18em` |
| Navegació | DM Sans | `0.78rem` | 400 | Majúscules, `letter-spacing: 0.08em` |

### Regla d'or

**Playfair per a coses que es llegeixen una vegada** (titulars, valors destacats, marca). **DM Sans per a tot el que es llegeix més d'una vegada** (paràgrafs, llistes, navegació, formularis).

Les **majúscules amb tracking ample** (`letter-spacing: 0.08em` o més) són la firma tipogràfica del lloc per a etiquetes, navegació i overlines. Mai aplicar majúscules a un títol Playfair.

---

## 4. Layout i espaiat

- **Amplada màxima** del contingut principal: `1100–1200px` (segons secció). Centrat amb `margin: 0 auto`.
- **Padding lateral** estàndard: `2rem`.
- **Amplada de lectura còmoda** (`.lead-text`): `max-width: 740px`. No fer paràgrafs a tota amplada de pantalla.
- **Graelles responsives**: `repeat(auto-fit, minmax(Xpx, 1fr))` per a cards (topics, members, dates).
- **Breakpoint únic**: `720px`. A sota, les graelles de dues columnes col·lapsen a una sola.

### Espaiat vertical entre seccions

- Entre títol de secció i contingut: `28–32px`.
- Entre blocs dins d'una secció: `40–48px`.
- Padding de `.tab-content`: `48px 0 80px`.

---

## 5. Components

### 5.1. Capçalera i navegació

- `<header>` sticky, fons blau marí, vora inferior daurada semitransparent.
- Logo en Playfair daurat, alçada fixa de `60px`.
- Menú horitzontal amb hover daurat. **Pendent**: no hi ha versió responsive del menú per a mòbil — és un *to-do* clar.

### 5.2. Hero

- Fons blau marí amb una **graella decorativa** generada per `repeating-linear-gradient` (40px). És un detall característic; conservar-lo.
- Etiqueta vermell Perú a sobre del títol.
- Títol Playfair amb una part en cursiva i daurat (`<em>`).
- Bloc de metadades inferior amb tres columnes: Dates / Seu / Modalitat.

### 5.3. Sistema de pestanyes (`.tabs-nav` + `.tab-content`)

- Una sola pestanya activa visible en cada moment (`display: block`).
- Pestanya activa: text `--gold-dark` + `border-bottom: 2px solid --gold`.
- Canvi via funció JS `showTab(id)` que també gestiona el `scrollTo` suau.
- Si s'amplien les pestanyes, **actualitzar el `tabMap`** dins de la funció.

### 5.4. Cards i blocs informatius

Tres variants principals, totes amb fons blanc i vora `--border`:

- **`.topic-card`**: vora esquerra `3px solid --gold`. Per a temes/àmbits.
- **`.info-block`**: títol Playfair amb separador inferior, llistes amb fletxa daurada `→` com a marcador.
- **`.member-card`**: més compacta, per a llistes de persones.

Patró de llista amb fletxa (signatura del lloc):
```css
.info-block ul li::before {
  content: '→ ';
  color: var(--gold);
}
```

### 5.5. Taules

Dos tipus:

- **`.schedule-table`** (programa): primera columna estreta (`150px`) amb hora, separador vertical, files de destacat (`.session-highlight`, fons `#FDF8EF`) i de pausa (`.session-break`, fons `--cream`).
- **`.fees-table`** (preus): capçalera fons `--ink` amb text `--gold`, files de secció amb fons `--cream` i text en majúscules. Preus en Playfair `--gold-dark`.

### 5.6. Botons

- **`.btn-gold`**: únic estil de botó del lloc. Fons daurat, text fosc, majúscules amb tracking, hover passa a `--gold-dark` amb text blanc.
- No hi ha botó secundari definit. Si en cal un, proposo: vora `1px solid --ink`, fons transparent, mateixa tipografia.

### 5.7. Avisos i banners

- **`.notice`**: fons `--gold-light`, vora esquerra `3px --gold`, text `--gold-dark`. Per a informació destacada però no urgent.
- **`.submit-box`**: bloc CTA fons `--ink`, per cridar a l'enviament de resums.
- **`.prize-box`**: vora superior `3px --gold` com a accent diferenciador.

### 5.8. Formulari de contacte

- Inputs amb vora `--border`, focus passa a `--gold`.
- Etiquetes en majúscules petites, color `--ink-soft`.
- Sense vora arrodonida (`border-radius: 0` implícit) — coherent amb l'estètica editorial.

### 5.9. Peu

- Fons blau marí, tres columnes (`2fr 1fr 1fr`) que col·lapsen a una a `<720px`.
- Marca en Playfair daurat.
- Línia de copyright inferior amb el nom complet de l'associació.

---

## 6. Convencions de codi

- **CSS dins de `<style>`** al `<head>` per ara (un sol fitxer). Si el projecte creix, separar en `styles.css`.
- **Variables CSS** per a tot el sistema cromàtic. Nou color = nova variable.
- **Sense frameworks** (ni Tailwind, ni Bootstrap). Mantenir-ho així llevat que hi hagi una raó forta.
- **Sense `border-radius`** generalitzat: el lloc és angular per disseny. Excepció: `.date-icon` (cercle).
- **Transicions** suaus i curtes (`0.2s`) només per a `color` i `background`. Evitar transicions de layout.
- Comentaris CSS amb format `/* ── SECCIÓ ── */` per separar blocs.

---

## 7. Idiomes i contingut

- **Idioma de la web: castellà** (`<html lang="es">`). És l'idioma natural per a una conferència a Lima amb públic llatinoamericà i espanyol.
- Aquesta guia està en català perquè és per a ús intern de l'organització.
- Si s'afegeix versió en anglès o català de cara al públic, cal preveure-ho com a sistema (selector d'idioma a la nav, no com a pàgines paral·leles).

### To del text

- Tractament formal (*usted* en castellà).
- Vocabulari institucional però llegible: "experiencias", "intercambio", "mejora verificable".
- Èmfasi amb `<strong>` i `<em>`, no amb majúscules ni colors.

---

## 8. Pendents coneguts

Llista de coses que la maqueta deixa obertes i que cal resoldre abans de publicar:

- Menú responsive (hamburguesa) per a mòbil.
- Promoure `#1a3a5c` a variable `--navy`.
- Integració del formulari de contacte amb un backend real.
- Embed real del Google Maps a `.venue-map`.
- Tots els camps marcats com `[Por confirmar]` (ponents, comitès, dotació del premi, restaurant de la cena de gala, domini de correu).
- Decidir si fa falta una versió en anglès i/o català de cara als participants internacionals.

---

*Última actualització: 1 de maig de 2026. Mantenir aquest fitxer al costat de `index.html` i actualitzar-lo cada vegada que s'introdueixi un patró visual nou o es modifiqui la paleta.*
