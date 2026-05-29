# The Stibo STEP Training Handbook

### A complete, slide-by-slide study companion to the STEP (STIBO Systems) MDM/PIM platform

*Compiled from the 14-deck "Training Material Revamp" course — 301 slides in total.*

For every slide you get **what the slide says** and a **plain-language explanation** of the concept behind it. Each chapter opens with a 30-second mental model and closes with a revision cheat-sheet and a "how this connects" map.

---

*Edition: May 2026*

<div style="page-break-after: always;"></div>

# Table of Contents

**Front Matter**

- How to use this handbook & topic map  
- The big-picture mental model  
- Glossary of recurring concepts

**Chapters**

1. Data Modeling  
2. STEP ID, URL & Key  
3. STEP Functions  
4. Business Rules  
5. STEP Workflows  
6. Approvals, Revisions & Deletions  
7. Search, Collections & Bulk Updates  
8. Matching & Linking  
9. STEP XML  
10. Generic XML  
11. Tabular Format Import & Export  
12. Integration Endpoints  
13. Portals / Web UI  
14. Digital Asset Management  

<div style="page-break-after: always;"></div>

# Front Matter — How to Use This Handbook

> Slide-by-slide companion guides for the full *Training Material Revamp* set — **14 decks, 301 slides**. Each guide gives, for every slide, *what it says* + a plain-language *explanation of the concept*, plus a 30-second mental model up top and a revision cheat-sheet at the bottom.

---

### Suggested learning order

Work through them in this order — each builds on the ones before it.

| # | Guide | Slides | What it covers |
|---|---|---|---|
| 01 | **Data Modeling** | 20 | The foundation: objects, Product hierarchy vs Classifications, Entities, Assets, Attributes (Specification vs Description), validation types, References, Dimensions/Contexts, Workspaces/Approval |
| 02 | **ID, URL & Key** | 12 | The three ways to identify an object; how Keys let external systems find STEP data |
| 03 | **STEP Functions** | 15 | The Excel-like formula language; calculated attributes; `value/if/iterate/list`; performance |
| 04 | **Business Rules** | 22 | Conditions vs Actions vs Libraries; the 5 trigger points; UI plugins → Functions → JavaScript |
| 05 | **STEP Workflows** | 16 | States/Transitions, the Designer, concurrency, task assignment, rule order, variables, deadlines, monitoring |
| 06 | **Approvals, Revisions & Deletions** | 21 | Main→Approved lifecycle; data ownership; partial/recursive/context approval; revisions; deletion |
| 07 | **Search, Collections & Bulk Updates** | 33 | Goto vs Search tab; wildcards; full-text; criteria logic; collections; the no-undo bulk-update wizard |
| 08 | **Matching & Linking** | 23 | Deduplication: match codes, matching algorithms, Golden Records, survivorship, event processor |
| 09 | **Step XML** | 16 | STEP's native format (data + config); DTAP; reading the XML; nested vs flat; limitations |
| 10 | **Generic XML** | 14 | Import/export *other* systems' XML via templates + processing instructions |
| 11 | **Tabular Import/Export** | 23 | Everyday Excel/CSV: the 8-step import & 7-step export wizards |
| 12 | **Integration Endpoints** | 20 | Automated, monitored inbound (IIEP) & outbound (OIEP) pipelines |
| 13 | **Portals / Web UI** | 31 | Browser-based configurable UIs; screens, mappings, Designer, workflow integration, localization |
| 14 | **Digital Asset Management** | 35 | Asset import/recognition, maintenance, the 4 export mechanisms, external storage |

---

### How the topics fit together

```
                         ┌─────────────────────────────┐
                         │   01  DATA MODELING          │  ← everything starts here
                         │   (objects, attributes,      │
                         │    contexts, workspaces)     │
                         └──────────────┬──────────────┘
                                        │
        ┌───────────────┬──────────────┼───────────────┬──────────────────┐
        │               │              │               │                  │
   02 ID/URL/KEY   03 FUNCTIONS   06 APPROVALS     07 SEARCH/         14 DAM
   (identity)      (formulas)     /REVISIONS       COLLECTIONS/       (assets)
        │               │         /DELETIONS       BULK UPDATES
        │               │              │               │
        │          04 BUSINESS RULES   │          08 MATCHING
        │          (logic: uses 03)    │          & LINKING
        │               │              │          (uses 03,04,07)
        │          05 WORKFLOWS ───────┘
        │          (orchestration:
        │           uses 04, approvals)
        │
   DATA EXCHANGE LAYER
        ├── 09 STEP XML        (native format)
        ├── 10 GENERIC XML     (foreign formats)
        ├── 11 TABULAR I/O     (Excel/CSV)
        └── 12 INTEGRATION ENDPOINTS  (automates 09/10/11)

   FRONT END
        └── 13 PORTALS  (web UI over everything; surfaces 05 workflows, 07 search)
```

#### Key cross-connections
- **STEP Functions (03)** is the engine behind **Calculated Attributes** (01), **Keys** (02), **Business Conditions** (04), and **Match Codes** (08).
- **Business Rules (04)** run during **Approval (06)**, **Import (11/12)**, **Workflows (05)**, **Bulk Updates (07)**, and clerical review in **Matching (08)**.
- **Workspaces & Contexts (01)** shape **Approval (06)**, **Export options (11)**, and **Portal localization (13)**.
- **The XML formats (09/10)** are the payloads that **Integration Endpoints (12)** move; **Tabular (11)** converts to STEPXML internally.
- **Assets (14)** build on **References (01)** and **Revisions (06)**, and ship via **Export/OIEP (11/12)**.
- **Portals (13)** are the web front-end for **Workflow tasks (05)** and **Search (07)**.

---

### Recurring STEP concepts (glossary)

| Term | Meaning |
|---|---|
| **Object** | STEP's universal data unit (replaces tables/rows) |
| **Object Type** | Blueprint defined in System Setup; instances live in the Tree |
| **Product hierarchy (blue)** | The one true home of each product; supports inheritance |
| **Classification (yellow)** | Flexible groupings; many per product; no inheritance |
| **Entity** | Any non-product object (customers, suppliers, reference data) |
| **Asset** | Object pointing at a digital file |
| **Specification vs Description attribute** | Inheritable product-only (must be linked in) vs flat, any-object, auto-appearing |
| **Validation Base Type** | An attribute's data type + rules (GTIN, LOV, Number…) |
| **Reference** | Typed, directional (source→target) relationship |
| **Dimension / Point / Context** | Localization axis / one value / a combo "lens" |
| **Dimension dependent** | The switch that makes something localizable |
| **Main / Approved** | Editable draft workspace / read-only signed-off copy |
| **Workspace vs Globally revisable** | Two copies needing approval vs one shared copy |
| **Revision** | Coarse historical snapshot (who + when, not field-level) |
| **STEP ID / URL / Key** | Internal id / unique address / business-value identifier |
| **STEP Function** | Excel-like formula language used across the platform |
| **Business Condition / Action** | Logic that checks (true/false) / logic that does |
| **Workflow State / Transition / Task** | Process step / move between steps / assigned work item |
| **STEPXML** | STEP's native, comprehensive XML format |
| **Background Process** | Async job (imports, exports, recursive approve, bulk update) |
| **Bind** | A Java object exposed to JavaScript in rules/matching |
| **Sidecar** | The Java app on a remote host that receives Asset Push files |

---

### Study tips
- **Start with deck 01** and don't skip the Contexts/Workspaces slides — they recur everywhere.
- Each guide's **30-second mental model** is the best thing to re-read before an exam or interview.
- The **cheat-sheet tables** at the end of each guide are designed for last-minute revision.
- Watch for the **gotchas** flagged in each guide (e.g., bulk update has *no undo*; same MIME type → random asset type; mapping rules are *first-match-wins*; inherited values aren't exported by default).
- The repeated **template / "Attention" slides** at the start of most decks are training scaffolding, not STEP content — each guide notes them so you don't waste time on them.


<div style="page-break-after: always;"></div>

# Chapter 1. Data Modeling

> A slide-by-slide companion to the *Data Modeling* deck (20 slides). For each slide you get **what the slide says** and a **plain-language explanation** that teaches the concept behind it. This is the foundation deck — almost every other topic (Keys, Functions, Business Rules, Workflows, Import/Export) assumes you understand the ideas here.

---

### The 30-second mental model (read this first)

Stibo STEP is a **Master Data Management (MDM)** platform. Instead of tables/rows/columns like a normal database, STEP stores everything as **objects**. There are four main "real-world" object families:

- **Products** (things you sell) — live in the *blue* Product hierarchy
- **Classifications** (groupings/taxonomies, e.g. a website category tree) — *yellow*
- **Entities** (anything that is *not* a product — customers, suppliers, addresses, reference data)
- **Assets** (digital files — images, PDFs, Word docs, etc.)

Every object has **Attributes** (its data), can have **References** (relationships to other objects), and lives inside a structure (hierarchy). Data can be **translated/localized** using **Dimensions and Contexts**, and edits flow through **Workspaces** (Main → Approved) via **Approval**.

Keep that picture in your head; the slides below just fill in the detail.

---

### Slide 1 — Title
**On the slide:** "Stibo STEP L1 Training — Data Modeling."

**Explanation:** This is a *Level 1* (introductory) module. "Data modeling" here means *how you describe your business data inside STEP* — what objects exist, what fields they have, and how they relate.

---

### Slide 2 — About the Author
**On the slide:** Created by the Stibo CoE (Center of Excellence) team; version 1.0; based on Cognizant's certified curriculum with references to official STIBO documentation.

**Explanation:** Housekeeping slide. The useful takeaway: the *authoritative* source is STIBO's official documentation; this deck is a curated training layer on top of it.

---

### Slide 3 — Objects
**On the slide:** Objects in STEP can model products, non-product entities, classifications, and assets, as well as system functionality. A traditional relational database uses tables/columns/rows; STEP uses **objects with properties** to reach the same goal. Every item is an object whose properties are metadata: IDs, attributes with values, and references/links to other objects.

**Explanation:** This is the single most important conceptual shift. In a relational DB you'd say "the Product table has a Color column and a row per product." In STEP you instead say "this **Product object** has a **Color attribute** with the value *Red*, and a **reference** linking it to an image object." Everything — even configuration and system behavior — is represented as an object. Three property types to remember:
- **IDs** — identity metadata
- **Attributes** — the actual data values
- **References/Links** — relationships to other objects

---

### Slide 4 — STEP Object Type Model (Definition vs Instance)
**On the slide:** Object Types are *defined/configured* in **System Setup → Object Types & Structures**. *Instances* are created in the **Tree** and **System Setup**.

**Explanation:** This is the class-vs-object idea. The **Object Type** is the blueprint (e.g., "a *Shirt* object type has these attributes and can live at this level of the hierarchy"). An **instance** is a concrete object built from that blueprint (e.g., "*Blue Oxford Shirt, SKU 12345*"). You design types in **System Setup**; business users create instances in the data **Tree**. Whenever you hear "configure" think *System Setup / definition*; whenever you hear "create data" think *Tree / instance*.

---

### Slide 5 — Product Basics
**On the slide:** A product is something the retailer buys from a supplier and sells to a customer (a "sell-side product/item"). Variant products are versions of one product (e.g., a shirt in many sizes/colors — *PCM only*). Other product types: **Samples** (distributed, not sold), **Kits** (e.g., a repair kit linking to other products), **Packs** (a group containing other items), **Bundles** (products plus an installation service).

**Explanation:** "Product" is the core sellable thing. Note the special variations:
- **Variants** — one logical product with sub-versions (size/color). *PCM* = Product Content Management.
- **Kit / Pack / Bundle** — these are products that are *composed of* other products via references, not standalone items. The distinction matters when you model relationships later.

---

### Slide 6 — (Image-only slide)
**On the slide:** No text — a diagram/screenshot.

**Explanation:** A visual illustrating product structure. No concept to memorize; refer to the original deck image if you want the picture.

---

### Slide 7 — Product Basics: Buy Side vs Sell Side
**On the slide:** Distinguish products you **buy** (buy side — what you purchase from a supplier) from products you **sell** (sell side — what you sell to customers). Product data = anything describing it: name, identifiers (GTIN, EAN, SKU), descriptions (GPC attributes, marketing texts), pictures, links to other products, classification links. Three buy/sell patterns:
- Same product is bought and sold (1:1).
- Multiple bought products sold as one (*VDO only*).
- One bought product sold as several different products.

**Explanation:** Real supply chains are messy: you may buy "the same" item from three suppliers but sell it under one SKU, or split one purchased item into several sold products. STEP models both sides so the buy-side complexity doesn't pollute your clean sell-side catalog. *VDO* = Vendor Data Onboarding. **Identifiers to know:** GTIN (Global Trade Item Number, the barcode number), EAN (European Article Number), SKU (your internal stock-keeping unit).

---

### Slide 8 — Products in STIBO (the blue Product hierarchy)
**On the slide:** Product is the super-type for sellable items and their primary structure. Key rules:
- A Product exists **exactly once** in the blue Product hierarchy and **must** exist there.
- The blue hierarchy contains *only* Product objects.
- It supports **inheritance** of attribute values and category-specific attributes, so the hierarchy groups products by shared properties.
- The hierarchy is a **logical model**, not a presentation/display structure.
- It's typically strictly structured with different Product Object Types per level; real implementations are usually **4+ levels deep**.
- Classification "content" comes in two flavors: **GPC classification** (standard GPC attributes auto-attach to each level) and **Open classification** (you manually define attributes per node).

**Explanation:** The "blue hierarchy" (PPH = Primary Product Hierarchy) is the *one true home* of every product — each product appears once and only once. Inheritance is the payoff: put "Warranty = 2 years" on a category node, and every product beneath it inherits that value unless overridden. Crucially, **don't model it for the website menu**; model it by *shared data properties*. You build alternative display structures separately using Classifications (next slide). *GPC* = Global Product Classification (a GS1 standard).

---

### Slide 9 — Product Object Data (the editor anatomy)
**On the slide:** In the product editor: (1) the **Product tab**, (2) the **Description flipper** shows basic info, (3) a **thumbnail** if a primary image is referenced, (4) **Specification attributes** appear in flippers named after the attribute group, (5) fields are editable inline. A product object carries: parent in the Product hierarchy; ID/Name/Object Type; any number of Classification links, references to other products, references to assets, and links to specification attributes.

**Explanation:** "Flippers" are STEP's collapsible UI panels (you "flip" them open/closed). The slide is teaching you to *read the product editor*: identity at top (ID/Name/Type), the Description flipper for core info, image thumbnail, then groups of specification attributes. Everything an object "has" is one of: an attribute value, a classification link, a product-to-product reference, or an asset reference.

---

### Slide 10 — Classification Basics (the yellow hierarchy)
**On the slide:** Classifications build hierarchies that bundle objects into groupings. Super-type for alternative classification of products and for storing assets. Products exist once in the blue hierarchy but can be linked into **any number of yellow Classifications**. Common use: modeling website hierarchies and other taxonomies. Configured the same way as Products. Classifications can hold **Description attribute** values and references, **but there is no value inheritance** between classifications or from classifications down to products.

**Explanation:** Classifications are your *flexible, reusable* groupings — a product can sit in many of them at once (e.g., "Summer Sale," "Men's > Shirts," "Eco-friendly"). This is how you build multiple navigation trees without duplicating products. The big contrast with the Product hierarchy: **classifications do NOT push attribute values down**. Use the blue hierarchy when you need inheritance; use yellow classifications when you need many overlapping groupings.

---

### Slide 11 — Assets
**On the slide:** An asset is any product-related electronic file (images, Word, Excel, PDF, PowerPoint, text). STEP objects reference the file content (content can be **dimension dependent** and replaced/modified). STEP auto-identifies type from **MIME-type / file-header** info, auto-extracts metadata, allows any number of additional description attributes, and can **convert** assets in many ways on retrieval.

**Explanation:** An asset is an *object that points at a file*. STEP reads the file header to know it's a JPEG vs PDF, pulls metadata (dimensions, color profile, etc.) automatically, and can deliver transformed versions on the fly (resize a 4000px master into a 200px thumbnail at request time) — so you store one master and generate variants. "Dimension dependent content" means you can have a different image file per language/market (covered on slide 18). This whole area is expanded in the separate *Digital Asset Management* deck.

---

### Slide 12 — Attributes
**On the slide:** An attribute is a characteristic or detailed piece of information about an object, or about a relation between objects. Attributes are defined in **System Setup**, grouped into **Attribute Groups**.

**Explanation:** Attributes are your "fields/columns." Two things to note: (1) they're *defined centrally* in System Setup and reused across many objects (not redefined per product), and (2) attributes can describe not just an object but also a *relationship* (e.g., a reference can carry an attribute like "quantity = 3" on a kit-to-component link). Attribute **Groups** are just folders for organizing related attributes.

---

### Slide 13 — Attribute Types (Specification vs Description)
**On the slide:**
- **Specification Attributes:** apply only to Products; values inherit through the Product hierarchy; are *linked into* the hierarchy and viewable/editable on products below; values only allowed on object types the attribute is valid for (two validity concepts: **hierarchical** and **object-type** validity).
- **Description Attributes:** apply to all object types that can hold values; **no inheritance**; appear automatically on objects, links, and references they're made valid for (not "linked in" like specification attributes).

**Explanation:** This is a frequently-tested distinction.
- **Specification attributes** = product-only, *inheritable*, and you must explicitly **link** them into the hierarchy at the level you want. Validity is two-fold: *hierarchical* (which branch they're attached to) and *object type* (which types may hold them).
- **Description attributes** = work on any object/link/reference, do **not** inherit, and appear *automatically* once made valid — no linking step.
Rule of thumb: need inheritance down a product tree → specification; need a flat field anywhere (entities, links, references) → description.

---

### Slide 14 — Attribute Validation Base Types
**On the slide:** Every attribute has a **Validation Base Type** (directly or via a referenced List of Values). It strictly limits valid input. The deck lists the full set, including: **Condition, Date, Embedded Number, Fraction, GLN, GTIN (and GTIN-8/12/13/14), Integer, ISO Date, ISO Date and Time, LOV, Number, Number Range, Numeric Text, Numeric Text (exclude tags), Regular Expression, Text, Text (exclude tags), URL, Validation Templates.**

**Explanation:** The validation base type is the attribute's *data type plus its rules*. Highlights worth remembering:
- **Text / Numeric Text** — free text; "(exclude tags)" variants don't count style/markup tags toward length limits.
- **Integer vs Number** — whole numbers vs any numeric (decimals, negatives); fractions like "50 1/2" are invalid for both (use **Fraction**).
- **Number Range** — e.g., `1.2-3.6`; first value must be ≤ second.
- **GTIN / GLN family** — validate *length and check digit* of standard trade/location numbers (catches typos automatically).
- **Date / ISO Date / ISO Date and Time** — date entry against a fixed mask (e.g., `YYYY-MM-DD`).
- **LOV** — value must come from a defined **List of Values** (e.g., Red/Green/Blue).
- **Regular Expression / Validation Templates** — custom pattern rules when the built-ins aren't enough.
- **Embedded Number** — stores prefix, number, unit, suffix separately (e.g., `≈35°C`).
The point: STEP enforces data quality at entry time based on this type.

---

### Slide 15 — Other Important Attribute Settings
**On the slide:**
- **Externally Maintained (Yes/No):** controls whether the attribute is *revised*. Externally-maintained attributes have the same value in all workspaces, don't store old versions, and changing them doesn't affect an object's approval status.
- **Dimension Dependencies:** controls whether the attribute can hold context-specific values.
- **Mandatory (Yes/No):** can the object be approved without a value? (Also configurable on Product→Attribute links.)
- **Full Text Indexable (Yes/No):** index words for wildcard-free search (use sparingly, only for real business need).
- **Calculated attributes:** values not stored in the DB; computed on the fly from other data.
- **Type / Description / Specification** and **Attribute Help Text** (a useful message shown to end users).

**Explanation:** These switches change behavior in big ways:
- **Externally Maintained** = "this value comes from an external source of truth, treat it as raw, skip the revision/approval machinery." Good for things like supplier-fed data.
- **Dimension Dependent** = "this value can differ per language/market" (e.g., the product name).
- **Mandatory** = approval gate: the object can't be approved until this is filled.
- **Full Text Indexable** = makes a field searchable but costs index space/performance — enable deliberately.
- **Calculated** = derived value (e.g., price incl. tax) recomputed dynamically rather than stored.
- **Help Text** = inline guidance for data stewards.

---

### Slide 16 — Entity
**On the slide:** An entity is *any object not defined as a product* — commonly customers, contacts, addresses, markets, or reference data, but usable for any modeling scenario.
Product features **NOT** available to Entities: specification attributes (so no category-specific attributes / hierarchical inheritance), classification in a classification hierarchy, tables, offline translation, GDSN tracking & packaging hierarchies, DTP functionality.
Entity features **NOT** available to Products: object-type-specific revisability settings (workspace-revisable / global-revisable), and the option to display reference target/source objects as children (which lets you build entity classification hierarchies from entities).
Example: an **address** entity with description attributes City, Country, State, Street, Zip plus Name; modeled as *globally revisable*, so approval isn't applicable and the Approval Status field isn't shown.

**Explanation:** "Entity = everything that isn't a product." Entities are leaner: no inheritance, no specification attributes, no tables. But they gain flexibility products don't have — notably **global revisability** (no Main/Approved approval cycle) and the ability to build their own hierarchies by displaying referenced entities as children. Use entities for master data *about* the business (customers, suppliers, locations, reference/lookup data) rather than the sellable catalog. *GDSN* = Global Data Synchronization Network; *DTP* = Desktop Publishing.

---

### Slide 17 — Reference Types
**On the slide:** References define a connection between two objects, creating rules for the relationship. The reference type name refers to the **target** of the reference (e.g., Product Reference Types target product objects). Allowed connections:
- **Product Reference Types:** Classification→Product, Product→Product, Entity→Product
- **Image/Document Reference Types:** Classification→Asset, Product→Asset, Entity→Asset
- **Classification Reference Types:** Classification→Classification, Product→Classification, Entity→Classification
- **Entity Reference Types:** Classification→Entity, Product→Entity, Asset→Entity, Entity→Entity, Publication→Entity
- **Context Reference Types:** Entity→Context
- **Workspace Reference Types:** Entity→Workspace

Each reference has a **direction**: one object is the **source**, the other the **target** (example: order code 98332 is the source, its component order codes are targets).

**Explanation:** References are *typed, directional relationships*. The type is named after what it points **to** (a "Product Reference Type" always ends at a product). Direction matters: **source → target**. This is how you model accessories, replacements, kit components, "products in this classification," asset links, and so on. References can also carry their own description attributes (e.g., a "quantity" on a kit-to-component reference). The allowed-connections table tells you which object families a given reference type may legally join.

---

### Slide 18 — Dimensions, Dimension Points & Contexts (localization)
**On the slide:** A **Dimension** could be "Language" with **Dimension Points** English/French/German, or "Country" with Germany/France. A **Context** groups one (and only one) dimension point from each dimension. Systems typically have a **Global Context** grouping the top dimension points so data entered there is inherited by sub-contexts. **Data is stored in dimension points, not in contexts.** To place data into different dimensions, the object type, attribute, and/or reference type must be made **dimension dependent**. Object types, attributes, reference types, and assets can be dimension dependent when they need different names, LOVs, or linked assets/objects per context (usually translation, sometimes market-specific differences).

**Explanation:** This is STEP's localization engine and it confuses everyone at first, so go slow:
- A **Dimension** is an axis of variation (Language, Country/Market).
- A **Dimension Point** is one value on that axis (English; Germany).
- A **Context** is a *combination* — exactly one point per dimension (e.g., {Language=French, Country=Canada}). A context is the "lens" you view/edit data through.
- **Storage rule:** the actual value lives on the **dimension point**, and a context just *assembles* the relevant points. That's why entering data in a **Global Context** flows down into more specific child contexts (inheritance again).
- Nothing is localizable *unless you mark it* **dimension dependent**. A dimension-independent attribute has one shared value everywhere; a dimension-dependent one can have a different value per context (e.g., the product name in each language).

---

### Slide 19 — Module Complete
**On the slide:** "You have successfully completed Data Modeling of Stibo STEP L1 Training."

**Explanation:** Wrap-up marker. (Note: slide 20 below adds Workspaces/Approval content that appears after this completion slide — make sure you don't skip it.)

---

### Slide 20 — Workspaces, Approval & Revision
**On the slide:** Workspaces hold different **revisions** of data. The two primary workspaces are **Main** (the editable working area) and **Approved** (verified data ready for publishing). You generally **cannot edit directly in Approved**; data gets there via the **Approve** operation in Main. New revisions are created when: a revisable object is created, approved, modified after approval, or modified by a *different* user than the one who triggered the previous revision. **Externally Maintained** attributes don't need approval — their values populate Approved as soon as they're added/edited in Main. Approvals can be **partial** and **context-specific**. Objects copy to Approved via *Object → Approve object* or automatically on system approval events.

**Explanation:** This is STEP's editorial workflow in miniature:
- **Main** = your sandbox/work-in-progress (editable).
- **Approved** = the clean, signed-off copy (read-only; the version downstream systems publish from).
- **Approve** = the action that copies Main's current state into Approved and creates a new **revision** (a saved historical version).
- **Revisions** = STEP's version history; a new one is cut on create/approve/post-approval edit/changed editor.
- **Partial & context-specific approval** = you can approve, say, just the English values without approving the whole object.
- **Externally Maintained** attributes bypass this entirely (they sync straight through) — connecting back to slide 15.
This Main→Approved→Revision model underpins the *Approvals, Revisions and Deletions* and *Workflows* decks.

---

### Quick-revision cheat sheet

| Concept | One-line memory hook |
|---|---|
| Object | STEP's universal unit; replaces tables/rows |
| Object Type vs Instance | Blueprint (System Setup) vs actual data (Tree) |
| Product / blue hierarchy | Sellable item; lives **once**; **inherits** values |
| Classification / yellow | Flexible groupings; product can be in many; **no** inheritance |
| Entity | Anything not a product; no spec attributes/inheritance; can be globally revisable |
| Asset | Object pointing to a file; auto type/metadata; on-the-fly conversion |
| Attribute | A field; defined in System Setup, grouped |
| Specification attr | Product-only, inheritable, must be **linked in** |
| Description attr | Any object/link/reference, no inheritance, auto-appears |
| Validation Base Type | The attribute's data type + rules (GTIN, LOV, Number…) |
| Reference | Typed, **directional** (source→target) relationship |
| Dimension / Point / Context | Axis / one value / a combo lens for localization |
| Dimension dependent | The switch that makes something localizable |
| Main / Approved | Editable work area / read-only signed-off copy |
| Revision | A saved historical version, cut on create/approve/edit |


<div style="page-break-after: always;"></div>

# Chapter 2. STEP ID, URL & Key

> A slide-by-slide companion to the *ID, URL, KEY* deck (12 slides). This deck answers one practical question: **"How do you identify a single object in STEP — internally, in the API, and from an outside system that doesn't know STEP's internal IDs?"** Three answers: **ID**, **URL**, and **Key**.

---

### The 30-second mental model (read this first)

- **STEP ID** — an object's *internal* identifier. Permanent, unchangeable, **not** unique on its own (two different *types* of object can share an ID).
- **STEP URL** — ID **+** node-type info combined into something that **is** unique; used for navigation and in the SOAP API.
- **Key** — a *business* identifier built from one or more **attribute values**, so an **external system** can find a STEP object without ever knowing its internal ID.

Think of it like a person: the ID is your internal database row number, the URL is "row number + which table," and the Key is "find the person whose passport number = X."

---

### Slide 1 — Read Me First (template guidelines)
**On the slide:** Internal slide-design guidance: follow the "How to avoid Death by PowerPoint" principles and the LCD/ABC training model; template slides carry guidelines that can be removed via Slide Master.

**Explanation:** Not course content — it's authoring instructions for whoever built the deck (how to format training slides, where the reusable template guidance lives, how to strip it out). You can skip this for learning purposes.

---

### Slide 2 — Title
**On the slide:** "Introduction to STEP ID, STEP URLs and Keys — STIBO CoE Team." Marked stage **"A"** (the introduction stage of the ABC training model).

**Explanation:** Section opener. Sets up the three identifier mechanisms you'll learn.

---

### Slide 3 — Module Objectives
**On the slide:** On completion, the trainee will understand STEP object-identifier concepts and be able to perform related tasks for: **STEP ID, STEP URL, Unique Key.**

**Explanation:** The learning contract. By the end you should be able to (1) read/recognize an ID, (2) read/build a STEP URL, and (3) define and activate a Key. Keep these three buckets separate in your mind.

---

### Slide 4 — STEP ID
**On the slide:** All **Tree** and **System Setup** objects have an ID. The ID **cannot be omitted** and **cannot be changed**; because it identifies an object it's the **same across all Contexts and Workspaces**. But IDs are **not unique** across **Node Types** — you can't have two Products with the same ID (if same object type), but you *can* have a Product, a Classification, and an Attribute that all share one ID. **Avoid spaces** in IDs. To get a truly unique identifier you must combine the ID with Node-Type information — which is exactly what a **STEP URL** does.

**Explanation:** The ID is identity bedrock: assigned once, never edited, identical no matter which language/context or which workspace (Main/Approved) you look at. The subtle gotcha: an ID is only unique *within a node type*. "node type" = the broad category (Product, Classification, Attribute, Reference, etc.). So `ABC123` could simultaneously be a product, a classification node, and an attribute. That's why the ID alone isn't a safe global key — you must also say *what kind of thing* it is. Practical tip: no spaces in IDs (they break URLs/APIs/imports).

---

### Slide 5 — Auto Generate ID
**On the slide:** STEP can auto-generate IDs for specific object types. Use it for objects that are **created often** and objects **created by end users**. **Note:** there's no guarantee an auto-generated ID isn't already in use by an existing object — this can happen when IDs are generated *both* automatically *and* manually (e.g., via import) and may produce an error.

**Explanation:** Rather than make a data steward invent a unique ID every time, STEP can mint one automatically. Good for high-volume, user-created objects. The warning is the real lesson: **don't mix** auto-generation and manual/import-assigned IDs on the same object type, or an auto number can collide with one that already exists and the create fails. Pick one strategy per object type.

---

### Slide 6 — STEP URL
**On the slide:** STEP URLs are used for navigation in the workbench and **extensively in the SOAP API**. Example URL pointing to the product with ID `wfObj_4234273` in the Dutch context (`context4`) and Main workspace:
`step://product?editor=Product&contextid=context4&id=wfObj_4234273&workspaceid=Main`
External systems that update STEP data typically **don't know** STEP IDs or URLs — so for them, **Keys** are used instead.

**Explanation:** A STEP URL is a fully-qualified address to one object *in a specific context and workspace*. Decode the example:
- `step://product` — the node type (product)
- `editor=Product` — which editor to open
- `contextid=context4` — the lens (here, Dutch)
- `id=wfObj_4234273` — the object's ID
- `workspaceid=Main` — Main vs Approved
Because it bundles ID + node type (+ context + workspace), the URL **is** unique — solving the "ID isn't unique alone" problem from slide 4. It's perfect *inside* STEP and for SOAP API calls. But it's useless to an external system that has never seen STEP's internal IDs — which is the bridge to Keys.

---

### Slide 7 — Keys: Definition
**On the slide:** The Key concept lets an external system identify a STEP object **not by ID/URL but by one or more attribute values**. A Key is a *string representation of an object that is unique for a specific key definition* — no two objects can share a key; it's an **alternative identifier**. A **Key definition** has an ID and a state and specifies:
- One or more **Object Types** the key applies to (**Product, Entity, Classification, Asset** only)
- One or more **Attributes** whose values build the unique key
- A **STEP Function** that generates/calculates the actual key

**Explanation:** A Key flips identification around: instead of "tell me STEP's ID," you say "find the object whose *SupplierPartNumber = 55489-W*." That works for outside systems because they already know business values like part numbers and barcodes. A **Key definition** is the configuration that says *which object types, which attribute(s), and which Function* combine into the key string. Note it only applies to Product/Entity/Classification/Asset (not, say, system-setup objects). The **Function** is what concatenates/transforms the attribute values into the final key string (see the *STEP Functions* deck).

---

### Slide 8 — Key Attribute Considerations
**On the slide:** Attributes chosen to build a key **must**:
- Be **valid** for the selected object types
- Be **externally maintained** (same value across all workspaces)
- Be **single-valued**, and if specification attributes are used, the values must be **local**
- **Not** be **dimension dependent** (same value across all contexts)
- **Not** be a **calculated** attribute (a single change could force re-calculating millions of keys)
- Be **≤ 1,000 characters**
- If a validation-base-type **LOV** is used, the LOV must not be dimension dependent and length must be ≤ 1,000 characters

**Explanation:** A key must be **stable, global, and unambiguous**, which dictates these rules:
- **Externally maintained + not dimension dependent** → the value is identical in every workspace and every language/market, so the key never shifts depending on which lens you view it through.
- **Single-valued + local** → one definite value, not a list and not inherited from elsewhere.
- **Not calculated** → calculated values can change as a side effect of other edits; if keys depended on them, one edit could trigger mass key recomputation (huge performance risk).
- **Length cap (1,000 chars)** → keys are indexed strings; keep them bounded.
In short: pick attributes that are *guaranteed identical everywhere and don't move*, like a clean external part number.

---

### Slide 9 — Defining Keys
**On the slide:** Key definitions are created/maintained in **System Setup → Keys**. To create one: **right-click "Keys" → "Create Key"**, then give it an **ID** and a **Name**.

**Explanation:** Mechanics. Keys live under System Setup (they're configuration, not data). Creating one is the same right-click-create pattern used throughout the workbench. At this point you've only made an empty key definition — you still need to fill in its object types, attributes, and function (next slide).

---

### Slide 10 — Defining Keys (continued)
**On the slide:** In the new key's editor you specify **Object Type(s), Attribute(s), and Function**. The slide shows a simple **non-composite** key definition.

**Explanation:** This is where the key definition gets its substance. A **non-composite** key is built from a *single* attribute (e.g., key = the GTIN). A **composite** key combines *several* attributes (e.g., SupplierID + SupplierPartNumber) so the combination is unique even when no single field is. The **Function** stitches the chosen attribute values into the final key string.

---

### Slide 11 — Activation of Key
**On the slide:** A newly-configured key is **inactive** and must be **activated**. Activation runs a **Background Process** that calculates and stores keys for affected objects; the key becomes active **only if unique keys can be created for all objects**. Once active, in the workbench the key-attribute fields with values become **read-only** — only users with the special **'Modify unique key value'** privilege can change them (*Edit menu → 'Edit Unique Key Values'*). The value **cannot** be updated via import or APIs after activation.

**Explanation:** Activation is a validation gate: STEP tries to compute a key for *every* affected object, and if **any** two would collide (non-unique), activation **fails** — guaranteeing keys are genuinely unique once live. After activation, STEP *protects* the key attributes: they go read-only so a casual edit (or an import/API) can't silently break identity. Only a privileged user, using a special menu action, may change a key value. This is why slide 8's "stable" requirement matters — once a key is live, its source attributes are effectively frozen.

---

### Slide 12 — Thank You / Contact
**On the slide:** "Thank You — STIBO CoE Team — Contact Information."

**Explanation:** Closing slide. No content.

---

### Quick-revision cheat sheet

| Mechanism | What it is | Unique? | Who uses it |
|---|---|---|---|
| **STEP ID** | Internal identifier, permanent & unchangeable, same across contexts/workspaces | **No** — only within a node type | Internal references |
| **STEP URL** | ID + node type (+ context + workspace) | **Yes** | Workbench navigation, SOAP API |
| **Key** | Built from business **attribute value(s)** via a Function | **Yes** (enforced at activation) | **External systems** (imports/integrations) |

**Key definition needs three things:** Object Type(s) + Attribute(s) + a Function.
**Key attributes must be:** externally maintained, single-valued, *not* dimension dependent, *not* calculated, ≤ 1,000 chars.
**Activation:** background process; succeeds only if all keys are unique; afterwards key fields are read-only (no import/API edits; only the special privilege can change them).

---

#### How this connects to other modules
- The **Function** that builds a key is covered in the **STEP Functions** deck.
- "Externally maintained" and "dimension dependent" come from **Data Modeling** (slides 15 & 18).
- Keys are the backbone of **Import/Integration** decks — they're how inbound data maps to existing STEP objects.


<div style="page-break-after: always;"></div>

# Chapter 3. STEP Functions

> A slide-by-slide companion to the *STEP Functions* deck (15 slides). STEP Functions are STEP's built-in **formula language** — think "Excel formulas, but for your master data." They power **Calculated Attributes**, **Keys**, **Business Conditions**, and more. This deck focuses on using them for calculated attributes.

---

### The 30-second mental model (read this first)

A STEP Function is a small formula that *reads other data in STEP and returns a value*. It's a **functional language** (very Excel-like): you nest functions, pass arguments, and get a result. You don't store the result — STEP recomputes it on demand. The most important building block is `value('attributeID')`, which fetches another attribute's value. Everything else is conditionals (`if`), text assembly (`list`), and looping over related objects (`iterate`).

---

### Slides 1–2 — Template / "Attention" intro slides
**On the slides:** Slide-design template guidance and the "Attention (What/How/Duration)" trainer framework.

**Explanation:** Authoring scaffolding from the training template, not STEP content. Skip for learning. (These same two template slides open most decks in this set.)

---

### Slide 3 — Module Objectives
**On the slide:** After this module you'll be able to **create calculated attributes** in STEP and know the **different functions** used to build them.

**Explanation:** The goal is practical: build attributes whose value is *computed* rather than typed in, using the function library.

---

### Slide 4 — Title
**On the slide:** "STEP Functions — STIBO CoE Team."

**Explanation:** Section divider.

---

### Slide 5 — What STEP Functions Are
**On the slide:** STEP Functions are built on a **functional programming language very similar to Excel's** formula language. They have several uses across STEP (the slide references a usage table).

**Explanation:** This is the key framing. If you can write `=IF(A1>B1,"WARNING","OK")` in Excel, you can read STEP Functions — same idea, different data source (STEP attributes instead of cells). Beyond calculated attributes, the *same* language is used in **Keys** (building the key string), **Business Conditions/Actions**, export mappings, and more. Learn it once, reuse it everywhere.

---

### Slide 6 — Calculated Attributes
**On the slide:** Calculated attributes are **not stored in the database** — their value is **computed on the fly** from other STEP data (e.g., when a product editor is displayed or an object is exported). Example: a calculated attribute "Dimensions with CM Units" shows Height × Width × Length, all in cm.

**Explanation:** A calculated attribute is a *derived* field. Because it's never persisted, it's always current — change Height, and the "Dimensions" string updates automatically the next time it's read. Computation happens at **read time** (opening the editor, exporting, publishing), which is why performance matters (slide 14). Classic uses: combining fields ("H × W × L"), formatting/units, status flags ("Enriched?"), price-with-tax.

---

### Slide 7 — Setup
**On the slide:** Make an attribute calculated by setting **"Calculated = Yes"** on the Attribute object editor. A **"Value template"** field then appears. Once calculated, **most normal attribute settings no longer apply** (the deck marks them in red).

**Explanation:** The toggle that turns an ordinary attribute into a calculated one. The moment you flip it, STEP shows the **Value template** (where the formula lives) and *disables* settings that no longer make sense — e.g., you can't set a value manually, mandatory/validation rules don't apply the same way, because the value is produced by the formula, not entered or stored.

---

### Slide 8 — The Value Template Field
**On the slide:** To edit/insert a function: click into the **Value template** field (so you see the cursor), **right-click → "Insert Function" / "Edit Function"** to open the **Function editor**.

**Explanation:** Pure mechanics — how you get from the attribute editor into the formula editor. The Value template holds the formula text; the Function editor is the friendlier place to write and test it.

---

### Slide 9 — The Function Editor
**On the slide:** The Function editor is where you **define and test** functions.

**Explanation:** Like Excel's formula bar plus a preview. You write the function and test it against a sample object to see the computed result *before* committing — catch errors early rather than discovering a broken formula across thousands of products.

---

### Slide 10 — Available Functions
**On the slide:** (Reference screenshot of the function catalog.)

**Explanation:** STEP ships a large library — value access, math, text, date, logical, list/iteration, and object-navigation functions. The next slides cover the handful you'll use constantly.

---

### Slide 11 — Common Functions for Accessing Values
**On the slide:**
- `value(attribute-id)` — the attribute's value (no unit)
- `value(attribute-id, unit-id)` — the value **converted** into the given unit
- `simplevalue(attribute-id)` — the value **concatenated with its unit's name**
- `simplevalue(attribute-id, unit-id)` — value converted to the given unit **and** concatenated with that unit's name

**Explanation:** These are the bread-and-butter functions — almost every formula starts by *reading* another attribute.
- Use **`value`** when you want the raw number for further math.
- The **2-argument** form does **unit conversion** for you (store length in mm, output in cm).
- Use **`simplevalue`** when you want a human-readable string *with the unit* (e.g., `35 cm` instead of `35`). Great for display/labels.

---

### Slide 12 — Conditional Functions
**On the slide:** `if(condition, then, else)` examples:
- `if(value('purchasePrice') > value('salesPrice'), 'WARNING', 'OK')` → text warning when purchase price exceeds sales price.
- `if(exact(value('Enriched'),'Yes'),'READY','NOT READY')` → a **text** comparison.
- `if(value('purchasePrice') > value('salesPrice'), value('purchasePrice'), value('salesPrice'))` → returns the **higher** of the two numbers.
- `if(and(value('salesPrice') > value('purchasePrice'), value('salesPrice') > 10), 'OK','NG')` → "OK" only if **both** conditions hold.

**Explanation:** `if` is your decision-maker, identical to Excel's. Two things worth noting:
- Use **`exact(a, b)`** for exact string comparison — don't use `=` for text the way you would for numbers.
- Combine conditions with **`and(...)`**, **`or(...)`**, **`not(...)`**. The third example shows `if` returning *values* (not just labels) — a "max of two fields" pattern.

---

### Slide 13 — Lists and Iterations
**On the slide:** For working with referenced or child objects you need lists and iterators:
- `list(list, separator [, last-separator])` — returns a single text of all elements (joined by the separator).
- `iterate(list, expression)` — returns a list where the **expression is applied to each element**; the expression is supplied as a **string/text**, and variables **`index`** and **`item`** are available inside it.

**Explanation:** This is how you reach *beyond the current object* into its relatives. Typical pattern: get the child/referenced products, run an expression on each (`iterate`), then join the results into one string (`list`). `item` = the current element, `index` = its position. Example use: collect every sub-product's color into one comma-separated string. This unlocks roll-up/aggregation formulas — but it also means you're touching many objects, which leads directly to the next slide.

---

### Slide 14 — Performance Considerations
**On the slide:** Functions can be **costly** when they pull data from many objects. Example:
```
{
  valstr := 'value("Contains Nuts")',
  vallist := iterate(subproducts(), valstr)
}
if(listcontains(vallist, 'Yes'), 'Allergy Warning', 'No Warnings')
```
This reads the attribute for **all sub-products**, builds a list, then checks it. Every evaluation must retrieve all sub-products from the DB (unless cached). On a product with hundreds of sub-products, loading the editor or exporting will be **much slower** than reading just the product's own data.

**Explanation:** The cost lesson. Because calculated attributes run at *read time*, a formula that walks across hundreds of related objects re-does that work every time the editor opens or the product exports. The example also shows two more features: **variable assignment** inside `{ ... }` (`valstr := ...`) and **`listcontains(list, text)`** (does the list contain this value?). Practical rule: a formula touching only the current object is cheap; one that iterates over large sets of children/references is expensive — design accordingly, and prefer simpler mechanisms when possible.

---

### Slide 15 — Thank You / Contact
**On the slide:** "Thank You — STIBO CoE Team."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Function | Does | Excel analogy |
|---|---|---|
| `value('id')` | Read an attribute's raw value | `=A1` |
| `value('id','unit')` | Read **and convert** to a unit | — |
| `simplevalue('id')` | Read value **+ unit name** as text | — |
| `if(cond, then, else)` | Branch | `=IF(...)` |
| `exact(a,b)` | Exact **string** compare | `=EXACT(...)` |
| `and / or / not` | Combine conditions | same |
| `iterate(list, expr)` | Apply expr to each item (`item`, `index`) | array formula |
| `list(list, sep[, last])` | Join list to one text | `=TEXTJOIN(...)` |
| `listcontains(list, text)` | Membership test | — |
| `subproducts()` | The current object's sub-products | — |
| `{ x := ... }` | Assign a variable in a formula | — |

**Setup recap:** Attribute → `Calculated = Yes` → **Value template** appears → right-click → **Insert/Edit Function** → write & **test** in the Function editor.
**Golden rule:** calculated = recomputed on every read → keep cross-object iteration minimal for performance.

#### How this connects to other modules
- The **same function language** builds **Keys** (the *ID/URL/Key* deck) and **Business Conditions** (the *Business Rules* deck).
- "Calculated attribute" first appeared in *Data Modeling* (slide 15) — this deck is the deep dive.


<div style="page-break-after: always;"></div>

# Chapter 4. Business Rules

> A slide-by-slide companion to the *Business Rules* deck (22 slides). Business Rules are STEP's **reusable logic objects** — they either *test* something (Conditions) or *do* something (Actions). They plug into approvals, imports, workflows, bulk updates, and dashboards.

---

### The 30-second mental model (read this first)

Two flavors of rule:
- **Business Condition** — asks a yes/no question about an object → returns **true/false**. Should have **no side effects** (it only *checks*).
- **Business Action** — *changes* things: edits data, sends email, starts a workflow/background process, etc.
- **Business Library** — a bundle of reusable rules shared across workflows and other rules.

You can author rules three ways, from easiest to most powerful: **UI plugins** (point-and-click), **STEP Functions** (the formula language), or **JavaScript** (full Java API access). And before writing any rule, always ask: *can a simpler built-in setting do this instead?*

---

### Slides 1–2 — Template / "Attention" intro slides
**On the slides:** Slide-design template guidance and the trainer's "Attention" framework.

**Explanation:** Authoring scaffolding, not STEP content. Skip.

---

### Slide 3 — Module Objectives
**On the slide:** After this module you'll be able to **differentiate types of business rules**, **create rules using JavaScript**, and **apply them wherever needed**.

**Explanation:** Three goals: know the taxonomy (Condition / Action / Library), be able to code one, and know the integration points (approval, import, workflow, bulk update).

---

### Slide 4 — Title
**On the slide:** "Introduction to STEP Business Rules and validations."

**Explanation:** Section divider.

---

### Slide 5 — About Business Rules (the two main types)
**On the slide:** Business Rules are **first-class objects**, each embodying a small piece of business logic. Two variants:
- **Business Conditions** — test something about an object; evaluate to **true/false**; should generally have **no side effects**.
- **Business Actions** — *do* something: change STEP data, send emails, start background processes or workflows, etc.

**Explanation:** "First-class objects" means rules are stored, named, versioned, and reusable like any other STEP object — not buried snippets. The crucial split: **Conditions check, Actions change.** Keep conditions "pure" (no side effects) so they're safe to evaluate anywhere; put all the *doing* in actions.

---

### Slide 6 — About Business Rules: Libraries
**On the slide:** **Business Libraries** comprise several business rules that can be reused across workflows or other business rules.

**Explanation:** A library is a shared toolbox of rules. Write a validation once (e.g., "is this product fully enriched?"), put it in a library, and call it from many workflows/rules — DRY (don't repeat yourself) for business logic.

---

### Slide 7 — Business Rule Usages (part 1)
**On the slide:** Where rules run:
- **Approval** — Conditions tested when a revisable object is approved (allow/prevent approval); Actions executed on approval (modify data, send email).
- **Imports / Inbound Integration Endpoints** — Conditions can allow/prevent create/update; Actions can modify imported objects, send email, start workflows.
- **Workflows** — Conditions allow/prevent state transitions; Actions run on entering/leaving a state, on a transition, or when a deadline is met (modify objects, change workflow behavior, send mail, start other workflows).

**Explanation:** This is the *map* of where logic hooks in. Same rule concept, many trigger points: at the **approval gate**, during **data load**, and throughout a **workflow's lifecycle**. Memorize these three — they're the backbone of automation in STEP.

---

### Slide 8 — Business Rule Usages (part 2)
**On the slide:**
- **Bulk Updates** — Actions executed via a bulk update, with a Condition as an optional **pre-condition**.
- **Data Profiles** — Conditions tested against all objects in a category (e.g., part of the Product hierarchy); results shown on the **Profile Dashboard**.

**Explanation:** Two more entry points. **Bulk Update** = run an Action across a big selection (with a Condition to filter which objects qualify). **Data Profiles** = use Conditions as data-quality probes and surface pass/fail counts on a dashboard (great for "how complete is our catalog?" reporting).

---

### Slide 9 — When SHOULD Business Rules Be Used?
**On the slide:** Especially for Conditions, always consider a **simpler** built-in alternative first:
- "Attribute has a value" → use the standard **Mandatory** setting (enforced on approval).
- Missing values on tabular import → reject via the **Import Manager**.
- Value restrictions (length, min/max, masks) → use **Validation Base Types** (globally enforced).
- "Only type X can sit below type Y" → use **Object Types & Structures** configuration.
- "References/links only between certain types" → configure reference/link validity.

**Explanation:** The single most important *judgment* slide. Business Rules are powerful but add maintenance cost and run-time overhead. Before coding a rule, ask whether a **declarative setting** already does it. Mandatory flags, validation base types, hierarchy restrictions, and reference validity are all *configuration* — globally enforced, fast, no code. Reserve rules for genuine logic the platform can't express declaratively.

---

### Slide 10 — Business Rules Creation
**On the slide:** (Section header / screenshot intro to creating rules.)

**Explanation:** Transition slide into the "how to build them" half of the deck.

---

### Slide 11 — Usage: Testing a Condition on Approval
**On the slide:** On approval, Business Conditions prevent/allow approval of revisable objects (**Products, Classifications, Assets, Entities**). You enable this via the **"On Approve"** field in the main Business Rules editor.

**Explanation:** The approval gate in detail. Flip "On Approve" on a Condition and STEP will evaluate it whenever someone tries to approve one of those four revisable object types — if it returns false, approval is blocked (and the user sees a message). This is how you enforce "can't approve until data quality criteria are met."

---

### Slide 12 — Usage: Executing an Action on Approval
**On the slide:** Actions can run when a revisable object is approved — modifying data, sending emails, starting workflows, etc.

**Explanation:** The companion to slide 11. Conditions *gate* the approval; Actions *react* to it. Example: on approval, stamp an "Approved date" attribute, email a downstream team, or kick off a publishing workflow — automatically.

---

### Slide 13 — Usage: Imports & Inbound Integration Endpoints
**On the slide:** When importing Products/Classifications/Entities/Assets via the Import Manager or Inbound Integration Endpoints, you can test Conditions and execute Actions **per imported object**.

**Explanation:** Logic at the data's front door. As each record loads, a Condition can reject bad data and an Action can clean/enrich it (set defaults, normalize, trigger follow-on processing). This keeps junk out and applies consistent treatment to inbound data.

---

### Slide 14 — Usage: Workflows
**On the slide:** Business Rules are used **extensively** in workflows to control flow logic, auto-change tracked objects, notify users of task assignments, etc. (Covered in depth in a separate course.) Actions can run:
- **On Entry** (object enters a state)
- **On Exit** (object leaves a state)
- **On deadline** (when the deadline-checker background process runs)
- **On Transition** (when a transition is performed)

**Explanation:** Preview of the Workflows deck. The four execution moments (Entry / Exit / Deadline / Transition) are the hooks where Actions fire as an object moves through a process. Conditions, meanwhile, guard whether transitions are even allowed.

---

### Slide 15 — Usage: Bulk Update
**On the slide:** Business Actions can be applied to a large data set via the Bulk Update **"Run Business Rule"** plug-in, basing updates on complex logic.

**Explanation:** Select thousands of objects, choose "Run Business Rule," and the Action executes on each — for mass changes that need real logic (not just "set field X to Y," which the plain bulk-update plugins already handle).

---

### Slide 16 — Construction: Condition Plugins with a UI
**On the slide:** You'll often write Conditions in STEP Functions or JavaScript, but **simple Conditions can use point-and-click plugins**. UI plugins generally **generate a user-facing message** when they evaluate to false.

**Explanation:** Start here for easy rules. The UI plugins are pre-built, configurable condition types — no code — and they come with built-in failure messages so end users understand *why* their object failed. Only drop to Functions/JavaScript when the plugins can't express what you need.

---

### Slide 17 — Construction: Attribute Value Comparison & Reference
**On the slide:**
- **Attribute Value Comparison** plugin — compare an attribute's value on the object against a **constant** or **another attribute** on the same object.
- **Reference other Business Condition** — reuse an existing condition inside another.

**Explanation:** The most common UI condition: "is price > cost?", "is field A = field B?". The "reference other condition" feature lets you compose conditions from smaller named ones (reuse, like libraries on slide 6).

---

### Slide 18 — Construction: Valid Hierarchies & LOV Cross-Validation
**On the slide:**
- **Valid Hierarchies** plugin — true if the object sits **below one of the specified hierarchy nodes**; false otherwise. Typically used on the **"Applies If"** tab as a **pre-condition**.
- **LOV Cross-Validation** plugin — define legal relationships between values in **two LOV-based attributes**. The LOVs must be configured so users can't add new values.

**Explanation:** Two powerful UI conditions.
- **Valid Hierarchies** scopes a rule to a branch — "only apply this check to products under *Electronics*." The **"Applies If"** tab is the *pre-condition* gate: the main rule/action only runs when "Applies If" is true.
- **LOV Cross-Validation** enforces dependent dropdowns — e.g., if Country = "USA" then State must be a US state. The LOVs must be locked (no user-added values) so the legal combinations stay valid.

---

### Slide 19 — Construction: Action Plugins with a UI
**On the slide:** Actions can be written in JavaScript, but several **UI plugins** exist for simple operations.

**Explanation:** Mirror of the condition plugins, for Actions: set/copy an attribute value, create a reference, send an email, etc. — all without code. Same principle: try the plugin first, code only when needed.

---

### Slide 20 — Construction: Conditions Based on STEP Functions
**On the slide:** Conditions can be written in **STEP Functions** (the same language used for calculated attributes). A condition is **true if the function returns "1"**, **false if "0"** — though you rarely write 1/0 explicitly because many functions return that automatically. Examples: comparison operators `<, >, <=, >=, =, !=`; `exact(s1,s2)`; `and(...)`, `or(...)`, `not(...)`; `listcontains(list, text)`.

**Explanation:** The middle tier of authoring power. Everything you learned in the *STEP Functions* deck applies — a comparison like `value('salesPrice') > value('cost')` already yields 1/0, so it *is* a condition. Use this when the UI plugins are too limited but you don't need full JavaScript.

---

### Slide 21 — Construction: Rules in JavaScript
**On the slide:** Both Actions and Conditions can be written in **JavaScript** using the **public Java API** (JavaDoc in the SDK docs). JavaScript rules have access to standard Java packages, and the STEP Java API is reached via **binds** (Java objects bound to JavaScript variables).

**Explanation:** The most powerful tier. When logic is too complex for plugins or functions, write JavaScript that calls STEP's Java API. "Binds" are the bridge: STEP injects ready-made Java objects (the current object, the workflow instance, etc.) into named JavaScript variables you can program against. With this you can do essentially anything the platform's API exposes — at the cost of more complexity and maintenance.

---

### Slide 22 — Thank You / Contact
**On the slide:** "Thank You — STIBO CoE Team."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Concept | Memory hook |
|---|---|
| **Condition** | *Checks* → true/false, no side effects |
| **Action** | *Does* → changes data, emails, starts workflows |
| **Library** | Reusable bundle of rules |
| **Usages** | Approval · Import/Inbound · Workflow · Bulk Update · Data Profiles |
| **Authoring tiers** | UI plugins → STEP Functions → JavaScript |
| **"Applies If" tab** | Pre-condition: rule only runs when this is true |
| **Function condition** | Returns **1 = true**, **0 = false** |
| **JavaScript** | Full Java API via **binds** |
| **Golden rule (slide 9)** | Prefer a built-in setting before writing a rule |

**Simpler-than-a-rule alternatives:** Mandatory flag · Import Manager rejection · Validation Base Types · Object Types & Structures · Reference/Link validity.

#### How this connects to other modules
- **STEP Functions** deck = the formula language used in function-based conditions.
- **Workflows** deck = the biggest consumer of Business Rules (Entry/Exit/Transition/Deadline).
- **Approvals/Revisions** + **Import** decks = the other major trigger points.


<div style="page-break-after: always;"></div>

# Chapter 5. STEP Workflows

> A slide-by-slide companion to the *STEP WorkFlows* deck (16 slides). A workflow is STEP's way of routing an object (a product, asset, etc.) through a **multi-step business process** — assignments, approvals, deadlines, and automation — using States and Transitions, powered by Business Rules.

---

### The 30-second mental model (read this first)

A workflow is a **map of States** (boxes) connected by **Transitions** (arrows). An object enters at a start state and moves along transitions until it reaches a final state. At each state, a **Task** is assigned to a user or group; **Business Rules** fire on entry/exit/transition/deadline to automate and validate; **Workflow Variables** carry temporary data alongside the object. You build it visually in the **Workflow Designer**, and monitor it with **Profiles/Dashboards**.

Mental picture: a board game. States = squares, Transitions = legal moves, Tasks = "whose turn is it," Business Rules = the rules of the game, Variables = your scorecard.

---

### Slides 1–2 — Template / "Attention" intro slides
**On the slides:** Slide-design template guidance and the trainer's "Attention" framework.

**Explanation:** Authoring scaffolding, not STEP content. Skip.

---

### Slide 3 — What a Workflow Is
**On the slide:** A workflow is a **progression of steps** (tasks, events, interactions) forming a work process, involving **two or more people**, that creates/adds value. **Sequential** = each step depends on the previous one. **Parallel** = two or more steps happen concurrently.

**Explanation:** The core definition. Workflows coordinate *people and automation* around an object. Two shapes to know: **sequential** (A→B→C, one after another) and **parallel** (B and C happen at the same time, then rejoin). Real workflows mix both.

---

### Slide 4 — STEP Workflow Features
**On the slide:** Visual designer in the workbench; user/group task assignment with **claim/release**; sequential & parallel execution with automatic **split/merge**; **deadlines & escalation**; **configurable Business Rules** for automation/validation; task lists in Workbench and Portal; configurable data views per task; **auto-launch on create**; can be started or triggered from Business Actions (on approval, during import, via SOAP API); **dashboards** for monitoring/KPIs; per-workflow setup privileges via **Setup Groups**.

**Explanation:** The capability checklist. Key ideas:
- **Claim/release** — a task assigned to a *group* must be "claimed" by an individual before they can act, then can be released back.
- **Split/merge** — parallel branches automatically fan out and rejoin.
- **Auto-launch / triggered start** — workflows can begin automatically (on object create, on approval, on import, via API), not just manually.
- **Portal task lists** — external/casual users can do workflow tasks through a Portal, not just the workbench.

---

### Slide 5 — Workflow Setup (where definitions live)
**On the slide:** Workflow **definitions** are stored in **System Setup → Setup Groups**. To create a workflow below a Setup Group, workflows must be **valid below that Setup Group type** (configured on the References tab of the Workflow Basic Object Type).

**Explanation:** Workflows are configuration objects, organized into **Setup Groups** (folders that also control *who can edit which workflows* — slide 4's per-workflow privileges). The validity note is the usual STEP pattern: an object type can only sit somewhere if it's been made valid there.

---

### Slide 6 — Steps to Create a Workflow
**On the slide:** 1) Create a workflow → 2) Create **states** → 3) Create **transitions** between states → 4) Add **events** to transitions → 5) Set **assignees** → 6) Set **validity** → 7) Set **workflow options**.

**Explanation:** The build recipe in order. First lay out the *structure* (states + transitions), then the *triggers* (events that fire transitions), then *who does what* (assignees), then *what it applies to* (validity — which object types can run this workflow), and finally global options. Follow this sequence and a workflow comes together cleanly.

---

### Slide 7 — Workflow Designer Layout
**On the slide:** Primary areas of the Designer: **Properties panel** (ID/Name), area for **Workflow Variables/Attachments**, area for **validation errors/warnings**, **overview/zoom** area, and the **Canvas** where states and transitions are defined.

**Explanation:** Orientation to the visual tool. You drag states onto the **canvas** and draw transitions between them; the **validation** panel flags structural problems (e.g., an unreachable state); **variables/attachments** are defined off to the side. It's a diagramming surface that compiles into a runnable process.

---

### Slide 8 — Workflow Editor
**On the slide:** The workflow editor is used to set the **default assignee** for the workflow and to **enable status flags**.

**Explanation:** Workflow-*level* settings (vs state-level on the next slide). The **default assignee** is the fallback for any state that doesn't specify its own. **Status flags** surface where an object is in its workflow as a visible indicator elsewhere in STEP.

---

### Slide 9 — State Editor
**On the slide:** Per-state settings: **Assignee** (add/remove/modify), **Comments**, **Deadline/Escalation**, **Mandatory Data** tab (attributes/groups/references required before a task can leave the state), **On Entry** / **On Exit** business actions, **State** (name/characteristics), **Web UI Screen Mapping** (link the state to a specific Web UI screen).

**Explanation:** The most-used editor. For each state you control *who* works it (assignee), *what must be complete* before moving on (**Mandatory Data** — a data-quality gate built into the flow), *what automation runs* when entering/leaving (On Entry/On Exit actions), and *which screen* the user sees (Web UI mapping — a tailored view showing only the fields relevant to that task).

---

### Slide 10 — Concurrency: Cluster & Parallel States
**On the slide:** Two state types beyond normal states: **Cluster** and **Parallel**.
- **Cluster** — groups other states.
- **Parallel** — is both a Cluster (can hold child states) *and* parallel (provides **auto-merge**, only allows clusters as children), and can also be the **initial** type (start the flow in parallel).

**Explanation:** How parallel processing is modeled. A **Cluster** is a container/grouping. A **Parallel** state runs multiple **clusters** at once (each cluster = one concurrent branch) and **auto-merges** them when all are done. So to run three things simultaneously: a Parallel state containing three clusters. The object proceeds only after all branches complete.

---

### Slide 11 — Task Assignment
**On the slide:** A task is always assigned to a **user or user group**. A user sees tasks assigned to them or to any group they belong to, but can only **submit** their own (group tasks must be **claimed** first). Exception: users with **Workflow Administrator** privilege see/submit all tasks. Assignment can be **static** (workflow-level default; specific user/group; the executing user; via a workflow variable; via custom plugins) or **dynamic** (via a Business Action on state entry).

**Explanation:** The "whose turn is it" engine. Key distinctions:
- **User vs group** assignment; group tasks need **claiming** (one person takes ownership) before submission.
- **Static assignment** = decided at design time / by simple rules (a fixed user/group, "whoever did the previous step," or read from a variable).
- **Dynamic assignment** = computed at run time by an On-Entry Action (e.g., "assign to the regional manager based on the product's market"). The **Workflow Administrator** privilege overrides all of this.

---

### Slide 12 — Business Rules in Workflow
**On the slide:** Actions run **On Entry**, **On Exit**, **On Deadline** (when the deadline-checker background process runs), and **On Transition** (limited use cases). Conditions are tested **on transitions** to allow/prevent them. Workflows can use **local or global** rules. **Order of execution:** Conditions → On Exit → On Transition → On Entry.

**Explanation:** This ties the *Business Rules* deck to workflows. The execution order matters: when an object moves from State A to State B, STEP first **evaluates conditions** (is this move allowed?), then runs **A's On Exit**, then the **transition's** actions, then **B's On Entry**. Knowing this order lets you predict exactly when your automation fires. "Local" rules belong to this workflow; "global" rules are shared/reusable.

---

### Slide 13 — Workflow Variables
**On the slide:** Variables are like product attributes/assets but **live with the workflow instance, not the tracked object**. They hold **transient data** no longer relevant after the workflow ends: supporting documents, rejection reasons / user-to-user notes, routing selections (e.g., "copy-writing required?"), user IDs for dynamic assignment. A variable can be a **simple text field**, **bound** to a STEP attribute (for validation / LOV dropdown), or a **calculated expression** (rare). Variables are **global to the workflow instance** (one value at a time, not per-state).

**Explanation:** Variables are the workflow's **scratchpad**. Crucially, they attach to the *process instance*, not the product — so when the workflow finishes, this temporary data goes away rather than cluttering the object. Uses: routing decisions, rejection reasons, attachments, and stashing a user ID computed for later dynamic assignment. **Binding** a variable to an attribute gives you free validation and dropdowns. "Global to the instance" means the variable has a single current value across all states (not a separate value per state).

---

### Slide 14 — Deadlines and Escalations
**On the slide:** Deadlines for tasks/states can be set: a fixed number of **hours/days** in the designer, **dynamically** via an On-Entry Business Action, or to a specific **date-time** via the **"WorkflowDeadline"** view plugin (admins can delete/modify deadlines this way). Actions on the **Deadline/Escalation** tab run when a deadline is met **and** the deadline-monitoring background process runs. Escalation actions typically **send email**, **trigger a transition**, or **reassign**.

**Explanation:** How STEP enforces "don't let work sit forever." You set a deadline (statically, dynamically, or as an explicit date), and when it passes, the **deadline-checker background process** triggers escalation actions — nudge by email, auto-move the task to another state, or reassign it to someone else. Note the dependency: deadlines only fire **when the background process runs**, so escalations are near-real-time, not instantaneous.

---

### Slide 15 — Monitoring Workflows
**On the slide:** Monitor via **Workflow Profiles**, which can focus on one of three domains:
- **States** — how many items are in each state, how long, who's assigned, throughput today vs. prior days.
- **Assignees** — how many tasks per user/group, how long held, completions today, average completion time week-over-week.
- **Workflows** — average time from start to final state, count currently in the workflow.
Profile data can be shown as **widgets on the Main Dashboard**.

**Explanation:** The reporting layer. Profiles answer the three management questions: *Where is everything?* (States), *Who's overloaded / how fast are people?* (Assignees), and *How long does the whole process take?* (Workflows). Surfacing these as dashboard widgets turns the workflow into a live operations view with throughput and KPI tracking.

---

### Slide 16 — Thank You / Contact
**On the slide:** "Thank You."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Concept | Memory hook |
|---|---|
| **State** | A box / step; holds a Task |
| **Transition** | An arrow / legal move between states |
| **Event** | What triggers a transition |
| **Task** | The work item, assigned to user/group |
| **Claim/Release** | Group task → one person takes/returns it |
| **Cluster state** | Container that groups states |
| **Parallel state** | Runs clusters concurrently + **auto-merge** |
| **Mandatory Data** | Fields required before leaving a state |
| **Static assignment** | Fixed/rule-based (user, group, executing user, variable) |
| **Dynamic assignment** | Computed at runtime via On-Entry Action |
| **Rule order** | Conditions → On Exit → On Transition → On Entry |
| **Workflow Variable** | Lives with the *instance*, transient scratchpad |
| **Deadline/Escalation** | Fires when met **and** background process runs |
| **Profiles** | Monitor States / Assignees / Workflows → Dashboard |

**Build order:** workflow → states → transitions → events → assignees → validity → options.

#### How this connects to other modules
- **Business Rules** deck = the logic that runs at Entry/Exit/Transition/Deadline.
- **Approvals/Revisions** deck = approval is one common trigger that starts/advances workflows.
- **Portals** deck = where external users pick up workflow tasks.


<div style="page-break-after: always;"></div>

# Chapter 6. Approvals, Revisions & Deletions

> A slide-by-slide companion to the *Approvals Revisions and Deletions* deck (21 slides). This deck goes deep on the **Main → Approved** lifecycle introduced in Data Modeling: how approval works (full, partial, context-specific), how STEP keeps version history (revisions), and how deletion works (recycle bin + approved-workspace removal).

---

### The 30-second mental model (read this first)

STEP keeps two copies of revisable data: **Main** (editable draft) and **Approved** (read-only, signed-off). The **Approve** operation copies data Main→Approved. Only **workspace-revisable** objects (Products, Classifications, Assets, and Entities configured that way) live in two copies; everything else (Attributes, References definitions, etc.) is **globally revisable** — identical in both. Each approval cuts a new **Revision** (a historical snapshot). Deletion mirrors approval in reverse: objects go to a **Recycle Bin** in Main, and you must **approve the deletion** to remove them from Approved before purging.

---

### Slide 1 — Read Me First (template)
**On the slide:** Internal slide-design guidance.

**Explanation:** Authoring scaffolding, not content. Skip.

---

### Slide 2 — Title
**On the slide:** "Approvals Revisions and Deletions — STIBO CoE Team."

**Explanation:** Section opener.

---

### Slide 3 — Module Objectives
**On the slide:** You'll become familiar with: the **Approval Process** (Full, Partial, Context-Specific), **Revisions & Traceability**, and **Deletions**.

**Explanation:** The roadmap. Three big topics: approving data, tracking its history, and removing it safely.

---

### Slide 4 — Workspace and Approval
**On the slide:** Data is logically split into two workspaces:
- **Main** — the editable "draft" workspace.
- **Approved** — "terminated" (non-editable); data appears here only via the **approval** operation.
The approval process **pushes data from Main to Approved** and can be done **manually or programmatically**.

**Explanation:** Reinforces the core model. "Terminated/non-editable" means you never type directly into Approved — it's a *copy destination*. Approval can be triggered by a person (menu/right-click) or by automation (a Business Action, an import, the API).

---

### Slide 5 — What Can Be Approved (revisability)
**On the slide:** The approval operation applies only to **workspace-revisable** objects: **Products, Classifications, Assets, and Entities configured to be workspace revisable.** All other objects are **globally revisable** — identical in Main and Approved (examples: **Attributes, References**).

**Explanation:** This is the dividing line. **Workspace-revisable** = has a separate draft and approved copy, needs approval. **Globally revisable** = one single copy that's the same everywhere, no approval cycle. Configuration objects (attribute definitions, reference type definitions) are global — change them and the change is live immediately. Note Entities are *optionally* workspace-revisable (from Data Modeling slide 16).

---

### Slide 6 — Approval Statuses (intro)
**On the slide:** Workspace-revisable objects are created in Main and **don't appear in Approved until first approved**. Each has an **"Approved" property** showing its approval status.

**Explanation:** A brand-new object exists only in Main until someone approves it. The "Approved" property is the at-a-glance indicator of where the object stands.

---

### Slide 7 — Approval Statuses (list)
**On the slide:** (Lists the possible statuses.)

**Explanation:** Typical statuses include *not yet approved* (new, never approved), *approved* (Main and Approved match), *modified after approval* (edited in Main since last approval — needs re-approval), and *partially approved* (some data approved, some not — see slide 11). The status tells a data steward whether re-approval is needed.

---

### Slide 8 — Data Ownership (intro)
**On the slide:** For an object to be **fully approved**, **all data it owns must also be approved.** (Figure shows data owned by a Product.)

**Explanation:** "Approval is only as complete as the data the object *owns*." So you need to understand precisely what an object owns — which is the next slide.

---

### Slide 9 — Data Ownership (the rules)
**On the slide:** Points to notice:
- A Product **owns its parent link** (also true for Classifications, Entities, Assets).
- A Product owns its **local values** but **not inherited** specification-attribute values. Modifying an inherited value at an ancestor **does not** change the Product's approval status; those values are approved with the object they're *local* to.
- A Product owns all **local References/Links where it is the Source**, plus **Description Attribute values on those Links/References**. When a Link/Reference is modified, it's the **Source** that changes; the **Target is unaffected**.

**Explanation:** Ownership = "what affects *this* object's approval status." Three takeaways:
1. You own your **parent link** (your place in the hierarchy).
2. You own **local** attribute values, not **inherited** ones — inherited values belong to (and are approved with) the ancestor where they were actually set. So editing a category-level value doesn't mark every child "modified."
3. You own the **references you originate** (you're the Source), including attributes carried on those references. Being a *Target* of someone else's reference doesn't affect you. This is why approval flows from Source side.

---

### Slide 10 — Conditions to Approve an Object
**On the slide:**
- Objects must be approved **from Main**.
- Can't approve if **parent objects aren't approved** (approve **top-down**).
- A Reference/Link can't be approved if its **Target doesn't exist in Approved**.
- **Mandatory** attributes / reference types must be populated to approve.
- **Externally Maintained** attributes/references are **not under revision control**.
- The **revision number changes automatically on approval**.
- The whole hierarchy can be approved via **Approve Recursively**.

**Explanation:** The rulebook for a successful approval:
- **Top-down** — a child can't exist in Approved without its parent there first.
- **Target must exist** — you can't approve a reference pointing at something not yet in Approved (leads to *partial approval*, slide 11).
- **Mandatory** gates approval (connects to Data Modeling slide 15).
- **Externally maintained** data bypasses the whole cycle (it syncs straight through).
- **Approve Recursively** (slide 13) handles whole branches at once.

---

### Slide 11 — Partial Approval (the mechanism)
**On the slide:** You *can* approve an object that has a Reference/Link to something **not** in Approved. The object becomes **partially approved**: everything approvable is approved, but the Reference/Link is **not**. If the Target is later approved, the **Source must be approved again** for the link to reach Approved.

**Explanation:** Partial approval is STEP's graceful handling of the "target not ready" problem from slide 10. Rather than blocking you, it approves what it can and leaves the dangling reference behind. Remember the catch: once the target catches up, you must **re-approve the source** to finally push the link through.

---

### Slide 12 — Partial Approval (when/how)
**On the slide:** Partial approval helps when **some elements need to be live in Approved before the rest can be approved**. Do it via **Maintain menu → Approval → Partial Approve**, or **right-click → Partial Approve**.

**Explanation:** The *use case* and the *clicks*. Useful when part of an object is publish-ready but other parts (or its references) aren't — you don't have to wait for everything.

---

### Slide 13 — Approve Recursively
**On the slide:** Recursive approval **searches for unapproved objects linked to (or below) a selected node** and approves them (copies to Approved). Do it via **Approval → Approve Recursively** or **right-click**. It runs as a **Background Process**.

**Explanation:** The bulk approver for a whole branch. Instead of approving each product one by one (and respecting top-down order manually), point at a category node and let STEP walk down and approve everything beneath. Because it can touch many objects, it runs in the background.

---

### Slide 14 — Context-Dependent Approvals
**On the slide:** Approval always happens **in a specific context** and applies only to data **visible in that context**. Example: a Product approved only in the **"EN"** context — the dimension-dependent "Color" value exists in the approved copy only for **EN**.

**Explanation:** Ties back to Dimensions/Contexts (Data Modeling slide 18). Because you're always viewing through a context lens, you approve *what that lens shows*. Approve in English and the English values go to Approved; the French values stay unapproved until you approve through the French context. This enables localized, staggered publishing (English live now, French when translation finishes).

---

### Slide 15 — Revisions and Traceability (section)
**On the slide:** Section header (marked stage "B").

**Explanation:** Transition into version-history.

---

### Slide 16 — Revisions and Traceability (how revisions form)
**On the slide:** Historical versions are stored as **Revisions** — a snapshot of an object. A revision is created automatically:
- on **creation** of a new workspace-revisable object,
- on **approval**,
- each time a change is made by a **different user**, or any change **following an approval**,
- when a user makes a change and the **current revision is older than a configurable threshold** (even if the same user made the previous change).
STEP does **not** create a revision for every change → **no field-level traceability**. But every revision is tied to a **user**, so you can always see *who* is responsible for a set of changes.

**Explanation:** Revisions are STEP's version history, but deliberately *coarse-grained*: it doesn't snapshot every keystroke (that would be huge). Instead it cuts a new version at meaningful moments — create, approve, change-of-author, post-approval edit, or after a time threshold. The trade-off: you get **who changed it and roughly when**, not a per-field audit trail. Knowing this manages expectations when someone asks "who edited this exact field?"

---

### Slide 17 — Revisions and Traceability (inspecting)
**On the slide:** Revisions are viewed from the object editor's **Status tab**, where you can see an old revision's data and **revert** to it.

**Explanation:** The practical "how." The Status tab is your time machine — browse prior snapshots and roll back if needed.

---

### Slide 18 — Deletion Process (section)
**On the slide:** Section header (stage "B").

**Explanation:** Transition into deletion.

---

### Slide 19 — Deletion (recycle bin)
**On the slide:** Deletion of workspace-revisable objects is **like Windows/Mac**: deleting a Product **doesn't purge it** — it goes to the **STEP Recycle Bin** (shown in Tree). Objects that are **not** workspace-revisable are **deleted directly** (no recycle bin). Deleting an object with **children deletes the children/ancestors** too. You can **purge** from the Recycle Bin's context menu.

**Explanation:** Two-stage deletion for revisable objects: first to the Recycle Bin (recoverable), then **purge** (permanent). Non-revisable (global) objects skip the bin and go straight away. Deleting a parent cascades to its descendants — be careful.

---

### Slide 20 — Deletion (removing from Approved)
**On the slide:** Just as approval transferred the object *into* Approved, **deletion must be approved** to remove it *from* Approved. If that succeeds, the object can be purged. Consistency restrictions:
- You **cannot approve deletion of an object with children in Approved** — delete children first.
- You **cannot approve deletion of an object that is a Target** of a Reference/Link in Approved — remove the link first (remove it in Main and approve the Source).

**Explanation:** The symmetry: it took an *approve* to push the object into Approved, so it takes an **approved deletion** to pull it back out. The restrictions mirror the approval rules (slide 10) in reverse — you can't leave Approved in a broken state (orphaned children or dangling references). So you delete **bottom-up** and clear incoming references before removing a target.

---

### Slide 21 — Thank You / Contact
**On the slide:** "Thank You — STIBO CoE Team."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Concept | Memory hook |
|---|---|
| **Main** | Editable draft workspace |
| **Approved** | Read-only signed-off copy; written only via Approve |
| **Workspace revisable** | Two copies; needs approval (Products, Classifications, Assets, opt. Entities) |
| **Globally revisable** | One copy, same everywhere (Attributes, Reference defs) |
| **Approve top-down** | Parent must be approved before child |
| **Target must exist** | Can't approve a reference to an un-approved target |
| **Partial approval** | Approve what you can; dangling refs left; re-approve source later |
| **Approve Recursively** | Approve a whole branch (background process) |
| **Context-specific approval** | Approve only the data in the current context lens |
| **Revision** | Coarse snapshot: on create/approve/new author/post-approval/threshold |
| **Traceability** | Who + when, **not** field-level |
| **Status tab** | View/revert old revisions |
| **Deletion** | Recycle Bin → purge; cascades to children |
| **Approve deletion** | Required to remove from Approved; delete bottom-up, clear inbound refs |

#### How this connects to other modules
- Builds directly on **Data Modeling** slide 20 (Workspaces/Approval) and slide 18 (Contexts).
- **Business Rules** can run on approval (conditions gate it, actions react to it).
- **Workflows** often drive approval as part of a process.


<div style="page-break-after: always;"></div>

# Chapter 7. Search, Collections & Bulk Updates

> A slide-by-slide companion to the *Search, Collections and Bulk Updates* deck (33 slides). Three connected tools for working with data at scale: **Search** (find objects), **Collections** (save sets of objects), and **Bulk Updates** (change many objects at once). The natural flow is: *search → save as collection → bulk update.*

---

### The 30-second mental model (read this first)

- **Search** = find objects by name, ID, attribute value, hierarchy location, type, etc. Two entry points: **Goto** (jump straight to one object) and the **Search tab** (build real queries, refine with the Profiling page).
- **Collection** = a saved, **flat** container of objects (regardless of where they live in the hierarchy). Created from a search or an import file.
- **Bulk Update** = apply operations to every object in a set (a collection, a search result, or a multi-selection). **There is no undo** — always preview and test small first.

---

### Slides 1–2 — Template / "Attention" intro slides
**On the slides:** Slide-design template and trainer framework.

**Explanation:** Authoring scaffolding. Skip.

---

### Slide 3 — Module Objectives
**On the slide:** You'll be able to **search** for objects, **create collections**, and **run bulk updates** on found items.

**Explanation:** The three-tool roadmap, in the order you'll use them.

---

### Slide 4 — Title
**On the slide:** "Search, Collections and Bulk Updates — STIBO CoE Team."

**Explanation:** Section opener.

---

### Slide 5 — Goto Search
**On the slide:** The workbench finds both **System Setup** and **Tree** objects. **Goto search:** type a **Name or ID**, press Enter (or click "Goto next object"), and STEP jumps straight to the object **without a results list**. It lands on the first hit; browse further hits with "Goto next object." You can also search by **unique key** by selecting the key from the Goto dropdown.

**Explanation:** Goto is the fast "I know what I want, take me there" search. No list, just navigation — great when you know the ID/name/key. Searching by **unique key** ties back to the Keys module: you can locate an object by its business key, not just its STEP ID.

---

### Slide 6 — The Search Tab (two approaches)
**On the slide:** The **Search navigator tab** + **Search Result Profiling page** offer advanced finding. Two approaches:
- **Know the details** → build a precise query (e.g., Products where Weight < "5 kg", below the "Office Chairs" folder, not of type "Item").
- **Don't know much** → start broad, then narrow using the **Profiling page**.

**Explanation:** The Search tab is the real query builder. Two strategies: *targeted* (compose exact criteria) or *exploratory* (cast a wide net, then whittle down with profiling — slide 17). The example shows you can combine **attribute conditions + hierarchy location + object type** in one query.

---

### Slide 7 — Search Tab (screenshot)
**On the slide:** (UI screenshot of the search tab.)

**Explanation:** Visual reference for the search interface; no new concept.

---

### Slide 8 — Basic Searches (name/ID)
**On the slide:** Default search mode searches **Name, ID, and Attribute values** — a text string matches anywhere those occur. **Wildcards `?` and `*`** are valid anywhere to broaden searches. Limit scope by prefixing with **`ID=`** or **`Name=`**.

**Explanation:** The simplest search. By default it's a broad text match across name/ID/attributes. `*` = any run of characters, `?` = single character. Use `ID=` / `Name=` to stop it matching attribute values when you only care about identity.

---

### Slide 9 — Basic Searches (attribute value, step 1)
**On the slide:** To search an attribute value: enter an **Attribute Name/ID**, pick it from the **typeahead** (it inserts "Attribute Name (Attribute ID)"), then enter or pick a **search operator**.

**Explanation:** Building an attribute query is guided: typeahead helps you select the exact attribute (avoiding ambiguity), then you choose how to compare it.

---

### Slide 10 — Basic Searches (attribute value, step 2)
**On the slide:** After the operator, typeahead lists **actual attribute values** stored in STEP for that attribute.

**Explanation:** STEP even suggests real existing values — so you match against data that actually exists rather than guessing spelling.

---

### Slide 11 — Basic Searches (operators)
**On the slide:** (Table of available search operators.)

**Explanation:** Operators include equals, not equals, less/greater than, contains, starts/ends with, is empty, etc. — the comparison vocabulary for attribute queries.

---

### Slide 12 — Full-Text Indexed Attribute Searches
**On the slide:** Searches in attributes marked **Full Text Indexable** behave differently. Example: a description containing "...diecast **aluminum** enclosure..." → `Description = aluminum` **returns** the object. If the attribute is **not** full-text indexable, you'd need wildcards on both sides: `Description = *aluminum*`. **Leading-wildcard searches are heavy and should be avoided.**

**Explanation:** This explains *why* full-text indexing exists (from Data Modeling slide 15). With it, STEP indexes individual **words**, so you can find a word inside a long text without wildcards — fast. Without it, you must wrap the term in `*...*`, and a **leading wildcard** (`*aluminum`) forces STEP to scan everything (slow). Lesson: enable full-text indexing for fields you'll word-search, and avoid leading wildcards.

---

### Slide 13 — Search Criteria (types)
**On the slide:** Different **search criterion types** are available from the **Search type** dropdown.

**Explanation:** Beyond text/attribute matching there are specialized criteria (object type, hierarchy position, approval status, references, etc.). You assemble a query from these criterion types.

---

### Slide 14 — Combining & Negating Criteria
**On the slide:** Click the **green plus** to combine criteria (default **AND**). To negate: hold the mouse on **"Add criterion"** and choose **"Add Exclude"** (NOT).

**Explanation:** Multiple criteria are **AND**ed by default (all must be true). **Exclude/NOT** lets you carve out a subset ("Products under Chairs **but not** of type Item").

---

### Slide 15 — OR Searches & Result List
**On the slide:** **OR separators** can be inserted between criteria via the add-criterion button. After running, results show in a **list below the search box**.

**Explanation:** Add **OR** when *any* of several conditions should match (vs AND where all must). With AND/OR/NOT you can express fairly complex logic visually. Results appear inline for inspection.

---

### Slide 16 — Search from List
**On the slide:** **Search from List** lets you search a given set of values by **ID/Name/Unique Keys or any attribute** (chosen from a dropdown). **Paste a list** (e.g., copied from Excel) into the box and run.

**Explanation:** Hugely practical for real work: you have a spreadsheet of 500 SKUs — paste them in and STEP finds all matching objects at once. No need to search one by one.

---

### Slide 17 — Search Result Profiling Page
**On the slide:** The **Profiling page** refines results: start with a broad search, then click links in the profile to **add criteria** and narrow down.

**Explanation:** This is the "exploratory" workflow from slide 6 made concrete. The profile breaks your result set down (by type, by value, by branch) with clickable facets — each click drills further. Think of it like the filter sidebar on a shopping site.

---

### Slide 18 — Bulk Updates (entry points)
**On the slide:** Bulk Update updates **large numbers of objects in one operation**. Start it from: a **Collection's context menu**, a **multi-selection** in Tree/System Setup via **"Run Bulk Update,"** or **directly from a Search result**.

**Explanation:** Three ways to feed objects into a bulk update — a saved collection, an ad-hoc selection, or a live search result. All lead to the same wizard.

---

### Slide 19 — Bulk Update Wizard (operations)
**On the slide:** The wizard lets you specify **operations** applied to the set (one object at a time). STEP ships several operation types out of the box.

**Explanation:** Operations are the *what to change*: set an attribute value, copy a value, add/remove a reference, change name, run a Business Rule, etc. Each is applied per object across the whole set.

---

### Slide 20 — Bulk Update Wizard (order & rollback)
**On the slide:** With multiple operations, they apply **in listed order**. If one operation **fails** for an object, **all changes to that object are rolled back.**

**Explanation:** Operations are sequential and **atomic per object** — an object is either fully updated or left untouched, never half-changed. Order matters when later operations depend on earlier ones.

---

### Slide 21 — Bulk Update Wizard (preview)
**On the slide:** The wizard shows a **preview** of applying the operations to the **first 10 objects**.

**Explanation:** A built-in safety check — see the effect on a sample before committing to the whole set.

---

### Slide 22 — Bulk Update Wizard (test first — no undo!)
**On the slide:** For a more precise preview, use the **"Advanced"** step. **Test on a small set first.** **Remember: there is NO undo!**

**Explanation:** The most important warning in the deck. Bulk updates are **irreversible**. Always: preview → test on a handful → then run on the full set. A bad bulk update can damage thousands of objects with no rollback.

---

### Slide 23 — Scheduling a Bulk Update
**On the slide:** From the **File menu** you can **schedule** a bulk update. It takes a **Collection** (the object set) and a **Bulk Update Configuration** (the operations) as arguments.

**Explanation:** For recurring/large jobs, schedule them to run later (e.g., overnight). Note the inputs: a **saved collection** + a **saved configuration** — which is why collections matter for repeatable, scheduled work.

---

### Slide 24 — Collections (what they are)
**On the slide:** Collections are **containers for sets of objects** from Tree and System Setup, **independent of hierarchy placement**. Created via **search or import**; all objects can be updated together. Found in the **Collections hierarchy** on the Tree tab.

**Explanation:** A collection is a saved bag of objects pulled from anywhere — handy for any task you'll repeat or run later. Decoupled from the hierarchy: a collection can mix objects from totally different branches.

---

### Slide 25 — Creating Collections (overview + flat view)
**On the slide:** Two creation methods: from a **Search** result, or from an **import file**. Either way, if a collection has **< 10,000 objects**, you can inspect them by expanding the Collection node — shown in a **completely flat structure**, ignoring any parent/child relationships.

**Explanation:** Collections are always **flat** — no hierarchy, just a list. (The 10,000 limit is only about *inline inspection* in the Tree, not the collection's size.)

---

### Slide 26 — Creating a Collection from Search (steps 1–2)
**On the slide:** Most common method: on the **Search tab**, enter criteria, click Search to verify, then click **"Save as Collection."**

**Explanation:** The everyday path: find what you want, then persist it as a collection in one click.

---

### Slide 27 — Creating a Collection from Search (step 3)
**On the slide:** Choose the **parent** in the collections hierarchy (top folder or a group folder), enter a **collection name** (ID auto-generated), click OK.

**Explanation:** You file the new collection under the Collections folder structure (folders/groups help organize many collections).

---

### Slide 28 — Creating a Collection from Search (step 4)
**On the slide:** A **background process** runs and the collection is created/saved under the chosen folder.

**Explanation:** Because it may gather many objects, creation runs in the background.

---

### Slide 29 — Creating a Collection from File Import
**On the slide:** Collections can be built from a **text/CSV file of STEP IDs** of products, assets, or classifications. Objects **must already exist** (import only places them in a collection — it won't create/update objects). **Important:** if your file has only **attribute values or unique keys** (no STEP ID), you must use the **Save as Collection from Search** approach instead.

**Explanation:** The file-import method works **only with STEP IDs**. If all you have is keys/attribute values, you can't import-to-collection directly — instead search by those values (e.g., "Search from List," slide 16) and save the results as a collection.

---

### Slides 30–32 — Creating a Collection from File (the steps)
**On the slide:** 30) **Right-click** the Collections top node or a group → **"Create Collection From File"** (this sets where it's saved). 31) In the dialog, locate the file (Collection ID auto-generated). 32) Enter a **Collection Name**, set **"File Contains"** (IDs of products / classifications / assets), click OK to start a **background process**.

**Explanation:** The click-by-click for file import. The key parameter is **"File Contains"** — you tell STEP which object type the IDs refer to so it links them correctly.

---

### Slide 33 — Thank You / Contact
**On the slide:** "Thank You — STIBO CoE Team."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Tool | Key points |
|---|---|
| **Goto search** | Jump to one object by Name/ID/Key; no result list |
| **Search tab** | Build queries; targeted or broad-then-refine |
| **Wildcards** | `*` = many chars, `?` = one; leading `*` is **slow** |
| **`ID=` / `Name=`** | Limit scope to identity |
| **Full-text indexable** | Word search without wildcards (fast) |
| **Criteria logic** | AND (default) · OR · Exclude/NOT |
| **Search from List** | Paste many values (e.g., from Excel) to find all |
| **Profiling page** | Facet-style drill-down to refine results |
| **Collection** | Saved, **flat** set of objects; from search or file |
| **File→Collection** | Needs **STEP IDs**; objects must already exist |
| **Bulk Update** | Operations per object, in order, atomic per object |
| **No undo** | Preview 10 → test small → then run full |
| **Schedule** | Collection + Bulk Update Configuration → run later |

**The classic flow:** Search → Save as Collection → (schedule) Bulk Update.

#### How this connects to other modules
- **Bulk Update "Run Business Rule"** ties back to the **Business Rules** deck (mass logic-driven changes).
- Searching by **unique key** ties back to the **ID/URL/Key** deck.
- Full-text indexing comes from **Data Modeling** (attribute settings).


<div style="page-break-after: always;"></div>

# Chapter 8. Matching & Linking

> A slide-by-slide companion to the *Matching and Linking* deck (23 slides). This is STEP's **deduplication** engine: finding records that are really the same thing (the same product, the same customer) and either merging them or building a single trusted **Golden Record**.

---

### The 30-second mental model (read this first)

The problem: in big datasets you can't compare every object with every other (that's billions of comparisons). The solution has four moving parts:

1. **Match Code** — a short text "fingerprint" of each object. Sort all fingerprints alphabetically; only compare objects whose fingerprints are **near each other** (controlled by **Window Size**). This slashes the number of comparisons.
2. **Matching Algorithm** — compares two candidate objects and outputs a **0–100% similarity** score.
3. **Match Action** — what to do with matches: **Identify Duplicates** (just flag them) or **Golden Record** (build one trusted record from the duplicates using **Survivorship Rules**).
4. **Event Processor** — the runtime that triggers matching automatically as data changes; near-miss scores go to a **clerical review** workflow for humans to decide.

---

### Slides 1–2 — Template / "Attention" intro slides
**On the slides:** Slide-design template and trainer framework.

**Explanation:** Authoring scaffolding. Skip. (Note: this deck carries the trainer's "Attention / Need-Benefits" notes throughout — those are facilitation prompts, not STEP content.)

---

### Slide 3 — Purpose
**On the slide:** You'll learn how matching/linking works: the **process to identify duplicates** and **how to handle potential duplicates**.

**Explanation:** Two halves to the whole module — *finding* duplicates and *resolving* them.

---

### Slide 4 — Title
**On the slide:** "Matching and Linking — STIBO CoE and Team."

**Explanation:** Section opener.

---

### Slide 5 — Terminal Objective (agenda)
**On the slide:** Topics: Matching & Linking; generating **match code** and **matching algorithm**; **identify** duplicates; **handle** duplicates; **configure event processor**.

**Explanation:** The agenda = the four moving parts plus the runtime. Use it as your checklist.

---

### Slide 6 — What Matching & Linking Is
**On the slide:** The component identifies and handles duplicate **Product, Entity, Asset, and Classification** objects. Two parts: **identifying** duplicates and **handling** them. Before "Trailblazer," handling was limited to **manual merging**; Trailblazer added **automatic Golden Records** using configurable **Survivorship Rules**.

**Explanation:** Sets scope (works on Products, Entities, Assets, Classifications) and history (modern STEP can auto-build golden records, not just manually merge). "Trailblazer" is a STEP release name — the takeaway is that automated golden-record creation is the modern capability.

---

### Slide 7 — Strategy for Identifying Duplicates
**On the slide:** First **define what makes two objects duplicates**: for Products, maybe same **EAN** or same/similar **manufacturer + part number**; for party data, similar **names + addresses**. Comparing every object to every other is **not viable** at scale. So **Match Codes** are generated and evaluated/matched by a **Matching Algorithm**. Matches can be handled by **merging** or by generating **Golden Records** (combining data into one "true" record). Matched objects can either **stay and link** to the golden record, or be **permanently merged** into it.

**Explanation:** The strategic overview. Step 1 is a *business* decision: what counts as "the same"? Step 2 is the scalability trick (match codes). Step 3 is resolution (merge vs golden record; link vs merge). Two resolution styles to remember:
- **Link Golden Record** — sources stay in STEP, linked to the golden record.
- **Merge Golden Record** — sources are merged/stored outside; one record remains.

---

### Slide 8 — The Four Underlying Elements
**On the slide:** Matching relies on four elements: **Match Codes, a Matching Algorithm, an Event Processor, and an Inbound Integration Endpoint.** Together they evaluate a dataset and initiate maintenance: match codes are generated, then the algorithm evaluates them for potential duplicates.

**Explanation:** The architecture in one line. Match codes (fingerprints) + algorithm (comparison) + event processor (automation trigger) + inbound endpoint (so incoming data gets matched on arrival). Keep these four straight — the rest of the deck details each.

---

### Slide 9 — Match Code (the core idea)
**On the slide:** A match code is a **string representing an object**, built via **STEP Functions or JavaScript** (e.g., two attribute values concatenated). Generated codes populate an **alphabetically sorted table**. Rather than comparing all objects, **only objects with codes near each other** in the sorted list are compared — making comparisons **linearly proportional** to the number of objects. How many an object compares against is set by the **Window Size**. Example: manufacturer info + manufacturer part number concatenated.

**Explanation:** This is the clever heart of the whole system. By turning each object into a sortable fingerprint and only comparing **neighbors** in the sorted list, STEP converts an impossible "everything-vs-everything" (quadratic) problem into a manageable linear one. **Window Size** = how many neighbors above/below to compare against (bigger = more thorough but slower). The fingerprint is built with the same STEP Functions / JavaScript you learned earlier.

---

### Slide 10 — Match Code (design considerations)
**On the slide:**
- **Profile the data first** — check how well-populated an attribute is before using it (use the data profiling tool).
- Put the **most significant data first** in a composite match code (because the list is sorted left-to-right).
- **Multiple match codes per object** are allowed — STEP Functions can return a **list**, JavaScript an **array**; each element is a separate code.
- Example: for customers with name + address, a single "address+name" code would **miss customers who moved** (their codes drift apart). Better: give each object **two** codes — one for **Name**, one for **Address** — so they can match on *either* (add a **hardcoded prefix** to each so name-codes only compare with name-codes, not address-codes).

**Explanation:** The practical wisdom. Three lessons:
1. **Garbage in, garbage out** — a match code built on a 10%-populated attribute is useless; profile first.
2. **Order matters** because codes sort left-to-right — lead with the most discriminating field.
3. **Multiple codes** let an object match on different dimensions. The moved-customer example is the classic case: index by name *and* by address separately, with prefixes (`NAME_…`, `ADDR_…`) so the two "domains" never cross-compare.

---

### Slide 11 — Matching Algorithm
**On the slide:** Match codes only **limit comparisons**; the actual comparison is done by a **Matching Algorithm**, which is also where the **Match Action** (Golden Record / Identify Duplicates) is configured. An algorithm compares two objects and returns **0%–100%** equality.

**Explanation:** Division of labor: **match codes pick *who* to compare; the algorithm decides *how alike* they are.** The output is a similarity percentage, and the algorithm object also holds the decision about what to do with matches (the Match Action).

---

### Slide 12 — Match Criteria
**On the slide:** The matching logic is defined under the **"Match Criteria"** flipper of the matching algorithm. **Binds** used in the logic are defined under the **"Global Binds"** flipper.

**Explanation:** Where you author the comparison. **Match Criteria** = the actual similarity rules. **Global Binds** = reusable variables/objects bound for use in those rules (same "binds" concept from the Business Rules/JavaScript world).

---

### Slide 13 — String Comparison (edit distance)
**On the slide:** One approach is **edit distance**, in STEP the **Levenshtein distance** — how many edits (substitution, insertion, deletion) to turn one string into another. STEP can apply **Levenshtein and Damerau-Levenshtein** distance to strings you build with STEP Functions and output an equality measure. String comparison alone often isn't enough, so additional criterion types exist (next slide).

**Explanation:** The math behind "similar strings." **Levenshtein distance** counts the minimal edits between two texts (e.g., "Jon" → "John" = 1 insertion). Fewer edits = more similar. **Damerau-Levenshtein** adds **transposition** (swapping two adjacent characters) as a single edit. STEP turns these into a 0–100% score — perfect for typos and minor spelling variants.

---

### Slide 14 — More Comparison Criteria
**On the slide:**
- **Multi Word Damerau-Levenshtein** — like Damerau-Levenshtein, but **swapping two whole words** doesn't count as an edit.
- **Number Distance** — relative closeness of two numbers as a percentage: **lowest / highest × 100**.
- **JavaScript Criterion** — write your own comparison; must return **0–100**.
- **Decision Tables** — break complex matching into smaller, manageable parts.

**Explanation:** The criterion toolbox beyond plain string distance. **Multi-word** handles "John Smith" vs "Smith John" (word order shouldn't penalize). **Number Distance** compares numeric fields (e.g., weights/prices) proportionally. **JavaScript** is the escape hatch for custom logic. **Decision Tables** let you compose many sub-comparisons into an overall match decision without one giant unreadable rule.

---

### Slide 15 — Handling Duplicates: the two Match Actions
**On the slide:**
- **Identify Duplicates** — possible matches are inspected from the Matching Algorithm object; the only parameter is a **threshold** (how equal objects must be to be flagged).
- **Golden Records** — instead of merging, create a **new "Golden Record"** from the duplicates' data. Setup tasks: create a golden-record **object type**; create a golden-record **reference type** (if applicable); create a golden-record **root node** (where golden records start); specify the golden-record object type in the **component models**; configure the object type/root node/reference type/default source system on the **match action**; set the **auto threshold** and **clerical review threshold**; optionally configure a **clerical review workflow**.

**Explanation:** Two ways to *resolve* matches.
- **Identify Duplicates** = just *flag* — humans/processes decide later. One knob: the similarity threshold.
- **Golden Record** = *build a single trusted record* automatically. It needs real setup (a place to put golden records, the types involved, source-system info) and **two thresholds**:
  - **Auto threshold** — above this, STEP auto-merges/creates the golden record (confident match).
  - **Clerical review threshold** — between the two thresholds, it's a *maybe* → routed to a human via a **clerical review workflow**. Below the review threshold, no match.

---

### Slide 16 — Survivorship Rules (intro + Trusted Source)
**On the slide:** Golden-record attribute/reference data is copied from the source objects automatically per **Survivorship Rules** set on the matching algorithm. Rules can be defined independently for **name, references, data containers, and attributes/attribute groups**. Survivorship rules apply to **Merge Golden Record** (sources stored outside STEP) and **Link Golden Record** (sources stored in STEP); both **require** survivorship rules. Two concepts decide which source to take data from — first: **Trusted Source** (requires source info to be available on the source objects).

**Explanation:** When three records say three different things, *which value wins?* That's **survivorship**. Rules are **field-class specific** (name vs references vs attributes can each have their own rule). **Trusted Source** = "prefer data from the more authoritative system" (e.g., ERP beats a spreadsheet) — which only works if each source object records *where it came from*.

---

### Slide 17 — Survivorship Rules (Most Recent + combining)
**On the slide:** **Most Recent** — take data from the source object with the **most recent** data. **Survivorship Rule Types** — you can **combine** Most Recent and Trusted Source strategies.

**Explanation:** The second survivorship strategy: **Most Recent** = "freshest value wins" (by timestamp). And you can blend strategies — e.g., *prefer the trusted source, but if tied, take the most recent.* This gives nuanced control over how the golden record is assembled.

---

### Slide 18 — Keeping Matching Up-to-Date (incremental)
**On the slide:** After initial match-code generation and algorithm application, you can keep things current **without regenerating everything**, via two **Business Action / Bulk Update** operations:
- **Generate Match Codes** — takes a Match Code ID; generates codes for the objects it's applied to.
- **Match Duplicates (apply matching algorithm)** — takes a Matching Algorithm ID; compares the just-coded object against objects with similar/identical codes (Window Size applies).

**Explanation:** Matching isn't a one-time batch. As new/changed objects arrive, you only need to (1) generate *their* match codes and (2) match *just them* against their neighbors — incremental, not a full re-run. These run as Business Actions (so they can be triggered automatically) or Bulk Updates (manual mass runs). This is what the Event Processor automates.

---

### Slide 19 — Configuring the Matching Event Processor
**On the slide:** To deduplicate automatically, configure an **event processor** to trigger the matching algorithm. It **creates events for matching** so the algorithm runs. Potential duplicates scoring **between the clerical review threshold and the auto threshold** are placed into **clerical workflow tasks** for manual deduplication. Steps: **create** the matching event processor → **enable** it → it's ready to run.

**Explanation:** The runtime that makes matching "live." Instead of you manually running the operations from slide 18, the event processor watches for changes, fires the match operations, and **routes the uncertain middle-band matches to humans** (the clerical review workflow from slide 15). This is how ongoing dedup happens without manual intervention.

---

### Slide 20 — Initial Configuration: the Matching Component Model
**On the slide:** Before any match codes/algorithms work, configure the **Matching Component Model**, which **defines all object types allowed to be matched.** In **System Setup → Component Models → Matching node → Component Model Configuration tab → Edit.**

**Explanation:** The prerequisite/foundation step. The component model is the *whitelist* of which object types matching is even allowed to operate on. Nothing else in this module functions until this is set — so in practice this is actually the **first** thing you configure.

---

### Slide 21 — Initial Configuration (screenshot)
**On the slide:** (UI screenshot of the configuration.)

**Explanation:** Visual reference for the component-model setup; no new concept.

---

### Slide 22 — Recap / Review
**On the slide:** Covered: matching & linking; generating match code and matching algorithm; identify duplicates; handle duplicates; configure event processor (plus references to Assets / export mechanisms as upcoming topics).

**Explanation:** The deck's own summary — a good self-test checklist before moving on.

---

### Slide 23 — Thank You / Contact
**On the slide:** "Thank You — STIBO CoE and Team."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Element | Role |
|---|---|
| **Match Code** | Sortable text fingerprint; only near-neighbors get compared |
| **Window Size** | How many neighbors to compare (thoroughness vs speed) |
| **Multiple match codes** | Match on different dimensions (name *and* address) + prefixes |
| **Matching Algorithm** | Compares two objects → 0–100% similarity |
| **Match Criteria / Global Binds** | Where the comparison logic / reusable binds live |
| **Levenshtein** | Edit distance (sub/ins/del); Damerau adds transposition |
| **Multi-word D-L** | Word swaps don't count |
| **Number Distance** | low/high × 100 |
| **Match Action: Identify Duplicates** | Just flag; one threshold |
| **Match Action: Golden Record** | Build one trusted record |
| **Auto threshold** | Above → auto golden record |
| **Clerical review threshold** | Between thresholds → human review workflow |
| **Survivorship Rules** | Which source's value wins per field |
| **Trusted Source / Most Recent** | Authority-based / freshness-based winners (combinable) |
| **Event Processor** | Automates matching on change; routes uncertain matches to humans |
| **Matching Component Model** | Whitelist of matchable object types (configure **first**) |

**Pipeline:** Component Model → Match Codes → Matching Algorithm + Criteria → Match Action (Identify / Golden Record + Survivorship) → Event Processor (live) → Clerical Review for the uncertain middle.

#### How this connects to other modules
- **STEP Functions / Business Rules / JavaScript** build match codes and match criteria.
- **Bulk Updates** (previous deck) run the Generate/Match operations manually.
- **Workflows** power the clerical review of uncertain matches.
- **Inbound Integration Endpoints** (upcoming) match incoming data on arrival.


<div style="page-break-after: always;"></div>

# Chapter 9. STEP XML

> A slide-by-slide companion to the *Step XML* deck (16 slides). STEPXML is STEP's **native** data format. Every piece of data that enters or leaves STEP is internally STEPXML — even a CSV import is converted to STEPXML first. It's the format for moving data *and configuration* between STEP systems and for system-to-system integration.

---

### The 30-second mental model (read this first)

STEPXML is STEP's own XML language. Two things make it special:
1. **It can carry almost everything** — not just product data, but configuration objects too (attributes, reference types, etc.). Other formats (CSV/Excel) only handle specific object types.
2. **It's the internal lingua franca** — all import/export ultimately flows through STEPXML, so a CSV is converted to STEPXML before importing.

Because it's native, **STEPXML needs no mapping** (the field names *are* STEP's structure). Its killer use case is moving data/config between **DTAP** environments (Dev → Test → Acceptance → Production).

---

### Slide 1 — Title
**On the slide:** "Stibo STEP L1 Training — STEP XML."

**Explanation:** Section opener.

---

### Slide 2 — About the Author
**On the slide:** Created by the Stibo CoE team; v1.0; references STIBO official docs.

**Explanation:** Housekeeping. Authoritative source = STIBO docs.

---

### Slide 3 — Introduction to STEP XML
**On the slide:** STEPXML is STEP's **native XML format**. Unlike other import/export formats (limited to specific super/node types), STEPXML can import/export **most STEP configuration and data objects**. Especially suited for transferring data/config across **DTAP** environments and for inbound integrations with systems/middleware that produce STEPXML. **All data entering/exiting STEP uses STEPXML** internally — e.g., a CSV selected for import is converted to STEPXML, then imported. **Limitations:**
- Historical data (old revisions) can't be exported/imported.
- Asset **content** (binary files) can be exported but **not** imported.
- **Table** data can be exported but not imported.
- Individual values of existing **multivalued** attributes can't be exported/imported.
- Legal source/target object types for existing reference/link definitions can't be added/removed.
- Legal **units** for existing attributes can't be removed.

**Explanation:** The defining slide. Two big ideas: STEPXML is **comprehensive** (data + config) and **internal** (everything becomes STEPXML under the hood). The DTAP use case is why admins love it — you can lift a configuration out of Dev and load it into Test/Prod. Memorize the limitations; they're common exam/interview points, especially **"asset content and table data export but don't import"** and **"no historical/revision data."**

---

### Slide 4 — General Steps to Export STEP XML
**On the slide:** The Export Manager steps:
- **Select Configuration** — reuse a saved config or start fresh.
- **Select Objects** — pick hierarchy nodes (or modify those from a config).
- **Select Format** — the output file format.
- **Map Data** — which info is extracted per object.
- **Advanced** — convert exported data to another output format.
- **Select Delivery Method** — how the output is delivered.

**Explanation:** The export pipeline you'll see for *all* exports (same wizard as tabular). For STEPXML specifically, "Map Data" matters less because the format already mirrors STEP's structure — but the steps are the same shape.

---

### Slide 5 — Export: Select Configuration & Objects
**On the slide:** STEPXML is exported via the **Export Manager** or **Outbound Integration Endpoints**. Because "Select Objects" only lets you pick **Tree** objects and a few System Setup objects — yet STEPXML can export far more — you can run a STEPXML export **without selecting any objects at all**. To export specific branches of the Product/Entity/Classification hierarchy, select the **root nodes** here. You must first select (or create) a **configuration**.

**Explanation:** A subtle but important point: with STEPXML you can export configuration/system objects *without picking tree objects* (since those aren't in the tree). When you *do* want data, you select root nodes and STEP walks down from there. Two delivery paths: ad-hoc (Export Manager) or automated (Outbound Integration Endpoint).

---

### Slide 6 — Export: Select Format (the options)
**On the slide:** Two STEPXML format options: **"STEPXML"** and **"Advanced STEPXML."** Choosing "STEPXML" reveals a long list of dropdown options that control exactly what goes in the file. Parameter categories:
- **Global Settings** — apply to both data and configuration objects.
- **Data Objects** — apply to data-holding objects (common options at top, similar options grouped).
- **Configuration** — listed alphabetically, applied to the labeled item.
- **Publishing** — typically for print applications.

**Explanation:** STEPXML export is highly configurable through these dropdown categories. You're deciding *how much* to pull (just the selected objects? their references too? their config?). The next slide gives a concrete example of the most important data-object options.

---

### Slide 7 — Export Example (the include options)
**On the slide:** To export a hierarchy *plus* the Product/Classification/Asset objects it references, with "Televisions" as root:
- **Include Products: Referenced** — selected product, its descendants, and referenced products.
- **Include Product Attribute Values: All** — get **local** values out (inherited values are **not** exported by default).
- **Include Assets: Minimum** — just the referenced assets.
- **Include Classifications: Minimum** — linked classifications **plus all ancestors up to the top** classification node (a special feature for classifications).

**Explanation:** These four "Include" settings are the heart of controlling export scope:
- **Include Products: Referenced** pulls related products, not just the branch.
- **Attribute Values: All** vs default — note **inherited values aren't exported by default** (only local). This trips people up: an exported product may look "empty" for fields it was inheriting.
- **Minimum** for assets/classifications pulls only what's needed to keep references valid. The classification quirk — it also grabs **all ancestor classifications** so the tree path stays intact.

---

### Slide 8 — Export: Flatten Hierarchy
**On the slide:** Products and Classifications export by default in **nested** structures (Product elements inside Product elements). For a **flat** structure (no nesting), select **"Flatten hierarchy: yes."**

**Explanation:** Two ways to represent a tree in XML: **nested** (children physically inside parents) or **flat** (every object listed separately, linked by `ParentID`). Flat is often easier for downstream systems to parse. Slide 13 shows both forms of the same data.

---

### Slide 9 — Export: Map Data
**On the slide:** Map data to export attributes, references, etc., and **transform** if necessary.

**Explanation:** Even for native STEPXML you can apply transformations (reformat values, convert units) during export. For pure STEPXML this step is lighter than for tabular exports.

---

### Slide 10 — Export: Advanced & Delivery
**On the slide:** **Advanced** adds flexibility: **tag conversion**, **resolve inline references**, etc. **Delivery method** controls how the recipient gets the data.

**Explanation:** "Tag conversion" handles STEP's inline rich-text style tags. "Resolve inline references" decides whether reference placeholders are expanded. Delivery options mirror the tabular export (file, FTP/SFTP, email, server-side — see the tabular deck).

---

### Slide 11 — Where Export STEP XML Is Used
**On the slide:** **Outbound Integration Endpoint** (send to downstream systems) and **Export Manager** (ad-hoc exports).

**Explanation:** Same two channels as slide 5: scheduled/automated integration vs manual one-offs.

---

### Slides 12–13 — STEP XML Example (the actual format)
**On the slide / notes:** A single Product of object type **SKU** (`UserTypeID="SKU"`) is shown, including a **linked Classification**, a **referenced Asset**, and **Attributes**. The notes give the real XML:
```xml
<STEP-ProductInformation ContextID="GL" WorkspaceID="Main">
  <Products>
    <Product ID="L6577" UserTypeID="SKU" ParentID="UNSPSC000.52161505">
      <Name>Samsung UN70ES8000F</Name>
      <ClassificationReference ClassificationID="TVs" Type="Web Classification"/>
      <ProductCrossReference ProductID="L6587" Type="HE Accessory"/>
      <AssetCrossReference AssetID="UN55ES8000F-1" Type="Primary Image"/>
      <Values>
        <Value AttributeID="Horizontal Pixels">1920</Value>
        <Value AttributeID="Diagonal Screen Size" UnitID="unece.unit.INH">55</Value>
        <MultiValue AttributeID="Ports">
          <Value>HDMI</Value>
          <Value>Component Video</Value>
        </MultiValue>
        ...
      </Values>
    </Product>
  </Products>
</STEP-ProductInformation>
```
It can also be **nested** vs **non-nested**, and a single XML can hold **multiple products + referenced products**.

**Explanation:** This is the format you must learn to *read*. Decode the structure:
- Root carries **`ContextID`** (the lens) and **`WorkspaceID`** (Main/Approved).
- Each `<Product>` has `ID`, **`UserTypeID`** (= the object type), and `ParentID` (its place in the hierarchy).
- `<ClassificationReference>`, `<ProductCrossReference>`, `<AssetCrossReference>` = the typed references (note `Type=` names the reference type).
- `<Values>` holds attributes; **`UnitID`** carries units; **`<MultiValue>`** holds multivalued attributes.
- **Nested vs non-nested** (slide 8): nested puts child `<Product>` inside parent; non-nested lists each product flatly with `ParentID` pointing up. Both express the *same* hierarchy. Being able to recognize `UserTypeID`, `ParentID`, `Values`, and reference elements is the practical skill here.

---

### Slide 14 — Import STEP XML
**On the slide:** STEPXML can carry **processing instructions** for import. Because these are similar to (or beyond) the Import Manager's tabular options, and **STEPXML needs no mapping**, there's little to configure when importing it. Import of STEPXML can: **create** objects (Tree and System Setup), **update/delete** existing objects, **delete values and references/links**, and **delete objects** (Products, Entities, Classifications, Assets, Attributes, LOVs, Units).

**Explanation:** The big advantage on import: **no mapping needed** (the XML field names *are* STEP's structure). And it's powerful — STEPXML can create *and* delete both data and configuration, including LOVs and Units. Contrast with the limitations on slide 3 (can't import asset content/table data/historical data). This makes STEPXML the tool for full system-to-system replication and DTAP promotion.

---

### Slide 15 — Where Import STEP XML Is Used
**On the slide:** **Inbound Integration Endpoint** (receive from source systems) and **Import Manager** (ad-hoc).

**Explanation:** Mirror of slide 11 for the inbound direction.

---

### Slide 16 — Module Complete
**On the slide:** "You have successfully completed STEP XML."

**Explanation:** Wrap-up marker.

---

### Quick-revision cheat sheet

| Point | Detail |
|---|---|
| **What it is** | STEP's **native** XML; the internal format all I/O converts to |
| **Coverage** | Data **and** configuration objects (unlike CSV/Excel) |
| **No mapping** | Field names = STEP structure → import needs little config |
| **Best use** | **DTAP** promotion; system-to-system integration |
| **Channels** | Export/Import Manager (ad-hoc) · Integration Endpoints (automated) |
| **Scope control** | Include Products/Assets/Classifications: Referenced/Minimum/All |
| **Inherited values** | **Not** exported by default (only local) |
| **Nested vs flat** | "Flatten hierarchy: yes" for flat; both express same tree |
| **Key XML bits** | `ContextID`, `WorkspaceID`, `UserTypeID` (=type), `ParentID`, `<Values>`, `<MultiValue>`, `UnitID`, reference elements |
| **Import can** | Create/update/delete data **and** config (incl. LOVs, Units) |
| **Limitations** | No historical data; asset content & table data **export-only**; can't add/remove existing reference legal types; can't remove existing units |

#### How this connects to other modules
- **Tabular Import/Export** uses the same wizard — and converts to STEPXML under the hood.
- **Integration Endpoints** (next) are the automated inbound/outbound channels.
- `ContextID`/`WorkspaceID` come from **Data Modeling** (contexts) and **Approvals** (workspaces).


<div style="page-break-after: always;"></div>

# Chapter 10. Generic XML

> A slide-by-slide companion to the *STEP Generic XML* deck (14 slides). Where STEPXML is STEP's *own* format, **Generic XML** lets STEP read and write **other systems' arbitrary XML formats** — without custom code — by using a **template with processing instructions**.

---

### The 30-second mental model (read this first)

External systems each have their own XML shape. Generic XML bridges them to STEP using a **sample/template XML** annotated with **processing instructions** (the `<?...?>` placeholders).

- **Inbound:** STEP matches the incoming XML against your template, extracts the marked values into a **tabular (row/column) form**, then imports it through the normal Import Manager — *as if it were a CSV*.
- **Outbound:** symmetrical — you define a template with placeholders, map STEP data into them, and STEP emits XML in that exact shape.

So Generic XML is essentially "**XML ↔ table converter driven by a template**," reusing the import/export machinery you already know.

---

### Slides 1–2 — Template / "Attention" intro slides
**On the slides:** Slide-design template and trainer framework.

**Explanation:** Authoring scaffolding. Skip.

---

### Slide 3 — Generic XML
**On the slide:** Generic XML lets STEP **import from and export to a variety of XML formats without extensions/customizations**. It's a widely accepted way to exchange data. Involves **inbound** (XML → STEP) and **outbound** (STEP → XML) options.

**Explanation:** The headline benefit: **no custom coding**. Before this, reading a partner's bespoke XML meant building an extension. Generic XML replaces that with configuration (a template). It works both directions.

---

### Slide 4 — Limitations
**On the slide:** Key limitations:
- Only **Products, Entities, Classifications, Assets, and Attribute Definitions** can be **imported**; only **Products** can be **exported**.
- It **cannot handle nested records**.
- You **cannot delete** data or objects when importing Generic XML.

**Explanation:** Important constraints (and a frequent point of confusion vs STEPXML):
- **Export is Products-only** — for anything else outbound, use STEPXML/tabular.
- **No nested records** — Generic XML flattens to rows, so deeply nested/recursive XML doesn't fit (unlike STEPXML, which handles nesting).
- **No deletion** on import — create/update only. If you need deletes, use STEPXML.
Rule of thumb: Generic XML for *talking to other systems' formats*; STEPXML for *full-fidelity STEP-to-STEP*.

---

### Slide 5 — Inbound Options (the idea)
**On the slide:** Inbound: parse the XML via a **template with processing instructions** that extracts data into a **tabular format**, then handle it with **standard Import Manager** functionality — just as if importing a CSV/Excel.

**Explanation:** The core trick. The template turns messy XML into a clean table; from there it's the ordinary import flow (map columns, identify objects, etc., from the Tabular deck). You only learn one new thing — the template syntax — and reuse everything else.

---

### Slide 6 — Inbound: the source XML example
**On the slide:** Example incoming XML — a product with a `<General>` block (ProductName, LongDescription, EndDate, FreeReturnFlag, SpecialFeatures), repeating `<Variants>` (Name/Value pairs for Color, Size, Width), and a `<Manufacturer>` block.

**Explanation:** This is the *partner's* format you must consume. Note the repeating `<Variants>` element — the same tag appears multiple times with different Name/Value pairs. Handling repetition is exactly what the processing instructions solve (next slide).

---

### Slide 7 — Inbound: the parsing template
**On the slide:** A template mirrors the source XML but replaces values with **processing instructions**:
```xml
<ProductName><?Source Name?></ProductName>
<LongDescription><?Source?></LongDescription>
...
<Variants>
  <?Repeated?>
  <Name><?SourceID?></Name>
  <Value><?Source?></Value>
</Variants>
```
Once the **sample XML** is provided, the input XML is **matched against it** and the system decodes each value as defined.

**Explanation:** The template is a *copy of the source structure* with the data swapped for instructions:
- **`<?Source?>`** — capture this element's value as a (description) attribute value.
- **`<?Source Name?>`** — map this to the object's **Name**.
- **`<?SourceID?>`** — use this value as an identifier/key.
- **`<?Repeated?>`** — this element repeats; loop over each occurrence (handles the multiple `<Variants>`).
STEP overlays your template onto each incoming file and pulls out the marked values into table columns. You build the template once per partner format.

---

### Slide 8 — Inbound: processing instructions
**On the slide:** (Table describing the available processing instructions.) Based on their usage in the sample XML, the system understands the input type and acts accordingly.

**Explanation:** The full inbound instruction set (e.g., `Source`, `Source Name`, `SourceID`, `Repeated`, and others for keys/parents). Each instruction tells STEP *what role* a given XML element plays. The inbound side is richer than outbound because parsing arbitrary input needs more cases than producing a fixed output.

---

### Slide 9 — Outbound Options (the idea)
**On the slide:** Outbound is **symmetrical**: define a template with **instructions/placeholders**, then **map STEP data into the XML template**, just like exporting CSV/Excel.

**Explanation:** Same mental model, reversed. Instead of "match input to template," it's "fill template with output." You reuse the Export Manager's Map Data step (Tabular deck) to feed STEP values into the placeholders.

---

### Slide 10 — Outbound: fewer instructions
**On the slide:** Generic XML **export is simpler** than import — only **four** processing instructions exist.

**Explanation:** Producing a known output shape needs far less vocabulary than parsing unknown input. The four cover product iteration, single targets, multi-targets, and target identity (next slide shows them in use).

---

### Slide 11 — Outbound: the export template
**On the slide:** Template using outbound instructions:
```xml
<?Product?>
  <GPC><?Target ID?></GPC>
  <PrimarySpecs><ProductInformation><General>
    <ProductName><?Target Name?></ProductName>
    <LongDescription><?Target Long Description?></LongDescription>
    ...
  </General>
  <Variants>
    <?MultiTarget?>
    <Name><?Target AttName?></Name>
    <Value><?Target AttValue?></Value>
  </Variants>
  ...
```

**Explanation:** Decode the outbound instructions:
- **`<?Product?>`** — iterate over each product being exported.
- **`<?Target ...?>`** — a placeholder to be filled with mapped STEP data (e.g., `Target Name`, `Target ID`).
- **`<?MultiTarget?>`** — repeat this block for each value in a multi-mapped set (mirrors inbound `<?Repeated?>`).
You write the *shape* the downstream system expects, mark where data goes, and STEP fills it in.

---

### Slide 12 — Outbound: mapping placeholders
**On the slide:** With this template, the Export Manager's **Map Data** step shows the **placeholders** to map data into. For `<Variants>`, **multiple attributes were selected and mapped at once**, then **transformations** output the attribute name and value into separate elements.

**Explanation:** This shows the power of combining Generic XML with transformations: select several attributes in one go, and use transformations to split each into the `<Name>`/`<Value>` pair the partner wants. The placeholder names from your template appear as mapping targets in the wizard.

---

### Slide 13 — Outbound: the result
**On the slide:** The output is exactly generic XML, easily understood by the downstream system. Summary: **both inbound and outbound flows convert files based on a defined template configured to be understood by STEP.**

**Explanation:** The closing synthesis: Generic XML = **template-driven conversion** in either direction. The downstream system gets XML in *its* shape; STEP internally still works in its own model. Note the example even transformed `FreeReturnFlag` from `Y` to `Yes` during export — transformations let you reshape values, not just move them.

---

### Slide 14 — Thank You / Contact
**On the slide:** "Thank You."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Point | Detail |
|---|---|
| **What it is** | Import/export **other systems' XML** with no custom code |
| **How** | A **template** with **`<?…?>` processing instructions** drives conversion |
| **Inbound** | XML → (template) → table → normal Import Manager |
| **Outbound** | STEP data → mapped into template placeholders → XML |
| **Import scope** | Products, Entities, Classifications, Assets, Attribute Definitions |
| **Export scope** | **Products only** |
| **No nested records** | Flattens to rows (unlike STEPXML) |
| **No deletes on import** | Create/update only |
| **Inbound instructions** | `<?Source?>`, `<?Source Name?>`, `<?SourceID?>`, `<?Repeated?>`, … |
| **Outbound instructions** | only **4** — `<?Product?>`, `<?Target …?>`, `<?MultiTarget?>` … |
| **Transformations** | Reshape values during map (e.g., `Y` → `Yes`) |

**Generic XML vs STEPXML:** Generic = *foreign* XML formats, limited scope, no nesting/deletes. STEPXML = *native*, full data+config, nesting, deletes — use it for STEP-to-STEP/DTAP.

#### How this connects to other modules
- Reuses the **Import/Export Manager** wizard from the **Tabular** deck (map, identify, transform).
- **STEP XML** (previous) is the native counterpart — know when to use which.
- Often wired into **Integration Endpoints** (next) for automated partner feeds.


<div style="page-break-after: always;"></div>

# Chapter 11. Tabular Format Import & Export

> A slide-by-slide companion to the *Tabular Format Export and Import* deck (23 slides). "Tabular" = **Excel/CSV** — objects in **rows**, properties in **columns**. This is the everyday, business-user-friendly way to get data in and out of STEP, driven by the **Import Manager** and **Export Manager** wizards.

---

### The 30-second mental model (read this first)

STEP works with spreadsheets where **each row = one object** and **each column = one property** (a name, ID, or attribute value). Two wizards:

- **Import Manager** — load a CSV/Excel: pick the file → tell STEP the format → **map columns to STEP fields** → **identify** which rows are new vs existing → set destination → optional business rules → advanced options → run (as a background process).
- **Export Manager** — same shape in reverse: pick objects → format → **map STEP data to columns** → advanced options → choose delivery.

Both let you **save the configuration** for reuse, and both run as **background processes** you can monitor.

---

### Slides 1–2 — Template / "Attention" intro slides
**On the slides:** Slide-design template and trainer framework.

**Explanation:** Authoring scaffolding. Skip.

---

### Slide 3 — Module Objectives
**On the slide:** You'll be able to **import and export** data via the **tabular (Excel) method** — steps to import, steps to export.

**Explanation:** Roadmap: the two wizards, end to end.

---

### Slide 4 — Section Title
**On the slide:** "Tabular Format Import and Export — STIBO CoE Team."

**Explanation:** Section opener.

---

### Slide 5 — What You Can Import
**On the slide:** The Import Manager can create/update: **Products, Classifications, Entities, Attributes (objects/definitions), Asset Metadata.**

**Explanation:** Tabular import covers the main data object types **plus** attribute definitions and asset *metadata* (note: metadata, **not** the binary asset files — those are handled by DAM). This is narrower than STEPXML (which also does full config), but it's what business users need day to day.

---

### Slide 6 — Import Basics (rows & columns)
**On the slide:** Out of the box, STEP handles tabular files where **objects are rows and properties are columns.**

**Explanation:** The fundamental shape. If your spreadsheet isn't "one object per row, one property per column," you must reshape it first (or use Generic XML / a transformation). This row/column expectation is the single most important thing to get right before importing.

---

### Slide 7 — Import Wizard: Steps 1–2
**On the slide:**
- **Step 1 — Select Configuration:** use an existing import configuration or create a new one.
- **Step 2 — Select Data Source:** choose where the data comes from (if a File, browse to the load file).

**Explanation:** Start by reusing a saved config (huge time-saver for recurring imports) or starting fresh, then point at the source file. "Data Source" can be more than a file (e.g., a delivered feed), but file is the common case.

---

### Slide 8 — Import Wizard: Step 3
**On the slide:** **Step 3 — Select Format:** choose the file type and basic file parameters.

**Explanation:** Tell STEP it's CSV vs Excel and set parameters like delimiter, encoding, header row, etc. Getting these right is what makes columns line up correctly.

---

### Slide 9 — Import Wizard: Step 4 (Map Data)
**On the slide:** **Step 4 — Map Data:** map the file's columns to the appropriate STEP data. You can map a **Constant** (fixed value), add **Transformations**, and use **variables**.

**Explanation:** The heart of import. You connect "Column B" → "the Weight attribute," and so on. Beyond straight mapping you can:
- inject a **Constant** (e.g., set every row's Status = "New"),
- apply **Transformations** (trim, uppercase, convert units, split/concatenate),
- use **variables** to reuse computed values.
This is where messy source data gets cleaned into STEP's expected form.

---

### Slide 10 — Import Wizard: Steps 5–6
**On the slide:**
- **Step 5 — Identify Products:** shows whether objects are **new or existing**. Without STEP IDs in the file, you can identify existing objects by **attribute values**.
- **Step 6 — Identify Destination:** specify a default **Object Type** and **parent** for new objects.

**Explanation:** Two crucial steps.
- **Identify** = matching incoming rows to existing STEP objects. If the file has STEP IDs, easy; if not, STEP can match on attribute values (this is where **unique keys** shine — tie back to the ID/URL/Key deck). Mismatch here → duplicates or failed updates.
- **Destination** = where new objects land (default type + parent), since a new row needs a type and a home in the hierarchy.

---

### Slide 11 — Import Wizard: Steps 7–8
**On the slide:**
- **Step 7 — Select Business Rules:** choose Business Conditions/Actions to test/execute during import (covered in a separate course).
- **Step 8 — Advanced Settings:** e.g., **approve data after import**, and **remove data for existing objects not in the import file**.

**Explanation:**
- **Business Rules** hook in here (ties to the Business Rules deck — conditions reject bad rows, actions enrich/clean).
- **Advanced** has two powerful, sometimes-dangerous options: **auto-approve after import** (data goes straight toward Approved) and **"remove data not in the file"** — a *full-sync* mode where anything missing from the file gets cleared. Use the latter carefully; it can wipe data if your file is incomplete.

---

### Slide 12 — Running the Import
**On the slide:** After the wizard, a **"Save Import Configuration"** dialog lets you save the config for reuse. From there you can **start the Import Background Process**, then jump to the process object in the **Background Processes Navigator**.

**Explanation:** Two outcomes from finishing the wizard: **save the recipe** (so next month's import is one click) and **launch the job**. Because imports can be large, they run as background processes rather than blocking your session.

---

### Slide 13 — Execution Report
**On the slide:** Monitor the import via the **Execution Report** of the started Background Process.

**Explanation:** Your audit/troubleshooting view — how many objects created/updated, what errored and why. Always check it after a run to confirm success and catch rejected rows.

---

### Slide 14 — Tabular Exports (what you can export)
**On the slide:** The Export Manager exports **Excel/CSV** for node types: **Products, Classifications, Entities, Attributes (objects/definitions), Asset Metadata.** Features: multiple ways to select objects, choose exactly what data to export and **transform** it, and **save an Export Configuration** for reuse.

**Explanation:** Mirror of slide 5 for output. Same object types; same reuse-via-saved-config benefit; transformations available on the way out (e.g., reformat dates, convert units).

---

### Slide 15 — Export Wizard: Step 1 (launch)
**On the slide:** Launch the Export wizard two ways: **File menu**, or **right-click a hierarchy node → "Export Data Below."**

**Explanation:** Right-clicking a node is the quick path — it pre-selects everything beneath that node (and skips the object-selection step, per slide 17).

---

### Slide 16 — Export Wizard: Step 2 (configuration)
**On the slide:** **Create or reuse** an Export Configuration.

**Explanation:** Same reuse pattern as import — saved configs make recurring exports trivial.

---

### Slide 17 — Export Wizard: Step 3 (select objects)
**On the slide:** Export Manager initially works on **all objects below and including your selection**. If started from a node's context menu, **this step is skipped.**

**Explanation:** Exports are hierarchy-scoped: pick a node and you get it plus its descendants. Launching from the right-click menu already chose the node, so the wizard skips ahead.

---

### Slide 18 — Export Wizard: Step 4 (format)
**On the slide:** **Select Format** offers several output formats; here only **Excel and CSV** are described.

**Explanation:** Same wizard also offers XML formats (STEPXML/Generic XML — the prior decks); this module focuses on the spreadsheet formats.

---

### Slide 19 — Export Wizard: Step 5 (Map Data)
**On the slide:** **Map STEP data to columns.** Each part can be manipulated by: selecting a different **Aspect**, mapping a **Constant**, applying a **Transformation**, or mapping **additional STEP data** to either part.

**Explanation:** The export counterpart to import mapping. New concept: **Aspect** — which "view" of a value to output (e.g., the value vs its unit, or a value in a particular context). Plus constants, transformations, and combining multiple STEP fields into one column. This controls exactly what each column contains.

---

### Slide 20 — Export Wizard: Step 6 (Advanced Options)
**On the slide:**
- **Tag conversion** — convert STEP rich-text tags into other tag formats in the output.
- **Locale conversion from context** — format dates/numbers per the **context's locale**.
- **Resolve Inline References** — whether to expand inline references.
- **Include Calculated Attribute Values** — whether to compute and include calculated attributes.
- **Workspace / Context** — run the export from a **different Context/Workspace** than where it was started.

**Explanation:** Important output controls:
- **Locale conversion** ensures dates/numbers come out in the right regional format for the target market (ties to Contexts).
- **Include Calculated Attribute Values** — off by default consideration; calculated values are computed at export time (recall the performance note from the Functions deck).
- **Workspace/Context** lets you export, say, the **Approved** workspace's **French** data even if you're working in Main/English — very useful for publishing.

---

### Slide 21 — Export Wizard: Step 7 (Delivery)
**On the slide:** Delivery options: **File** (available on the Export Background Process instance), **FTP/SFTP**, **Email**, **Server-Side Delivery** (to a directory on the application server).

**Explanation:** How the finished file reaches its destination. **File** = download from the job; **FTP/SFTP** and **Server-Side** = automated drop to a system/folder; **Email** = send to people. These same delivery options apply to XML exports too.

---

### Slide 22 — Running the Export
**On the slide:** With **File** delivery, the exported CSV/Excel is available from the **Background Process instance**.

**Explanation:** Like imports, exports run as background processes; with File delivery you retrieve the result from that job once it finishes.

---

### Slide 23 — Thank You / Contact
**On the slide:** "Thank You — STIBO CoE Team."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Import Manager (8 steps) | Export Manager (7 steps) |
|---|---|
| 1. Select Configuration | 1. Launch (File menu / right-click node) |
| 2. Select Data Source | 2. Create/reuse Configuration |
| 3. Select Format | 3. Select Objects (skipped if from node) |
| 4. **Map Data** (constant/transform/variables) | 4. Select Format (Excel/CSV) |
| 5. **Identify** (new vs existing; by ID or attribute) | 5. **Map Data** (Aspect/constant/transform) |
| 6. Identify Destination (default type & parent) | 6. Advanced (tag/locale/inline refs/calc/workspace) |
| 7. Select Business Rules | 7. **Delivery** (File/FTP-SFTP/Email/Server-side) |
| 8. Advanced (auto-approve; remove data not in file) | — |

| Key idea | Hook |
|---|---|
| **Tabular shape** | Objects = rows, properties = columns |
| **Save configuration** | Reuse for recurring jobs (both wizards) |
| **Background process** | Both run async; monitor via Execution Report |
| **Identify by attribute** | No STEP ID? Match on unique key/attribute |
| **"Remove data not in file"** | Full-sync mode — use carefully |
| **Locale/Workspace/Context on export** | Publish the right region & approved data |

#### How this connects to other modules
- **Business Rules** run inside import Step 7.
- **Unique Keys** (ID/URL/Key deck) power "identify by attribute value."
- **Calculated attributes / contexts / workspaces** (Functions, Data Modeling, Approvals) shape export options.
- Internally, every tabular import is converted to **STEPXML** before loading.


<div style="page-break-after: always;"></div>

# Chapter 12. Integration Endpoints

> A slide-by-slide companion to the *Integration Endpoints* deck (20 slides). Integration Endpoints are STEP's **automated, monitored connections** to other systems. They wrap the import/export functionality you learned in the XML and Tabular decks into managed, scheduled, event-driven pipelines.

---

### The 30-second mental model (read this first)

A standard import/export is something *you* run by hand. An **Integration Endpoint** is a *standing, monitored* version that runs on its own:

- **IIEP (Inbound)** — receives files/messages from other systems and imports them. Near-real-time (polls as often as every 1 minute, or fires instantly on a REST POST).
- **OIEP (Outbound)** — publishes STEP data out. Either **Event-Based** (push changes as they happen, e.g., on approval) or **Select Objects** (scheduled export of a hierarchy, like the normal Exporter).

Both pass data through a pipeline of **Receiver/Delivery + Pre-processor → Processing Engine → Post-processor (+ Error Reporter)** plugins, and both show a clear **status** (Enabled / Disabled / Failed).

---

### Slide 1 — Read Me First (template)
**On the slide:** Internal slide-design guidance.

**Explanation:** Authoring scaffolding. Skip.

---

### Slide 2 — Title
**On the slide:** "Introduction to Integration End Points — STIBO CoE Team."

**Explanation:** Section opener.

---

### Slide 3 — Module Objectives
**On the slide:** You'll understand Integration Endpoints and be able to create/configure **Inbound (IIEPs)** and **Outbound (OIEPs)** endpoints.

**Explanation:** Two things to master — the inbound side and the outbound side.

---

### Slide 4 — Integration Endpoints (overview)
**On the slide:** Endpoints are a **centralized interface for monitoring and maintaining integrations** with other systems. On a typical setup, a **large percentage** of data entering/leaving STEP goes through them. Two classes:
- **IIEP** — centralized interface for systems that **send data to STEP** (files or messages).
- **OIEP** — in many ways a way to **manage STEP export**; here STEP is the **data source** publishing to downstream systems.

**Explanation:** The key framing: endpoints turn ad-hoc import/export into **managed, observable integrations**. "Centralized monitoring" is the value — one place to see whether every feed is healthy. Inbound = data *to* STEP; Outbound = data *from* STEP.

---

### Slide 5 — Section: Inbound
**On the slide:** "Introduction to Inbound Integration End Points."

**Explanation:** Transition into IIEPs.

---

### Slide 6 — Inbound Integration Endpoint (timing)
**On the slide:** IIEPs offer **"real-time" or "near-real-time"** integrations. They can **consume data at predefined intervals** (invoked on a schedule, **minimum 1 minute**). Alternatively, true real-time happens when the source is **REST** and a **POST invokes** the endpoint.

**Explanation:** Two trigger styles for inbound:
- **Polling** — check the source every N minutes (≥ 1 min). "Near-real-time."
- **Push (REST)** — the external system POSTs data, firing the endpoint instantly. "Real-time."
Choose based on whether the source can push or must be polled.

---

### Slide 7 — IIEP Receiver Methods
**On the slide:** Data can arrive via these **receiver methods**:
- **Amazon SQS** — messages from Amazon Simple Queue Service.
- **Hot Folder Receiver** — a watched data folder, typically on the app server.
- **JMS Receiver** — consume/dequeue messages from a JMS queue.
- **Oracle AQ Receiver** — Oracle Advanced Queuing message exchange.
- **REST Receiver** — receive via REST web service.
- **Web UI File Loading Receiver** — for the Web UI "File Loading Widget" (non-hotfolder types).

**Explanation:** The **Receiver** is *how the data physically arrives*. The classic is the **Hot Folder** (drop a file in a folder, STEP picks it up). Queues (**SQS, JMS, Oracle AQ**) are for message-based systems. **REST** enables push. **Web UI File Loading** lets portal users upload files manually. Pick the receiver that matches the sending system's capabilities.

---

### Slide 8 — IIEP Plugins (the three types)
**On the slide:** The inbound framework supports **3 plugin types**:
- **Pre-processor Plugin** — has access to the retrieved file/message; can convert it into a format the STEP Importer handles.
- **Post-processor Plugin** — has access to import events; can trigger system changes based on them.
- **Error Reporter Plugin** — reports errors.

**Explanation:** The processing pipeline. **Pre-processor** = "fix the data before import" (e.g., transform a partner's XML into something importable). **Post-processor** = "react after import" (e.g., kick off a workflow for newly imported objects). **Error Reporter** = "tell someone when it breaks." Same three-plugin pattern appears on the outbound side (slide 15).

---

### Slide 9 — Pre/Post-processor Details
**On the slide:** A **pre-processor** can access and **manipulate or discard** files/messages from the receiver. Three pre-processing types:
- **No pre-processing** (default).
- **XML Normalizer** — minor layout tweaks so STEP can process inbound XML as **Generic XML**.
- **XSLT** — transforms valid inbound XML into **STEPXML**, or into non-STEPXML importable via **Generic XML**.
**Post-processor** logic is implemented via **business rules** referenced from the processing engine configuration.

**Explanation:** This is where the XML decks connect. Inbound XML rarely matches STEP's format, so the pre-processor reshapes it:
- **XML Normalizer** — light touch-up → handle as **Generic XML**.
- **XSLT** — heavy transformation → produce **STEPXML** (or feed Generic XML). XSLT is the powerful general-purpose XML transformer.
And post-processing reuses your **Business Rules** — so an import can automatically trigger downstream logic (approve, route to workflow, etc.).

---

### Slide 10 — Overall Inbound Flow
**On the slide:** (Diagram of the end-to-end inbound flow.)

**Explanation:** The full pipeline: **Receiver** (file/message arrives) → **Pre-processor** (reshape to importable format) → **STEP Importer** (create/update objects) → **Post-processor** (react via business rules) → **Error Reporter** (on failure). Hold this chain in your head; it's the inbound architecture.

---

### Slide 11 — Section: Outbound
**On the slide:** "Introduction to Outbound Integration End Points."

**Explanation:** Transition into OIEPs.

---

### Slide 12 — Outbound Integration Endpoints (two modes)
**On the slide:** Outbound, the data source is STEP. Two ways to select what to export:
- **Event-Based Outbound** — incremental output; publishes data based on **events** (e.g., an object being **approved**). With the **"Event Queue Data Source"** option, the endpoint checks its **Event Queue** for unhandled events and publishes them.
- **Select Objects Outbound** — publishes data from **selected hierarchies** on **scheduled intervals**, like the standard export.

**Explanation:** The crucial outbound distinction:
- **Event-Based** = **incremental / change-driven**. Only what changed gets published, triggered by events (approval, edit, etc.). Efficient for keeping a downstream system in sync continuously.
- **Select Objects** = **full / scheduled**. Export a whole branch on a timer — same as the normal Exporter, just automated. Use event-based for live sync, select-objects for periodic full feeds.

---

### Slide 13 — Outbound Delivery Methods (intro)
**On the slide:** Compared with the standard Exporter, OIEPs offer a **different set of delivery options.**

**Explanation:** Because OIEPs feed *systems* (not people), they support more machine-to-machine delivery channels than the manual Export Manager (listed next).

---

### Slide 14 — Outbound Delivery Methods (the list)
**On the slide:** OIEP delivery options: **Amazon SQS, Copy to Directory, Email, FTP, GDSN Data Pool, IBM WebSphere MQ SSL, JDBC, JMS, Mongo, Oracle AQ, Product Data Syndication, REST, REST Direct, SFTP.**

**Explanation:** A broad menu of integration targets — file drops (Copy to Directory, FTP/SFTP), message queues (SQS, JMS, MQ, Oracle AQ), databases (**JDBC, Mongo**), web services (**REST, REST Direct**), and syndication channels (**GDSN Data Pool, Product Data Syndication** — for publishing to retail/industry networks). You pick whichever the downstream system speaks.

---

### Slide 15 — Outbound Plugins
**On the slide:** Outbound also has **3 plugins**:
- **Pre-processor** — for **event-based** OIEPs, accesses generated **events**, can **filter** them / decide which objects to pass to the Processing Engine.
- **Post-processor** — accesses the file output by the Processing Engine; can **manipulate/split it into multiple files**; output goes to Delivery.
- **Error Reporter** — out-of-the-box **"Send Error Report"** plugin (or a custom one).

**Explanation:** Mirror of the inbound plugins, repurposed for output. Outbound **pre-processor** filters *which events/objects* to publish; **post-processor** shapes the *output file* (e.g., split one big export into per-category files) before delivery. Same Error Reporter concept.

---

### Slide 16 — Event Triggering Definitions (Event-Based OIEP)
**On the slide:** Triggering definitions define **what changes (events) the OIEP monitors**:
- **Triggering Object** — which object type(s) are valid for this OIEP.
- **Triggering Attributes** — events fire when a triggering attribute's value changes on a valid object.
- **Triggering Table** — filter which table types fire events when tables owned by triggering objects change.
- **Reference Type** — filter which reference/link types to listen to for changes.

**Explanation:** This is how you tune an event-based OIEP to fire **only on the changes that matter**. Instead of republishing on every tiny edit, you say "only when *these* attributes / *these* references / *these* tables on *these* object types change." Precise triggering keeps the feed efficient and avoids noise.

---

### Slide 17 — Event-Based OIEP Queue Status
**On the slide:** Two queue statuses:
- **Read Events** — the OIEP **registers events** as they occur (per its config and triggering definitions).
- **Discard Events** — **ignores** generated events that match the config.

**Explanation:** A control switch for the event stream. **Read** = actively capture matching events (normal operation). **Discard** = let matching events pass without queuing them — useful to temporarily stop capturing (e.g., during maintenance) without reconfiguring the triggers.

---

### Slide 18 — Overall Outbound Flow
**On the slide:** (Diagram of the end-to-end outbound flow.)

**Explanation:** The outbound pipeline: **Event Queue / Object Selection** → **Pre-processor** (filter events/objects) → **Processing Engine** (build the export, in your chosen format) → **Post-processor** (shape/split files) → **Delivery** (to the target system) → **Error Reporter** (on failure). The symmetric counterpart of slide 10.

---

### Slide 19 — Status of an Integration Endpoint
**On the slide:** Status icons:
- **Enabled** — active, connected, running.
- **Disabled** — stopped; no data imported/published.
- **Failed** — an error caused the background process to fail; **no data flows until the endpoint is resumed.**

**Explanation:** The monitoring payoff from slide 4. At a glance you see whether each integration is healthy. **Failed** is the one to watch — it halts the flow entirely until someone resumes it, so failed endpoints need prompt attention.

---

### Slide 20 — Thank You / Contact
**On the slide:** "Thank You."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| | Inbound (IIEP) | Outbound (OIEP) |
|---|---|---|
| **Direction** | Data → STEP | STEP → systems |
| **Trigger** | Poll (≥1 min) or REST POST | Event-Based (incremental) or Select Objects (scheduled) |
| **Entry/Exit** | **Receiver** (Hot Folder, SQS, JMS, Oracle AQ, REST, Web UI File) | **Delivery** (Copy to Dir, FTP/SFTP, SQS, JMS, MQ, JDBC, Mongo, REST, GDSN, PDS, Email) |
| **Pre-processor** | Reshape file (None / XML Normalizer / XSLT) | Filter events/objects |
| **Engine** | STEP Importer | Export/Processing Engine |
| **Post-processor** | React via Business Rules | Shape/split output file |
| **Error Reporter** | Report errors | "Send Error Report" (or custom) |

| Key idea | Hook |
|---|---|
| **Why endpoints** | Centralized, monitored, automated integration |
| **XML Normalizer** | Minor tweaks → Generic XML |
| **XSLT** | Transform → STEPXML (or Generic XML) |
| **Event-Based OIEP** | Publish changes (e.g., on approval) incrementally |
| **Triggering definitions** | Object / Attribute / Table / Reference filters |
| **Read vs Discard events** | Capture vs ignore matching events |
| **Status** | Enabled / Disabled / **Failed** (halts until resumed) |

#### How this connects to other modules
- **STEP XML** and **Generic XML** are the formats; XSLT/Normalizer convert between them.
- **Tabular Import/Export** is the manual version of what endpoints automate.
- **Business Rules** power inbound post-processing.
- **Approvals / events** drive event-based outbound; **Matching** uses an IIEP to match on arrival.
- **Asset Push** (DAM deck) uses event queues — the same event-driven idea.


<div style="page-break-after: always;"></div>

# Chapter 13. Portals / Web UI

> A slide-by-slide companion to the *Portals* deck (31 slides). Portals (a.k.a. **Web UI**) are STEP's **browser-based, configurable user interfaces** — tailored screens for specific user groups and tasks, replacing the heavy Java workbench for everyday users. Built and edited visually in the **Portal Designer**.

---

### The 30-second mental model (read this first)

The STEP **workbench** is a powerful but intimidating Java desktop client. A **Portal** is a **lightweight web UI** you configure for a particular audience (data stewards, suppliers, reviewers) showing only what they need. Each portal is made of **screens**, and each screen is built from reusable **components/widgets**. Three screens always exist: **Main** (the frame — nav/header/footer/global settings), **Homepage** (landing page), and **Login**. **Mappings** decide *which custom screen shows for which object*. You edit everything live in the **Portal Designer** (a WYSIWYG, in-browser tool). Portals integrate tightly with **Workflows** and support **localization** in two senses (app language vs data language).

---

### Slides 1–2 — Template / "Attention" intro slides
**On the slides:** Slide-design template and trainer framework.

**Explanation:** Authoring scaffolding. Skip.

---

### Slide 3 — Module Objectives
**On the slide:** You'll be able to **create Web UI screens from design mode**, **configure workflow navigation** in the Web UI, and **configure searches/advanced searches** and other Web UI features.

**Explanation:** Three skills: build screens (Designer), wire up workflow navigation, and set up search. These map to the deck's three main sections.

---

### Slide 4 — Title
**On the slide:** "Portals — STIBO CoE Team."

**Explanation:** Section opener.

---

### Slide 5 — Icons Used
**On the slide:** Legend of icons (Questions, Contacts, Reference, Demonstration, Hands-on Exercise, etc.).

**Explanation:** Training legend, not product content.

---

### Slide 6 — STEP Portals (why they exist)
**On the slide:** Portals were introduced for an **easy-to-use web interface** targeted at specific work tasks and user groups. The **workbench Java client** is often **too feature-rich** and its look/feel doesn't meet normal users' expectations. Portals are **web-based** (no download), each configured to a specific business case. The **long-term vision** is to **phase out the workbench entirely** in favor of web portals for both normal users and super-users/admins.

**Explanation:** The strategic context: portals exist to make STEP usable for people who don't need (or want) the full workbench. Key selling points: nothing to install, purpose-built per audience, modern UX. And the direction of travel — STEP is moving toward **web-only**, so Web UI skills are increasingly central.

---

### Slide 7 — Concept of STEP Portals
**On the slide:** Browser-based access to STEP data; a highly configurable/customizable framework (built on **Google Web Toolkit**); customers build their own tailored interfaces; a large set of **standard portal components** is available; can **tie in STEP workflows**; supports **internal and external** users (suppliers, vendors) to onboard/maintain data; works on **Windows, Mac, iPad, iPhone, and mobile**.

**Explanation:** The capability summary. Two standout points: (1) portals let **external** parties (suppliers/vendors) work directly in STEP through a controlled UI — huge for data onboarding; and (2) **cross-device/mobile** support, unlike the desktop workbench. You assemble portals from pre-built **components** rather than coding from scratch.

---

### Slides 8–11 — Creating a Portal via Workbench
**On the slide:**
- **Slide 8:** In Workbench → **System Setup** → right-click the parent **setup group** for Web UI configs → **New Setup Group** (name it). Recommended: put each Web UI in its own group so you can **limit user access** (so users only see Web UIs relevant to them).
- **Slide 9:** From the setup group, right-click → **New Web UI**. (If the option is missing, you're in the wrong setup group folder.)
- **Slide 10:** In the **Create New Web UI** dialog, enter **ID and Name** → **Create**. The config appears under the setup group and is editable in System Setup and accessible via a browser.
- **Slide 11:** If **Default** is checked on the Configuration tab, the Web UI gets a **simpler URL** (no config ID required) than non-default Web UIs.

**Explanation:** How a portal is born. The recommended practice — one **setup group per Web UI** — exists for **privilege control**: it lets you grant edit/access rights per portal (slide 29). The **Default** flag is a small convenience: one portal can be the "default" and reachable by a clean URL; others need their config ID in the URL.

---

### Slide 12 — Portal Structure (access + the 3 hardcoded screens)
**On the slide:** Access in a browser via the Web Start page or `http://[ServerURL]/portal/[UserID]UserPortal`; log in with your normal **User credentials**. Each portal has **screens**, each built from **portal components**. Every portal always has **3 "hardcoded" screens**: **[MAIN]**, **[HOMEPAGE]**, **[LOGIN]**.

**Explanation:** The skeleton of every portal. **Main** = the frame around everything; **Homepage** = where users land; **Login** = the sign-in page. These always exist; you add **custom screens** on top. Users authenticate with their normal STEP credentials (so privileges carry over).

---

### Slide 13 — Main Screen
**On the slide:** The **Main** screen controls the optional **left side navigation panel, header, footer, right-side objects**, and all **global configuration settings**.

**Explanation:** Main is the **template/chrome** shared by all screens — define the header/footer/side panel once here and every screen inherits it. It's also where global settings live.

---

### Slide 14 — Main: Side Panel
**On the slide:** The Main side panel is typically a placeholder for **browsing the Tree, searching, navigation, and working with Workflows**. Alternatively, that functionality can be exposed via **Widgets on the Homepage** (Tree excluded).

**Explanation:** Two design choices for navigation: a persistent **left side panel** (always visible) or **homepage widgets** (dashboard-style). Note the Tree browser can only live in the side panel, not as a homepage widget.

---

### Slide 15 — Homepage
**On the slide:** The Homepage is the **first page after login**. The Main side panel is **optional** alongside it. It can contain a **Widget Grid** component holding different widget types.

**Explanation:** The landing experience. You decide whether to show the side panel here, and you populate the Homepage with a grid of **widgets** (search boxes, task lists, KPIs, shortcuts) — much like a customizable dashboard.

---

### Slide 16 — Login Screen
**On the slide:** Beyond basic login, the Login screen can include a **locale selector** for choosing the **UI language**.

**Explanation:** Lets users pick their interface language *before* logging in (ties to localization, slide 30).

---

### Slide 17 — Custom Screens
**On the slide:** Custom screens show **details for selected objects, search results, task lists**, etc. The side panel is **optional** for them (configured via Main). Example shown: a **Node Details Screen**.

**Explanation:** Custom screens are the **content** you build (vs the always-present Main/Homepage/Login). A "Node Details" screen, for instance, shows one object's editable fields. Which custom screen appears when is decided by **mappings** (next slide).

---

### Slide 18 — Mappings (the routing logic)
**On the slide:** Mappings are **key** — they define **under which conditions a custom screen is displayed**. Typically configured via **Main**, on a special **ForwardingSwitchScreen** component, or on **NodeList** components. Example rules:
- Show **"SkuDetails"** whenever a **SKU** product is selected.
- Show the custom **Enrich** screen when an object in a workflow's **Enrich state** is selected.
- Show **ClassificationDetails** whenever a **Classification** is selected.
**Rules are evaluated in order; the first match wins.**

**Explanation:** Mappings are the portal's **router** — "if the user selects *this kind of thing*, show *that screen*." This is how one portal can show different editors for products vs classifications vs workflow tasks. Critical detail: **first-match-wins, evaluated top to bottom** — so order your mapping rules from most specific to most general, or a broad rule will shadow the specific ones.

---

### Slides 19–20 — The Portal Designer
**On the slide:**
- **Slide 19:** Portal configs are maintained in the **Portal Designer** — add/delete screens, add/delete/edit component properties. It's a **WYSIWYG editor that runs inside the browser**.
- **Slide 20:** Accessed by privileged users via **buttons in the Portal UI** (usually not on production portals) or via the **URL** by appending `[?/&/#]designmode=true`.

**Explanation:** The Designer is where you actually build/edit portals — visually, live, in the browser. Important practical detail: enter design mode by adding **`designmode=true`** to the URL. Production portals usually hide the design buttons (so end users can't accidentally edit), but privileged users can still reach the Designer via that URL parameter.

---

### Slide 21 — Feature: Children Screen
**On the slide:** A common feature: a **Children** screen type to **view and edit child nodes from a parent**.

**Explanation:** Lets users see/edit all children of a selected object in one place — e.g., open a category and edit all its products inline. A frequent, high-value pattern for bulk-ish editing in the UI.

---

### Slides 22–23 — Feature: Multi Reference Editor
**On the slide:** The **Multi Reference** component displays references with **multiple reference types and classification link types in one table**. It can be configured with a list of types to narrow what's shown, and to display **forward** or **reverse** ("referenced by") references. It's pre-configured with a **Node List in Multi Edit Display Mode** plus **Add / Remove Reference** toolbar actions — so users can **link/unlink** objects from the Web UI.

**Explanation:** A powerful relationship editor. It consolidates many reference/link types into a single table so users can manage all of an object's relationships in one spot. Two notable options: showing **reverse references** ("what points *at* this object") and the **Add/Remove** actions that let business users create/break links without touching the workbench.

---

### Slides 24–26 — Feature: Advanced Search
**On the slide:**
- **Slide 24:** Advanced Search lets users find data using **combinable search criteria** with operators **And/Or/Not**. The Advanced Search link can be added to the Homepage; the criteria panel is **configurable** so designers present only job-relevant criteria. Example 1: `Object type (Item) AND Attribute (Primary Color)=Almond`. Multiple values can be searched at once; for **LOV** attributes, a dropdown gives the actual list of values.
- **Slide 25:** Example 2: `[Item AND Primary Color=Almond] OR [Item AND Primary Color=Apricot]` — combines both result sets.
- **Slide 26:** (Advanced Search results screenshot.)

**Explanation:** The web equivalent of the workbench's search (Search/Collections deck), with And/Or/Not logic. The configurable criteria panel is the key design point — you expose only the fields a given user group needs to search on, keeping it simple. LOV dropdowns prevent typos by offering the valid values directly.

---

### Slides 27–28 — Workflows in Portals
**On the slide:**
- **Slide 27:** The Portal framework is **tightly integrated** with STEP Workflows. A portal can be **centered around a workflow** (users only reach objects via workflow **Tasks**), or workflows can be **just one entry point** among browse/search.
- **Slide 28:** A special feature is creating new objects via an **"InitiateItem" screen** — objects created this way are **automatically started in a workflow**, and (unlike normal creation) you can **set attribute values *before* the object is created**. The **StatusSelector** component controls whether the initiate option is shown and which InitiateItem screen to use.

**Explanation:** Portals are the natural front-end for workflow participants (recall the Workflows deck mentioned Portal task lists). You can build a **task-driven portal** where users only act on their assigned tasks. The **InitiateItem** screen is special: it gathers data *first*, then creates the object already inside a workflow — perfect for guided "create a new product" flows for suppliers.

---

### Slide 29 — Portals and Privileges
**On the slide:** The only special portal-related **Setup Action** is **"Update Web UI configuration"** (edit a config via XML/Designer). It can be granted **per Setup Group**, so a user group can edit one portal but not another. Privileges to **view a screen** can also be controlled via the **`<restrict>` tag** in the UI XML.

**Explanation:** Two layers of access control. **Edit rights** are granted per setup group (which is why slide 8 recommended one group per Web UI). **View rights** for individual screens are controlled inline with the `<restrict>` tag in the configuration XML — so you can hide specific screens from specific users even within one portal.

---

### Slide 30 — Localization (two kinds of language)
**On the slide:** Portal screens can be shown in different languages, but distinguish:
- **Data language** — names of STEP attributes/reference types, and attribute *values* maintained in different languages. **Defined in STEP** (this is the **Context**).
- **Application language** — the portal's **labels and titles**. Translate by setting the title/label to a **translation key**, then adding that key to a **translation file on the server** with the correct value (one file per language).
End users can change **both** the application language (**locale**) and the data language (**context**) in the portal.

**Explanation:** A frequently-confused but important distinction:
- **Data language = Context** — the actual *content* (product names, attribute values) in different languages, handled by STEP's dimension/context system (Data Modeling deck).
- **Application language = locale** — the *UI chrome* (button labels, menu titles), handled by **translation key files** on the server, separate from your data.
Users can switch each independently — e.g., a French-speaking user (app language = French) reviewing German market data (context = German).

---

### Slide 31 — Thank You / Contact
**On the slide:** "Thank You — STIBO CoE Team."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Concept | Memory hook |
|---|---|
| **Portal / Web UI** | Browser-based, configurable UI per user group (replaces workbench) |
| **Built from** | Screens → components/widgets (GWT framework) |
| **3 hardcoded screens** | **Main** (frame), **Homepage** (landing), **Login** |
| **Main** | Header/footer/side panel + global settings (shared chrome) |
| **Custom screens** | Object details, search results, task lists |
| **Mappings** | Which screen for which object; **first match wins** |
| **Portal Designer** | In-browser WYSIWYG; enter via `designmode=true` |
| **Children screen** | View/edit a parent's child nodes |
| **Multi Reference Editor** | Manage many ref/link types in one table; forward/reverse; add/remove |
| **Advanced Search** | And/Or/Not, configurable criteria, LOV dropdowns |
| **Workflow integration** | Task-driven portals; **InitiateItem** sets values *before* create |
| **Privileges** | "Update Web UI configuration" per setup group; `<restrict>` per screen |
| **Localization** | **Data language = Context**; **App language = locale (translation keys)** |

#### How this connects to other modules
- **Workflows** deck — portals are the front-end for workflow tasks; InitiateItem starts flows.
- **Search/Collections** deck — Advanced Search is the web version.
- **Data Modeling** (Contexts) — "data language" = context switching.
- **Integration Endpoints** — the Web UI File Loading receiver lets portal users upload feeds.


<div style="page-break-after: always;"></div>

# Chapter 14. Digital Asset Management

> A slide-by-slide companion to the *Digital Asset Management* deck (35 slides — the largest in the set). DAM covers how STEP **stores, recognizes, edits, converts, exports, and distributes** digital files (images, documents, etc.) — and the important question of **where the heavy binary files actually live**.

---

### The 30-second mental model (read this first)

An **Asset** is a STEP object that points at a digital file (recall Data Modeling slide 11). DAM is the lifecycle around those files:

1. **Import & auto-recognition** — load files; STEP reads the **MIME type** to auto-create the right Asset type and auto-extract metadata. Two tools: the **Manual Asset Importer** (small batches) and the **Asset Importer** (mass loading).
2. **Maintenance** — edit a file in a local app and save the new version back (creates a revision).
3. **Export** — four mechanisms: the **Export Images & Documents wizard**, **Export Manager / OIEP**, **Asset Push**, and the **REST API**. Images can be **converted** (format/size/color) on the way out, with **caching** for performance.
4. **Storage strategy** — binaries default to the **database (BLOB)**, but that bloats backups, so you can store them **externally** (External DAM via URL, or External File System via filename) — with the trade-off that external storage is **the customer's responsibility, not Stibo-supported.**

---

### Slides 1–2 — Template / "Attention" intro slides
**On the slides:** Slide-design template and trainer framework.

**Explanation:** Authoring scaffolding. Skip. (This deck carries trainer "Need/Benefits" notes throughout — facilitation prompts, not content.)

---

### Slide 3 — Purpose
**On the slide:** You'll learn about DAM in STEP: how digital assets are **stored and maintained**, and the **import/export** process.

**Explanation:** Roadmap: store → maintain → import/export.

---

### Slide 4 — Title
**On the slide:** "Digital Asset Management — STIBO CoE and Team."

**Explanation:** Section opener.

---

### Slide 5 — Terminal Objective (agenda)
**On the slide:** Topics: **Import & auto-recognition; different import mechanisms; maintaining assets; exporting assets; different export mechanisms.**

**Explanation:** The agenda = the lifecycle from the mental model. Use it as your checklist.

---

### Slide 6 — Import & Auto-Recognition: Manual Asset Importer
**On the slide:** The **Manual Asset Importer** imports digital media files, **auto-creating Assets** of a specific Object Type (Image or Document). This depends on STEP reading the file's **MIME type** and matching it to the MIME type configured on an Asset Object Type. **If multiple Asset Object Types share the same MIME type, STEP randomly picks one.**

**Explanation:** The core auto-recognition mechanism: STEP inspects each file's **MIME type** (e.g., `image/jpeg`) and creates the matching Asset type automatically — no manual typing. The warning matters: **don't configure two asset types with the same MIME type**, or STEP picks one at random (unpredictable results). Keep MIME-to-type mappings unique.

---

### Slide 7 — Import & Auto-Recognition (continued)
**On the slide:** STEP **doesn't support all media types** out of the box; some need special handling. On import, the **binary is stored as a BLOB in the Oracle database**, and **metadata is extracted** and shown under the **"System Properties" flipper** on the Asset object (**read-only**). Selecting multiple files in the wizard is possible, but **not viable for large volumes**.

**Explanation:** Three key facts: (1) the binary lands in the **database as a BLOB** by default (the storage concern revisited at slides 32–33), (2) **metadata is auto-extracted** (dimensions, color space, etc.) into a read-only System Properties panel, and (3) the manual importer doesn't scale — for bulk you need the **Asset Importer** (slides 9–10).

---

### Slides 8–10 — The Asset Importer (bulk loading)
**On the slide:**
- **Slide 8:** (Screenshot.)
- **Slide 9:** The **Asset Importer** is a robust tool for **mass loading** images/documents/other assets — core functionality to import and update asset data. To use it, set **'Asset Import Compatibility Mode'** (Users & Groups → System Settings → Image & Document Settings) to **'Advanced.'**
- **Slide 10:** It requires a new Setup Group **'Asset Import Configurations'** (central home for all import configs), plus a child setup group **'Asset Import Configuration Type'** to hold the actual configurations.

**Explanation:** The scalable counterpart to the manual importer. Two setup prerequisites to remember: flip the compatibility mode to **'Advanced'**, and create the **Asset Import Configurations** setup-group structure so all asset-import configs live in one organized place (mirrors the configuration-reuse pattern seen across STEP).

---

### Slides 11–12 — Asset Maintenance (edit in place)
**On the slide:**
- **Slide 11:** You can **edit a stored file in a local editor** and save the edited version back to STEP. Choose **"Edit Asset"** from the Asset Tree object's context menu, or right-click the **file thumbnail** on the Asset editor → **"Edit Asset."**
- **Slide 12:** This opens the file in your locally-associated editor **and** a STEP dialog to save the modified version back. After saving, **a new revision is created.**

**Explanation:** Round-trip editing: STEP hands the file to whatever app your OS associates with that extension (Photoshop for a PSD, Word for a DOCX), you edit, and save back through the STEP dialog. Each save-back cuts a **new revision** (ties to the Revisions deck) — so you keep the version history of the binary, not just the metadata.

---

### Slide 13 — Export Asset (the four mechanisms)
**On the slide:** Assets can be exported via: **Export Images and Documents wizard; Export Manager or an OIEP; Asset Push; REST API.**

**Explanation:** The four export paths — memorize these four. Each suits a different need: the **wizard** for manual/ad-hoc to disk; **Export Manager/OIEP** for including assets in data exports/integrations; **Asset Push** for keeping an external file system in sync; **REST API** for on-demand retrieval. The rest of the deck details each.

---

### Slides 14–18 — Export Mechanism 1: Export Images & Documents Wizard + Conversions
**On the slide:**
- **Slide 14:** Export media to disk manually from the workbench via **"Export Images & Documents"** (from an Asset object or a Classification containing assets). For image assets, STEP offers **conversion options**; for a custom conversion choose **"Custom…"** in step 2 of the wizard.
- **Slide 15:** Configure **format, size, and color** settings.
- **Slide 16:** (Screenshot.)
- **Slide 17:** **Cache step** — a checkbox enables caching; radio buttons set **when** caching occurs. Caching is available via the **Export Manager** or asynchronously via the **Image Cache event processor**. For performance, configure the **Image Cache Event Processor** to listen for selected asset object types and apply conversions automatically; conversions set to **'cache on import'** become available. **Save and Finish** completes the conversion config for reuse.
- **Slide 18:** To make a **reusable conversion configuration**, select a **Classification** to store it under (stored as a special Asset type) → **"New Image Conversion Configuration…"** from the Maintain/Insert menu. Once created, it's selectable in the **"Image Conversion"** step of the export wizard.

**Explanation:** This cluster is about **image conversion** — STEP can transform images on export (resize, reformat, recolor) so you store one high-res master and deliver whatever variant a channel needs (recall Data Modeling slide 11's "convert on retrieval"). The performance lever is **caching**: pre-compute conversions (via the **Image Cache Event Processor**, ideally "cache on import") so they're ready instantly rather than generated on every request. And conversions can be saved as **reusable Image Conversion Configurations** so the same recipe applies everywhere.

---

### Slides 19–21 — Export Mechanism 2: Export Manager / OIEP
**On the slide:**
- **Slide 19:** **STEPXML and Advanced STEPXML** in the Export Manager can export asset **metadata, references, and digital content** for images and non-images. For automatic event-based exports, an **OIEP** can listen for new/changed/deleted assets. Choose an option for the **Include Assets** parameter.
- **Slide 20:** **Include Assets = None** → neither assets nor content in output. For **Include Asset Content**, choose **Binary** or **REST**: **Binary** embeds content as **BASE64** (decodable by the external system); **REST** includes a **relative REST resource URL** (the external system completes the path to fetch it). If no content is available for an image, the XML tag isn't exported.
- **Slide 21:** Click **Select Image Conversions** and pick **at least one** conversion to enable Next/Finish. Selecting multiple conversions is allowed but **increases export time and file size.**

**Explanation:** This path bundles assets into your **data exports/integrations** (ties to the STEPXML and Integration Endpoints decks). The key decision is **how to deliver the binary**:
- **Binary (BASE64)** — embed the file *inside* the XML (self-contained but large).
- **REST** — embed a *link* instead, and let the consumer fetch the file separately (lean XML, deferred retrieval).
The OIEP variant makes this **event-driven** (publish assets as they change). Note the cost warning: multiple conversions inflate export size/time.

---

### Slides 22–30 — Export Mechanism 3: Asset Push (sync to external file system)
**On the slide:**
- **Slide 22:** Embedding binaries (above) **isn't viable** when a downstream system needs the actual files. So asset content is **typically not** included in exports; instead **Asset Push** distributes media files from STEP to an **external file system on another host**, ensuring that location always has the **latest version**.
- **Slide 23:** Setup steps: (optional) create an **Image Conversion Configuration**; create an **Asset Push Event Queue**; create one or more **Asset Push Configurations**; install the **Java Sidecar** app on the host that will hold the files; **initiate** the push.
- **Slide 24:** Set up the **Asset Push Event Queue** in **System Setup → Event Queues**. Decide queue behavior such as **how long to retain events** after processing (enables reprocessing).
- **Slide 25:** Other queue settings: **Unread events** (approx. count waiting); **Asset Push Sidecar** (shows the sidecar's IP, or "No activity yet"); **Consumer Read** — **Disabled** (processed events not delivered — useful to pause, e.g., when the destination disk is full) vs **Enabled** (delivers to destination).
- **Slide 26:** The **Asset Push Configuration** governs behavior and is created **below** an Asset Push Event Queue. Decide **where** files are stored on the Sidecar Host and whether images are **converted** when pushed. Each configuration creates a folder (named after the config) on the Sidecar Host; subfolders come from the **relative path template**.
- **Slide 27:** Asset Push Configuration settings: **Workspace** (push from — typically **Approved**); **Image Conversion Configuration**; **Relative Path Template** (folder structure on the host); **Auto Cleanup** (remove old file versions); **Include Classification** (which part of the hierarchy); **Include MIME Type(s)** (filter by type); **Include Attribute(s)** (restrict to assets with specific values, format `[Attribute ID]=[value]`).
- **Slide 28:** The **Sidecar** is a Java app (jar) deployed on the destination host. A sidecar jar is **auto-created for download** after you create an Asset Push Configuration (host needs latest JRE). Download from `http://[application server]/sidecar`.
- **Slide 29:** The chosen directory becomes the **root** for stored files. Install on Windows: `java -jar <name-of-assetpush-queue-jar>.jar –install`. Then edit **`assetpush.properties`** in the install dir and set a **username and password**.
- **Slide 30:** Monitor via the **Asset Push Configuration → Statistics tab**, and per-asset status on the **Status tab** of pushed assets.

**Explanation:** Asset Push is the **production-grade file distribution** mechanism — the right answer when a website/PIM consumer needs the *actual files on disk*, not embedded blobs. The architecture:
- An **Event Queue** captures asset changes; a **Sidecar** Java app on the *target* host receives files and writes them to its file system; **Asset Push Configurations** define *what* (classification/MIME/attribute filters), *from where* (typically the **Approved** workspace), *converted how*, and *into what folder structure* (relative path template).
- **Consumer Read: Disabled** is a handy pause switch when the destination is unavailable.
- It keeps the external location **continuously up to date** with STEP's latest approved files. This is the most involved export path (8 slides) because it's the most operationally important — know the **Event Queue + Sidecar + Configuration** trio.

---

### Slide 31 — Export Mechanism 4: REST API
**On the slide:** The **REST API** lets you **upload files to a REST server**, later usable by invoking the STEP REST API.

**Explanation:** The on-demand path — programmatic upload/retrieval of asset content via REST (pairs with the "REST" delivery option on slide 20, where the XML carries a REST URL the consumer calls).

---

### Slides 32–33 — Store Asset Externally (the storage strategy)
**On the slide:**
- **Slide 32:** Storing assets **inside STEP greatly increases database size**, which lengthens **backup time**. Deleting assets **doesn't automatically shrink** the DB — recovering space requires **compressing then restoring** the database. The fix: **store assets outside STEP** while still displaying/exporting them from STEP. **External storage is NOT supported by Stibo Systems** — it increases your responsibility for managing the assets and the external system.
- **Slide 33:** Two external options: **External DAM** — a **URL** retrieves the asset content; the external DAM holds the binaries while the **asset object and metadata stay in STEP**. **External File System (EFS)** — a **unique filename** retrieves content; assets sit in an external file system **on the STEP app server** rather than the DB. EFS management/backup is the **customer's responsibility** (not Stibo-supported). For both, **configuration asset files** (transformation lookup tables, export configs) **stay within STEP**.

**Explanation:** The critical architectural decision. By default binaries are **BLOBs in the database** — simple but it bloats the DB and slows backups (and deletions don't reclaim space without a costly compress/restore). The alternatives keep **metadata in STEP** but move the **binaries out**:
- **External DAM** — binaries live in a dedicated DAM product, fetched by **URL**.
- **EFS** — binaries live in a **file system** on the app server, fetched by **filename**.
Big caveat: both are **the customer's responsibility and unsupported by Stibo** — you gain a smaller, faster database but take on managing/backing up the external store yourself. Either way, STEP keeps the asset *objects*, *metadata*, and *configuration* files.

---

### Slide 34 — Recap / Review
**On the slide:** Covered: import & auto-recognition (Manual Asset Importer, Asset Importer); maintaining assets; exporting assets (Export Images & Documents wizard, Export Manager/OIEP, Asset Push, REST API); storing asset data externally; different import/export mechanisms.

**Explanation:** The deck's own checklist — good for self-testing before moving on.

---

### Slide 35 — Thank You / Contact
**On the slide:** "Thank You — STIBO CoE and Team."

**Explanation:** Closing slide.

---

### Quick-revision cheat sheet

| Stage | Key points |
|---|---|
| **Asset** | STEP object pointing at a file (image/document) |
| **Auto-recognition** | By **MIME type** → asset type + auto-extracted (read-only) metadata |
| **Don't** | Map two asset types to the same MIME (random pick) |
| **Manual Asset Importer** | Small batches |
| **Asset Importer** | Mass loading; needs Compatibility Mode = **Advanced** + Asset Import config groups |
| **Default storage** | Binary as **BLOB in Oracle DB** |
| **Maintenance** | "Edit Asset" → local editor → save back → **new revision** |
| **Export #1** | **Export Images & Documents** wizard (to disk; conversions) |
| **Conversions** | Format/size/color; **cache** via Image Cache Event Processor; reusable Image Conversion Configurations |
| **Export #2** | **Export Manager / OIEP** (STEPXML); content as **Binary (BASE64)** or **REST URL** |
| **Export #3** | **Asset Push** — Event Queue + **Sidecar** + Push Config → sync files to external host (push from **Approved**) |
| **Export #4** | **REST API** (upload/retrieve programmatically) |
| **External storage** | **External DAM** (by URL) or **EFS** (by filename); shrinks DB but **unsupported by Stibo / customer-managed** |

#### How this connects to other modules
- **Data Modeling** slide 11 introduced Assets and on-retrieval conversion.
- **Revisions** deck — editing an asset cuts a new revision.
- **STEPXML** deck — asset content export options (Binary/REST); note STEPXML *can't import* asset content.
- **Integration Endpoints** deck — OIEPs publish asset changes; Asset Push uses the same event-queue idea.


<div style="page-break-after: always;"></div>
