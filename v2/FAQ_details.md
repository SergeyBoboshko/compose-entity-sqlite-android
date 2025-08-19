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

📌 **More questions will be added to this FAQ as the project evolves.**
