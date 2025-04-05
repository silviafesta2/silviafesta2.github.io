+++
title = "MySQL Database for Smart Buildings"
url = "database"
summary = "Design and Implementation of a MySQL database for intelligent monitoring and predictive analytics"
author = "silviafesta2"
draft = false
hero_thumb = "/images/smart-buildings.png"
hero_thumb_height = 200       # Altezza visibile in pixel
hero_thumb_offset_y = 130
tags = ["università di pisa","databases"]
featured = true
+++

# Project Specification
This project involves the design and implementation of a relational database using Oracle MySQL to support a Smart Buildings system, which manages construction, renovation, and structural monitoring of buildings. The system stores detailed architectural and geographic data, tracks construction progress and materials, and integrates sensor data for real-time safety assessment and predictive maintenance. Advanced data analytics features are required to evaluate structural risks, estimate damage after disasters, and recommend interventions. The database supports entity-relationship modeling, functional dependency analysis, and performance optimization through redundancy and normalization strategies.

> 📄 [click here](/doc/Progetto-A.A.21-22.pdf) to download the project specification

# Project Objective
The goal is to design and implement a relational database system capable of:
- Storing detailed information about buildings, rooms, sensors, actuators, and occupants.
- Efficiently handling real-time sensor data and control signals for actuators.
- Providing support for complex queries to assist in building automation and management decisions.

# Requirement Analysis
The requirements analysis phase was divided into several sub-areas to identify the specific data and functionalities required by the database system:

## General Area
In this area, information was gathered about the geographic location, building structures, and associated risks:
- **Geographic and Structural Information**: Buildings are identified by their geographic locations, types (single-family house, condominium, etc.), and detailed topologies. Each building comprises multiple floors, and each floor has a specific floor plan represented by polygons.
- **Rooms**: Each floor is subdivided into rooms, each with maximum width, length, and height. Rooms can have irregular shapes and serve various functions (bedrooms, bathrooms, storerooms).
- **Access Points**: Each room has access points such as doors, arches, or windowed openings. Details about these openings (dimensions, orientation) are essential for the database.
- **Risk Assessment**: Each geographic area is subject to risks like seismic and hydrogeological hazards. Risk coefficients for each area are dynamic, and their historical values must be stored for future analysis.
  
## Construction Area
This section details construction projects, materials, and progression:
- **Building Projects**: Projects include new constructions and renovations, each with unique codes, presentation, approval, and estimated completion dates.
- **Construction Materials**: Detailed information about materials (bricks, plaster, tiles, stones) used for construction or decorative purposes, their types, dimensions, costs, and suppliers.
- **Progression and Personnel Management**: Each construction project has defined stages of progress, recording timelines, involved workforces, assigned responsibilities, and workforce management.

## Monitoring Area
Dedicated to dynamic building monitoring:
- **Sensors and Measurements**: Smart buildings are equipped with sensors measuring parameters such as temperature, humidity, precipitation, accelerations, angular velocities, and structural displacements.
- **Data Storage**: Measurements are continuously stored with timestamps, associated with alerts triggered upon exceeding predefined thresholds, which are critical for structural safety assessment.

## Risk Analysis and Damage Monitoring Area
This area focuses on risk assessment and damage management:
- **Building Condition Monitoring**: The state of each building is continuously assessed based on sensor data, historical trends, and specific risk thresholds.
- **Calamity Management**: Information regarding calamities (type, date, severity, and geographical impact) is recorded, including automatic severity assessment based on sensor data.
- **Damage Recording**: Post-event damage assessments are stored, detailing affected areas, types of damage, severity, and the necessary interventions or sensor installations for continuous monitoring.

---

At the conclusion of this phase, a comprehensive glossary was developed. This glossary contains all identified terms and potential entities along with their precise definitions, in order to eliminate ambiguity in the following stages of documentation and design. Each term entry includes synonyms and relational links to other relevant concepts, which help inform the expected attributes of corresponding entities. The glossary is structured as a table with the following columns: Term, Description, Synonyms, and Links.


| Term  | Description | Synonyms   | Links     |
|----|--------|-------|---------------|
| Intonaco              | Wall coating material with both protective and aesthetic purposes, made of a hardening mortar with sand. | parete, materiale         | parete, materiale                      |
| Mattone               | Brick made of clay or concrete, usually parallelepiped-shaped, solid or hollow, used in masonry work. | muro, parete, materiale   | muro, parete, materiale, alveolatura   |
| Alveolatura di mattone | Internal cavity pattern in bricks, which may be empty or filled with insulating material. | alveolatura               | mattone                                |
| ...                   | ...                                                                         | ...                       | ...                                    |

---

# Conceptual Design: Entity-Relationship Diagrams
The conceptual design phase consists of a thorough modeling of the Smart Buildings database using Entity-Relationship (ER) diagrams. For each functional area of the system, a dedicated ER diagram has been developed to visually and structurally represent entities, relationships, attributes, and constraints. The modeling work has been further supplemented with comprehensive documentation, including data dictionaries and rules that are not immediately apparent from the diagrams alone.

## Functional Areas Covered
This phase includes the design of ER models for four primary areas:

- General Area
- Construction Area
- Monitoring Area
- Risk Analysis and Damage Monitoring Area

Each of these areas has been analyzed independently and documented with dedicated resources, as outlined below.

## Entity Data Dictionary
For each area, a detailed Entity Data Dictionary was created. This consists of a tabular summary where each row defines an entity and includes:

- **Entity Name**: the conceptual object modeled (e.g., Building, Floor, Wall, Sensor).
- **Description**: a concise explanation of the entity’s real-world meaning.
- **Attributes**: a list of fields with their respective data types (e.g., INT, FLOAT, VARCHAR(50)).
- **Identifier**: the primary key(s) uniquely identifying each record.

This dictionary facilitates clarity during database implementation and ensures all expected attributes are well-defined from the start.

## Association Data Dictionary
Complementing the entities, the Association Data Dictionary lists all relationships between entities. For each association, the following details are documented:
- **Name of the Relationship**
- **Description**
- **Participating Entities**
- **Attributes** (if the relationship is not binary or has its own properties)
This helps capture the logical structure of the database, ensuring correct cardinalities, join conditions, and additional properties of the associations.

## Constraint Documentation
To enforce data integrity beyond what the ER diagram can express, a full set of constraints and business rules was specified for each area. These include:
- **Business Rules**: Constraints based on real-world logic (e.g., a building must have at least one floor).
- **Tuple Constraints**: Conditions on single rows (e.g., wall thickness depends on whether it’s a load-bearing wall).
- **Inter-relational Constraints**: Rules involving multiple entities or relationships (e.g., a room must belong to a floor, which must belong to a building).

These constraints will later guide both the logical schema definition and physical database implementation to maintain consistency and accuracy of the data.

---
## Example of ER-scheme documentation for a single entity:
An example of documentation for a single Entity (copied from the original documentation, hence in Italian).
![edificio](/images/Edificio.png)

<br>

| Entity   | Description  | Attributes    | Identifier   |
|-----|-----------|-----------|--------------|
| Edificio | Mansory construction intended for residential or specific uses | IdEdificio (INT), AnnoCostruzione (DATE), Tipologia (VARCHAR(50)), Citta (VARCHAR(50)), Civico (INT), Via (VARCHAR(50)) | IdEdificio   |
| ...   | ...  | ...     | ...    |

<br>

Un `Edificio` e' identificato per mezzo di un ID progressivo (“IdEdificio”) ed e' caratterizzato
da un indirizzo (”Indirizzo”), una tipologia (“Tipologia”) e dall’anno di costruzione
(“AnnoCostruzione”).
- “Indirizzo” e' un attributo composto formato da “Citta”, “Via” e “Civico” che permette di
individuare in modo univoco la collocazione di un edificio all’interno della propria area
geografica. E’ possibile che in aree geografiche diverse gli indirizzi si ripetano, pertanto
“Indirizzo” (senza l’aggiunta di altri attributi) non puo' essere una chiave di “Edificio”,
l’indirizzo risulta invece essere unico all’interno di ciascuna area geografica esiste quindi un
vincolo che impedisce l’inserimento di edifici con stesso indirizzo all’interno della medesima
area geografica. Per l’identificazione di “Edificio” e' possibile scegliere tra un’identificazione
interna (per mezzo di un id progressivo) ed un’identificazione esterna (usando una chiave
esterna formata dall’attributo composto “Indirizzo” e dalle “Coordinate” dell’area
geografica all’interno della quale l’edificio ha sede). E’ stato scelto di adottare la prima
soluzione in quanto essa rende l’identificazione piu' immediata (la prima soluzione richiede
un unico attributo come chiave primaria mentre la seconda soluzione ne richiederebbe 5 di
cui 2 esterni).
- “IdEdificio” e' un identificatore numerico auto incrementale.
- “Citta” e' un attributo di tipo varchar(50) senza vincoli di dominio che indica la citta'
all’interno della quale l’edificio e' situato.
- “Via” e' un attributo di tipo varchar(70) senza vincoli di dominio.
- “Civico” e' un attributo di tipo int, questo puo' assumere solo valori positivi.
- “AnnoCostruzione” e' un attributo di tipo int che indica l’anno in cui l’edificio e' stato
completato (non quello in cui sono iniziati i lavori di costruzione), questo puo' assumere
valore null nel caso in cui l’edificio non sia ancora esistente (lavori di costruzione non
ancora iniziati oppure edificio in fase di costruzione). La presenza dell’attributo
- “AnnoCostruzione” permette sia di distinguere fra edifici esistenti e non (come richiesto da
specifiche) sia di condurre analisi statistiche sul deterioramento degli edifici nel tempo.
L’attributo “AnnoCostruzione” non e' ridondante in quanto, se non fosse presente, sarebbe
possibile stimare solamente l’anno di costruzione di edifici interamente costruiti da Smart
Buildings ma non di edifici presi in carico dall’azienda per ristrutturazioni (saranno
ovviamente necessari controlli di consistenza per quanto riguarda gli edifici interamente
costruiti da Smart Buildings). Affinch´e le date di completamento degli edifici
(AnnoCostruzione) non siano date stimate nel futuro e' previsto un vincolo che impedisce
l’inserimento di interi maggiori del valore dell’anno in corso al momento dell’inserimento.
- “Tipologia” e' un attributo di tipo varchar(50) che permette di classificare un fabbricato in
base alla presenza di determinate caratteristiche dimensionali, funzionali ed organizzative,
29
per non limitare la possibilita' di definire nuove tipologie di edificio ritenute di interesse
dall’azienda non sono stati previsti vincoli sul dominio di questo attributo; esistono
tuttavia alcune categorie consigliate di cui riportiamo le caratteristiche distintive:
  - **Casa unifamiliare**: edificio caratterizzato dalla presenza di una singola unita'
abitativa.
  - **Condominio**: edificio caratterizzato dalla presenza di piu unita' immobiliari con
caratteristiche comuni come la pianta o la suddivisione in vani di un piano.
  - **Fabbricato industriale**: edificio solitamente caratterizzato da grandi dimensioni e
ampi vani modulabili.
  - **Edificio storico**: edificio dall’importante valore storico-culturale, e' solitamente
caratterizzato da una grande complessita' e dalla numerosa presenza di dettagli
architettonici.

## Full ER-scheme

![schema-ER](/images/ProgettazioneLogica.png)

# ER Diagram Restructuring
After the conceptual modeling, it became necessary to refine the ER diagrams by restructuring them to improve clarity and align with the relational model. The restructuring focused on simplifying the diagrams and resolving modeling complexities that are not directly supported in relational schema translation.

This restructuring phase consists of three primary operations:
## Elimination of Generalizations
Generalizations were removed by replacing them with equivalent flattened structures. For each superclass-subclass relationship, two common strategies were considered:
- **Option 1**: Single Table Inheritance
All attributes of the superclass and subclass are merged into a single entity. A discriminator attribute is used to indicate the subtype.
- **Option 2**: Class Table Inheritance
A table is created for the superclass and each subclass, connected via foreign keys.

Examples:

In the General Area, the entity `Apertura` was generalized into sub-entities `Porta`, `Finestra`, `Arco`, and `Portafinestra`. These were flattened into a single table with conditional attributes and a type indicator field.

In the Construction Area, `ParteEdificio` and its specializations (e.g., `Parete`, `Pavimento`, `Solaio`) were denormalized similarly to allow direct referencing in relational schemas.

## Elimination of Multivalued Attributes
Attributes that could contain multiple values for a single entity instance were extracted into separate entities with one-to-many relationships. This process prevents the violation of first normal form.

Example:

The multivalued attribute `Funzione` in the `Vano` entity was extracted into a separate entity `FunzioneVano`, where each row represents one function of a room.

## Elimination of Composite Attributes
Composite attributes were replaced with their atomic components to comply with relational modeling principles.

Example:

The composite attribute `Indirizzo` of `Edificio` (consisting of `Via`, `Civico`, `Citta`) was split into individual atomic attributes, while maintaining a unique constraint on the combination to ensure address uniqueness per area.

# Identification of Interesting Data Operations
This section defines a set of representative operations that the system must support efficiently. These operations simulate real-world use cases and guided the design of indexes, optimization strategies, and the restructuring of the ER diagram to meet expected performance.

Each operation is analyzed in terms of:
- A **description** of its business purpose
- The **portion of the ER diagram** it involves
- A **volume table** estimating data size and query frequency
- An **access table** detailing involved attributes and relationships
- Any **redundancy** introduced to improve performance

## Volume Table
This table summarizes the expected data volume and query frequency for each main entity and operation. It helps in anticipating indexing needs and performance bottlenecks.

| Concept     | Type    | Volume | Reasoning                                                      |
|-------------|---------|--------|----------------------------------------------------------------|
| Edificio    | Entità  | 50     | Assumed as a base hypothesis                                   |
| Piano       | Entità  | 150    | 3 floors per building on average                               |
| Vano        | Entità  | 1500   | 10 rooms per floor on average                                  |
| ...         | ...     | ...    | ...                                                            |



## Example Operation: Reading the Topology of a Building
### Description
This operation allows querying the structural layout of a specific building, including the list of floors, rooms per floor, and their respective dimensions and access points.

### Relevant Portion of the ER Diagram
- Entities: `Edificio`, `Piano`, `Vano`, `Parete`, `Apertura`
- Associations: `CollocazionePiano`, `CollocazioneVano`, `DelimitazioneVano`

### Volume Table for the Operation
- Buildings: 10,000
- Average floors/building: 4
- Rooms per floor: 5
- Queries/day: ~500

## Access Table
| Entity     | Access Type | Attributes Needed                |
|------------|-------------|----------------------------------|
| Edificio   | Read        | IdEdificio, Tipologia           |
| Piano      | Read        | NumeroPiano                     |
| Vano       | Read        | Dimensioni, Funzione            |
| Apertura   | Read        | Tipologia, Altezza, Larghezza   |


# Logical Model
This phase consists of translating the conceptual design into the logical relational model. For each area of the system, entities, relationships, and constraints previously defined in the ER diagram are mapped to relational tables with primary and foreign keys.

The logical model respects normalization principles and integrates all integrity constraints (referential, domain, and tuple-level) derived during earlier design phases.

## Example Logical Model: General Area
The General Area concerns the physical structure of buildings, rooms, walls, and access points. Below is a sample of the main tables:

### Tables:
```sql
Edificio(IdEdificio, AnnoCostruzione, Citta, Civico, Via, Latitudine, Longitudine)

Piano(NumeroPiano, IdEdificio, IdParte)

Vano(IdVano, NumeroPiano, IdEdificio, Superficie, LarghezzaMassima,
     LunghezzaMassima, AltezzaMassima, AltezzaMinima)

AdibizioneVano(IdVano, NomeFunzione)

Funzione(NomeFunzione)

AccessoInternoEsterno(IdApertura, IdVano, IdParte)

AccessoInternoInterno(IdApertura, VanoIdMaggiore, VanoIdMinore)

AccessoProprieta(IdApertura, IdVano)

Apertura(IdApertura, IdParte, Larghezza, Altezza, Tipologia)

PortaFinestra(IdApertura, IsolamentoTermico, IsolamentoAcustico)

Porta(IdApertura, Materiale, Colore, Serratura)

Arco(IdApertura, Raggio)

Finestra(IdApertura, IsolamentoAcustico, 
IsolamentoTermico)

```

### Referential Integrity Constraints
- (Latitudine, Longitudine) of Edificio → AreaGeografica(Latitudine, Longitudine)

- Piano.IdEdificio → Edificio(IdEdificio)

- Piano.IdParte → Solaio(IdParte)

- (NumeroPiano, IdEdificio) of Vano → Piano(NumeroPiano, IdEdificio)

- AdibizioneVano.IdVano → Vano(IdVano)

- AdibizioneVano.NomeFunzione → Funzione(NomeFunzione)

- AccessoInternoEsterno.IdVano → Vano(IdVano)

- AccessoInternoEsterno.IdParte → ParteEsterna(IdParte)

- AccessoInternoEsterno.IdApertura → Apertura(IdApertura)

- AccessoInternoInterno.VanoIdMinore → Vano(IdVano)

- AccessoInternoInterno.VanoIdMaggiore → Vano(IdVano)

- AccessoInternoInterno.IdApertura → Apertura(IdApertura)

- AccessoProprieta.IdVano → Vano(IdVano)

- AccessoProprieta.IdApertura → Apertura(IdApertura)

- Apertura.IdParte → Muro(IdParte)

- PortaFinestra.IdApertura, Porta.IdApertura, Arco.IdApertura, Finestra.IdApertura → Apertura(IdApertura)


# Functional Dependency Analysis
The purpose of this phase is to identify the functional dependencies (FDs) that exist between attributes in each relation of the logical model. This analysis is fundamental for validating the quality of the schema and for guiding normalization or denormalization decisions where needed. In this case, apart from redundancies introduces to have better performances, the **Third Normal Form** should hold.

## Methodology
A complete analysis of all possible functional dependencies with a single attribute on the right-hand side is combinatorially complex (factorial in the number of attributes). Therefore, a full enumeration has been avoided, except for key examples like the Dipendente relation.

## Example: Functional Dependencies on `Dipendente(Matricola, Nome, Cognome, CodFiscale)`

| Dependency                            | Holds? | Motivation                                         |
|---------------------------------------|--------|----------------------------------------------------|
| Matricola → Nome, Cognome, CodFiscale | ✓      | Each employee ID uniquely identifies a person      |
| CodFiscale → Matricola, Nome, Cognome | ✓      | Fiscal code is unique per employee                |
| Nome → Matricola                      | ✗      | Many people can share the same name               |
| Cognome → Nome                        | ✗      | Same as above                                     |
| Matricola, Nome → CodFiscale          | ✓      | Combined, these ensure uniqueness                 |
| CodFiscale, Nome → Cognome            | ✓      | Not minimal, but valid                            |
| ...                                   | ...    | (Full matrix omitted for brevity)                 |

The table is followed by a logical justification of the dependencies:

- ✅ IdEdificio → all other attributes

- ✗ (Citta, Civico, Via) → Latitudine, Longitudine: same address can exist in multiple cities or areas.


- ✅ IdSolaio → (IdEdificio, NumeroPiano)

- ✗ IdEdificio → NumeroPiano: a building may have multiple floors.

# Custom Analytics
After completing the full documentation of the database design process—including requirements analysis, conceptual modeling, ER restructuring, logical schema translation, and dependency analysis—the final step involved the implementation of advanced analytics functionalities.

Among all custom analytics, the most significant is the computation of the **Stato dell’Edificio** (Building Status): a comprehensive indicator designed to estimate the health and safety of a building using sensor data.

![stato_edificio](/images/stato_edificio.png)

This metric was designed with the goals of sustainability and structural monitoring in mind, key aspects of Smart Buildings' mission.

## Building Status (Stato dell’Edificio)
Evaluating the status of a building is a complex operation involving periodic processing of large volumes of sensor data. To ensure performance and accessibility:
- The status is computed monthly.
- It is stored in a **materialized view**.
- The materialized value may be slightly outdated, but it is always available for analytics and decision support.

The building status consists of:

- A global numeric indicator: `StatoGenerale` (0–100).
- Three underlying coefficients:
    - `Danni` (Damage)
    - `AlertNonGestiti` (Unresolved Alerts)
    - `StatoSprechi` (Waste)
  
### Damage (`Danni`)

This coefficient is derived from the monitoring sensors that **did not trigger alerts**. For each sensor:

- All readings from the last month are collected.
- A **normalized progression score** is computed:



Where:
- \\( X \\) is the current measured value (or the vector magnitude for triaxial sensors).
- \\( X_0 \\) is the first value measured by the sensor upon installation.
- `soglia` is the sensor's safety threshold.

- A **damage score** is computed per sensor:

$$
\text{stato_danno} = 2 \cdot \overline{X}_{\text{rel}} + 3 \cdot \text{MaxV}
$$

Where:

- `\(\overline{X}_{\mathrm{rel}}\)` is the **average relative damage** over the past month.
- `\(\mathrm{MaxV}_{\mathrm{rel}}\)` is the **maximum relative worsening speed**, computed as:


And each pairwise worsening speed is computed as:

$$
V_p = \frac{X_{\text{rel}, 2} - X_{\text{rel}, 1}}{T_2 - T_1}
$$

Finally, the overall damage score for the building is calculated as:

$$
\text{Danni} = \frac{\sum_i E_i \cdot \text{stato\_danno}_i}{\sum_i E_i}
$$

Where:
- \( E_i \) is the **importance (Entità)** of the damaged component.

---

### Unresolved Alerts (`AlertNonGestiti`)

This value indicates the percentage of alerts that have not yet been addressed:

$$
\text{AlertNonGestiti} = \frac{\text{NumeroAlertNonGestiti}}{\text{NumeroAlertTotali}}
$$

---

## Waste (`StatoSprechi`)

#### Thermal Insulation:

$$
\text{isolamento} = \frac{\text{escursione termica interna media}}{\text{escursione termica esterna media}} \in [0, 1]
$$

#### Plumbing Leaks:

$$
\text{stato\_impianto\_idraulico} = \frac{\text{umidità media mensile}}{60}
$$

#### Combined Waste Score:

$$
\text{StatoSprechi} = \text{isolamento} + \text{stato\_impianto\_idraulico} \in [0, 2]
$$

---

### Final Aggregated Score: `StatoGenerale`

The overall health status of the building is computed as:

$$
\text{StatoGenerale} = 100 - 60 \cdot \frac{\text{Danni}}{5} + 10 \cdot \frac{\text{StatoSprechi}}{2} + 30 \cdot \text{AlertNonGestiti}
$$

All values are normalized between 0 and 1 before being applied.

- `Danni` weighs the actual and worsening state of structural damage.
- `StatoSprechi` quantifies inefficiencies.
- `AlertNonGestiti` highlights unresolved alarms.

The result ranges from **0 (critical)** to **100 (ideal)**, enabling **prioritized intervention planning**.

---
## Download documentation
> 📄 [click here](/doc/DB.pdf) to download the final documentation