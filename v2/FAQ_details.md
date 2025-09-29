# ComposeEntity FAQ

This page contains answers to common questions and pitfalls you may encounter when working with ComposeEntity.

---

<details>
<summary>❓ Why doesn’t a related field (`related` / `SELECT`) refresh in the form until I restart the app?</summary>

**Reason:**  
The entity is defined as a `data class`.  

In Kotlin, a `data class` automatically generates `equals()` and `hashCode()` methods that compare **all fields**.  
If the data in the table or `Flow`/`LiveData` looks the same "by equality," the UI assumes nothing has changed, even if the object reference is new.  

**Solution:**  
Use a **regular `class`** for entities (as shown in the official ComposeEntity examples).  
With `class`, equality is based on reference (`===`), so the UI will always react to updates.

```kotlin
// ❌ Avoid this
data class DetailsTariffRegistry(
    override var id: Long,
    override var parentId: Long,
    ...
) : CommonDetailsEntity(id, parentId)

// ✅ Correct way
class DetailsTariffRegistry(
    override var id: Long,
    override var parentId: Long,
    ...
) : CommonDetailsEntity(id, parentId)
```

**When is it safe to use `data class`?**  
- If the entity **has no related fields (`related`)** and is only used for serialization/storage.  
- If you **manually handle refreshing** and do not rely on automatic `refreshAllExt`.  

In all other cases, for reliable behavior, prefer `class`.  

</details>

---

<details>
<summary>❓ I created an entity but I don’t see the UI class for this entity</summary>

Elements like ext class, DAO, repository, ViewModel, and UI for the entity are generated via KSP generation.  
If you performed `clean` or `clean + make` but there were errors and `make` did not complete, these objects might have been removed.  
Simply rebuild the project, and all objects will be restored.  
To ensure these objects are generated and everything works smoothly, always rebuild the project after adding a new entity object

</details>

---
<details>
<summary>❓ Why should I explicitly declare the `conditions` field in a report entity, even if it’s already in the base class?</summary>

**Reason:**  
KSP processes only the properties **declared directly in the entity class**.  
Inherited fields from base classes (like `conditions`, `groups`, or `resources`) are **not automatically detected** during code generation.  

If you rely on inheritance and skip redeclaring `conditions`, the code generator will:
- ❌ not include it in the table schema (`CREATE TABLE`),  
- ❌ not handle it during migrations,  
- ⚠️ cause inserted data to be ignored because the column does not exist.

**Solution:**  
Always explicitly declare the `conditions` field in every report entity, even if it’s inherited from `ReportEntity`.

```kotlin
// ❌ Avoid this
data class ReportUtilityPaymentsFreeEntity(
    override var id: Long,
    override var name: String,
    override var describe: String,
    var addressId: Long,
    var amount: Double
) : ReportEntity(id, "addressId", "amount", name, describe)

// ✅ Correct way
data class ReportUtilityPaymentsFreeEntity(
    override var id: Long,
    override var name: String,
    override var describe: String,
    var addressId: Long,
    var amount: Double,
    // 👇 Explicitly redeclare the field
    override var conditions: String = ""
) : ReportEntity(id, "addressId", "amount", name, describe, conditions)
When is redeclaration required?

✅ When the field must exist in the database schema.

✅ When the field participates in migrations or is saved via insert().

🚫 You may skip it only if the field is not stored in the database and used purely in logic.

</details> ```
---

📌 **More questions will be added to this FAQ as the project evolves.**
