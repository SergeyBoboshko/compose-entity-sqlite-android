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

📌 **More questions will be added to this FAQ as the project evolves.**
