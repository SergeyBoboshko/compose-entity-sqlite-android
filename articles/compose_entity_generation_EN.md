
# How Generation Works in Compose Entity (CE)

Imagine you want to create an Android application. Let's take a "Shop" app as an example.

Here is a list of tables (10 total) with their fields, fully aligned with CE capabilities — including references, documents, registers, and possible reports.

---

### 1. Product – Products  
**Fields:**  
- name – product name  
- sku – stock keeping unit (SKU)  
- price – price  
- unit – measurement unit (pcs, kg, etc.)  
- isActive – active or not  
**Purpose:** list of products sold or purchased.

### 2. Customer – Customers  
**Fields:**  
- name – customer name or company  
- phone – phone number  
- email – email address  
- discountPercent – discount percentage  
**Purpose:** regular buyers.

### 3. Supplier – Suppliers  
**Fields:**  
- name – supplier name  
- contactPerson – contact person  
- phone – phone number  
**Purpose:** who supplies products to the shop.

### 4. Invoice – Document "Sale to Customer"  
**Fields:**  
- date – sale date  
- customer – reference to customer  
- items – list of products (positions)  
**Purpose:** records sales of products to customers.

### 5. InvoiceItem – Sale Positions  
**Fields:**  
- invoiceId – reference to document  
- product – product  
- quantity – quantity  
- price – unit price  
**Purpose:** list of products in each sale.

### 6. Receipt – Document "Product Arrival"  
**Fields:**  
- date – date  
- supplier – supplier  
- items – list of positions  
**Purpose:** records receipt of products to the shop.

### 7. ReceiptItem – Arrival Positions  
**Fields:**  
- receiptId – reference to document  
- product – product  
- quantity – quantity  
- price – purchase price  
**Purpose:** what and how much was received.

### 8. StockRegister – Register "Product Stock"  
**Fields:**  
- product – product  
- warehouse – warehouse  
- quantity – stock amount  
**Purpose:** calculates product stocks by warehouses.

### 9. Warehouse – Warehouses  
**Fields:**  
- name – warehouse name  
- address – address  
**Purpose:** distribution of products by locations.

### 10. CashRegister – Register "Money"  
**Fields:**  
- date – date  
- customer – customer (if any)  
- supplier – supplier (if any)  
- income – income amount  
- outcome – expense amount  
**Purpose:** accounting of money operations.

---

This gives a great structure for comparison:

- how to do this manually (separate DAOs, ViewModels, UI forms, register update logic, etc.),
- and how CE takes just these 10 descriptions and creates everything automatically.

If needed, I can prepare a code lines comparison table or a modeled ER diagram.

---

You said:  
Now let's imagine how much code such an app would roughly require. We are not limited to CRUD operations only. Sorting, search, and master/detail relationships in documents are also needed.

ChatGPT responded:  
Great.  
Let's estimate approximately how many lines of code would be required to implement such an app manually, even without complex business logic — only standard functionality: CRUD, relations, filtering, sorting, UI.

---

## General structure of the "Shop" app without CE:

| Component                 | Count | Avg. Lines per Unit | Description                                   |
|---------------------------|-------|---------------------|-----------------------------------------------|
| Entity (tables)           | 10    | 30                  | fields, annotations, converters, relations    |
| DAO                       | 10    | 40                  | CRUD, sorting, search                          |
| ViewModel                 | 10    | 60                  | repositories, state, pagination                |
| Repository                | 10    | 50                  | DAO access with logic                          |
| UI – lists                | 10    | 80                  | forms, lists, sorting, search                  |
| UI – editing forms        | 10    | 100                 | validation, two-way binding, selects/dropdowns|
| Registers / postings      | 2     | 150                 | manual register updates on document posting   |
| Document/item relations   | 2     | 100                 | 1:N logic, nested lists, saving                |
| Services/interfaces/utils | ~     | 200+                | date formatting, conversions, dialogs          |

---

### Summary:

| Component                 | Lines of Code    |
|---------------------------|-----------------|
| Entity                    | 10 x 30 = 300   |
| DAO                       | 10 x 40 = 400   |
| ViewModel                 | 10 x 60 = 600   |
| Repository                | 10 x 50 = 500   |
| UI – lists                | 10 x 80 = 800   |
| UI – forms                | 10 x 100 = 1000 |
| Registers                 | 2 x 150 = 300   |
| Document/items relations  | 2 x 100 = 200   |
| Utility code              | 200+            |
| **Total**                 | **~4300–4500**  |

---
But our estimated total of 4500 lines of code is a very optimistic assessment. In real life, it is often much more. For example, my Addresses table with utility services in detailed records took almost 3000 lines of code, including the entire chain from entity to UI/UX
---

### Problems with manual implementation:

- Code duplication: DAO/ViewModel/Repo often repeat.
- Relations between tables created manually — especially hard in document items.
- Registers must be updated manually each time a document is saved.
- Lists and forms are largest in size due to all fields, validation, dropdowns, nullables, enums, etc.
- Search and sorting need to be implemented for each list separately.
- Testing and maintenance become costly when changing a single table.

---

## CE approach:

The same 10 tables are described in about 10–20 lines each (total approx. 150–200 lines), and CE generates:

- Room entities  
- DAO  
- ViewModel  
- Repository  
- UI list and form  
- Document posting logic  
- Register updates  
- Basic reports  

---

### Conclusion:

| Approach        | Lines of Code | Automation | Maintenance |
|-----------------|---------------|------------|-------------|
| Manual          | ~4500         | No         | Hard        |
| ComposeEntity   | ~200          | Yes        | Easy        |

---

### What CE generates and what the programmer writes?

The programmer describes entities as done in Room but does not create DB and dependencies. CE handles this. CE also generates Ext class, DAO, Repository, ViewModel, and UI including all CRUD operations, list sorting, navigation between forms, detailed records (table parts) for dependent tables, selection from dependent objects on forms, and a professional typical UI/UX look.

The programmer writes only the entity (table in DB) and the entry point from a menu or page to the generated list/edit/view UI form.

---

CE has rules for naming generated objects based on the entity's name.

Example code:

```kotlin
@CeGenerator(
  type = GeneratorType.Reference,
  label = "Products",
  generationLevel = GenerationLevel.UI,
  ...
)
@Parcelize
@Entity(tableName = "ref_products")
//@CeMigrationEntity(1)
data class RefProducts(
  @PrimaryKey(autoGenerate = true)
  override var id: Long,

  ...
) : CommonReferenceEntity(id, date, name, isMarkedForDeletion), Parcelable {
  override fun toString(): String {
    return "$id: $name"
  }
}
```

After building the project, you get a full professional form for this entity. No more code, just field descriptions instead of "...".

CE generates service classes for this entity:

- RefProductsExt  
- RefProductsDao  
- RefProductsRepository  
- RefProductsViewModel  
- RefProductsUI  

You can always get a ViewModel instance from the special global object `AppGlobalCE`. For example, in this case it is `AppGlobalCE.refProductsViewModel`. You can also easily access the DAO object via `AppGlobalCE.refProductsViewModel.repository.dao`. If you create a UI object, it already has a `viewModel` property pointing to the same ViewModel as `AppGlobalCE`: `RefProductsUI().viewModel.repository.dao` — access whatever you want!

---

### Will all these objects be created just by writing the code above?

If you ask this question, you are a good programmer on the right path. Of course not! All these objects, including `AppGlobalCE`, must be generated by KSP, so they do not exist initially, but will appear after you run Clean & Make on the project.

Some tips to remember:

- CE-generated objects are available only after building the project.
- Running only Clean removes generated classes and objects like `AppGlobalCE` or `RefProductsUI` — this is normal; running Make brings them back.
- If you see errors about missing `AppGlobalCE` objects and you did nothing, or your CE classes like `RefProductsRepository` are missing, this might be an Android Studio or KSP glitch — just run Clean & Make again.
- If the above does not help, in the project root console run `/gradlew --stop` then `/gradlew --daemon`, then you can safely run or build the project. This is a known Android Studio problem where it cannot delete generated jars or resources because the daemon locked some files or folders.

---

A normal programmer will then ask: "What is an Ext class? What do generated objects do? What benefits do I get from them? What else is useful in CE?"

Actually, there is a lot of useful stuff, and answers exist for all these questions, but if you read this far, you might be tired — we will cover these later, stay tuned to the blog!

---

### Can I take the automatically generated code and extend it manually?

Yes, you can take the generated code from the `generated` directory, copy it to your own `.kt` file, and extend it there. You must change the generation level in the annotation to match the copied object's level. Also, copy all dependent objects that come after in the list. For example,
