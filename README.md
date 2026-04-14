# Nemanjici Ontology 🏰

> RDF/SPARQL ontology of the medieval Serbian Nemanjić dynasty (1166–1371)

[![SPARQL](https://img.shields.io/badge/SPARQL-1.1-blue?style=flat-square)](https://www.w3.org/TR/sparql11-query/)
[![RDF](https://img.shields.io/badge/RDF-Turtle-green?style=flat-square)](https://www.w3.org/TR/turtle/)
[![Wikidata](https://img.shields.io/badge/Wikidata-Endpoint-orange?style=flat-square)](https://query.wikidata.org/)
[![Java](https://img.shields.io/badge/Java-21-red?style=flat-square)](https://adoptium.net/)

---

## 🔍 Overview

A formal ontology modeling the Serbian medieval dynasty of the Nemanjićs — covering rulers, churches, territories, battles, legal documents, and key historical figures. Built as part of a master's course project in Smart Grid Software Architecture.

The project includes:
- A **UML class diagram** designed in Enterprise Architect
- An **RDF/XML schema** exported from EA
- **Turtle (TTL) files** with 39 hand-crafted instances
- **20 SPARQL queries** of varying complexity (10 local + 10 Wikidata)

---

## 📁 Project Structure

```
Nemanjici/
├── 01_model/
│   ├── Nemanjici.qea                         ← Enterprise Architect project
│   ├── NemanjiciSchema-rdfs-augmented.xml    ← RDF/XML schema
│   ├── Nemanjici.ttl                         ← Ontology in Turtle format
│   └── Nemanjici.png                         ← UML diagram screenshot
│
├── 03_ttl/
│   ├── ttl-data/
│   │   ├── ontology.ttl                      ← Class & property definitions
│   │   ├── resource.ttl                      ← Instance data (39 instances)
│   │   └── prefixes.ttl                      ← Namespace prefixes
│   └── queries/
│       ├── 01.rq – 10.rq                     ← Local SPARQL queries
│       └── 11.rq – 20.rq                     ← Wikidata SPARQL queries
│
└── Nemanjici_Dokumentacija.pdf               ← Full project documentation
```

---

## 🧩 Ontology Model

### Classes (12 total)

| Class | Description | Inherits |
|-------|-------------|----------|
| `Osoba` | Base class for all persons | — |
| `Vladar` | Rulers with title and reign period | Osoba |
| `Svestenik` | Church officials | Osoba |
| `Plemic` | Nobles and regional lords | Osoba |
| `Dinastija` | Ruling family (Nemanjići) | — |
| `Drzava` | State entity (principality, kingdom, empire) | — |
| `Teritorija` | Geographic region under rule | — |
| `Bitka` | Military conflict with date and location | — |
| `PravniDokument` | Laws and charters | — |
| `Ugovor` | Interstate treaties | — |
| `Crkva` | Monasteries and churches | — |
| `Grad` | Cities and capitals | — |

### Enumerations (3 total)

| Enumeration | Values |
|-------------|--------|
| `TipVladara` | VelikaZupan, Kralj, Car, Knez, Despot |
| `TipTeritorije` | Zupanija, Kraljevina, Carstvo, Oblast, Zupa |
| `TipCrkve` | Manastir, Crkva |

### Key M:N Relation

```
Vladar ──── vladaoTeritorijom ────► Teritorija
       ◄─── vladao ─────────────────
```

One ruler can govern multiple territories, and one territory can be governed by multiple rulers across different time periods.

---

## 🗄️ Instance Data (resource.ttl)

| Class | Count | Examples |
|-------|-------|---------|
| Vladar | 10 | Stefan Nemanja, Stefan Dušan, Stefan Milutin... |
| Crkva | 6 | Studenica, Hilandar, Žiča, Gračanica, Dečani, Peć |
| Teritorija | 5 | Raška, Zeta, Kosovo, Makedonija, Hum |
| Drzava | 3 | Velika Županija, Kraljevina, Srpsko Carstvo |
| Bitka | 3 | Velbužd, Skoplje, Marica |
| Grad | 3 | Ras, Skoplje, Prizren |
| Svestenik | 2 | Sveti Sava, Joanikije II |
| Plemic | 2 | Vuk Branković, Lazar Hrebeljanović |
| PravniDokument | 2 | Dušanov Zakonik, Povelja Stefana Nemanje |
| Ugovor | 2 | Ugovor sa Vizantijom, Ugovor sa Mlečanima |
| Dinastija | 1 | Nemanjići |
| **Total** | **39** | |

---

## 💡 SPARQL Queries

### Local queries (01–10) — SPARQL Playground

| # | Title | Features |
|---|-------|----------|
| 01 | All rulers with titles | SELECT, ORDER BY |
| 02 | Monasteries with founders | JOIN, FILTER |
| 03 | Rulers whose name contains Stefan | CONTAINS |
| 04 | Number of churches per ruler | GROUP BY, COUNT |
| 05 | Succession chain | Self-reference |
| 06 | Battles with winners | OPTIONAL |
| 07 | Legal documents with issuers | JOIN |
| 08 | Rulers who governed 2+ territories | M:N, HAVING |
| 09 | Churches in Kosovo | Location filter |
| 10 | Clergy and their monasteries | OPTIONAL |

### External queries (11–20) — Wikidata

| # | Title | Wikidata properties |
|---|-------|-------------------|
| 11 | Serbian monastery founders | P31, P17, P112 |
| 12 | Medieval Serbian rulers | P27, P39 |
| 13 | Battles involving Serbia | P710, UNION |
| 14 | Children of Stefan Nemanja | P22 (father) |
| 15 | Medieval Serbian states | Q3024240, P571 |
| 16 | Members of Nemanjić dynasty | P53, CONTAINS |
| 17 | Serbian rulers with reign period | P39 qualifier P580/P582 |
| 18 | Serbian monasteries on UNESCO list | P757 |
| 19 | Details about Saint Sava | P569, P570, P27, P106 |
| 20 | Serbian participants at Kosovo 1389 | P607, P27 |

---

## 🚀 Getting Started

### Prerequisites

- Java 21 ([Adoptium](https://adoptium.net/temurin/releases/?version=21))
- SPARQL Playground master branch ([GitHub](https://github.com/calipho-sib/sparql-playground))

### Running Local Queries

```bash
# 1. Clone / download sparql-playground-master
# 2. Copy TTL files
cp 03_ttl/ttl-data/*.ttl sparql-playground-master/default/ttl-data/

# 3. Copy local query files
cp 03_ttl/queries/0*.rq sparql-playground-master/default/queries/

# 4. Start the playground
cd sparql-playground-master
start.bat         # Windows
./start.sh        # Linux/Mac

# 5. Open browser
# http://localhost:8888
```

> ⚠️ Use `sparql-playground-master` (Spring Boot 2.7.9), NOT v1.5.1 — it's incompatible with Java 21.

### Running Wikidata Queries

1. Open [https://query.wikidata.org/](https://query.wikidata.org/)
2. Paste the contents of any `11.rq` – `20.rq` file
3. Press **Ctrl+Enter** or click **Run**

---

## 🔧 Tech Stack

| Component | Technology |
|-----------|-----------|
| Modeling | Enterprise Architect (UML) |
| Schema format | RDF/XML |
| Data format | Turtle (TTL) |
| Query language | SPARQL 1.1 |
| Local endpoint | SPARQL Playground (Spring Boot 2.7.9) |
| External endpoint | Wikidata Query Service |
| Runtime | Java 21 |

---

## 📖 Namespace

```
http://iec.ch/TC57/NemanjiciSchema#
```

Used as `nemanjicischema:` prefix throughout all TTL and SPARQL files.

---

## 📚 Course

**Arhitektura softvera za upravljanje pametnim mrezama**
Master Academic Studies (MAS)
