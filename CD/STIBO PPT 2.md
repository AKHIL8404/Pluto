# Stibo STEP — Complete Beginner's Training Guide

*A structured, slide-by-slide lesson built from the "Training Material Revamp" curriculum (Stibo STEP L1, Cognizant CoE).*

---

## How to use this guide

This guide turns 14 PowerPoint decks (~301 slides) into one connected lesson. I have **reordered the modules into a logical learning sequence** so each concept builds on the previous one, but **within each module the slides are explained in their original order** so you can follow along with the source decks.

A few honest notes so nothing surprises you:

- Some decks begin with **template/housekeeping slides** ("Read Me First", "Slide Design Guidelines", "Attention – What/How/Duration", "About the Author", "Icons Used", "Thank You"). These contain *instructions for the trainer*, not Stibo content. I flag them quickly rather than inventing Stibo material for them — that would mislead you.
- Where a slide was mostly a screenshot with little text, I **fill the gap from general Stibo STEP knowledge** so the concept is still complete.
- Each module ends with a **mini-recap**. The very end of the guide has a **master summary, key takeaways, and a large interview/practice question bank**.

**What is Stibo STEP, in one paragraph?** STEP is a **Master Data Management (MDM)** and **Product Information Management (PIM)** platform made by Stibo Systems. Think of it as a single, trusted "source of truth" where a business stores, enriches, governs, and distributes its core data — products, customers, suppliers, locations, digital assets, and more — so that every downstream system (websites, marketplaces, ERPs, print catalogs) receives clean, consistent, approved data.

---

## Learning roadmap (module order in this guide)

1. **Data Modeling** — the foundation: how STEP represents the world (objects, products, attributes, references, dimensions).
2. **ID, URL, Key** — the three ways to identify an object.
3. **STEP Functions** — the Excel-like formula language and calculated attributes.
4. **Business Rules** — conditions and actions (the logic layer).
5. **STEP Workflows** — modeling and automating business processes.
6. **Approvals, Revisions & Deletions** — the data lifecycle and governance.
7. **Search, Collections & Bulk Updates** — finding and mass-maintaining data.
8. **Matching & Linking** — de-duplication and Golden Records.
9. **Digital Asset Management (DAM)** — images, documents, and how they move.
10. **Portals (Web UI)** — building user-facing screens.
11. **Tabular Import & Export** — CSV/Excel in and out.
12. **STEP XML** — the native data exchange format.
13. **Generic XML** — importing/exporting *any* XML shape.
14. **Integration Endpoints** — the framework that orchestrates all inbound/outbound flows.

---
---

# MODULE 1 — Data Modeling

> **Why this is first:** Everything in STEP — products, customers, images, even the system's own configuration — is built from a small set of modeling building blocks. If you understand objects, attributes, references and dimensions, the other 13 modules become much easier.

### Slide 1 — Title slide
*"Stibo STEP L1 Training — Data Modeling."* No content to learn; it just names the module.

### Slide 2 — About the Author
Housekeeping: created by the **Stibo CoE (Center of Excellence) team**, v1.0, dated 23/07/2021, with a few references taken from official Stibo documentation. Nothing to memorize.

### Slide 3 — Objects
**Main point:** In STEP, *everything* is modeled as an **object**.

**Detailed explanation.** In a traditional relational database you'd use **tables, columns, and rows** to store data in a "normalized" way (data split across many linked tables to avoid duplication). STEP achieves the same goal with a different concept: the **object**.

An object is a thing with **properties**. Those properties are:
- **Metadata** like an ID,
- **Attributes** (named pieces of information with values), and
- **References / links** to other objects.

Objects take many forms: a product, a non-product business entity (like a customer or address), a classification (a category/grouping), an asset (a picture, PDF, Word doc), and even pieces of *system functionality* (STEP configures itself using objects too).

**Analogy.** Picture a filing cabinet where every item — whether a product spec sheet, a customer card, or even the cabinet's own labeling rules — is a "card" (object) with fields filled in (attributes) and string ties connecting related cards (references).

> 💡 **Tip:** "Everything is an object" is the single most important idea in STEP. When something feels confusing later, ask: *"What kind of object is this, and what are its properties?"*

### Slide 4 — STEP Object Type Model (Definition vs. Instance)
**Main point:** There's a difference between **defining a type of thing** and **creating an actual thing of that type**.

**Detailed explanation.** Two layers:
- **Object Type (the definition / blueprint):** configured by administrators under **System Setup → Object Types & Structures**. Example definition: *"A 'SKU' is a kind of product."*
- **Instance (the actual object):** the real data records created in the **Tree** (your live data) and in **System Setup**. Example instance: *the specific SKU "Red T-Shirt, Size M, item #12345."*

**Analogy.** "Object Type" is the *cookie cutter*; an "instance" is each *cookie* you cut with it.

> 📌 **Remember:** Object Types live in **System Setup**. Their instances (your real products, etc.) live in the **Tree**.

### Slide 5 — Product Basics
**Main point:** A **product** is something the retailer **buys from a supplier and sells to a customer** (a "sell-side product/item" in PIM terms).

**Detailed explanation & vocabulary:**
- **Product** — any item you sell.
- **Variant products** — versions of one product (e.g., a shirt in many sizes/colors). *(Available in PCM — Product & Catalog Management.)*
- **Samples** — items distributed but not sold.
- **Kits** — e.g., a repair kit that links to other products.
- **Packs** — a group containing a selection of items.
- **Bundles** — a set of products **plus** a service (e.g., a dishwasher **plus** professional installation).

**Real-world use case.** An electronics retailer sells a "TV" product, offers it in 3 screen sizes (**variants**), ships review units to journalists (**samples**), and sells a "TV + wall-mount install" **bundle**.

### Slide 6 — (image-only slide)
No text — a diagram slide. Conceptually it sets up the next slide's "buy side vs. sell side" idea.

### Slide 7 — Product Basics (Buy side vs. Sell side)
**Main point:** Distinguish what you **buy** from what you **sell**, because they don't always line up one-to-one.

**The four scenarios:**
1. **Same product bought and sold** — buy a product, sell that same product.
2. **Multiple products sold as one** — buy equivalent items from several suppliers, sell them as a single product *(VDO only — a specific solution edition)*.
3. **One product sold as different products** — buy one item, sell it under different sell-side products.

**Product data** = everything describing the product: its **name, identifiers** (GTIN, EAN, SKU id), **descriptions** (e.g., GPC attributes, marketing text), **pictures**, **links to other products**, **link to a classification**, etc.

**Real-world use case.** A grocery chain buys identical bottled water from three different bottlers (buy side) but lists it as a single "Spring Water 500ml" product on its website (sell side).

> 💡 **Term:** **GTIN** = Global Trade Item Number; **EAN** = European Article Number (a GTIN-13 barcode); **SKU** = Stock Keeping Unit (your internal item id).

### Slide 8 — Products in STIBO (the Product hierarchy)
**Main point:** Products live in **one** master hierarchy — the **"blue" Product hierarchy** — and that structure should reflect *logic*, not the website's look.

**Detailed explanation:**
- The Product super type is the **primary structure** for sellable items/services.
- A product can **exist only once** in the blue Product hierarchy, and it **must** exist there.
- The Product hierarchy supports **inheritance** of attribute values and category-specific attributes — so grouping products by shared properties is powerful.
- **Model logically, not for presentation.** The Product hierarchy is your clean data backbone; the way products appear on a website is handled separately (via Classifications — next slide).
- Hierarchies are usually **strictly structured** using different Product Object Types per level, and average implementations are **at least 4 levels deep**.

**Two classification "content" styles inside the Product hierarchy (PPH = Primary Product Hierarchy):**
- **GPC classification** — uses the **GS1 Global Product Classification** standard, which auto-attaches standard GPC attributes to each relevant level.
- **Open classification** — you manually define the attributes needed at each node.

**Analogy.** The Product hierarchy is like the **org chart of a company** (logical reporting lines), while the website menu is like the **seating map at an event** (how people are arranged for the audience). Same people, different purpose.

> 📌 **Color code to memorize:** **Blue = Products** (the one true home). **Yellow = Classifications** (alternative groupings). You'll see these colors in the workbench.

### Slide 9 — Product Object Data (what a product record shows)
**Main point:** Anatomy of a product object in the editor.

**What a product carries:**
- A **parent** in the Product Hierarchy, plus its **ID, Name, Object Type**.
- Any number of **Classification Links** (alternative structuring).
- Any number of **References to other Products**.
- Any number of **References to digital media files (Assets)**.
- Any number of **Links to Specification Attributes**.

**Editor UI features:**
1. The **Product tab**.
2. The **Description flipper** shows basic info. *(A "flipper" is STEP's name for a collapsible/expandable section in the editor.)*
3. If a **primary image** is referenced, a **thumbnail** displays.
4. **Specification attributes** appear in flippers named after their **attribute group**.
5. Click any editable field to **edit values**.

> 💡 **Term:** **Flipper** = an expand/collapse panel in the STEP object editor. You'll hear this word constantly.

### Slide 10 — Classification Basics
**Main point:** **Classifications** ("yellow") are hierarchies that **group/bundle** objects — the most common use is building **website category trees**.

**Detailed explanation:**
- Classifications are the **super type for alternative groupings** of products and for **storing assets**.
- A product exists **once** in the blue hierarchy but can be **linked into any number** of yellow Classifications.
- Customers model many taxonomies with Classifications (website navigation is the classic one).
- Classification Object Types and legal structures are configured **the same way** as Products.
- **Big difference:** Classifications can hold Description Attribute values and References, **but there is NO value inheritance** between Classifications, or from a Classification down to Products.

**Real-world use case.** One bicycle product (single home in the blue hierarchy) is linked into: website category "Mountain Bikes," a seasonal "Summer Sale" classification, and a "Best Sellers" classification — three yellow groupings, one product.

> ⚠️ **Common confusion:** Inheritance flows down the **blue Product hierarchy** (via Specification attributes), **not** through yellow Classifications.

### Slide 11 — Assets
**Main point:** An **asset** is any product-related electronic file (images, Word, Excel, PDF, PowerPoint, text…). Images are the most common.

**Key behaviors:**
- An asset is a STEP **object with referenced content** (the file). Content can be **dimension-dependent** (e.g., different image per market) and can be replaced/modified.
- **Auto-identification** of file type via **MIME-type / file header** info.
- **Automatic metadata extraction** on import (dimensions, color space, etc.).
- Assets can have any number of additional **Description Attributes**.
- Assets can be **converted** many ways as they're pulled out of STEP (resize, reformat, recolor).

> 💡 **Term:** **MIME type** = a standard label for a file's format, e.g., `image/jpeg`, `application/pdf`. STEP reads it to decide what kind of asset object to create. We revisit assets in depth in **Module 9 (DAM)**.

### Slide 12 — Attributes
**Main point:** An **attribute** is a single characteristic of an object (or of a relationship between objects).

**Detailed explanation:** Attributes are **defined in System Setup** and organized into **Attribute Groups** (e.g., a "Dimensions" group holding Height, Width, Length). They are the columns-of-data equivalent in STEP's object world.

**Example.** For a laptop product: `Brand = Dell`, `Weight = 1.4 kg`, `Color = Silver` — each is an attribute with a value.

### Slide 13 — Attribute Types (Specification vs. Description)
**Main point:** Two fundamental attribute families, and the difference is mostly about **inheritance**.

| | **Specification Attributes** | **Description Attributes** |
|---|---|---|
| Apply to | **Product objects only** | **All object types** that can hold values |
| Inheritance | **Yes** — values inherit down the Product hierarchy | **No** inheritance |
| How they appear | **Linked into** the hierarchy; viewable/editable on products below | **Automatically appear** on the objects/links/references they're valid for |
| Validity | Two validity concepts: **hierarchical** and **object-type** validity | Made valid for object types directly |

**Why it matters.** Specification attributes let you set a value once high in the hierarchy and have it cascade to thousands of products below (huge time saver). Description attributes are simpler, value-by-value, and work everywhere (including on customers, assets, and even on the links between objects).

**Real-world use case.** Set `Warranty = 2 years` once on the "Laptops" node (Specification) → every laptop inherits it. Meanwhile `City` on a customer-address entity is a Description attribute (no inheritance needed).

### Slide 14 — Attribute Validation Base Types
**Main point:** Every attribute has a **Validation Base Type** that **strictly limits** what you can type in.

**Detailed explanation.** The base type acts as a gatekeeper for data quality — it's enforced everywhere (UI, import, API). You set it directly, or indirectly via a **List of Values (LOV)**. Key base types from the slide:

- **Condition** — allows applying conditions, e.g., `[AttributeID] = [Value1];[Value2]`.
- **Date** — date in a defined mask (e.g., `DD-MON-YYYY` → `15-JAN-2025`).
- **Embedded Number** — stores prefix, number, unit, suffix separately (e.g., `±2g of protein`, `≈35°C`, `≤0.2% THD`).
- **Fraction** — numbers with dash/slash (valid `1/2`, `1-1/2`; invalid `1 1/2`).
- **GLN** — validates length + check digit of a 13-digit **Global Location Number**.
- **GTIN / GTIN-8 / -12 / -13 / -14** — validate length and check digits for the various barcode lengths.
- **Integer** — whole numbers only (valid `5, 26, -23`; invalid `.250, 67.34`).
- **ISO Date** — mask `YYYY-MM-DD` (e.g., `2025-01-15`).
- **ISO Date and Time** — mask `YYYY-MM-DD HH24:MI:SS`.
- **LOV** — value must be chosen from a List Of Values (e.g., Red, Green, Blue).
- **Number** — any numeric (valid `-15, .34, 384.5`; invalid fractions like `50 1/2`).
- **Number Range** — a range with a dash; first ≤ second (valid `1.2-3.6, 5-7`; invalid `7-5`).
- **Numeric Text** — any characters, can link a Unit (e.g., `14 mm`, `N/A`).
- **Numeric Text (exclude tags)** — like Numeric Text but style tags don't count toward length.
- **Regular Expression** — apply a regex pattern, e.g., `[a-z]{3} ([0-9]{3})`.
- **Text** — any characters.
- **Text (exclude tags)** — like Text but excludes style tags from counts.
- **URL** — must be a valid URL (valid `http://www.stibo.com`; invalid `www.stibo.com`).
- **Validation Templates** — extend the standard validations with new ones based on regular expressions.

> 💡 **Term:** A **check digit** is an extra calculated digit in codes like GTIN/GLN that catches typos. STEP verifies it so a mistyped barcode is rejected at entry.

> 📌 **Big idea:** Choosing the right base type is your **first line of defense for data quality** — invalid data simply can't be saved.

### Slide 15 — Other Important Attribute Settings
**Main point:** Several per-attribute switches change how the attribute behaves in approval, contexts, search, and calculation.

- **Externally Maintained (Yes/No)** — if **Yes**, the attribute is **not revised**: its value is the **same in all workspaces**, old versions aren't stored, and changing it **does not affect approval status**. (Used for system-owned/source-of-record values.)
- **Dimension Dependencies** — whether the attribute can hold **context-specific values** (e.g., a different value per language/market).
- **Mandatory (Yes/No)** — whether an object can be **approved without** a value (can also be set on the Product → Attribute Link).
- **Full Text Indexable (Yes/No)** — whether words are indexed so they're searchable **without wildcards** (use sparingly — only for real business needs, as it costs index space).
- **Calculated Attributes** — values **not stored** in the DB but **computed on the fly** from other STEP data (covered fully in Module 3).
- **Attribute Help Text** — a helpful message shown to end users explaining the attribute.

> ⚠️ **Watch-out:** "Externally Maintained" is a frequent exam/interview point. Its values appear in the **Approved** workspace immediately because they aren't under revision control.

### Slide 16 — Entity
**Main point:** An **entity** is *any object that is NOT a product* — typically used for **customer-related** and **reference data**.

**Detailed explanation.** Entities model contacts, addresses, markets, customers, suppliers, reference/lookup data — really any non-product scenario.

**Product features NOT available to Entities:**
- No **Specification attributes** (so no category-specific attributes and no hierarchical inheritance).
- No **classification in a classification hierarchy**.
- No **Tables**.
- No **offline translation**.
- No **GDSN tracking / packaging hierarchies**.
- No **DTP** (desktop-publishing/print) functionality.

**Entity features NOT available to Products:**
- **Object-type-specific revisability** settings (Workspace-revisable / Global-revisable) — entities can be configured one way or the other.
- The option to display **reference target/source objects as children**, letting you build **classification-like hierarchies for entities using entities**.

**Example from the slide.** An entity modeled as an **address** with Description attributes `City, Country, State, Street, Zip` (plus `Name`). Because this entity type is configured **globally revisable**, approval doesn't apply, so the "Approval Status" field isn't shown.

> 💡 **Term:** **GDSN** = Global Data Synchronization Network, a standard for sharing product data between trading partners. **DTP** = Desktop Publishing (print catalog features).

### Slide 17 — Reference Types
**Main point:** A **reference** is a defined connection between two objects, with rules about which object types may connect.

**Detailed explanation.** The reference type's **name refers to the target** of the reference (e.g., a *Product Reference Type* always points **to** a product). Each reference has a **direction**: one object is the **source**, the other is the **target**.

**Allowed connections by reference type (from the slide):**
- **Product Reference Types:** Classification→Product, Product→Product, Entity→Product.
- **Image/Document Reference Types:** Classification→Asset, Product→Asset, Entity→Asset.
- **Classification Reference Types:** Classification→Classification, Product→Classification, Entity→Classification.
- **Entity Reference Types:** Classification→Entity, Product→Entity, Asset→Entity, Entity→Entity, Publication→Entity.
- **Context Reference Types:** Entity→Context.
- **Workspace Reference Types:** Entity→Workspace.

**Example from the slide.** Order code **98332** is the **source**; component part codes (`55489-W`, `55490-W`, …) are the **targets** — modeling "this product is made of these parts."

> 📌 **Remember (ties to approval later):** The **source owns the reference**. Editing a link changes the source, not the target. This rule reappears in Module 6.

### Slide 18 — Dimensions, Dimension Points & Contexts
**Main point:** STEP stores **multi-variant data** (e.g., per language or per market) using **Dimensions, Dimension Points, and Contexts**.

**The vocabulary, built up step by step:**
- **Dimension** — an axis of variation, e.g., **"Language"** or **"Country."**
- **Dimension Point** — a specific value on that axis, e.g., **English, French, German** (for Language) or **Germany, France** (for Country).
- **Context** — a **bundle** that picks **exactly one** Dimension Point from each Dimension. A "German + EUR" context, say.
- Systems usually have a **Global Context** grouping the top-level dimension points, so data entered there is **inherited** by sub-contexts.

**Crucial subtlety:** **Data is stored in dimension points, not in contexts.** To give an object/attribute/reference different values per context, you must make it **dimension dependent**.

**What can be dimension dependent:** Object Types, Attributes, Reference Types, and Assets — used when they should have **different names, LOVs, assets, or linked objects** per context (usually translations, sometimes per-market differences).

**Real-world use case.** A product description attribute is made dimension-dependent on "Language" so the same product shows an English description in the EN context and a French one in the FR context — one product, many localized values.

> 💡 **Mnemonic:** **Dimension = the question** ("which language?"), **Dimension Point = an answer** ("French"), **Context = a full set of answers** ("French + France + EUR").

### Slide 19 — Module completion slide
*"You have successfully completed Data Modeling."* No content.

### Slide 20 — Workspaces, Approval & Revision (preview)
**Main point:** A first look at **Workspaces** — where different revisions of data live. (Module 6 covers this fully.)

- The two primary workspaces are **Main** (the editable working area) and **Approved** (verified data ready to publish).
- You usually **can't edit directly in Approved**; data gets there from Main via the **Approve** operation.
- **New revisions** are created when a revisable object is **created**, **approved**, **modified after approval**, and **modified by a different user** than the one who made the previous revision.
- **Externally Maintained** attributes need no approval — their values appear in Approved as soon as edited in Main.
- Approvals can be **partial** and **context-specific**.

| Workspace | Description |
|---|---|
| **Main** | Standard editable maintenance area for objects. |
| **Approved** | Un-editable; formally approved data ready for translation/publishing. Objects arrive via *Object → Approve object* or automatic approval events. |

> 📌 **Bridge:** Hold this thought — Module 6 turns this preview into the full lifecycle story.

---

### ✅ Module 1 Recap — Data Modeling
- **Everything is an object** with properties (metadata, attributes, references).
- **Object Type = blueprint** (System Setup); **instance = real record** (Tree).
- **Products** live once in the **blue** hierarchy (with inheritance); **Classifications** ("yellow") are alternative groupings (no inheritance).
- **Attributes**: **Specification** (products only, inherits) vs. **Description** (everywhere, no inheritance). A **Validation Base Type** enforces quality.
- **Entities** = anything not a product (customers, addresses, reference data).
- **References** connect objects with a **source → target** direction; the **source owns** the reference.
- **Dimensions → Dimension Points → Contexts** deliver per-language / per-market values; objects must be **dimension dependent** to vary.
- **Main vs. Approved** workspaces, plus revisions — the lifecycle backbone.

---
---

# MODULE 2 — STEP ID, STEP URL & Keys

> **Why this is here:** Module 1 said "everything is an object." Naturally the next question is: *how do we point to a specific object?* STEP has three answers — ID, URL, and Key — each solving a different problem.

### Slides 1–2 — Template + title
Slide 1 is a "Read Me First / Slide Design Guidelines" trainer template. Slide 2 is the title ("Introduction to STEP ID, STEP URLs and Keys," STIBO CoE Team). No Stibo content.

### Slide 3 — Module objectives
You'll learn three identifier concepts and tasks around them: **STEP ID**, **STEP URL**, and **Unique Key**.

### Slide 4 — STEP ID
**Main point:** Every Tree and System Setup object has an **ID**, but an ID alone is **not globally unique**.

**Key facts:**
- The ID **cannot be omitted** and **cannot be changed**.
- Because it identifies the object, it is the **same across all Contexts and Workspaces**.
- **IDs are NOT unique across Node Types.** You can't have two **Products** with the same ID, but you *can* have a Product, a Classification, and an Attribute that all share the same ID.
- Avoid **spaces** in IDs (since they can't be changed later, get them clean up front).
- To get a truly unique identifier, you must **combine the ID with the Node Type** — and that's exactly what a **STEP URL** does.

**Analogy.** An ID is like a **house number**. "Number 12" isn't unique by itself — there's a "12" on many streets. You need the street name (Node Type) to be unambiguous.

> ⚠️ **Interview favorite:** "Is a STEP ID unique?" → *Unique within a node type, but not across node types.* The globally unique identifier is the **STEP URL**.

### Slide 5 — Auto-Generate ID
**Main point:** STEP can **auto-generate IDs** for chosen object types.

**Use it when:**
- Objects are **created very often**, or
- Objects are **created by end users** (who shouldn't have to invent IDs).

**Caution:** There's **no guarantee** an auto-generated ID isn't already in use — this can collide if IDs are generated **both automatically and via manual import**, producing an error.

**Real-world use case.** A web portal where vendors onboard new products: let STEP auto-assign IDs so vendors never type one.

### Slide 6 — STEP URL
**Main point:** A **STEP URL** is the **globally unique** identifier and is used for navigation in the workbench and heavily in the **SOAP API**.

**Example URL (decode it piece by piece):**
```
step://product?editor=Product&contextid=context4&id=wfObj_4234273&workspaceid=Main
```
- `step://product` — it's a product object,
- `editor=Product` — open it in the Product editor,
- `contextid=context4` — the Dutch context,
- `id=wfObj_4234273` — the object's ID,
- `workspaceid=Main` — in the Main workspace.

**Limitation that motivates Keys:** External systems updating STEP usually **don't know** STEP's internal IDs or URLs. So they can't use them — instead they use **Keys**.

> 💡 **Term:** **SOAP API** = an older, XML-based web-service interface to STEP. The URL format above is how SOAP calls and workbench navigation point at exact objects.

### Slide 7 — Keys: Definition
**Main point:** A **Key** lets an external system identify a STEP object by its **attribute values** instead of by ID/URL.

**Detailed explanation.** A Key is a **string representation** of an object that is **unique for a specific Key definition** — no two objects can share the same key. A **Key definition** has an ID and a state, and specifies:
- One or more **Object Types** it applies to (**Product, Entity, Classification, Asset** types only),
- One or more **Attributes** whose values build the key,
- A **STEP Function** used to generate/calculate the actual keys.

**Real-world use case.** Your supplier's system knows a product only by its `ManufacturerName + ManufacturerPartNumber`. Define a Key from those two attributes; now the supplier can update the right STEP product without ever knowing its STEP ID.

### Slide 8 — Key Attribute Considerations
**Main point:** Attributes used in a Key must satisfy strict rules (so keys stay stable and unique).

Each key attribute must:
- Be **valid** for the selected object types.
- Be **externally maintained** (so the value is the **same across all workspaces**).
- Be **single-valued**; if it's a Specification attribute, the value must be **local**.
- **Not** be **dimension dependent** (same value across all contexts).
- **Not** be a **calculated attribute** (one change could force re-calculating millions of keys).
- Have **length ≤ 1,000 characters**.
- If based on an **LOV**, that LOV must **not** be dimension dependent and must be ≤ 1,000 characters.

> ⚠️ **Why these rules?** A key must be **rock-stable and unambiguous**. If it varied by workspace, context, or recalculation, an external system could lose track of the object.

### Slide 9 — Defining Keys
**Main point:** Create Keys in **System Setup → Keys**.

**How:** Right-click **"Keys" → "Create Key,"** give it an **ID and a Name**.

### Slide 10 — Defining Keys (continued)
In the new key's editor you specify the **Object Type(s), Attribute(s), and Function**. The slide shows a simple **non-composite** key (a key built from a single attribute, vs. a **composite** key combining several).

### Slide 11 — Activation of a Key
**Main point:** A new Key is **inactive** until **activated**, and activation only succeeds if every affected object can get a **unique** key.

**Details:**
- Activation runs as a **Background Process** that calculates and stores keys.
- The Key becomes active **only if unique keys can be created for ALL objects** (any duplicate blocks activation).
- After activation: key-attribute fields **become read-only**; only users with the special **"Modify unique key value"** privilege can change them (**Edit → "Edit Unique Key Values"**). You **cannot** update the value via import or APIs.

> 💡 **Term:** **Background Process** = a long-running job STEP executes server-side (so the UI stays responsive). You'll meet these throughout STEP — imports, exports, recursive approvals, bulk updates, and key activation all run as background processes.

### Slide 12 — Thank You
Closing slide. No content.

---

### ✅ Module 2 Recap — ID, URL, Key
- **ID**: mandatory, immutable, same across contexts/workspaces, **unique only within a node type**.
- **STEP URL**: ID + node type ⇒ **globally unique**; used in navigation and the **SOAP API**.
- **Key**: identify objects by **attribute values** so **external systems** can address them without knowing STEP IDs. Strict attribute rules; activated by a background process; only unique configurations activate.

---
---

# MODULE 3 — STEP Functions

> **Why this is here:** Keys are *generated by a STEP Function* (Module 2), and Business Rules and Matching also use this same little language. So learning the function language now pays off everywhere.

### Slides 1–2, 4 — Template + title
Slide 1 is the design-guidelines template; Slide 2 is the trainer's "Attention/What-How-Duration" template; Slide 4 is a title slide (STIBO CoE). No Stibo content on these.

### Slide 3 — Module objectives
You'll learn to **create calculated attributes** in STEP and get to know the **different functions** used to build them.

### Slide 5 — What STEP Functions are
**Main point:** STEP Functions are a **functional programming language very similar to Excel formulas**, used in several places across STEP.

**Detailed explanation.** If you can write `=IF(A1>B1, "WARNING", "OK")` in Excel, you can read STEP Functions. They're used for: **Calculated Attributes**, **Keys**, **Business Rules** (conditions/actions), **Match Codes** (Module 8), and export mapping transformations — a single skill reused widely.

### Slide 6 — Calculated Attributes
**Main point:** A **Calculated Attribute** has a value that is **not stored** in the database but **computed on the fly** from other STEP data.

**When it's computed:** e.g., when a **Product editor is displayed** or an **object is exported**.

**Example from the slide:** a calculated attribute "Dimensions with CM Units" that shows `Height × Width × Length` (all converted to cm).

**Real-world use case.** Show a combined `"Brand – Model (Color)"` display name, or a `Profit Margin` computed from `SalesPrice − PurchasePrice`, without storing (and having to maintain) that derived value.

> 💡 **Why "on the fly" matters:** because the value isn't persisted, it's **always current** — change the inputs and the calculated value updates automatically. The trade-off is **performance** (Slide 14).

### Slide 7 — Setup
**Main point:** Make an attribute calculated by setting **Calculated = Yes** on the Attribute editor.

**Effect:** a **"Value template"** field appears (where the formula lives), and **most normal attribute settings stop applying** (the slide marks those in red — e.g., validation/mandatory settings become irrelevant because nothing is stored).

### Slide 8 — The Value Template field
**Main point:** This field holds the function.

**How to edit:** activate the **Value template** field (so you see the cursor), **right-click → "Insert Function" / "Edit Function"** to open the **Function editor**.

### Slide 9 — The Function Editor
**Main point:** The **Function editor** is where you **define and test** functions. Testing against a sample object before saving is the safe way to work.

### Slide 10 — Available Functions
A reference slide (a catalog of built-in functions). The next slides cover the most common ones.

### Slide 11 — Common Functions for Accessing Values
**Main point:** The everyday functions for **reading attribute values**:

- `value(attribute-id)` — returns the value (no unit).
- `value(attribute-id, unit-id)` — returns the value **converted** to the given unit.
- `simplevalue(attribute-id)` — value **concatenated with the unit name**.
- `simplevalue(attribute-id, unit-id)` — converted to the given unit **and** concatenated with that unit's name.

**Example.** If `Weight = 1.4` (kg): `value('Weight')` → `1.4`; `simplevalue('Weight')` → `1.4 kg`; `value('Weight','g')` → `1400`.

> 💡 **Mnemonic:** **`value` = number only**, **`simplevalue` = number + unit text**.

### Slide 12 — Conditional Functions
**Main point:** `if(...)` and logical helpers drive decisions.

**Examples (read them like Excel):**
- `if(value('purchasePrice') > value('salesPrice'), 'WARNING', 'OK')` — flag when cost exceeds price.
- `if(exact(value('Enriched'), 'Yes'), 'READY', 'NOT READY')` — a **text** comparison (`exact` compares strings).
- `if(value('purchasePrice') > value('salesPrice'), value('purchasePrice'), value('salesPrice'))` — returns the **larger** of the two numbers.
- `if(and(value('salesPrice') > value('purchasePrice'), value('salesPrice') > 10), "OK", "NG")` — "OK" only if **both** conditions hold (`and(...)`).

> 💡 **Term:** `exact(a, b)` = case-sensitive string equality. Use it for text; use `=`, `>`, `<` for numbers.

### Slide 13 — Lists and Iterations
**Main point:** To work across **referenced or child objects**, use **lists** and **iterators**.

- `list(list, separator [, last-separator])` — returns text joining all elements (e.g., comma-separated).
- `iterate(list, expression)` — returns a new list applying `expression` (supplied as **text**) to each element. Inside, you get variables **`index`** and **`item`**.

**Example.** Build a comma-separated list of all child product names, or apply a calculation to each variant.

### Slide 14 — Performance Considerations
**Main point:** Functions that pull data from **many objects** can be **slow**.

**Example from the slide:**
```
{
  valstr := 'value("Contains Nuts")',
  vallist := iterate(subproducts(), valstr)
}
if(listcontains(vallist, 'Yes'), 'Allergy Warning', 'No Warnings')
```
This reads `Contains Nuts` for **all sub-products**, builds a list, then checks if any is "Yes." On a product with **hundreds of sub-products**, every editor load or export must fetch all of them from the database (unless cached) — far slower than reading the product's own data.

> ⚠️ **Best practice:** Keep calculated attributes lean. If a calculation must traverse large numbers of related objects, consider whether a **stored** (non-calculated) attribute, updated by a process, would perform better.

### Slide 15 — Thank You
Closing slide. No content.

---

### ✅ Module 3 Recap — STEP Functions
- A small **Excel-like functional language**, reused for **calculated attributes, keys, business rules, match codes, and export transforms**.
- **Calculated attributes** aren't stored — computed live, so always current.
- Core verbs: **`value` / `simplevalue`** (read), **`if` / `and` / `or` / `not` / `exact`** (decide), **`list` / `iterate` / `listcontains`** (work across collections).
- **Mind performance** — traversing many related objects is expensive.

---
---

# MODULE 4 — Business Rules

> **Why this is here:** Business Rules are the **logic layer** that uses everything so far — they read attributes (Module 1), can be written in the function language (Module 3), gate approvals (Module 6), and power Workflows (Module 5). Master them and STEP becomes programmable.

### Slides 1–2, 4 — Template + title
Slide 1 design-guidelines template; Slide 2 trainer "Attention" template; Slide 4 title slide. No Stibo content.

### Slide 3 — Module objectives
You'll learn to **differentiate types of business rules**, **create them using JavaScript**, and **apply them wherever needed**.

### Slide 5 — About Business Rules (the two variants)
**Main point:** Business Rules are **first-class objects**, each holding a small piece of business logic, in **two variants**:
- **Business Conditions** — **test** something about an object and evaluate to **true or false**. Conditions should generally have **no side effects** (they only check, they don't change data).
- **Business Actions** — **do** something: change data in STEP, send emails, start Background Processes or Workflows, etc.

**Analogy.** A **Condition** is a *question with a yes/no answer* ("Is the price filled in?"). An **Action** is a *command* ("Email the manager").

### Slide 6 — About Business Rules (Libraries)
**Main point:** **Business Libraries** bundle several reusable business rules that can be shared **across workflows or other Business Rules**.

**Real-world use case.** A library of helper functions (e.g., "format a price," "look up a manager's email") reused by many rules — write once, use everywhere.

### Slide 7 — Business Rules usages in STEP (part 1)
**Main point:** Where rules run — **Approval**, **Imports/Inbound Endpoints**, **Workflows**:
- **Approval:** Conditions tested when a revision-controlled object is approved → **allow/prevent** approval. Actions run on approval → modify data, send emails, etc.
- **Imports & Inbound Integration Endpoints:** Conditions can **allow/prevent** creating/updating objects; Actions can **modify** imported objects, send mail, start Workflows, etc.
- **Workflows:** Conditions allow/prevent **state transitions**; Actions run on **entering/leaving a state, on a transition, or when a deadline is met**.

### Slide 8 — Business Rules usages in STEP (part 2)
- **Bulk Updates:** Actions run via a Bulk Update, with a Condition acting as a **pre-condition** for the action.
- **Data Profiles:** Conditions tested against **all objects in a category** (e.g., part of the Product hierarchy); results display on the **Profile Dashboard** (great for data-quality reporting).

### Slide 9 — When should Business Rules be used?
**Main point:** Before writing a rule, check whether a **simpler built-in setting** does the job.

Often-simpler alternatives:
- "Attribute must have a value" → use the standard **Mandatory** setting (enforced on approval).
- Reject rows with missing values during a tabular import → enable that check in the **Import Manager**.
- Restrict the kinds of values entered → **Validation Base Types**, max length, min/max, masks (globally enforced).
- Restrict which object types can sit below others → **Object Types & Structures** configuration.
- Restrict which objects can link to which → make **References/Links valid only** between specific types.

> 💡 **Principle:** *Configuration over code.* A built-in setting is cheaper to maintain and globally enforced; reach for a Business Rule only when configuration can't express the logic.

### Slide 10 — Business Rules Creation
Section divider introducing how rules are built (covered in the following slides).

### Slides 11–12 — Usage: Approval
- **Slide 11 (Condition on approval):** On approval, **Business Conditions** prevent/allow approval of revisable objects (**Products, Classifications, Assets, Entities**). You enable this via the **"On Approve"** field in the main Business Rules editor.
- **Slide 12 (Action on approval):** **Actions** can run when approving — modifying data, sending emails, starting Workflows, etc.

**Real-world use case.** On approving a product, a Condition checks all mandatory marketing fields are filled (else block), and an Action stamps `ApprovedDate = today` and emails the catalog team.

### Slide 13 — Usage: Imports & Inbound Endpoints
When importing **Products, Classifications, Entities, Assets** (via Import Manager **or** Inbound Integration Endpoints), you can have **Conditions tested** and **Actions executed** per imported object.

### Slide 14 — Usage: Workflows
**Main point:** Rules are used **heavily** in Workflows (full detail in Module 5). **Actions** can run when:
- An object **enters** a state (**On Entry**),
- An object **leaves** a state (**On Exit**),
- A **deadline** is met (and the deadline-checker background process runs),
- A **transition** is performed (**On Transition**).

### Slide 15 — Usage: Bulk Update
**Actions** can be applied to a large data set via the Bulk Update **"Run Business Rule"** plug-in — letting mass updates use complex logic.

### Slide 16 — Construction: Condition Plugins with a UI
**Main point:** Simple conditions can be built with **no code** using ready-made **UI plugins** (the rest you write in **STEP Functions** or **JavaScript**). UI plugins usually generate a **user-facing message** when they evaluate to false.

### Slide 17 — Construction: more Condition plugins
- **Attribute Value Comparison** — compare an attribute's value on the object to a **constant** or to **another attribute** on the same object.
- **Reference other Business Condition** — reuse an existing condition inside another.

### Slide 18 — Construction: more Condition plugins
- **Valid Hierarchies** — true if the object sits **below one of the specified hierarchy nodes**. Typically used on the **"Applies If"** tab as a **pre-condition** (only test/act when the object is in a given branch).
- **LOV Cross-Validation** — define **legal combinations** between values in two LOV-based attributes. (The LOVs must be locked so users can't add new values.)

**Real-world use case (LOV Cross-Validation).** Only allow `Material = Leather` when `ProductLine = Premium`; block illegal combinations automatically.

### Slide 19 — Construction: Action Plugins with a UI
Actions can be written in JavaScript, but for simple operations several **UI action plugins** exist (e.g., set an attribute value, create a reference) — described on-screen.

### Slide 20 — Construction: Conditions based on STEP Functions
**Main point:** You can express conditions in the **STEP Function language**.

**How it evaluates:** the condition is **true if the function returns "1"**, **false if "0."** You don't always have to return 1/0 explicitly — many functions do it automatically:
- Binary comparisons `<, >, <=, >=, =, !=` (numeric),
- `exact(string1, string2)`,
- `and(...)`, `or(...)`, `not(...)`,
- `listcontains(list, text)`.

### Slide 21 — Construction: Business Rules in JavaScript
**Main point:** Both **Actions and Conditions** can be written in **JavaScript**, using the public **Java API** (documented as JavaDoc in the SDK).

**How it connects:** JavaScript rules can use standard Java packages, and you wire Java objects into JavaScript variables via **"binds."**

> 💡 **Term:** A **bind** = a named variable that exposes a Java/STEP object (e.g., the current node, the workspace, a logger) to your script. Binds are how your code "reaches into" STEP. **SDK** = Software Development Kit (the developer tools + API docs).

### Slide 22 — Thank You
Closing slide. No content.

---

### ✅ Module 4 Recap — Business Rules
- Two variants: **Conditions** (test → true/false, no side effects) and **Actions** (do something).
- **Libraries** hold reusable rules.
- Run on **approval, imports/IIEPs, workflows, bulk updates, data profiles**.
- Prefer **built-in configuration** first (mandatory, validation, structure rules); use rules for logic config can't express.
- Build with **UI plugins** (simple), **STEP Functions** (true="1"), or **JavaScript** (full power via the Java API + binds).

---
---

# MODULE 5 — STEP Workflows

> **Why this is here:** Workflows orchestrate **people + Business Rules (Module 4)** to move data through a process (draft → enrich → review → approve). They sit right on top of the logic layer.

### Slides 1–2 — Template
Slide 1 design template; Slide 2 trainer "Attention" template. No Stibo content.

### Slide 3 — What a Workflow is
**Main point:** A **workflow** is a **progression of steps** (tasks, events, interactions) forming a work process that **involves two or more people** and **adds value**.
- **Sequential workflow:** each step depends on the previous one.
- **Parallel workflow:** two or more steps happen **concurrently**.

**Analogy.** An assembly line: sequential = one station after another; parallel = several stations working at once, then results merge.

### Slide 4 — STEP Workflow Features
**Main point:** What STEP's workflow engine offers:
- **Visual designer** integrated in the workbench.
- **User and group** task assignment with **claim/release**.
- **Sequential and parallel** execution with automatic **split/merge**.
- **Deadlines and escalation**.
- **Configurable Business Rules** for automation/validation.
- **Task lists** in Workbench and Portal.
- **Configurable data views** per workflow task.
- **Auto-launch on create** option.
- Can be **started/triggered from Business Actions** (on approval, during import, via SOAP API).
- **Dashboards** for monitoring and **KPI reporting**.
- **Per-workflow setup privileges** via Setup Groups.

### Slide 5 — Workflow Setup
**Main point:** Workflow definitions are stored in **System Setup → Setup Groups**. To create a workflow under a Setup Group, **workflows must be valid below that Setup Group type** (set on the **References tab** of the Workflow Basic Object Type).

> 💡 **Term:** A **Setup Group** = an organizing folder in System Setup that also controls **privileges** — who can edit what configuration.

### Slide 6 — Steps to Create a Workflow
The standard build order:
1. Create a new workflow,
2. Create **states**,
3. Create **transitions** between states,
4. Add **events** to transitions,
5. Set **assignees**,
6. Set **validity** (which objects the workflow applies to),
7. Set **workflow options**.

> 💡 **Vocabulary:** **State** = a stage an object sits in (e.g., "Enrich"). **Transition** = the path between two states. **Event** = the trigger that fires a transition (often a button the user clicks).

### Slide 7 — Workflow Designer (layout)
**Main point:** The visual **Workflow Designer** has these areas:
- **Properties panel** (set ID and Name),
- **Workflow Variables/Attachments** area,
- **Validation errors/warnings** area,
- **Overview/zoom** area,
- **Canvas** where you draw States and Transitions.

### Slide 8 — Workflow Editor
Used for workflow-wide changes: **set the default assignee** and **enable status flags** for the workflow.

### Slide 9 — State Editor
**Main point:** Per-state configuration. You can set:
- **Assignee** — add/remove/modify who is responsible in this state.
- **Comments** — manage comments.
- **Deadline/Escalation** — set deadlines.
- **Mandatory Data tab** — attributes/groups/references that **must be populated before a task can leave** the state.
- **On Entry / On Exit** — Business Actions that run when entering/leaving the state.
- **State** — rename / change characteristics.
- **Web UI Screen Mapping** — link the state to a specific Web UI screen.

**Real-world use case.** The "Enrich" state requires `MarketingDescription` and a primary image (Mandatory Data) before the user can submit it onward.

### Slide 10 — Concurrency in Workflow
**Main point:** Two special state types enable parallelism:
- **Cluster** — groups other states.
- **Parallel** — is both a **Cluster** (can hold child states) **and** parallel (the auto-merge behavior; only allows **clusters** as children); it can also be of the **initial** type (start the flow with a parallel split).

**Analogy.** A parallel state is a fork in the road that later automatically rejoins — STEP handles the **split** and the **merge** for you.

### Slide 11 — Task Assignment
**Main point:** Every task is assigned to a **user or user group**, with claim rules.
- A user **sees** tasks assigned to them **or to any group** they belong to.
- A user can **submit** only tasks assigned to **them**; **group tasks must be claimed first**.
- **Exception:** users with the **Workflow Administrator** privilege see and submit **all** tasks.

**Assignment styles:**
- **Static — at workflow level** (a default for the whole flow): specific user/group, or the **executing user** ("dynamic via static rule").
- **Static — at task level**: workflow default, specific user/group, via a **workflow variable** set earlier, or via custom assignee plugins.
- **Dynamic** — via a **Business Action on state entry** (i.e., decided when the task is created).

> 💡 **Claim/release** = grabbing a shared group task so it becomes yours (claim), or putting it back for the group (release). Prevents two people doing the same task.

### Slide 12 — Business Rules in Workflow
**Main point:** Rules drive workflow logic. Actions run **On Entry, On Exit, on deadline, On Transition**; Conditions are tested **on transitions** to allow/prevent them. A workflow can use **local or global** rules.

**Order of execution (memorize this):**
1. **Conditions** evaluated,
2. **On Exit**,
3. **On Transition**,
4. **On Entry**.

> ⚠️ **Interview favorite:** the execution order above (Conditions → On Exit → On Transition → On Entry).

### Slide 13 — Workflow Variables
**Main point:** **Workflow Variables** are like attributes/assets but they **live with the workflow instance**, not with the tracked object — for **transient** data no longer relevant once the workflow ends.

**Examples:** supporting documents (instructions, data sheets), rejection reasons / user-to-user notes, routing selections (e.g., "is copy-writing required?"), or holding **user IDs** for dynamic assignment.

**Behaviors:** a variable can be a **simple text field**, **bound to a STEP attribute** (for validation/LOV dropdowns), or a **calculated expression** (rare). Variables are **global to the workflow instance** (same value across states at any moment).

### Slide 14 — Deadlines and Escalations
**Main point:** Deadlines can be set as a fixed number of **hours/days** in the designer, **dynamically via a Business Action (On Entry)**, or to a specific date-time via the view plug-in **"WorkflowDeadline"** (admins can delete/modify deadlines this way).

**Escalation:** Actions on the **Deadline/Escalation** tab run when a deadline is met **and** the **deadline-monitoring background process** runs. Typical escalations: **send an email**, **trigger a transition** to another state, or **reassign** the task.

> ⚠️ **Key nuance:** Deadlines don't fire by magic — the **deadline checker background process** must run for escalation actions to execute.

### Slide 15 — Monitoring Workflows
**Main point:** Monitor via **Workflow Profiles**, each focused on one of three domains:
- **States** — how many items are in each state, how long, who's assigned, daily throughput, etc.
- **Assignees** — how many tasks each user/group has, for how long, completion rates and average times, etc.
- **Workflows** — average time to reach the final state, count currently in the workflow, etc.

Profile data can be shown as **widgets on the Main Dashboard**.

### Slide 16 — Thank You
Closing slide. No content.

---

### ✅ Module 5 Recap — STEP Workflows
- A workflow = **states** + **transitions** + **events**, built in a **visual designer**.
- Tasks assigned to **users/groups**, with **claim/release**; admins see all.
- **Concurrency** via **Cluster** and **Parallel** states (auto split/merge).
- **Business Rules** automate/validate; execution order = **Conditions → On Exit → On Transition → On Entry**.
- **Workflow Variables** hold transient, instance-level data.
- **Deadlines/escalations** depend on the **deadline-checker** background process.
- Monitor with **Workflow Profiles** (States / Assignees / Workflows) on dashboards.

---
---

# MODULE 6 — Approvals, Revisions & Deletions

> **Why this is here:** This is the **governance and lifecycle** layer that gives the Module 1 "Main vs. Approved" preview its full meaning. It explains how data becomes "trusted," how history is tracked, and how things are safely removed.

### Slides 1–2 — Template + title
Slide 1 design template; Slide 2 title. No Stibo content.

### Slide 3 — Module objectives
You'll get familiar with: the **Approval Process** (Full, Partial, Context-Specific), **Revisions & Traceability**, and **Deletions**.

### Slide 4 — Workspace and Approval
**Main point:** STEP data is logically split into **two workspaces**:
- **Main** — the editable **"draft"** workspace.
- **Approved** — **terminated** (you cannot edit here); data appears via the **approval** operation.

The **approval process pushes data from Main → Approved**, and can be done **manually or programmatically**.

**Analogy.** Main is your **working draft**; Approved is the **published edition**. You edit the draft, then "publish" (approve) it.

### Slide 5 — What gets approved (revisability)
**Main point:** Approval applies only to **workspace-revisable** objects:
- **Products, Classifications, Assets**, and **Entities configured to be workspace-revisable**.

Everything else is **Globally revisable** — identical in Main and Approved (e.g., **Attributes, References** — i.e., configuration/setup objects).

> 💡 **Term:** **Workspace-revisable** = has separate Main/Approved versions and an approval status. **Globally revisable** = one shared version everywhere, no approval needed.

### Slide 6 — Approval Statuses (intro)
**Main point:** A workspace-revisable object is **created in Main** and **doesn't appear in Approved until its first approval**. Every such object has an **"Approved" property** showing its status.

### Slide 7 — Approval Statuses (list)
A reference slide listing the possible statuses. In practice these include states such as: **never approved** (exists only in Main), **approved** (Main matches Approved), **modified after approval** (Main has newer changes than Approved), and **partially approved** (some parts approved, some not — see Slide 11).

### Slide 8 — Data Ownership (intro)
**Main point:** For an object to be **fully approved, all data it OWNS must also be approved.** The slide shows the data a Product owns.

### Slide 9 — Data Ownership (the rules)
**What a Product (also Classification/Entity/Asset) owns:**
- Its **parent link**.
- Its **local values** — but **NOT inherited Specification values**. So changing an inherited value at an ancestor **doesn't change** this product's approval status; inherited values are approved **with the object they're local to**.
- All **local References/Links where it is the Source**, plus **Description Attribute values on those links**.

**Consequence:** when a link/reference is modified, it's the **Source** that changes; the **Target** is unaffected.

> 📌 **Connects to Module 1, Slide 17:** "the source owns the reference." This is the same rule, now in the approval context.

### Slide 10 — Conditions to Approve an Object
**The rules for a successful approval:**
- Must approve **from Main**.
- **Cannot approve if the parent isn't approved** (approve **top-down**).
- A reference/link **can't be approved if its Target doesn't exist in Approved**.
- If an attribute or reference/link type is **Mandatory**, you **can't approve** without it populated.
- **Externally Maintained** attributes/references aren't under revision control (they bypass approval).
- The **revision number changes automatically** on approval.
- The **entire hierarchy** can be approved at once via **Approve Recursively**.

### Slide 11 — Partial Approval (concept)
**Main point:** You **can** approve an object even if it has a reference/link to an object **not yet in Approved**. The result is **"partially approved":** the object and all approvable data are approved, but **that reference/link is not**. If the target is later approved, you must **approve the source again** for the link to reflect in Approved.

### Slide 12 — Partial Approval (how)
**Main point:** Partial approval is useful when **some elements must go live before the rest can be approved**. Do it via **Maintain → Approval → Partial Approve** (or right-click the object → **Partial Approve**).

**Real-world use case.** A new product references an accessory not yet ready. Partially approve the product now (so it's live), and approve the reference later once the accessory exists in Approved.

### Slide 13 — Approve Recursively
**Main point:** **Approve Recursively** searches for unapproved objects **below (or linked to)** a selected node and approves them all (copying to Approved). Do it via **Approval → Approve Recursively** (or right-click → Approve Recursively). It runs as a **Background Process**.

> ⚠️ **Caution:** Recursive approval can touch huge subtrees — it's powerful but should be used deliberately.

### Slide 14 — Context-Dependent Approvals
**Main point:** Approval always happens **in a specific context** and applies only to data **visible in that context**.

**Example from the slide.** A product approved only in the **"EN" context** → the dimension-dependent `Color` value is present in the Approved container **only for EN**. Other contexts remain unapproved until approved in those contexts.

> 📌 **Ties to Module 1:** dimension-dependent data + context-specific approval work hand in hand for localized/market data.

### Slide 15 — Section divider: Revisions and Traceability
A divider slide. No content.

### Slide 16 — Revisions and Traceability (how revisions are created)
**Main point:** Historical versions are stored as **Revisions** — each a **"snapshot"** of the object.

A revision is created:
- **Automatically on creation** of a new workspace-revisable object,
- **Automatically on approval**,
- **Automatically when a change is made by a different user**, or any change **following an approval**,
- **Automatically** when a user makes a change and the **current revision is older than a configurable threshold** (even by the same user).

**Important limit:** STEP does **NOT** track changes at the **field level** (no per-field history). But a revision is **always tied to a user**, so you can always see **who** is responsible for a set of changes.

### Slide 17 — Revisions and Traceability (inspecting)
**Main point:** Inspect revisions from the object editor's **Status tab** — you can **view an old revision** and **revert** to it.

> 💡 **Practical value:** made a bad bulk change? Revisions let you see prior snapshots and roll back, and audit who changed what (at the snapshot level).

### Slide 18 — Section divider: Deletion Process in STEP
A divider slide. No content.

### Slide 19 — Deletion
**Main point:** Deleting **workspace-revisable** objects is like the **Windows/Mac Recycle Bin**.
- Delete a product → it's **not purged**, it goes to the **STEP Recycle Bin** (visible in Tree).
- Objects that are **not workspace-revisable** are deleted **directly** (no recycle bin).
- Deleting an object with **children** deletes the **children/ancestors** as well.
- You can **purge** items from the Recycle Bin via its context menu.

### Slide 20 — Deletion (continued — removing from Approved)
**Main point:** Just as approval put the object **into** Approved, the **deletion must be approved** to remove it **from** Approved. Once that succeeds, the object can be **purged**.

**Consistency restrictions in Approved:**
- You **cannot approve the deletion** of an object that **has children in Approved** — delete children first.
- You **cannot approve the deletion** of an object that is the **Target of a reference/link in Approved** — remove the reference/link first (remove it in Main and approve the **Source**).

> ⚠️ **Mental model:** Deletion mirrors approval. Removing from Approved follows the same **top-down, target-before-source** discipline (reversed) that approval uses.

### Slide 21 — Thank You
Closing slide. No content.

---

### ✅ Module 6 Recap — Approvals, Revisions & Deletions
- **Main (draft) → Approve → Approved (published).** Only **workspace-revisable** objects (Products, Classifications, Assets, revisable Entities) get approved; config objects are **globally revisable**.
- Full approval needs **all owned data** approved; approve **top-down**; targets before sources; mandatory fields filled.
- **Partial approval** lets parts go live early; **Approve Recursively** does whole subtrees (background process).
- Approval is **context-specific** (pairs with dimension-dependent data).
- **Revisions** are snapshots (no field-level history) but always tied to a **user**; revert via the **Status tab**.
- **Deletion** = Recycle Bin for revisable objects; removing from Approved must be **approved** and respects children/reference constraints.

---
---

# MODULE 7 — Search, Collections & Bulk Updates

> **Why this is here:** Now that data exists and is governed, you need to **find** it and **maintain it at scale**. These three tools (Search → Collections → Bulk Updates) form the daily data-steward toolkit.

### Slides 1–2 — Template
Slide 1 design template; Slide 2 trainer "Attention" template. No Stibo content.

### Slide 3 — Module objectives
You'll learn to **search** for objects, **create collections**, and run **bulk updates** on found items.

### Slide 4 — Title slide
"Search, Collections and Bulk Updates," STIBO CoE. No content.

### Slide 5 — Workbench Search: Goto Search
**Main point:** **Goto Search** jumps you **straight to an object** (no result list).
- Type a **Name or ID**, press Enter (or click "Goto next object"); STEP takes you to the **first hit**.
- Browse further hits with the **Goto next object** button.
- You can also search by **unique Key** by selecting the key from the Goto dropdown.

**Analogy.** Goto is the browser's "I'm Feeling Lucky" — straight to the best match.

### Slide 6 — Workbench Search: The Search Tab
**Main point:** The **Search navigator tab** + **Search Result Profiling page** give advanced search. Two approaches:
- **Know the details?** Build a precise query (e.g., Products where `Weight < 5 kg`, below the "Office Chairs" folder, not of type "Item").
- **Don't know much?** Start **broad**, then **narrow** using the Search Result Profiling page.

### Slide 7 — Search (screenshot)
A screenshot of the Search tab UI. No additional text to learn.

### Slide 8 — Basic Searches (Name/ID)
**Main point:** Default search looks across **Name, ID, and Attribute values**; matching text anywhere counts.
- **Wildcards** `?` (single char) and `*` (many chars) are valid **anywhere** in the string.
- **Scope it** by prefixing `ID=` or `Name=` to search only IDs or only Names.

### Slide 9 — Basic Searches (Attribute value — how to)
**Steps:** enter an **Attribute Name/ID** → pick it from the typeahead (it inserts `Attribute Name (Attribute ID)`) → enter a **search operator** (or space, then pick one from the typeahead).

### Slide 10 — Basic Searches (typeahead values)
After the operator, the typeahead lists **actual values stored** for that attribute — so you pick a real value rather than guessing.

### Slide 11 — Basic Searches (operators)
A reference slide of available **search operators** (equals, not equals, greater/less than, contains, begins/ends with, is empty, etc.).

### Slide 12 — Searches in Full-Text-Indexed Attributes
**Main point:** Attributes set to **Full Text Indexable** search **differently**.

**Example.** Value: *"Black powder coated diecast aluminum enclosure…"*
- If **Full Text Indexable**, `Description = aluminum` **finds it** (word-level match, no wildcards).
- If **not**, you'd need `Description = *aluminum*` (wildcards both sides).

**Performance note:** searches **starting with a wildcard** (`*term`) are **heavy** and should generally be avoided.

> 📌 **Connects to Module 1, Slide 15:** "Full Text Indexable (Yes/No)" — this is *why* you'd turn it on: word-level search without wildcards.

### Slide 13 — Search Criteria (types)
Different **search criterion types** are available from the **Search type drop-down** (by attribute, object type, hierarchy location, approval status, references, and more).

### Slide 14 — Combining & Negating Criteria
- **Combine:** the green **plus** icon adds criteria; by default they are **AND**'ed.
- **Negate (Exclude/NOT):** hold the **"Add criterion"** button to reveal **"Add Exclude."**

### Slide 15 — OR Searches & Result List
- **OR separators** can be inserted between criteria via the add-criterion button.
- The **Search Result List** appears **below the search box** after executing.

### Slide 16 — Search from List
**Main point:** **Search from List** lets you search a **pasted set of values** (from Excel or another file) by **ID/Name/Unique Keys or any attribute** (choose from dropdown). Paste the list into the box, click search.

**Real-world use case.** Marketing hands you 500 SKUs in a spreadsheet — paste the column, choose "ID," and pull exactly those products.

### Slide 17 — Search Result Profiling Page
**Main point:** The **Search Result Profiling page** refines results conveniently: run a broad search, then **click links in the profile** to add criteria and narrow down (faceted refinement).

### Slide 18 — Bulk Updates (entry points)
**Main point:** **Bulk Update** updates **large amounts of objects in one operation.** Start it from:
- A **Collection's** context menu,
- A **multi-selection** in Tree/System Setup via **"Run Bulk Update,"**
- A **search result** directly from the Search tab.

### Slide 19 — Bulk Update Wizard (operations)
**Main point:** The wizard lets you specify **operations** applied to the set, **one object at a time**. STEP ships several out-of-the-box operation types (set attribute value, add/remove reference, change object type, run a business rule, etc.).

### Slide 20 — Bulk Update Wizard (ordering & rollback)
**Main point:** Multiple operations run **in the listed order**. If **one operation fails for an object, all changes to that object are rolled back** (per-object atomicity).

### Slide 21 — Bulk Update Wizard (preview)
The wizard shows a **preview** of applying the operations to the **first 10 objects**.

### Slide 22 — Bulk Update Wizard (advanced preview & caution)
**Main point:** For a more precise preview, use the wizard's **"Advanced"** step. **Test on a small set first.**

> ⚠️ **CRITICAL:** There is **no "undo"** for Bulk Updates. Always preview/test small, and remember revisions (Module 6) are your safety net — but prevention beats recovery.

### Slide 23 — Scheduling a Bulk Update
**Main point:** From the **File menu**, schedule a Bulk Update. Scheduling takes two inputs: a **Collection** (the set of objects) and a **Bulk Update Configuration** (the operations).

### Slide 24 — Collections (what they are)
**Main point:** **Collections** are **containers for sets of objects** from Tree/System Setup, **independent of hierarchy placement.** Created via **search or import**; all objects in a collection can be updated together. Found in the **Collections hierarchy** on the Tree tab.

**Analogy.** A Collection is a **playlist** — songs (objects) from anywhere in your library, grouped for a purpose, leaving the originals in place.

### Slide 25 — Creating Collections (two ways + flat view)
**Two ways:** (1) from a **Search** result; (2) from an **import file.**
- If a collection has **< 10,000 objects**, you can inspect it by expanding the Collection node in the Tree.
- It displays as a **completely flat structure**, regardless of parent-child relationships elsewhere.

### Slide 26 — Creating Collections (from Search — steps)
Most common method: go to the **Search tab**, run a search, verify results, click **"Save as Collection."**

### Slide 27 — Creating Collections (from Search — choose location)
Pick the **parent** in the Collections hierarchy (top folder or a collection group), **name** it (ID auto-generated), click **OK**.

### Slide 28 — Creating Collections (from Search — background process)
A **background process** runs and the collection is created under the chosen folder.

### Slide 29 — Creating Collections (from File Import)
**Main point:** Collections can be created from a **text/CSV file containing STEP IDs** of products, assets, or classifications. **Objects must already exist** (import won't create/update — it only **places** them in a collection).
- **Important:** if the file has only **attribute values or unique keys** (no STEP ID), you must use the **"from Search"** method instead.

### Slide 30 — Creating Collections (from File — start)
In the Tree, right-click the **Collections** top node (or a group) → **"Create Collection From File."**

### Slide 31 — Creating Collections (from File — locate file)
In the dialog, locate the file to import. The **Collection ID is auto-generated.**

### Slide 32 — Creating Collections (from File — finish)
Set a **Collection Name**, choose what the file **contains** (IDs of products/classifications/assets), click **OK** to start the **background process**.

### Slide 33 — Thank You
Closing slide. No content.

---

### ✅ Module 7 Recap — Search, Collections & Bulk Updates
- **Goto** = jump to one object; **Search tab** = precise or broad-then-refine (via **Search Result Profiling**).
- Search across **Name/ID/Attributes**; **wildcards `? *`**; prefix **`ID=`/`Name=`**; combine with **AND/OR/NOT**.
- **Full Text Indexable** attributes allow **word-level search without wildcards**; avoid leading `*` (slow).
- **Search from List** searches a pasted value set.
- **Collections** = hierarchy-independent containers (like playlists), built from **search or import** (import needs existing objects + STEP IDs), shown **flat**.
- **Bulk Updates** apply ordered operations (per-object rollback on failure), can be **scheduled** with a Collection + Configuration, and have **NO undo** — preview and test first.

---
---

# MODULE 8 — Matching & Linking

> **Why this is here:** With lots of data flowing in (often from many sources), you get **duplicates**. Matching & Linking finds them and produces a single trusted **"Golden Record."** It builds on functions (Module 3), business rules/workflows (Modules 4–5), and feeds clean data downstream.
>
> *Note: every slide in this deck repeats a trainer "Need/Benefits (WIIFM)" template box — that's coaching for the presenter, not Stibo content, so it's omitted below.*

### Slides 1–2 — Template + title
Slide 1 design template; Slide 2 trainer "Attention" template. No Stibo content.

### Slide 3 — Purpose
You'll learn how matching/linking works: a **process to identify duplicates** in STEP and **how to handle** potential duplicates.

### Slide 4 — Title slide
"Matching and Linking," STIBO CoE. No content.

### Slide 5 — Terminal Objective (agenda)
Topics: **Matching and Linking**, **generating match codes & the matching algorithm**, **identifying duplicates**, **handling duplicates**, and **configuring the event processor**.

### Slide 6 — Matching & Linking (overview)
**Main point:** The component **identifies** and **handles** duplicate **Product, Entity, Asset, and Classification** objects — two parts:
1. Functionality to **identify** duplicates,
2. Functionality to **handle** identified duplicates.

**History:** older STEP could identify duplicates and do **manual merges**; **Trailblazer** added **automatic Golden Records** using configurable **Survivorship Rules**.

> 💡 **Term:** **Golden Record** = the single "best" version of a record, assembled from the best pieces of all its duplicates. **Trailblazer** = a STEP release name.

### Slide 7 — Strategy for Identifying Duplicates
**Main point:** First **define what makes two objects duplicates.**
- For **products:** same **EAN**, or same/similar **manufacturer + manufacturer part number**.
- For **party (people) data:** same/similar **names + addresses**.

**The scale problem:** comparing **every object with every other** is unviable at thousands/millions of records. Solution: generate **Match Codes** for objects, then compare only similar ones via a **Matching Algorithm**. Matches are handled by **merging** or **creating Golden Records**; matched objects can either **stay and link** to the golden record or be **permanently merged** into it.

### Slide 8 — The four underlying elements
**Main point:** Matching/Linking relies on **four** pieces working together:
1. **Match Codes**,
2. a **Matching Algorithm**,
3. an **Event Processor**,
4. an **Inbound Integration Endpoint**.

Match codes are generated for the dataset; the algorithm evaluates those codes for **potential duplicates**.

### Slide 9 — Match Code
**Main point:** A **Match Code** is a **string representing an object**, built via **STEP Functions or JavaScript**.

**How it limits work:** match codes populate an **alphabetically sorted table**; STEP compares **only objects whose match codes are near each other** in that sorted list. This makes comparisons **linear** with the number of objects (not exponential). How many neighbors each object compares against is set by the **Window Size**.

**Example.** For products, a match code = `manufacturer value + manufacturer part number value` concatenated.

**Analogy.** Sort everyone in a room **alphabetically by name**, then only compare each person to the few standing **next to them** — not to the entire room.

### Slide 10 — Match Code (design considerations)
**Best practices:**
- **Profile the data first** (the data-profiling tool helps); check **how well-populated** an attribute is before using it in a match code.
- When combining several pieces, **put the most significant data first** (so similar records sort together).
- You can generate **several match codes per object** (STEP Functions can return a **list**; JavaScript can return an **array** — each element is a separate match code).

**Worked example.** Customers with a **name** and an **address**:
- A single `address + name` code **misses** customers who **moved** (their codes drift apart).
- Better: give each object **two** codes — one for **Name**, one for **Address** (with a **hardcoded prefix** to prevent cross-domain comparisons) — so they can match on **either** similar names **or** similar addresses.

### Slide 11 — Matching Algorithm
**Main point:** Match Codes only **limit comparisons**; the **Matching Algorithm** does the **actual comparison**, producing a **0%–100%** equality score, and is where the **Match Action** (Golden Record / Identify Duplicates) is configured.

### Slide 12 — Match Criteria
**Main point:** The real matching logic lives under the algorithm's **"Match Criteria"** flipper. Reusable variables go under the **"Global Binds"** flipper.

### Slide 13 — String Comparison Algorithm (edit distance)
**Main point:** One comparison approach is **edit distance**, specifically **Levenshtein distance** — a measure of **how many edits** (substitution, insertion, deletion) turn one string into another. STEP can apply **Levenshtein / Damerau-Levenshtein** directly to strings you build with STEP Functions, outputting an equality measure. String comparison alone often isn't enough, so other criterion types exist (next slide).

> 💡 **Term:** **Levenshtein distance** — "kitten" → "sitten" → "sittin" → "sitting" = 3 edits. **Damerau-Levenshtein** additionally counts a **transposition** of two adjacent characters as a single edit.

### Slide 14 — More Criterion Types
- **Multi Word Damerau-Levenshtein** — like Damerau-Levenshtein, except **swapping two whole words** doesn't count as an edit (so "John Smith" ≈ "Smith John").
- **Number Distance** — relative closeness of two numbers: `lowest / highest × 100`.
- **JavaScript Criterion** — write your **own** comparison; only requirement: return a number **0–100**.
- **Decision Tables** — break complex matching into **smaller, manageable parts**.

### Slide 15 — Handling Identified Duplicates
**Two Match Actions:**
- **Identify Duplicates** — flags possible matches for inspection from the algorithm object. Only parameter: a **threshold** (how equal to be flagged).
- **Golden Records** — instead of merging, **create a new "Golden Record"** from the duplicates' data.

**Golden Record setup tasks:** create a **golden record object type**; a **golden record reference type** (if applicable); a **golden record root node** (where new golden records first appear); specify the golden record object type in the relevant **component models**; configure the **match action** (object type, root node, reference type, default source system if applicable) and set the **auto threshold** and **clerical review threshold**; optionally configure a **clerical review workflow**.

> 💡 **Two thresholds:** **Auto threshold** (score ≥ this ⇒ auto-create/merge golden record) and **Clerical Review threshold** (score between the two ⇒ a **human reviews** it in a workflow task). Below the review threshold ⇒ not a match.

### Slide 16 — Survivorship Rules (concept + Trusted Source)
**Main point:** A Golden Record's attribute/reference data is copied from contributing objects **automatically**, governed by **Survivorship Rules** set on the algorithm. Rules can be defined **independently** for the object's **name, references, data containers, and attributes/attribute groups.**

Survivorship rules apply to **Merge Golden Record** (sources stored **outside** STEP) and **Link Golden Record** (sources stored **in** STEP) configurations; both **require** survivorship rules.

**Strategy 1 — Trusted Source:** take data from a **trusted/ranked source**; requires that **source info is available** on the source objects.

### Slide 17 — Survivorship Rules (Most Recent + combinations)
- **Most Recent** — take data from the source object with the **most recent data**.
- **Survivorship Rule Types** — you can **combine** Most Recent and Trusted Source strategies.

**Real-world use case.** For a customer golden record: take **phone** from the most-recently-updated source, but take **legal name** from the **trusted** CRM source.

### Slide 18 — Keeping Matching & Linking Up-to-Date
**Main point:** After initial setup, you can keep things current **without regenerating everything** via two Business Action / Bulk Update operations:
- **Generate Match Codes** — takes a **Match Code ID**; generates match-code values for the objects it's applied to.
- **Match Duplicates (apply matching algorithm)** — takes a **Matching Algorithm ID**; using the just-inserted match-code value(s), compares the object against others with similar/identical codes (the **Window Size** applies as before).

### Slide 19 — Configuring the Matching Event Processor
**Main point:** To deduplicate **continuously**, configure an **Event Processor** that triggers the matching algorithm. When invoked, it **creates matching events** so the algorithm runs; potential duplicates scoring **between the clerical-review and auto thresholds** become **clerical workflow tasks** for manual handling.

**Steps:** (1) **Create** a matching event processor → (2) **Enable** it → it's ready to run.

> 💡 **Term:** An **Event Processor** reacts to changes (events) in STEP automatically — here, it kicks off matching whenever relevant data changes, so dedup happens in near-real-time rather than only in big batch runs.

### Slide 20 — Initial Configuration: the Matching Component Model
**Main point:** Before any of this works, configure the **"Matching Component Model,"** which **defines all object types allowed to be matched.** Path: **System Setup → Component Models → Matching node → Component Model Configuration tab → Edit.**

### Slide 21 — Initial Configuration (screenshot)
A configuration screenshot. No additional text.

### Slide 22 — Recap (in-deck)
The deck's own recap of: matching & linking, match codes & algorithm, identify/handle duplicates, configure event processor.

### Slide 23 — Thank You
Closing slide. No content.

---

### ✅ Module 8 Recap — Matching & Linking
- Four pieces: **Match Codes + Matching Algorithm + Event Processor + Inbound Endpoint.**
- **Match Codes** (strings, sorted) limit comparisons to nearby records (**Window Size**); design them with the **most significant data first**, and use **multiple codes** (e.g., name *and* address) to catch movers.
- The **Matching Algorithm** scores **0–100%** using **Levenshtein/Damerau-Levenshtein, Number Distance, JavaScript, Decision Tables.**
- Two **Match Actions**: **Identify Duplicates** (one threshold) and **Golden Records** (**auto** vs. **clerical-review** thresholds → human review workflow).
- **Survivorship Rules** (**Trusted Source**, **Most Recent**, or a mix) decide whose data wins, per field/reference.
- Keep current with **Generate Match Codes** + **Match Duplicates**; automate via the **Matching Event Processor**; enable types in the **Matching Component Model.**

---
---

# MODULE 9 — Digital Asset Management (DAM)

> **Why this is here:** Module 1 introduced **assets** (images/docs as objects). This module is the full lifecycle: **import → recognize → maintain → export/distribute → store externally**. It connects to Integration Endpoints (Module 14) and the REST API.
>
> *Note: most slides repeat the trainer "Need/Benefits (WIIFM)" template box — omitted below as it isn't Stibo content.*

### Slides 1–2 — Template + title
Slide 1 design template; Slide 2 trainer "Attention" template. No Stibo content.

### Slide 3 — Purpose
You'll learn how digital assets are **stored and maintained** in STEP, and the **import/export** process.

### Slide 4 — Title slide
"Digital Asset Management," STIBO CoE. No content.

### Slide 5 — Terminal Objective (agenda)
Topics: **import & auto-recognition**, **different import mechanisms**, **maintaining assets**, **exporting assets**, **different export mechanisms**.

### Slide 6 — Import & Auto-Recognition (Manual Asset Importer)
**Main point:** Importing media files can **auto-create Assets of a specific Object Type** (Images or Documents).
- This relies on STEP reading the file's **MIME type** and matching it to the **MIME type configured on an Asset Object Type.**
- If **multiple** Asset Object Types share the **same MIME type**, STEP picks one **at random.**

> ⚠️ **Watch-out:** don't configure two asset types with the **same** MIME type unless you accept random assignment.

### Slide 7 — Import & Auto-Recognition (storage & limits)
- Not **all** media types are supported out of the box; some need **special handling.**
- On import the binary is stored as a **BLOB in the Oracle database**; **metadata is extracted** and shown under the **"System Properties"** flipper (this data **cannot be modified**).
- The Asset import wizard allows multiple files, but for **large volumes** this manual option **isn't viable** (use the Asset Importer instead).

> 💡 **Term:** **BLOB** = Binary Large Object — how the raw file bytes are stored in the database. (Slide 32 explains why storing many BLOBs grows the DB and complicates backups.)

### Slides 8–9 — The Asset Importer
**Main point:** The **Asset Importer** is the **robust, core tool** for **mass-loading** images/documents/other assets and **updating** asset data.
- To enable it, set **"Asset Import Compatibility Mode" = "Advanced"** (under **Users & Groups → System Settings → Image & Document Settings**).
- *(Slide 8 was largely a screenshot; the descriptive text appears across slides 9–10.)*

### Slide 10 — Asset Importer (setup groups)
**Main point:** The Asset Importer needs a **Setup Group** called **"Asset Import Configurations"** to hold all configs centrally, plus a **child setup group** named **"Asset Import Configuration Type"** for the actual import configuration — so all asset import configs live in one place.

### Slide 11 — Asset Maintenance (edit in place)
**Main point:** You can **edit a stored file in a local editor** and **save the edited version back to STEP.** Trigger via **"Edit Asset"** from the Asset Tree object's context menu, or right-click the **thumbnail** on the Asset editor → **"Edit Asset."**

### Slide 12 — Asset Maintenance (continued)
The file opens in your **locally associated editor** while a **STEP dialog** lets you **save the modified version back.** Saving creates a **new revision.**

**Real-world use case.** Open a product photo in Photoshop directly from STEP, crop it, save — STEP keeps the new version with full revision history.

### Slide 13 — Export Asset (the four mechanisms)
**Main point:** Assets can be exported via:
1. **Export Images and Documents wizard**,
2. **Export Manager or an OIEP**,
3. **Asset Push**,
4. **REST API.**

### Slide 14 — Export: Image Conversion Configuration
**Main point:** Export media to disk via **"Export Images & Documents"** from the context menu of an **Asset** or a **Classification containing assets.** Image assets can be **converted** during export — choose **"Custom…"** in step 2 of the wizard to configure manually.

### Slides 15–16 — Image Conversion (settings)
You can configure **format, size, and color** settings (the on-screen screenshots show the dialogs). *(Slide 16 was a screenshot continuation.)*

### Slide 17 — Image Conversion (caching)
**Main point:** A **Cache** step lets you enable caching and choose **when** it happens (radio buttons). Caching is available via the **Export Manager** or **asynchronously** via the **Image Cache event processor.**
- For best performance, configure the **"Image Cache Event Processor"** to listen for incoming asset object types and **apply conversions automatically.** Conversions set to **"cache on import"** become available.
- **Save and Finish** completes the conversion so it can be **reused later.**

> 💡 **Why cache?** Converting images on demand is CPU-heavy. Pre-generating (caching) common sizes/formats means downstream requests are served instantly.

### Slide 18 — Reusable Image Conversion Configuration
**Main point:** To create a **reusable** conversion config, select a **Classification** to store it under (it's saved as a special **Asset**), then **Maintain/Insert → "New Image Conversion Configuration…"**. Once created, pick it in the **"Image Conversion"** step of the export wizard.

### Slide 19 — Export Manager (asset options)
**Main point:** The **STEPXML** and **Advanced STEPXML** formats in the **Export Manager** can export **asset metadata, references, and digital content** for images and non-images. For **automatic, event-based** exports, configure an **OIEP** listening for new/changed/deleted assets. Set the **"Include Assets"** parameter as needed.

### Slide 20 — Export Manager (asset content options)
- **None** → neither assets nor content in output.
- **Include Asset Content** → choose:
  - **Binary** — content **BASE64-encoded** (external system decodes it), or
  - **REST** — a **relative REST resource URL** (external system completes the path to fetch it).
- If **no content** is available for an image, the XML tag is **not exported.**

> 💡 **Term:** **BASE64** = a way to represent binary (image bytes) as text so it can travel inside an XML/JSON file. Bigger payload, but self-contained.

### Slide 21 — Export Manager (selecting conversions)
Click **"Select Image Conversions"** and pick **at least one** conversion to enable Next/Finish. Selecting **multiple** conversions is allowed but **increases export time and file size.**

### Slide 22 — Asset Push (what & why)
**Main point:** Embedding asset content in exports isn't viable when a **downstream system needs the actual files.** Normally STEP **doesn't include** asset content in exports; instead it uses **Asset Push.**
- Asset Push **shares/distributes** media files from STEP to an **external file system on another host**, keeping that location **always updated** with the latest version from STEP.

### Slide 23 — Enabling Asset Push (steps)
1. (Optional) create an **Image Conversion Configuration**,
2. Create an **Asset Push Event Queue**,
3. Create one or more **Asset Push Configurations**,
4. Install the **Java Sidecar application** on the **sidecar host** that will hold the pushed files,
5. **Initiate Asset Push.**

> 💡 **Term:** A **Sidecar** is a small helper Java app installed on the *receiving* server. STEP pushes files to it, and it writes them to that server's file system.

### Slides 24–25 — Creating an Asset Push Event Queue
- Configure under **System Setup → Event Queues.** Decide behaviors like **how long the queue retains events** after processing (enables **reprocessing**).
- Other settings:
  - **Unread events** — approximate count of unprocessed events,
  - **Asset Push Sidecar** — shows the sidecar's **IP** (from the host running the Java app); "No activity yet" if none detected,
  - **Consumer Read** — **Disabled** (processed events **not delivered** — useful to pause, e.g., if the destination disk is full) or **Enabled** (deliver to destination).

### Slides 26–27 — Creating Asset Push Configurations
**Main point:** The **Asset Push Configuration** governs behavior and is created **below** an Asset Push Event Queue. It decides **where** files land on the sidecar and **whether images are converted** on push. Each configuration creates a **folder of the same name** on the sidecar host (subfolders per the relative-path template).

**Settings (Slide 27):**
- **Workspace** — which workspace to push from (typically **Approved**),
- **Image Conversion Configuration** — optional conversion,
- **Relative Path Template** — how to organize the output folder structure,
- **Auto Cleanup** — whether to clean up old file versions,
- **Include Classification** — which part of the classification hierarchy to export,
- **Include MIME Type(s)** — filter to specific file types,
- **Include Attribute(s)** — restrict to assets with specific values, format `[Attribute ID]=[Attribute value]`.

### Slides 28–29 — Installing the Java Sidecar
- The Sidecar is a **Java app in a jar file** for deployment on the receiving host. A **jar is auto-created** for download after you create an Asset Push Configuration. The sidecar server needs the **latest JRE.**
- Download from **`http://[application server]/sidecar`** into the install directory (this becomes the **root directory** for stored files).
- Install on **Windows** with: `java -jar <name-of-assetpush-queue-jar>.jar –install`.
- After deployment, edit **`assetpush.properties`** in the install dir to set a **username and password.**

> 💡 **Term:** **JRE** = Java Runtime Environment (what's needed to run Java apps).

### Slide 30 — Monitoring Asset Push
View statistics on the **Asset Push Configuration → Statistics** tab. From individual **Asset objects** configured to be pushed, see status on the **Status** tab.

### Slide 31 — Export: REST API
**Main point:** The **REST API** lets you **upload files to a REST server**, later usable by invoking the **STEP REST API.**

> 💡 **Term:** **REST API** = a modern, web-friendly (HTTP/JSON) interface — the contemporary counterpart to the older SOAP API mentioned in Module 2.

### Slide 32 — Store Asset Externally (why)
**Main point:** Storing assets **inside** STEP grows the **database** significantly:
- Larger DB → **longer backups.**
- **Deleting** assets does **not** auto-recalculate (shrink) the DB size, so backups stay slow.
- To reclaim space you must **compress then restore** the DB.
- **Better:** store assets **outside** STEP while still **displaying/exporting** them from STEP.
- **Caveat:** externally stored assets are **not supported by Stibo Systems** — you take on more responsibility.

### Slide 33 — Store Asset Externally (two options)
- **External DAM** — a **URL** retrieves the content; the **files** live in an external DAM while the **asset object + metadata** stay in STEP.
- **External File Structure (EFS)** — a **unique file name** retrieves content; assets live in an **external file system on the STEP application server** (you maintain/back it up; not Stibo-supported).
- For **both**, **configuration asset files** (transformation lookup tables, export configs) **stay within STEP.**

### Slide 34 — Recap (in-deck)
The deck's own recap: import & auto-recognition (Manual Importer, Asset Importer), maintenance, export (wizard, Export Manager/OIEP, Asset Push, REST), and storing externally.

### Slide 35 — Thank You
Closing slide. No content.

---

### ✅ Module 9 Recap — Digital Asset Management
- Assets auto-recognized by **MIME type**; binaries stored as **BLOBs**; metadata auto-extracted (read-only "System Properties").
- **Manual Asset Importer** (small) vs. **Asset Importer** (mass-load; needs **Advanced** mode + setup groups).
- **Edit Asset** opens files locally and saves back as a **new revision.**
- Export four ways: **Images & Documents wizard, Export Manager/OIEP, Asset Push, REST API.**
- **Image Conversion Configurations** (format/size/color) are reusable; **cache** conversions (Image Cache Event Processor) for performance; content can ship as **Binary (BASE64)** or **REST URL.**
- **Asset Push** distributes files to an external host via an **Event Queue + Configuration + Java Sidecar** (push from **Approved**).
- Store **externally** (**External DAM via URL** or **EFS via filename**) to keep the DB small — but it's **customer-managed and unsupported by Stibo.**

---
---

# MODULE 10 — Portals (Web UI)

> **Why this is here:** All previous modules used the power-user **Workbench**. Portals are the **friendly web interface** business users (and external suppliers) actually work in. Portals surface the data, workflows, and searches you've configured.

### Slides 1–2 — Template
Slide 1 design template; Slide 2 trainer "Attention" template. No Stibo content.

### Slide 3 — Module objectives
You'll learn to **create Web UI screens from design mode**, **configure workflow navigation** in the Web UI, and **configure searches/advanced searches** and other Web UI features.

### Slide 4 — Title slide
"Portals," STIBO CoE. No content.

### Slide 5 — Icons Used
A legend of presentation icons (Questions, Contacts, Reference, Demonstration, Hands-on Exercise, etc.). Trainer scaffolding, not Stibo content.

### Slide 6 — STEP Portals (why they exist)
**Main point:** Portals provide an **easy-to-use web interface** targeted at specific tasks and user groups.
- The **Workbench Java client** is often **too feature-rich** and its look/feel doesn't match normal-user expectations.
- Portals are **web-based** (no app download), each **configured to a specific business case.**
- **Long-term vision:** phase out the Workbench entirely, serving both normal users and admins via web portals.

### Slide 7 — Concept of STEP Portals
**Main point:** A **browser-based, highly configurable** framework (built on **Google Web Toolkit**) that lets customers build their **own tailored interfaces.**
- Large set of **standard portal components.**
- Can **tie in STEP Workflows.**
- Enables **internal and external** users (suppliers, vendors) to **onboard and maintain** data.
- Works on **Windows, Mac, iPad, iPhone**, and other mobile devices.

> 💡 **Term:** **Google Web Toolkit (GWT)** = a framework for building browser apps; you don't need to know GWT to *configure* portals.

### Slides 8–11 — Creating a Portal (Web UI) via Workbench
**The steps:**
- **(Slide 8)** In **System Setup**, right-click the **parent setup group** for Web UI configs → **New Setup Group** and name it. *Recommended:* put each Web UI in its own group so you can **limit user access** (important when many specialized Web UIs exist).
- **(Slide 9)** From the setup group, right-click → **New Web UI.** (If the option is missing, you're in the wrong setup group folder.)
- **(Slide 10)** In **Create New Web UI**, enter an **ID and Name** → **Create.** It then appears under the setup group and is editable in System Setup and accessible via a browser.
- **(Slide 11)** If **Default** is enabled on the **Configuration tab**, the Web UI is reachable via a **simpler URL** (no config ID needed) than non-default Web UIs.

### Slide 12 — Portal Structure
**Main point:** Access via the **Web Start page** or `http://[ServerURL]/portal/[UserID]UserPortal`; log in with normal credentials. Each portal = several **screens**, each built from **portal components.** Every portal has **3 "hardcoded" screens:**
- `---[MAIN]---`
- `---[HOMEPAGE]---`
- `---[LOGIN]---`

### Slide 13 — Portal Structure: Main
**Main point:** **Main** controls the optional **left side-navigation panel, header, footer, right-side objects**, and all **"global" configuration settings.**

### Slide 14 — Main (Side Panel)
**Main point:** The Main side panel typically holds **Tree browsing, search, navigation, and Workflow** work areas. Alternatively, that functionality can live in **Widgets on the Homepage** (Tree excluded).

### Slide 15 — Homepage
**Main point:** The **Homepage** is the **first page after login.** A Main side panel is **optional** alongside it. It can contain a **Widget Grid** holding various widget types.

### Slide 16 — Login
**Main point:** Besides basic login, the **Login screen** can hold a **locale selector** so users pick the **UI language.**

### Slide 17 — Custom Screens
**Main point:** **Custom screens** show details for selected objects, search results, task lists, etc. The side panel is **optional** (configured via Main). Example shown: a **Node Details Screen.**

### Slide 18 — Mappings (a key concept)
**Main point:** **Mappings** define **under which conditions a custom screen is displayed.** Configured via **Main**, on a **ForwardingSwitchScreen** component, or on **NodeList** components.

**Example mapping rules:**
- Show screen `SkuDetails` whenever a **product of type SKU** is selected.
- Show the **Enrich** screen when an object in the **Enrich state** of a Workflow is selected.
- Show `ClassificationDetails` whenever a **Classification** is selected.

**Critical behavior:** mapping rules are evaluated **in listed order**, and the **first match wins.**

> 📌 **Remember:** Order matters in mappings — put more specific rules **above** general ones.

### Slides 19–20 — The Portal Designer
**Main point:** Portals are maintained with the **"Portal Designer"** — a **WYSIWYG editor** that runs **inside the browser**, letting admins add/delete screens and add/delete/maintain component properties.
- Access it via **buttons in the Portal UI** (usually not present in production) **or** by appending **`?designmode=true`** (or `&`/`#`) to the URL.

> 💡 **Term:** **WYSIWYG** = "What You See Is What You Get" — you edit the page visually, as it will appear.

### Slide 21 — Portal Features: Children screen
A common feature: a **Children** screen lets you **view and edit child nodes** from a parent.

### Slides 22–23 — Multi Reference Editor
**Main point:** The **Multi Reference** component shows references with **multiple reference types and classification link types in one table.**
- Configurable with a list of reference/link types to **narrow** what's shown.
- Can show **forward references** or **reverse references** ("referenced-by" mode).
- Pre-configured with a **Node List in Multi Edit Display Mode** with **Add** and **Remove Reference** toolbar actions, letting users **link/unlink** objects from the Web UI. *(Slide 23 is a screenshot.)*

### Slides 24–26 — Advanced Search
**Main point:** **Advanced Search** lets users find data using **combinable criteria** with operators **And, Or, Not.**
- The **Advanced Search link** can be added to the homepage; the **criteria panel is configurable** so designers show only **job-relevant** criteria.
- **Example 1:** `Object type (Item) AND Attribute (Primary Color)=Almond` → items whose color is Almond. Multiple values can be searched at once; for LOV attributes, a dropdown gives the actual values.
- **(Slide 25) Example 2:** `[Item AND Primary Color=Almond] OR [Item AND Primary Color=Apricot]` → combines Almond items with Apricot items.
- **(Slide 26)** shows the **results** screen.

### Slides 27–28 — Workflows in Portals
- **(Slide 27)** The Portal framework is **tightly integrated** with Workflows. A portal can be **centered on a Workflow** (access objects only via **Tasks**), or Workflows can be **one entry point among others** (browse, search).
- **(Slide 28)** A special feature: create new objects via an **"InitiateItem"** screen. Such objects are **automatically started in a Workflow**, and — unlike normal creation — you can **set attribute values before the object is created.** The **StatusSelector** component controls whether the initiate option shows and which InitiateItem screen to use.

**Real-world use case.** A supplier portal where vendors click "Add New Product," fill a guided InitiateItem form, and the product is **born directly into the onboarding workflow.**

### Slide 29 — Portals and Privileges
**Main point:** The only special portal **Setup Action** is **"Update Web UI configuration"** (edit a config via XML/Designer).
- The privilege can be scoped to specific **Setup Groups** (so a user group edits one portal but not another).
- Privileges to **view a screen** can also be controlled via the **`<restrict>` tag** in the UI XML.

### Slide 30 — Localization (two kinds of language)
**Main point:** Distinguish **two language types** in portals:
- **Data language ("Context")** — names of STEP attributes/reference types **and** attribute values in different languages; defined **in STEP.**
- **Application language ("Locale")** — the **labels/titles within the portal**; translated by setting the title/label to a **translation key**, then adding that key to a **translation file** on the server (one file per language).
- End users can change **both** the **Application language (locale)** and the **Data language (context)** in the portal.

> 📌 **Two-axis localization:** **Context** = *what the data says* (translated values); **Locale** = *what the interface chrome says* (button labels). Ties straight back to **Dimensions/Contexts** from Module 1.

### Slide 31 — Thank You
Closing slide. No content.

---

### ✅ Module 10 Recap — Portals (Web UI)
- Portals = **configurable, browser-based** UIs (GWT) for task/role-specific work; the long-term replacement for the Workbench.
- Built from **screens** + **components**; 3 hardcoded screens: **MAIN, HOMEPAGE, LOGIN**; **Main** controls global chrome and the side panel.
- **Mappings** decide which **custom screen** shows for a given selection — **first matching rule wins.**
- Maintained in the **WYSIWYG Portal Designer** (`?designmode=true`).
- Key features: **Children** editor, **Multi Reference** editor, **Advanced Search** (And/Or/Not), and deep **Workflow** integration (including **InitiateItem** creation).
- Privileges via **"Update Web UI configuration"** + the **`<restrict>`** tag; localize on **two axes**: **Context** (data) and **Locale** (application labels).

---
---

# MODULE 11 — Tabular Format Import & Export

> **Why this is here:** This begins the **data-exchange cluster** (Modules 11–14). Tabular (Excel/CSV) is the **simplest, most common** way data enters and leaves STEP — the natural starting point before XML and integration endpoints.

### Slides 1–2 — Template
Slide 1 design template; Slide 2 trainer "Attention" template (mostly empty). No Stibo content.

### Slide 3 — Module objectives
You'll learn to **import and export** data using the **tabular (Excel/CSV)** method — the **steps to import** and the **steps to export.**

### Slide 4 — Title slide
"Tabular Format Import and Export," STIBO CoE. No content.

### Slide 5 — Tabular Format Imports (what you can create/update)
**Main point:** The **Import Manager** creates/updates these object types:
- **Products, Classifications, Entities, Attributes (objects/definitions),** and **Asset Metadata.**

> 📌 **Note:** tabular import handles **asset metadata**, not the binary file content itself (that's DAM territory — Module 9).

### Slide 6 — Tabular Import Basics
**Main point:** Out of the box, STEP only handles files where **objects are rows** and **properties are columns** (a normal spreadsheet shape).

**Visual model.** One row = one object; each column = one attribute/property to map into STEP.

### Slides 7–11 — Import Manager Wizard (the 8 steps)
- **Step 1 — Select Configuration:** use an **existing** Import Configuration or create a **new** one.
- **Step 2 — Select Data Source:** choose the source; if a **File**, browse and pick the load file.
- **Step 3 — Select Format:** choose the **file type** and basic file parameters (delimiter, encoding, header row, etc.).
- **Step 4 — Map Data:** map file **columns → STEP data.** You can map a **Constant** (fixed value), add **Transformations**, and use **variables.**
- **Step 5 — Identify Products:** see whether objects are **new or existing**; if the file lacks **STEP IDs**, identify existing objects by **attribute values.**
- **Step 6 — Identify Destination:** set a **default Object Type and parent** for new objects.
- **Step 7 — Select Business Rules:** pick **Business Conditions/Actions** to test/execute during import (covered in Module 4).
- **Step 8 — Advanced Settings:** e.g., **approve after import**, and **remove data for existing objects not in the import file.**

> ⚠️ **Powerful + dangerous (Step 8):** "remove data for existing objects not in the file" can wipe values en masse if the file is incomplete. Use deliberately.

> 💡 **Term:** A **Transformation** during mapping tweaks data on the way in (e.g., uppercase text, replace strings, convert units, prefix a value) without changing the source file.

### Slide 12 — Running the Import
**Main point:** After the wizard, a **"Save Import Configuration"** dialog lets you save the config for **re-use.** From there you can **start the Import Background Process**, then jump to the **Background Process object** in the Background Processes navigator.

### Slide 13 — Execution Report
**Main point:** Monitor the import via the **"Execution Report"** of the started **Background Process** (counts of created/updated/failed, error details).

### Slide 14 — Tabular Format Exports (what & features)
**Main point:** The **Export Manager** exports **Excel/CSV** for **Products, Classifications, Entities, Attributes, Asset Metadata.** Features:
- Multiple options for **selecting which objects** to export,
- Choose **exactly what data** to export per object and **transform** it,
- **Save an Export Configuration** for re-use.

### Slide 15 — Export Wizard (starting it)
Launch the Export Manager **two ways:**
- **Option 1:** from the **File menu.**
- **Option 2:** right-click a **hierarchy node → "Export Data Below."**

### Slide 16 — Export Wizard (configurations)
Step 2: **create or reuse** Export Configurations.

### Slide 17 — Export Wizard (selecting objects)
Export works on **all objects below and including** your selection. (If launched from a node's context menu, this step is **skipped**.)

### Slide 18 — Export Wizard (output format)
The **Select Format** step offers several output formats; this module covers **Excel and CSV.**

### Slide 19 — Export Wizard (mapping data → columns)
**Main point:** In **Map Data**, map STEP data to **output columns**, with manipulation options per part:
- Select a different **"Aspect,"**
- Map a **constant** value,
- Apply a **Transformation,**
- Map **additional STEP data** to either part.

> 💡 **Term:** An **Aspect** is a particular "view"/facet of a value (e.g., the value itself vs. its unit vs. a referenced object's name) you can choose to output.

### Slide 20 — Export Wizard (Advanced options)
- **Tag conversion** — convert STEP tags in values into other tag formats in the output.
- **Locale conversion from context** — convert dates/numbers per the **Context's locale.**
- **Resolve Inline References** — whether inline references are resolved.
- **Include Calculated Attribute Values** — whether calculated values are resolved during export.
- **Workspace / Context** — run the export from a **different Context/Workspace** than the one you started in.

### Slide 21 — Export Wizard (Delivery)
**Delivery options:**
- **File** (made available on the Export Background Process instance),
- **FTP / SFTP,**
- **Email,**
- **Server Side Delivery** (to a directory on the application server).

### Slide 22 — Running the Export
If **File** delivery was selected, the exported CSV/Excel is **available from the Background Process instance.**

### Slide 23 — Thank You
Closing slide. No content.

---

### ✅ Module 11 Recap — Tabular Import & Export
- Tabular = **Excel/CSV**, **rows = objects, columns = properties**; handles **Products, Classifications, Entities, Attributes, Asset Metadata.**
- **Import Manager (8 steps):** Configuration → Data Source → Format → **Map Data** (constants, transformations, variables) → Identify Products → Identify Destination → Business Rules → **Advanced** (approve-after-import; remove-missing-data ⚠️).
- **Export Manager:** select objects → format (Excel/CSV) → **Map Data** (Aspects, constants, transformations) → **Advanced** (tag/locale conversion, resolve inline refs, calculated values, alternate Context/Workspace) → **Delivery** (File/FTP/SFTP/Email/Server-side).
- Both run as **Background Processes** with **Execution Reports**; **configurations are reusable.**

---
---

# MODULE 12 — STEP XML

> **Why this is here:** STEP XML is STEP's **native** data format — *everything* in/out of STEP becomes STEP XML internally. It's the most complete format (data **and** configuration) and the backbone of system-to-system transfers.

### Slides 1–2 — Title + author
Slide 1 title ("STEP XML"); Slide 2 "About the Author." No content.

### Slide 3 — Introduction to STEP XML
**Main point:** **STEPXML is the native XML format** for STEP. Unlike other formats (limited to specific super/node types), STEPXML can import/export the **majority of STEP configuration and data objects.**
- Especially suited for transferring data/config between **DTAP** environments and for **inbound integrations** with systems/middleware that can produce STEPXML.
- **Crucial fact:** *all* data entering/exiting STEP via any inbound/outbound functionality **uses STEPXML** internally. (e.g., a CSV chosen for import is **converted to STEPXML** first, then imported.)

**Limitations:**
- **Historical data** (old revisions) can't be exported/imported.
- **Asset content** (binaries) can be **exported but not imported.**
- **Table data** can be **exported but not imported.**
- **Individual values** of existing multivalued attributes can't be exported/imported.
- Legal source/target object types for existing reference/link definitions can't be **removed or added.**
- Legal **units** for existing attributes **can't be removed.**

> 💡 **Term:** **DTAP** = Development, Testing, Acceptance, Production — the staged environments software moves through. STEPXML is how you migrate config/data between them.

### Slide 4 — General Steps to Export STEP XML
The Export Manager steps for STEP XML:
- **Select Configuration** — reuse a stored config or start new.
- **Select Objects** — pick hierarchy nodes (or modify a config's selection).
- **Select Format** — the delivery file format.
- **Map Data** — which info is extracted per object.
- **Advanced** — convert exported data to another output format.
- **Select Delivery Method** — how it's delivered.

### Slide 5 — Export: Select Configuration & Objects
**Main point:** STEP XML is exported via the **Export Manager** or an **OIEP.**
- The **Select Objects** step only lets you pick **Tree objects** and a **few** System Setup objects — yet **many** object types can be exported in STEP XML, so you **can run a STEP XML export with no objects selected at all.**
- To export specific **Product/Entity/Classification** branches, **select the root nodes** here.
- You must first **select or create a configuration.**

### Slide 6 — Export: Select Format
**Main point:** Two options: **"STEPXML"** and **"Advanced STEPXML."** Choosing **STEPXML** reveals a long list of dropdown options controlling exactly what data goes into the file, grouped into:
- **Global Settings** (apply to data **and** config objects),
- **Data Objects** (data-holding objects; common options first, similar ones grouped),
- **Configuration** options (alphabetical; apply to the labeled item),
- **Publishing** options (typically for **print** applications).

### Slide 7 — Export: Select Format (worked example)
**Main point:** To export a hierarchy **plus** referenced Products/Classifications/Assets, select **"Televisions"** as root with:
- **Include Products: Referenced** — selected product, its descendants, **and referenced products.**
- **Include Product Attribute Values: All** — to get **local** values out (inherited values **aren't** exported by default).
- **Include Assets: Minimum** — the **referenced** assets only.
- **Include Classifications: Minimum** — linked classifications **plus all ancestors** up to the top classification node (a special classification behavior).

### Slide 8 — Export: Nested vs. Flat
**Main point:** Products and Classifications export in **two nested structures** by default. To get a **flat structure** (no Product-inside-Product, no Classification-inside-Classification), set **"Flatten hierarchy: yes."**

### Slide 9 — Export: Map Data
**Main point:** **Map** the data to export (attributes, references, etc.) and apply **data transformation** if necessary.

### Slide 10 — Export: Advanced & Delivery
- **Advanced:** extra flexibility — **tag conversion, resolve inline references,** etc.
- **Delivery Method:** how the recipient wants the data delivered.

### Slide 11 — Where Export STEP XML is used
- In an **OIEP** to send data to a **downstream system,**
- In the **Export Manager** for **ad-hoc** exports.

### Slide 12 — STEP XML Example
**Main point:** A single Product of object type **SKU** (shown as `UserTypeID` in the XML), illustrating the building blocks: a **Linked Classification**, a **Referenced Asset**, and **Attributes** — all expressed as XML elements.

### Slide 13 — STEP XML Example (continued)
**Main point:** The XML can be **nested** (a Product inside a Product) **or** non-nested (flat). It can hold **multiple Products in a single XML**, including **referenced Products.**

### Slide 14 — Import STEP XML
**Main point:** STEP XML carries its own **processing instructions**, and **needs no mapping** — so there's **little to configure** in the Import Manager. Use STEP XML import for:
- **Object creation** (new Tree and System Setup objects),
- **Updates and deletions** of existing objects,
- **Deleting values and references/links,**
- **Deleting objects:** Products, Entities, Classifications, Assets, Attributes, LOVs, Units.

> 📌 **Contrast with tabular:** STEP XML is **self-describing** (no column-to-attribute mapping needed) and can **delete** objects/values — things tabular and Generic XML can't fully do.

### Slide 15 — Where Import STEP XML is used
- In an **IIEP** to receive data from a **source system,**
- In the **Import Manager** for **ad-hoc** imports.

### Slide 16 — Module completion slide
"You have successfully completed STEP XML." No content.

---

### ✅ Module 12 Recap — STEP XML
- The **native, most complete** format — handles **data AND configuration**, ideal for **DTAP** migration and integrations.
- **Everything** in/out of STEP becomes STEP XML internally (CSV is converted to it first).
- Export via **Export Manager / OIEP**; control content with rich **format options**; choose **nested vs. flat (Flatten hierarchy)**; **inherited values aren't exported by default.**
- Import is **self-describing (no mapping)** and uniquely supports **deletions** (objects, values, references).
- **Limits:** no historical data; asset content/table data **export-only**; some structural definitions can't change.

---
---

# MODULE 13 — Generic XML

> **Why this is here:** STEP XML (Module 12) is powerful but **rigid** — both sides must speak STEP's dialect. **Generic XML** lets STEP exchange data in **any XML shape** a partner uses, via a **template**.

### Slides 1–2 — Template
Slide 1 design template; Slide 2 trainer "Attention" template. No Stibo content.

### Slide 3 — Generic XML (what it is)
**Main point:** **Generic XML** lets STEP **import from and export to a variety of XML formats** **without extensions/customizations** — a widely accepted way to handle input/output. It has **inbound** (XML → STEP) and **outbound** (STEP → XML) options.

### Slide 4 — Limitations
- Only **Products, Entities, Classifications, Assets, and Attribute Definitions** can be **imported**; only **Products** can be **exported.**
- Cannot handle **nested records.**
- Currently **cannot delete** data or objects on import.

> 📌 **Trade-off vs. STEP XML:** Generic XML is **flexible on format** but **limited on scope** (fewer object types, no nesting, no deletes). STEP XML is the opposite.

### Slide 5 — Inbound Options (the idea)
**Main point:** On inbound, a **template with processing instructions** parses the XML and represents it in a **tabular form** that the **standard Import Manager** handles — just like a CSV/Excel import.

### Slide 6 — Inbound (sample source XML)
The slide shows a real product XML (`<ProductInformation>` with `<General>` fields like `ProductName`, `LongDescription`, repeating `<Variants>` of Name/Value pairs, and `<Manufacturer>`).

### Slide 7 — Inbound (the parsing template)
**Main point:** You provide a **template that mirrors the source** and inserts **processing instructions** where data should be captured, e.g.:
- `<ProductName><?Source Name?></ProductName>` — capture as the object **Name**,
- `<LongDescription><?Source?></LongDescription>` — capture a value,
- `<Variants><?Repeated?> … </Variants>` — handle a **repeating** element,
- `<Name><?SourceID?></Name>` — use as an **attribute ID.**

STEP then **matches the input XML against the sample** and decodes each value as defined.

### Slide 8 — Inbound (processing instructions)
A reference slide of the available **inbound processing instructions** (`<?Source?>`, `<?Source Name?>`, `<?SourceID?>`, `<?Repeated?>`, etc.). Based on how these appear in the sample, STEP **infers the input structure** and acts accordingly.

### Slide 9 — Outbound Options (the idea)
**Main point:** The outbound side is **symmetrical**: define a **template with placeholders**, then **map STEP data** into it — just like exporting CSV/Excel.

### Slide 10 — Outbound (processing instructions)
**Main point:** Outbound is **simpler** — only **four** processing instructions exist (shown in the slide's table), e.g., `<?Product?>`, `<?Target …?>`, `<?MultiTarget?>`.

### Slide 11 — Outbound (the export template)
The slide shows a template mirroring the same structure for export, with placeholders like `<ProductName><?Target Name?></ProductName>`, `<?MultiTarget?>` for repeating variants, etc.

### Slide 12 — Outbound (mapping)
**Main point:** With the template, the **Map Data** step of the Export Manager shows **placeholders to map into.** For repeating elements like `Variants`, **multiple attributes** are selected and mapped at once, then **transformations** output the attribute **name** and **value** in separate elements.

### Slide 13 — Outbound (result)
**Main point:** The output is a clean **Generic XML** matching the partner's expected structure (e.g., `FreeReturnFlag` transformed from `Y` to `Yes`). **Overall, both flows convert files based on a defined template** that STEP is configured to understand.

> 💡 **Big idea:** Generic XML = **"describe the partner's XML once as a template; STEP fills it in (export) or reads it out (import)."** Transformations bridge any value differences.

### Slide 14 — Thank You
Closing slide. No content.

---

### ✅ Module 13 Recap — Generic XML
- Exchange **any XML shape** without code, via a **template + processing instructions.**
- **Inbound:** template parses XML into a **tabular form** for the standard Import Manager (`<?Source?>`, `<?Source Name?>`, `<?SourceID?>`, `<?Repeated?>`).
- **Outbound:** template with **4 placeholders**; map STEP data in and use **transformations** to shape values.
- **Limits:** import = Products/Entities/Classifications/Assets/Attribute Definitions; **export = Products only**; **no nested records; no deletes.**

---
---

# MODULE 14 — Integration Endpoints (IIEP & OIEP)

> **Why this is here (the finale):** Endpoints are the **orchestration framework** that wraps everything in the data-exchange cluster — they schedule/trigger imports and exports, choose receivers/delivery methods, run **pre/post-processors** and **Business Rules**, and are how **most** data flows in and out of a real STEP system.

### Slides 1–2 — Template + title
Slide 1 design template; Slide 2 title ("Introduction to Integration End Points"). No Stibo content.

### Slide 3 — Module objectives
You'll become familiar with the concept of Integration Endpoints and be able to **create/configure IIEPs and OIEPs.**

### Slide 4 — Integration Endpoints (overview)
**Main point:** Integration Endpoints provide a **centralized interface for monitoring and maintaining integrations** with other systems. On a typical setup, **a large percentage of data** entering/leaving STEP goes through endpoints. Two kinds:
- **Inbound (IIEP)** — for systems **sending data to STEP** (files/messages).
- **Outbound (OIEP)** — think of it as **managing STEP's export** functionality; here **STEP is the data source** publishing to downstream systems.

### Slide 5 — Section divider: Inbound
Divider. No content.

### Slide 6 — Inbound Integration Endpoint (timing)
**Main point:** IIEPs support **"real-time" or "near-real-time"** integrations.
- They can **consume data at predefined intervals** (be **invoked**) — minimum interval **1 minute.**
- A **true real-time** alternative: when the data source is **REST**, a **POST invokes the endpoint** immediately.

### Slide 7 — IIEP Receiver Methods
**Main point:** Data can arrive via these **receiver methods:**

| Method | Description |
|---|---|
| **Amazon SQS** | Receives messages from Amazon Simple Queue Service. |
| **Hot Folder Receiver** | A standard data **hot folder** (drop files in, usually on the app server). |
| **JMS Receiver** | Consume/dequeue messages on a defined queue. |
| **Oracle AQ Receiver** | Oracle Advanced Queuing message exchange between systems. |
| **REST Receiver** | REST-based web-service intake. |
| **Web UI File Loading Receiver** | For the Web UI **"File Loading Widget"** (non-hot-folder receivers). |

> 💡 **Term:** A **hot folder** is a watched directory — drop a file in and the system automatically picks it up and processes it.

### Slide 8 — IIEP Plugins (three types)
**Main point:** The IIEP framework supports **3 plugin types:**
- **Pre-processor Plugin** — has access to the received file/message; can **convert it into a format the STEP Importer handles.**
- **Post-processor Plugin** — has access to **import events**; can **trigger system changes** based on them.
- **Error Reporter Plugin** — handles **error reporting.**

### Slide 9 — Pre/Post-Processor Details
**Pre-processing** (access to received files/messages; can manipulate or **discard** them) has **3 options:**
- **No pre-processing** (default),
- **XML Normalizer** — minor layout tweaks so STEP can process inbound XML via the **Generic XML** format,
- **XSLT** — transforms valid inbound XML into **STEPXML**, or into non-STEPXML importable via **Generic XML.**

**Post-processor** logic is implemented via **Business Rules** referenced from the **processing engine configuration.**

> 💡 **Term:** **XSLT** = a language for transforming one XML shape into another. **JMS** = Java Messaging Service (enterprise message queues). These are the plumbing standards endpoints can speak.

### Slide 10 — Overall Inbound Flow
A diagram slide summarizing the inbound pipeline: **Receiver → Pre-processor → Processing Engine (Importer) → Post-processor**, with **Error Reporter** alongside.

### Slide 11 — Section divider: Outbound
Divider. No content.

### Slide 12 — Outbound Integration Endpoints (selecting data)
**Main point:** On outbound, the data source is **STEP.** Two ways to choose what to export:
- **Event-Based Outbound** — publishes **incrementally** based on **events** (e.g., an object is **approved**). With the **"Event Queue Data Source"** option, the endpoint checks its **Event Queue** for unhandled events.
- **Select Objects Outbound** — publishes data from **selected hierarchies** on **scheduled intervals** (like the standard export).

> 💡 **Event-based vs. Select-objects:** event-based = "send changes as they happen" (efficient, incremental); select-objects = "send this whole branch on a schedule" (full snapshots).

### Slide 13 — Outbound Delivery Method (intro)
Compared with the standard Exporter, OIEPs offer a **different set of delivery options** (listed next).

### Slide 14 — Outbound Delivery Methods (the list)
Available OIEP delivery methods: **Amazon SQS, Copy to Directory, Email, FTP, GDSN Data Pool, IBM WebSphere MQ SSL, JDBC, JMS, Mongo, Oracle AQ, Product Data Syndication, REST, REST Direct, SFTP.**

> 💡 Notable ones: **JDBC** (write to a database), **Mongo** (a NoSQL database), **GDSN Data Pool / Product Data Syndication** (publish to retail data-sync networks).

### Slide 15 — Configure Pre/Post-Processor (Outbound)
The outbound side also supports **3 plugins:**
- **Pre-processor** — for **event-based** OIEPs, has access to generated **events** and can **filter** them / decide which objects pass to the Processing Engine.
- **Post-processor** — has access to the **output file**; can **manipulate or split** it into multiple files before delivery.
- **Error Reporter** — out-of-the-box **"Send Error Report"** plugin; custom ones can report errors.

### Slide 16 — Event Triggering Definitions (Event-Based OIEP)
**Main point:** These define **what changes (events) the OIEP monitors:**
- **Triggering Object** — which **object type(s)** are valid for this OIEP.
- **Triggering Attributes** — events register when a **triggering attribute value changes** on valid objects.
- **Triggering Table** — filter which **table types** register events when tables owned by triggering objects change.
- **Reference Type** — filter which **reference/link types** to listen to for changes.

**Real-world use case.** An OIEP that fires only when a Product's `Price` or `Status` attribute changes — so the webshop receives just the relevant updates.

### Slide 17 — Event-Based OIEP Queue Status
Two queue statuses:
- **Read Events** — the OIEP **registers events** as they occur (per its config and triggering definitions).
- **Discard Events** — **ignores** generated events matching the config. *(Useful to temporarily stop collecting.)*

### Slide 18 — Overall Outbound Flow
A diagram slide summarizing the outbound pipeline: **Event Queue / Selected Objects → Pre-processor → Processing Engine (Exporter) → Post-processor → Delivery.**

### Slide 19 — Status of an Integration Endpoint
Status indicators:
- **Enabled** — active, connected, running.
- **Disabled** — stopped; no data imported/published.
- **Failed** — an error caused the endpoint's background process to fail; **no data flows until resumed.**

### Slide 20 — Thank You
Closing slide. No content.

---

### ✅ Module 14 Recap — Integration Endpoints
- The **central framework** for most data in/out; **IIEP** (inbound) vs. **OIEP** (outbound, STEP is the source).
- **IIEP**: real-time via **REST POST** or scheduled (min **1 min**); **receivers** = SQS, **Hot Folder**, JMS, Oracle AQ, REST, Web UI File Loading; **pre-processors** (None / **XML Normalizer** / **XSLT**), **post-processors** (Business Rules), and **error reporters.**
- **OIEP**: **Event-Based** (incremental, via **Event Queue** + **triggering definitions**) or **Select Objects** (scheduled snapshots); many **delivery methods** (FTP/SFTP, Email, JDBC, REST, GDSN, etc.); same **3 plugin** types.
- Endpoint status: **Enabled / Disabled / Failed** (Failed halts flow until resumed).

---
---

# 🎓 MASTER SUMMARY — How the 14 Modules Fit Together

You've now walked through the whole STEP L1 curriculum. Before the takeaways and questions, here is the **big picture** — how every module connects into one coherent system. Read this section slowly; it's the "map" that makes everything click.

### The one-sentence version
**Stibo STEP is a single trusted home for a company's core data, where you (1) model the data, (2) identify it, (3) compute and govern it with rules and workflows, (4) clean and find it, (5) enrich it with assets and present it in screens, and (6) move it in and out through well-defined integrations.**

### The story, module by module

Think of STEP as a **factory for trustworthy data**, and the modules as stations on the line:

1. **Data Modeling** is the *blueprint of the factory*. Before anything else, you decide what kinds of things exist (objects, products, classifications, assets), what facts they carry (attributes), how they connect (references), and how the same fact can vary by market or language (dimensions). Everything downstream depends on this foundation.

2. **ID, URL & Key** are the *labels and barcodes*. Once you have objects, you must be able to point at exactly one of them — internally (ID), globally across systems (STEP URL), or by recognizable business values for external partners (Key).

3. **STEP Functions** are the *small calculators on the line*. They compute values on the fly (calculated attributes) using an Excel-like formula language — no storage, always current.

4. **Business Rules** are the *automation logic*. Conditions ask yes/no questions; Actions do work. They plug into imports, workflows, approvals, bulk updates and more — letting you encode policy ("if no image, block approval") without custom software.

5. **Workflows** are the *conveyor belts and stations*. They route an object through human and automated steps (Draft → Enrich → Review → Approve), assign work to people/groups, and enforce deadlines.

6. **Approvals, Revisions & Deletions** are *quality control and the audit log*. The Main↔Approved model separates messy work-in-progress from the clean, published truth; revisions are the snapshots that let you look back or revert; deletions are governed so nothing vanishes silently.

7. **Search, Collections & Bulk Updates** are *finding parts and fixing many at once*. Search locates objects; Collections gather them into reusable, hierarchy-independent baskets; Bulk Updates apply the same change to thousands of objects in one ordered, reportable run.

8. **Matching & Linking** is the *duplicate detector and the "golden record" press*. It finds records that represent the same real-world thing and either flags duplicates or fuses them into one trusted master using survivorship rules.

9. **Digital Asset Management** is the *parts that aren't text* — images, PDFs, videos. STEP stores them, auto-reads their metadata, converts/resizes them, and ships them out in several ways.

10. **Portals (Web UI)** are the *control panels operators actually touch*. Configurable browser screens (eventually replacing the Workbench) where business users search, edit, and run workflows without needing the thick client.

11–14. **Tabular, STEP XML, Generic XML & Integration Endpoints** are the *loading docks*. Tabular handles Excel/CSV; STEP XML is the native, most-complete format (data *and* configuration, ideal for migrating between environments); Generic XML adapts STEP to *any* XML shape a partner demands; and **Integration Endpoints (IIEP/OIEP)** is the overarching framework that orchestrates nearly all of this inbound and outbound traffic, in real time or on a schedule.

### The mental flow of a single product
To cement it, follow one product through STEP:

> A supplier file arrives → an **IIEP** (Integration Endpoint) receives it → an **Import** (Tabular or XML) maps it onto a **Product object** you defined in **Data Modeling**, identified by its **Key** → **Business Rules** validate it and **STEP Functions** compute derived fields → it enters a **Workflow** where a user attaches an **image (DAM)** and enriches localized values across **Dimensions** → **Matching** confirms it isn't a duplicate → a reviewer **Approves** it (creating a **Revision**) → it's added to a **Collection** for a seasonal push → an **OIEP** exports the **Approved** data as **STEP XML / Generic XML / a tabular feed** to the webshop, while business users manage exceptions through a **Portal**.

That single sentence touches **all 14 modules** — which is exactly why they were taught in this order.

---

# 🔑 KEY TAKEAWAYS (Consolidated Cheat-Sheet)

If you remember nothing else, remember these. They're the highest-value facts from each module — the kind that come up constantly in real work and in interviews.

### Foundations
- **Everything in STEP is an object** with three property types: **metadata (ID), attributes, and references.**
- **Object Type = the blueprint** (lives in **System Setup**); **instance = the real record** (lives in the **Tree**). Cookie-cutter vs. cookie.
- **Products inherit; Classifications do not.** Products live in a hierarchy (blue) where a child inherits attribute *links* and values from parents. Classifications (yellow) are for grouping/categorizing and pass nothing down.
- **Two attribute types:** **Specification** attributes attach to products and **inherit**; **Description** attributes can attach to *anything* and **do not inherit**.
- **References are owned by the source object.** The reference type defines what can link to what; deleting the source removes the reference.
- **Dimensions → Dimension Points → Contexts** let one attribute hold *different values* per market, language, or channel.

### Identity
- **ID:** immutable after creation, unique only **within its node/object type** (not globally).
- **STEP URL:** **globally unique**, used by the SOAP/API layer to address an object across systems.
- **Key:** identifies an object by its **attribute values** for external systems. Strict rules — the key attribute must be **externally maintained, single-valued, not dimension-dependent, not calculated, ≤1000 chars**, and keys activate only if **all values are unique.**

### Logic layer
- **Calculated attributes** are computed **on the fly and never stored** — always current, but heavy if they traverse many objects.
- **STEP Functions** = an **Excel-like** formula language; a Function used as a Business Condition returns **true via the string `"1"`.**
- **Business Rules = Conditions (test, no side effects) + Actions (do something).** Prefer **configuration over custom code**; implement via UI plugins, STEP Functions, or JavaScript (with Java API + binds).

### Process & governance
- **Workflows** = **states + transitions + events**; event execution order is **Conditions → On Exit → On Transition → On Entry.** Variables are **transient and per-instance**; deadlines need the **deadline-checker** background process.
- **Main vs. Approved:** Main is the **editable draft**; Approved is the **clean, published** copy. Approve **top-down**, and **targets before sources** (referenced objects before the objects pointing to them).
- **Revisions are snapshots** — there is **NO field-level change history**, and every revision is **tied to a user.** Revert from the Status tab.
- **Deletion is governed:** objects go to a **Recycle Bin**, and a deletion must itself be **approved** to be removed from the Approved workspace.

### Finding & fixing
- **Search:** `?` = single char, `*` = multiple; `ID=` and `Name=` prefixes target those fields. **Full Text Indexable** search is **word-level** and **doesn't support wildcards** (avoid leading `*`).
- **Collections** are **hierarchy-independent containers** shown as a flat list — great for working sets that cut across the tree. Importing into a collection needs **existing IDs.**
- **Bulk Updates** run **ordered operations** with **per-object rollback** but **NO global undo.** Schedule them with a **Collection + Configuration.**

### Mastering & enriching
- **Matching needs 4 things:** **Match Codes + a Matching Algorithm + an Event Processor + an Inbound Endpoint.**
- **Match Codes** are **sorted strings** built **most-significant-data-first**; **Window Size** caps how many neighbors get compared.
- **Match Actions:** **Identify Duplicates** (one threshold) vs. **Golden Records** (auto-merge threshold **plus** a clerical-review threshold that routes borderline cases to a review workflow). **Survivorship rules** (Trusted Source / Most Recent / mixes) decide which value wins.
- **DAM:** STEP **auto-recognizes MIME type**, stores the file as a **BLOB**, and reads metadata into **read-only System Properties.** Editing an asset creates a **new revision.** Assets export via the **Images & Documents wizard, Export/OIEP, Asset Push, or REST API.**

### Presentation & integration
- **Portals** are configurable **browser (GWT) screens** with **three hardcoded screens (MAIN / HOMEPAGE / LOGIN)**; **Mappings decide which custom screen loads (first match wins)**; design live with **`?designmode=true`.** Localization has **two axes: Context (data) vs. Locale (app labels).**
- **Tabular Import (Import Manager)** follows **8 steps**; beware **"remove missing data"** ⚠ and use **"approve after import"** deliberately. Both import and export run as **background processes with Execution Reports.**
- **STEP XML** is the **native, most-complete** format — carries **both data and configuration**, is the standard for **DTAP/environment migration**, **uniquely supports deletions on import**, and is **self-describing (no mapping needed).** Internally, *everything* (even CSV) is converted to STEP XML.
- **Generic XML** exchanges **any XML shape** via a **template + processing instructions** — but is limited (export **Products only**, **no nesting**, **no deletes**).
- **Integration Endpoints:** **IIEP = inbound** (real-time REST POST or scheduled, min **1 minute**); **OIEP = outbound** (STEP is the source; **Event-Based** incremental or **Select Objects** snapshot). Status is **Enabled / Disabled / Failed.**

> 💡 **The single most common interview trap:** *"Do classifications inherit like products?"* — **No.** Only the **product hierarchy** inherits. Say it with confidence.

---

# 📝 INTERVIEW & PRACTICE QUESTION BANK

Use this to test yourself. Each module has **conceptual questions** (definitions/theory) and **scenario questions** (applied thinking). Try to answer *before* reading the **▶ Answer** — that's where the learning happens. Answers are intentionally brief; expand them in your own words.

---

## Module 1 — Data Modeling

**Q1 (Concept).** What is an "object" in STEP, and what three kinds of properties can it hold?
> ▶ **Answer:** An object is any "thing" STEP models. Its properties are **metadata (e.g., ID), attributes (named values), and references (links to other objects).**

**Q2 (Concept).** Explain the difference between an Object Type and an instance, and where each lives.
> ▶ **Answer:** The **Object Type** is the blueprint/definition (in **System Setup**); an **instance** is an actual record built from it (in the **Tree**). Cookie-cutter vs. cookie.

**Q3 (Concept).** Which hierarchy supports inheritance — products or classifications — and what gets inherited?
> ▶ **Answer:** **Products** (the blue hierarchy). A child product inherits attribute **links and values** from its parents. **Classifications do not inherit.**

**Q4 (Concept).** Contrast Specification attributes and Description attributes.
> ▶ **Answer:** **Specification** attributes attach to **products** and **inherit** down the product tree. **Description** attributes can attach to **any object type** and **do not inherit.**

**Q5 (Concept).** Who "owns" a reference, and what does the reference type control?
> ▶ **Answer:** The **source object** owns the reference. The **reference type** defines which object types may be linked and the nature of the link; deleting the source removes the reference.

**Q6 (Concept).** Define Dimension, Dimension Point, and Context.
> ▶ **Answer:** A **Dimension** is an axis of variation (e.g., Language). A **Dimension Point** is a value on that axis (e.g., "French"). A **Context** is a combination of dimension points used to view/edit values for a specific situation (e.g., "French / Web").

**Q7 (Scenario).** A retailer sells a jacket in 4 colors and 3 sizes, each with its own barcode but sharing a description and brand. How would you model this so the shared data isn't typed 12 times?
> ▶ **Answer:** Model a **parent product** holding the shared attributes (description, brand) and create the 12 combinations as **variant products / children** that **inherit** the shared values, overriding only what differs (color, size, barcode).

**Q8 (Scenario).** Marketing needs the product name to differ between the US site and the German site. Which modeling feature handles this?
> ▶ **Answer:** **Dimensions** — specifically a Language/Market dimension. The Name attribute becomes dimension-dependent, holding different values per **Context.**

---

## Module 2 — ID, URL & Key

**Q1 (Concept).** Is an object's ID globally unique? Explain.
> ▶ **Answer:** No. An ID is unique only **within its node/object type**, and it is **immutable** once set. For global uniqueness you use the **STEP URL.**

**Q2 (Concept).** What is a STEP URL used for?
> ▶ **Answer:** It's the **globally unique** address of an object, used by the **API/SOAP** layer to reference an object unambiguously across systems.

**Q3 (Concept).** List the rules an attribute must satisfy to be used as a Key.
> ▶ **Answer:** It must be **externally maintained, single-valued, not dimension-dependent, not calculated, and ≤1000 characters.** Keys activate only if **all key values are unique.**

**Q4 (Scenario).** An external ERP recognizes products by their manufacturer part number, not by STEP's internal ID. How do you let the ERP find them?
> ▶ **Answer:** Configure a **Key** based on the manufacturer-part-number attribute (assuming it meets the key rules), so external systems can identify the object by that business value.

**Q5 (Scenario).** You try to activate a Key and STEP refuses. What's the most likely reason?
> ▶ **Answer:** The key attribute has **duplicate values** across objects (or it violates a key rule, e.g., it's multi-valued/calculated/dimension-dependent). Keys only activate when **all values are unique.**

---

## Module 3 — STEP Functions

**Q1 (Concept).** What is a calculated attribute, and what's its main trade-off?
> ▶ **Answer:** A value **computed on the fly** by a STEP Function and **never stored.** Trade-off: it's always current but can be **performance-heavy** if it traverses many objects.

**Q2 (Concept).** When a STEP Function is used as a Business Condition, how does it signal "true"?
> ▶ **Answer:** By returning the string **`"1"`.**

**Q3 (Concept).** Name a few common STEP Function building blocks.
> ▶ **Answer:** `value` / `simplevalue`, logical `if / and / or / not`, `exact`, and list operations like `list`, `iterate`, `listcontains`.

**Q4 (Scenario).** You need a "Display Price" that always equals base price × (1 + tax rate), reflecting any change instantly. Stored attribute or calculated? Why?
> ▶ **Answer:** **Calculated** — so it recomputes automatically whenever base price or tax rate changes, with no stale stored value to maintain.

---

## Module 4 — Business Rules

**Q1 (Concept).** Distinguish a Condition from an Action.
> ▶ **Answer:** A **Condition** tests something and returns **true/false** with **no side effects.** An **Action** actually **does something** (sets a value, sends data, etc.).

**Q2 (Concept).** Name several places (usages) where business rules can be attached.
> ▶ **Answer:** **Approvals, imports, IIEP/integration, workflows, bulk updates, and data profiles**, among others.

**Q3 (Concept).** What are the three main ways to implement a business rule, and which is preferred?
> ▶ **Answer:** **UI plugins, STEP Functions, and JavaScript** (Java API + binds). **Configuration is preferred over custom code** wherever possible.

**Q4 (Scenario).** Policy: a product cannot be approved unless it has at least one image. How would you enforce this?
> ▶ **Answer:** Attach a **Condition** to the **approval** usage that checks for a linked image; if false, **block approval** (optionally with an Action that messages the user).

---

## Module 5 — STEP Workflows

**Q1 (Concept).** What are the three core building blocks of a workflow?
> ▶ **Answer:** **States, transitions, and events.**

**Q2 (Concept).** What is the execution order of a workflow's events?
> ▶ **Answer:** **Conditions → On Exit → On Transition → On Entry.**

**Q3 (Concept).** What's special about Workflow Variables?
> ▶ **Answer:** They are **transient** (not permanently stored on the object) and exist **per workflow instance.**

**Q4 (Concept).** What do Cluster and Parallel states do?
> ▶ **Answer:** They **automatically split** an object into multiple concurrent paths and **merge** it back — enabling parallel processing within a workflow.

**Q5 (Concept).** What background process must run for workflow deadlines to fire?
> ▶ **Answer:** The **deadline-checker** background process.

**Q6 (Scenario).** New products must be enriched by a copywriter and, in parallel, have images attached by a designer; only when both finish does a manager review. How do you model this?
> ▶ **Answer:** Use a **Parallel/Cluster state** that splits into a "copywriting" branch and an "imaging" branch (assigned to the respective **groups**), then **merges** into a single "Manager Review" state.

**Q7 (Scenario).** Two users keep grabbing the same task. What workflow mechanic prevents the conflict?
> ▶ **Answer:** **Claim/Release** — a user **claims** a task (locking it to them) and **releases** it if they can't finish, so others don't double-handle it.

---

## Module 6 — Approvals, Revisions & Deletions

**Q1 (Concept).** Explain Main vs. Approved.
> ▶ **Answer:** **Main** is the **editable working/draft** copy; **Approved** is the **clean, published** copy that downstream systems consume. Approving copies Main into Approved.

**Q2 (Concept).** In what order do you approve referenced objects?
> ▶ **Answer:** **Targets before sources** — approve the objects being pointed to before the objects that reference them (and generally **top-down**).

**Q3 (Concept).** Do revisions store field-level change history?
> ▶ **Answer:** **No.** Revisions are **snapshots** of the object at points in time; there's no per-field audit trail. Each revision is **tied to a user.**

**Q4 (Concept).** How is deletion governed?
> ▶ **Answer:** Deleted objects go to a **Recycle Bin**, and the **deletion itself must be approved** to remove the object from the **Approved** workspace.

**Q5 (Concept).** What's the difference between workspace-revisable and globally revisable items?
> ▶ **Answer:** **Workspace-revisable** items (Products, Classifications, Assets, revisable Entities) have separate Main/Approved copies. **Globally revisable** items (much configuration) are revised globally rather than per-workspace.

**Q6 (Scenario).** A bad bulk edit corrupted 200 product descriptions yesterday. The data was approved last week. How do you recover?
> ▶ **Answer:** Use **Revisions** — revert the affected objects to the **prior revision/snapshot** (via the **Status tab**), restoring the last good state. (Note: you restore the snapshot, not individual fields, since there's no field-level history.)

**Q7 (Scenario).** Why might approving a product fail because of a "source/target" issue?
> ▶ **Answer:** The product **references** another object that **isn't approved yet.** You must **approve the target first**, then the source.

---

## Module 7 — Search, Collections & Bulk Updates

**Q1 (Concept).** What do the wildcards `?` and `*` mean in a STEP search?
> ▶ **Answer:** `?` matches a **single character**; `*` matches **multiple characters.**

**Q2 (Concept).** Why can't you use a leading `*` on a Full Text Indexable search?
> ▶ **Answer:** Full Text search is **word/token-level** and **doesn't support wildcards**; a leading `*` is especially problematic. Use it for whole-word matching, not pattern matching.

**Q3 (Concept).** What makes Collections different from the product hierarchy?
> ▶ **Answer:** Collections are **hierarchy-independent containers** displayed as a **flat list.** An object can be in many collections regardless of where it sits in the tree.

**Q4 (Concept).** Do Bulk Updates have an undo? What protection do they have?
> ▶ **Answer:** **No global undo.** They run **ordered operations** with **per-object rollback** (if one object's operation fails, that object rolls back), and they produce an **Execution Report.**

**Q5 (Scenario).** You must raise the price of 5,000 specific products by 10%, but they're scattered across the hierarchy. Outline the approach.
> ▶ **Answer:** **Search** (or import IDs) to find them → add them to a **Collection** → run a **Bulk Update** with a price-increase operation on that collection → review the **Execution Report.** Schedule it with a **Collection + Configuration** if needed.

**Q6 (Scenario).** Importing a list into a Collection fails because the objects "don't exist." Why?
> ▶ **Answer:** Importing **into a collection requires the objects to already exist** (you reference existing IDs); a collection import doesn't create new objects.

---

## Module 8 — Matching & Linking

**Q1 (Concept).** What four elements are required to perform matching in STEP?
> ▶ **Answer:** **Match Codes, a Matching Algorithm, an Event Processor, and an Inbound Endpoint.**

**Q2 (Concept).** How are Match Codes constructed, and what is Window Size?
> ▶ **Answer:** Match Codes are **sorted strings** built **most-significant-data-first.** **Window Size** limits how many neighboring records are compared to each other (controls performance vs. recall).

**Q3 (Concept).** Contrast the two Match Actions.
> ▶ **Answer:** **Identify Duplicates** uses a **single threshold** to flag likely duplicates. **Golden Records** uses **two thresholds** — an **auto-merge** threshold and a lower **clerical-review** threshold that routes borderline matches to a **review workflow.**

**Q4 (Concept).** What do Survivorship Rules decide, and name a couple of strategies.
> ▶ **Answer:** They decide **which value wins** when records merge. Strategies include **Trusted Source** (prefer a specific system), **Most Recent** (prefer newest), or a **mix** per attribute.

**Q5 (Scenario).** A customer is entered twice — "Bob Smith, 12 Main St" and "Robert Smith, 12 Main Street." How does STEP catch and resolve this?
> ▶ **Answer:** Match Codes + a fuzzy **Matching Algorithm** (e.g., Levenshtein/Multi-Word) score the pair highly; if above the **auto threshold** they merge into a **Golden Record** per **survivorship rules**; if in the **clerical-review** band, a steward reviews it in a workflow.

**Q6 (Scenario).** A person changed their surname after marriage, so their old and new records don't share a Match Code. How can matching still work?
> ▶ **Answer:** Configure **multiple Match Codes** (e.g., one keyed on other stable data like address/DOB), so "movers" or name-changers still collide on at least one code.

---

## Module 9 — Digital Asset Management (DAM)

**Q1 (Concept).** What happens automatically when you import an asset into STEP?
> ▶ **Answer:** STEP **auto-recognizes the MIME type**, stores the file as a **BLOB**, and extracts metadata into **read-only System Properties.**

**Q2 (Concept).** What happens when you edit an existing asset?
> ▶ **Answer:** STEP creates a **new revision** of the asset (the old version is retained as a prior revision).

**Q3 (Concept).** Name the ways assets can be exported from STEP.
> ▶ **Answer:** The **Images & Documents export wizard**, **Export Manager / OIEP**, **Asset Push**, and the **REST API.**

**Q4 (Concept).** What is an Image Conversion Configuration, and what speeds up repeated conversions?
> ▶ **Answer:** It defines on-the-fly transformations (resize/format/crop). The **Image Cache** (via the **Image Cache Event Processor**) stores generated renditions so they aren't recomputed every time.

**Q5 (Scenario).** The webshop needs 200×200 thumbnails and 1200px hero images from one master photo, without storing three copies manually. How?
> ▶ **Answer:** Keep one **master asset** and define **Image Conversion Configurations** for each size; STEP generates (and **caches**) the renditions on demand, exporting them via wizard/OIEP/REST as needed.

**Q6 (Scenario).** A company wants STEP to manage metadata but keep the heavy video files in their existing external DAM. What's the approach and the caveat?
> ▶ **Answer:** Store the asset **content externally** (External DAM via **URL**, or EFS via **filename**) while STEP holds the metadata. **Caveat:** these external-storage setups are **customer-managed and not supported by Stibo.**

---

## Module 10 — Portals (Web UI)

**Q1 (Concept).** What technology are Portals built on, and what are they expected to replace long-term?
> ▶ **Answer:** They're **browser-based (GWT)** screens, expected to **eventually replace the Workbench** thick client.

**Q2 (Concept).** Name the three hardcoded screens every Web UI has.
> ▶ **Answer:** **MAIN, HOMEPAGE, and LOGIN.**

**Q3 (Concept).** What do Mappings do, and what's the selection rule?
> ▶ **Answer:** Mappings decide **which custom screen loads** for a given object/situation; the rule is **first match wins.**

**Q4 (Concept).** How do you edit a Portal visually, and via which URL parameter?
> ▶ **Answer:** With the **WYSIWYG Portal Designer**, entered by appending **`?designmode=true`** to the URL.

**Q5 (Concept).** Explain the two localization axes in a Portal.
> ▶ **Answer:** **Context** localizes the **data** (which values you see, e.g., French product names); **Locale** localizes the **application labels/UI text** (buttons, menus).

**Q6 (Scenario).** Suppliers should see a stripped-down editing screen while internal staff see the full one. How is this controlled?
> ▶ **Answer:** Use **Mappings** to route each user/object to the right screen, and **privileges** (e.g., "Update Web UI configuration") plus the **`<restrict>`** tag to limit what each group can see/do.

---

## Module 11 — Tabular Import & Export

**Q1 (Concept).** In a tabular import, what do rows and columns represent?
> ▶ **Answer:** **Rows = objects** (records); **columns = properties** (attributes/fields).

**Q2 (Concept).** Roughly outline the Import Manager steps.
> ▶ **Answer:** **Configuration → Data Source → Format → Map Data (constants/transformations/variables) → Identify Products → Identify Destination → Business Rules → Advanced** (e.g., approve-after-import, remove-missing-data).

**Q3 (Concept).** Which Advanced option is dangerous and why?
> ▶ **Answer:** **"Remove missing data"** ⚠ — if a column is blank/absent, STEP can **wipe existing values**, causing accidental data loss.

**Q4 (Concept).** How do imports and exports run, and how do you check results?
> ▶ **Answer:** Both run as **background processes**; you review the **Execution Report** for successes/errors.

**Q5 (Scenario).** Marketing sends a spreadsheet updating only the "Color" of 1,000 products, but some rows leave Color blank meaning "no change." What must you avoid?
> ▶ **Answer:** Avoid **"remove missing data"** for that field, or the blanks will **erase** existing Color values instead of leaving them unchanged.

---

## Module 12 — STEP XML

**Q1 (Concept).** Why is STEP XML called the "native, most-complete" format?
> ▶ **Answer:** It can carry **both data and configuration**, represents the full object model, and is what STEP uses **internally** (even CSV is converted to STEP XML on import).

**Q2 (Concept).** What is STEP XML especially used for between environments?
> ▶ **Answer:** **DTAP migration** — moving data and configuration between **Dev → Test → Acceptance → Production** systems.

**Q3 (Concept).** What can STEP XML do on import that the other formats can't?
> ▶ **Answer:** It **uniquely supports deletions**, and it's **self-describing** (no mapping step needed).

**Q4 (Concept).** Are inherited values exported by default?
> ▶ **Answer:** **No** — inherited values are not exported by default (you export what's explicitly set, unless you choose otherwise).

**Q5 (Scenario).** You need to copy a newly built data model *and* sample products from the Test system to Production. Which format and why?
> ▶ **Answer:** **STEP XML**, because it carries **both configuration (the model) and data**, making it the standard tool for **environment migration.**

---

## Module 13 — Generic XML

**Q1 (Concept).** What problem does Generic XML solve?
> ▶ **Answer:** It lets STEP **import/export arbitrary XML shapes** that a partner requires, using a **template + processing instructions** to map between STEP and the foreign structure.

**Q2 (Concept).** Name the inbound processing instructions.
> ▶ **Answer:** `<?Source?>`, `<?Source Name?>`, `<?SourceID?>`, and `<?Repeated?>` — they turn the incoming XML into a **tabular form** the Import Manager can consume.

**Q3 (Concept).** What are Generic XML's key limitations?
> ▶ **Answer:** **Export is Products only**, there's **no nesting**, and it **doesn't support deletes.** (Import can handle Products/Entities/Classifications/Assets/Attribute Definitions.)

**Q4 (Scenario).** A marketplace demands a very specific custom XML layout for product feeds. STEP XML doesn't match it. What do you use?
> ▶ **Answer:** **Generic XML** outbound — build a **template** with placeholders/transformations that emits exactly the marketplace's required structure.

---

## Module 14 — Integration Endpoints

**Q1 (Concept).** Distinguish IIEP from OIEP.
> ▶ **Answer:** **IIEP = Inbound** Integration Endpoint (data **into** STEP). **OIEP = Outbound** (data **out of** STEP, where **STEP is the source**).

**Q2 (Concept).** What are the two ways an IIEP can run, and the minimum schedule interval?
> ▶ **Answer:** **Real-time** (via **REST POST**) or **scheduled**; the minimum scheduled interval is **1 minute.**

**Q3 (Concept).** What are the two OIEP modes?
> ▶ **Answer:** **Event-Based** (incremental, driven by an **Event Queue** + **triggering definitions**) and **Select Objects** (scheduled **snapshot** of chosen objects).

**Q4 (Concept).** What are the three endpoint statuses?
> ▶ **Answer:** **Enabled, Disabled, and Failed** (Failed halts data flow until resumed).

**Q5 (Concept).** What's the role of pre-processors and post-processors?
> ▶ **Answer:** **Pre-processors** prepare/normalize/filter data before the engine (e.g., **XML Normalizer, XSLT**, or event filtering); **post-processors** act after (often **Business Rules**, or splitting the output file).

**Q6 (Scenario).** The webshop should be notified within a minute whenever a product's price or status changes — but you don't want to resend the entire catalog each time. Which endpoint and mode?
> ▶ **Answer:** An **Event-Based OIEP** whose **triggering attributes** are Price and Status, so only the **changed objects** are published incrementally (near real-time).

---

## 🧩 Cross-Module Scenario Questions (Senior-level thinking)

These deliberately span several modules — exactly how real projects and tougher interviews work.

**CM-1.** *A supplier sends a daily CSV of 50,000 products. New ones must be created, existing ones updated, images attached, duplicates caught, and the clean result published to a webshop within minutes of approval. Walk through the STEP components involved.*
> ▶ **Answer:** **IIEP** receives the file → **Tabular Import (Import Manager)** maps it (carefully avoiding "remove missing data") onto **Product objects** identified by **Key** → **Business Rules/STEP Functions** validate and compute fields → a **Workflow** routes items for **DAM** image attachment and enrichment across **Dimensions** → **Matching** flags/merges duplicates (**Golden Records** + survivorship) → reviewer **Approves** (Main→Approved, creating a **Revision**) → an **Event-Based OIEP** publishes the **Approved** data (as **STEP XML / Generic XML / tabular**) to the webshop.

**CM-2.** *Why is it risky to point your outbound feed at the Main workspace instead of Approved?*
> ▶ **Answer:** **Main** holds **unfinished/unvalidated drafts.** Publishing from Main would push **incomplete or incorrect** data downstream; **Approved** is the governed, clean source meant for consumption.

**CM-3.** *You must migrate a brand-new configuration plus its data from Test to Production, then set up a recurring partner feed in a bespoke XML layout. Which two formats do you reach for, and why each?*
> ▶ **Answer:** **STEP XML** for the **migration** (carries both **config and data**), and **Generic XML** for the **partner feed** (emits an **arbitrary custom XML** shape STEP XML can't natively match).

**CM-4.** *A steward complains they can't see the change that broke a product last Tuesday at the field level. What do you explain, and what's the recovery path?*
> ▶ **Answer:** Explain that STEP **doesn't keep field-level history** — only **revision snapshots** tied to users. Recovery is to **revert to the prior revision** from the **Status tab** (snapshot-level, not field-level).

**CM-5.** *Performance is degrading. You discover a calculated attribute that traverses thousands of linked objects, evaluated on every screen load. What's the trade-off and a possible fix?*
> ▶ **Answer:** Calculated attributes are **always current but computed on the fly**, so heavy traversals are expensive. Options: **simplify the function**, reduce traversal scope, or switch to a **stored attribute** updated by a **business rule/workflow/bulk process** if real-time freshness isn't essential.

---

## 🎯 Quick self-rating

Rate yourself 1–5 on each module. Anything below a 4, reread that module's section and re-attempt its questions:

| Module | Topic | Your score (1–5) |
|---|---|---|
| 1 | Data Modeling | |
| 2 | ID, URL & Key | |
| 3 | STEP Functions | |
| 4 | Business Rules | |
| 5 | Workflows | |
| 6 | Approvals, Revisions & Deletions | |
| 7 | Search, Collections & Bulk Updates | |
| 8 | Matching & Linking | |
| 9 | Digital Asset Management | |
| 10 | Portals (Web UI) | |
| 11 | Tabular Import & Export | |
| 12 | STEP XML | |
| 13 | Generic XML | |
| 14 | Integration Endpoints | |

---

## 📌 Final word

You now have a complete, connected mental model of Stibo STEP at the L1 level: **model it → identify it → compute & govern it → clean & find it → enrich & present it → integrate it.** Keep the **Key Takeaways** cheat-sheet handy, run through the **question bank** until the answers feel automatic, and revisit the **master summary's "single product" walkthrough** whenever the pieces feel disconnected — it stitches all 14 modules into one story.

*Good luck — you've got this!* 🚀

*— End of guide —*
