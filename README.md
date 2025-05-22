# ComposeEntity: The Easiest Way to Build Android Apps with SQLite Forms

**ComposeEntity** is a free Kotlin library for Android that lets you build full-featured apps with **SQLite**, dozens of tables, and auto-generated forms — with almost no boilerplate.

🚀 **Perfect for indie developers and small teams**: all you need is **Android Studio** + **Kotlin** — no Firebase, no backend, no monthly fees.

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

Create your entities, and Compose Entity will handle everything. Just to compare the volume of code and result. We create appication with one reference anf full CRUD operation:

'''Kotlin
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

): CommonReferenceEntity(id,date,name,isMarkedForDeletion), Parcelable{
    override fun toString(): String {
        return "$id: $name"
    }
}```

![image](https://github.com/user-attachments/assets/38aac061-1180-4841-87d1-09ef9cfb65a8)
![image](https://github.com/user-attachments/assets/6bbd9e59-dd71-4b48-8dd8-7db3e3f22908)

And result of this code example on pictures. The fields id and name are presenting on the form by standart way for all of references:

CE_Example 1 CE_Example 2

Run the Project 🚀
Your UI and database are automatically generated, and you can start using the app immediately.

📝 Customization
You can extend the default setup by:

Adding custom UI elements using customComposable.
Modifying form layouts for better UX.
Implementing custom save logic within ViewModels.
📜 License
This project is licensed under the MIT License.
