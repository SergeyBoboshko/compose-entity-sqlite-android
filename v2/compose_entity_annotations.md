## Changes in Annotations

### 1. `@Entity` → `@CeEntity`
```kotlin
@CeEntity(tableName = "person")
```
- Replaces Room's `@Entity`.
- **Does not** create a table in the database automatically like Room does.  
- Used to mark a class as an entity for Compose Entity code generation.

---

### 2. `@CeCreateTable`
```kotlin
@CeCreateTable(tableName = "person")
```
- Independent of `@CeEntity`.  
- Creates a table in the `onCreate` section of `SQLiteHelper`.  
- If linked to the same entity as `@CeEntity`, ensure `tableName` values match in both annotations.  
- Can be used for manually created tables — in that case, `@CeEntity` is not required.

---

### 3. `@CeMigration`
```kotlin
@CeMigration(tableName = "person", version = 2)
```
- Creates a table in the `onUpdate` section for the specified DB version.  
- You may either:
  - create tables manually as usual, or
  - annotate the corresponding entity with `@CeMigration`.

---

### 4. `@PrimaryKey` and Cascade Delete
- No longer required for `id` fields or for cascade delete on `parentId`.  
- Compose Entity automatically adds these SQL expressions when generating the table.  
- **Important:** The field names must be exactly `id` and `parentId` to be recognized as primary key or parent reference in detail tables.

---

## Example

The following example will:
- Create the `groupe` table in SQLite
- Generate DAO, repository, ViewModel
- Generate fully functional UI forms with navigation for a "Group" reference table in your app

```kotlin
package io.github.sergeyboboshko.cereport.references

import io.github.sergeyboboshko.composeentity.daemons.FieldTypeHelper
import io.github.sergeyboboshko.composeentity.references.base.CommonReferenceEntity
import io.github.sergeyboboshko.composeentity_ksp.base.CeCreateTable
import io.github.sergeyboboshko.composeentity_ksp.base.CeEntity
import io.github.sergeyboboshko.composeentity_ksp.base.CeField
import io.github.sergeyboboshko.composeentity_ksp.base.CeGenerator
import io.github.sergeyboboshko.composeentity_ksp.base.GeneratorType
import io.github.sergeyboboshko.composeentity_ksp.entity.GenerationLevel

@CeEntity(tableName = "groupe")
@CeGenerator(type = GeneratorType.Reference, generationLevel = GenerationLevel.UI)
@CeCreateTable(tableName = "groupe")
data class RefGroupes(
    override var id: Long,
    override var date: Long,
    @CeField(type = FieldTypeHelper.TEXT, label = "name")
    override var name: String,
    override var isMarkedForDeletion: Boolean
): CommonReferenceEntity(id, date, name, isMarkedForDeletion) {
    override fun toString(): String {
        return "$id: $name"
    }
}
```

---

**Note:**  
Version 2 requires **at least one table** in the database created using Compose Entity annotations.  
That’s why the example already includes reference tables.  
In future releases, this limitation will be removed, though Compose Entity is designed primarily for applications working with databases.
