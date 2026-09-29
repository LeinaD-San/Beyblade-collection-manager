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