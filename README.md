# CE (ComposeEntity): The Easiest Way to Build Android Apps with SQLite Forms !
<table>
    <tr>
        <td><img src="https://github.com/user-attachments/assets/48b44bd1-de84-4468-9d30-d7423867dec0"/></td>
        <td><b>CE ComposeEntity</b> is a free Kotlin library for Android that lets you build full-featured apps with **SQLite**, dozens of tables, and auto-generated forms — with almost no boilerplate.</td>
    </tr>
</table>


🚀 **Perfect for indie developers and small teams**: all you need is **Android Studio** + **Kotlin** — no Firebase, no backend, no monthly fees.

---
[We are strongly recomending creating THE NEW PROJECT with compose entity by this page->](https://cetempl.homeclub.top/)
---

## ✨ Why Use ComposeEntity?

- ✅ Define only your entities — the forms and ViewModels are generated automatically  
- ✅ Works entirely offline with **SQLite**  
- ✅ No XML, no manual migration logic  
- ✅ Auto-forms with CRUD, navigation, and reports  
- ✅ Extensible with custom UI  
- ✅ Fully free and open for use  

**ComposeEntity** is a Kotlin-based library that automatically generates database logic and UI forms for Android apps using **Jetpack Compose** and **Room**.

With just your entity classes, you can get:
- A working database (based on Room),
- ViewModels and repositories,
- And fully functional CRUD **forms with Jetpack Compose**.

No XML. No manual DAO. No hand-coded ViewModel logic.  
Just define your data model — ComposeEntity does the rest.

> ❓ Hesitant to start with Compose Entity? You're not alone. Many developers are cautious about code-generation tools because of the fear of black boxes or losing control.  
> [Why Compose Entity is different — and why you don’t need to be afraid](./whynoafraid.md)


---

## ⚡ Who Is It For?

This tool is ideal for:
- Android developers building apps with **many tables and forms**
- Anyone wanting to prototype **admin panels**, **databases**, or **offline tools**
- Kotlin devs who want to avoid writing boilerplate CRUD logic

---

## 🚀 Key Features

✅ **Auto-Generated Forms**  
Define your entity once — the UI is built for you.

✅ **SQLite + Room Integration**  
You get all Room features, without writing any DAOs.

✅ **KSP-powered**  
Uses Kotlin Symbol Processing to generate code at compile time.

✅ **Full MVVM structure**  
Repositories and ViewModels are generated automatically.

✅ **Free & Works Offline**  
No Firebase, no cloud backend — just Android Studio + Kotlin.

---

## 🧰 Requirements

- Android Studio Giraffe or newer  
- Kotlin 1.9+  
- Jetpack Compose  
- No backend or internet connection needed  

Create your entities, and ComposeEntity will handle everything. Just to compare the volume of code and result. We create application with one reference and full CRUD operation:

```kotlin
@ObjectGeneratorCE(type = GeneratorType.Reference
    , label = "The Meter Zones")
@Parcelize
@Entity(tableName="ref_meterzones")
data class RefMeterZones(
    @PrimaryKey(autoGenerate = true)
    override var id: Long,
    override var date: Long,
    override var name: String,
    override var isMarkedForDeletion: Boolean

): CommonReferenceEntity(id, date, name, isMarkedForDeletion), Parcelable {
    override fun toString(): String {
        return "$id: $name"
    }
}
```

![image](https://github.com/user-attachments/assets/38aac061-1180-4841-87d1-09ef9cfb65a8)  
![image](https://github.com/user-attachments/assets/6bbd9e59-dd71-4b48-8dd8-7db3e3f22908)

The fields `id` and `name` are presented on the form in a standard way for all references.

---

## ▶️ Run the Project

Your UI and database are automatically generated, and you can start using the app immediately.

---

## 📝 Customization

You can extend the default setup by:
- Adding **custom UI elements** using `customComposable`
- Modifying **form layouts** for better UX
- Implementing **custom save logic** within ViewModels

---

## 🧠 Full Control When You Need It

One of the biggest concerns developers have when adopting any framework is:

> **“Will I lose control over my code?”**

With **ComposeEntity**, the answer is:  
**No — you keep full control. Always.**

### 🔧 You Can Choose What Gets Generated

ComposeEntity lets you selectively enable or disable:
- UI generation
- ViewModel generation
- Repository generation

If needed, you can even:
- Copy the generated code (from `build/generated/...`) into your project
- Customize or completely rewrite any part

### 🎯 Fine-Grained Customization

You can:
- Inject custom Composables into any form
- Override field rendering, layout, or input behavior
- Intercept lifecycle events like `onSave`, `onDelete`, or `onFieldChange` via the ViewModel

### ✅ You Are Always In Charge

Even though ComposeEntity generates a lot of code for you, nothing is hidden:
- All generated code is readable and well-structured
- You can explore, copy, and modify it anytime
- ComposeEntity respects your overrides — if you define a ViewModel, it won’t generate one

> ComposeEntity automates the boring parts,  
> but leaves **you in control of everything that matters**.


---
## 🧪 Try It Out: Sample Projects

To get started quickly, you can clone one of the ready-to-run demo projects:

- 🧱 **Basic Starter Template**  
  Minimal example with one entity and auto-generated form:  
  👉 [ComposeEntitySample](https://github.com/SergeyBoboshko/ComposeEntitySample)

- 📚 **Full-Scale Example: Utility Payment Book**  
  A complete app that demonstrates a real-world use case with many directories, documents, registers, reports and dozens of tables:  
  👉 [CePowerPaymentBook](https://github.com/SergeyBoboshko/CePowerPaymentBook)

These projects show how ComposeEntity handles everything from simple CRUD to complex UI and navigation.

---

- [What's new in Compose Entity (KSP)](https://www.homeclub.top/?p=1115)
    
- [What newest version of Compose Entity is?](https://www.homeclub.top/?p=1036)
    
---

## More Examples And Tutorials About ComposeEntity and ComposeEntity KSP

- [Compose Entity KSP Manual Pages](https://wool-fontina-39f.notion.site/Compose-Entity-KSP-1bbac9e714318004866fd9fd627a25e1)

- [Compose Entity KSP my Blog](https://www.homeclub.top/?cat=51)

- [Compose Entity my Blog](https://www.homeclub.top/?cat=50)

- [ComposeEntity and ComposeEntity KSP Youtube Project](https://www.youtube.com/@ComposeEntity)

---
## [Local Manuals](/local-manuals.md)
---

[Check out this video on this topic](https://youtu.be/SY90XoTxYuQ)

## 📜 License

This project is licensed under the **MIT License**.
