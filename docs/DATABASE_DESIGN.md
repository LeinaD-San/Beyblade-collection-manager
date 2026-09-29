# Database Design

## Main Entities

### Product
Represents an official Beyblade product or release.

Examples:
- BX-00 Cobalt Drake 4-60F
- BX-01 Dran Sword 3-60F

A product can contain one or more Beyblades, parts, or accessories.

---

### Part
Represents an individual Beyblade component.

Part types may include:
- Blade
- Ratchet
- Bit
- CX Lock Chip
- CX Main Blade
- CX Assist Blade

Each part may have multiple color or release variants.

---

### Product Contents
Connects a product to the parts included with it.

Example:

Cobalt Drake 4-60F contains:
- Cobalt Drake Blade
- 4-60 Ratchet
- Flat Bit

---

### Collection Item
Represents a product that the user personally owns.

Stores information such as:
- Quantity
- Condition
- Purchase date
- Purchase price
- Notes

---

### Owned Part
Represents individual parts the user owns.

This allows the app to know how many copies of a Blade, Ratchet, or Bit are available for custom combinations.

---

### Custom Combo
Represents a Beyblade combination created by the user.

Example:

Cobalt Drake
+
3-60
+
Flat

---

### Compatibility Rule
Stores special compatibility rules between parts.

Examples:
- Compatible
- Incompatible
- Unverified

This will support BX, UX, CX, and special part architectures.


## Entity Relationships

### Product → Product Contents
Relationship: One-to-Many

One product can contain multiple items.

Example:

BX-00 Cobalt Drake 4-60F
- Cobalt Drake Blade
- 4-60 Ratchet
- Flat Bit

---

### Part → Product Contents
Relationship: One-to-Many

The same part can appear in multiple products.

Example:

The Flat Bit may appear in multiple different releases.

---

### Product → Collection Item
Relationship: One-to-Many

A user may own multiple copies of the same product.

Example:

Cobalt Drake 4-60F
- Copy 1
- Copy 2

---

### Part → Owned Part
Relationship: One-to-Many

A user may own multiple copies of the same part.

Example:

4-60 Ratchet
- Red version
- Blue version
- Another duplicate

---

### Custom Combo → Parts
Relationship: Many-to-One per slot

Each saved combo references:
- one Blade
- one Ratchet
- one Bit

Future CX combinations may reference:
- one Lock Chip
- one Main Blade
- one Assist Blade
- one Ratchet
- one Bit

---

### Part → Compatibility Rule
Relationship: Many-to-Many

A part may have compatibility rules with many other parts.

Example:

Part A
→ compatible with Part B

Part A
→ incompatible with Part C

Part A
→ unverified with Part D


Product
   |
   v
Product Contents
   |
   v
Part

Product
   |
   v
Collection Item

Part
   |
   v
Owned Part

Owned Parts
   |
   v
Custom Combo

Part <----> Compatibility Rule <----> Part



## Initial Table Design

### products
Stores official Beyblade products.

- id
- product_code
- name
- product_line
- manufacturer
- region
- release_type
- release_date
- verification_status
- catalog_source

---

### parts
Stores reusable Beyblade components.

- id
- name
- part_type
- part_code
- product_line
- connection_standard
- description

---

### part_variants
Stores color or release variations of a part.

- id
- part_id
- color
- variant_name
- image_path
- model_path

---

### product_contents
Connects official products to the parts they contain.

- id
- product_id
- part_variant_id
- quantity

---

### collection_items
Stores products personally owned by the user.

- id
- product_id
- quantity
- condition
- purchase_date
- purchase_price
- notes

---

### owned_parts
Tracks individual parts available in the user's collection.

- id
- part_variant_id
- quantity
- source_product_id
- condition
- notes

---

### custom_combos
Stores custom Beyblade builds.

- id
- name
- blade_part_id
- ratchet_part_id
- bit_part_id
- created_at
- notes

---

### compatibility_rules
Stores special compatibility restrictions.

- id
- part_a_id
- part_b_id
- status
- reason
- source
- last_verified