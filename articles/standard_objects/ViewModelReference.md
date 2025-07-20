# 📦 Base ViewModel Fields and Functions in Compose Entity

In Compose Entity, objects such as directories, documents, registers, and reports are implemented to give the programmer more than just database tables. These are real-world objects expressed in the infological model, automatically transformed into the information model.

Each object is served by a corresponding **ViewModel**, typically derived from `_BaseFormVM`. Most of the functionality is shared across object types and is implemented in this base ViewModel.

In a typical Compose UI, the ViewModel is always located in the `viewModel` field of the form.

---

## 🧩 Common Fields of the ViewModel

These are the fields you’ll most often interact with:

### `var anyItem: Any`
Holds the current `EntityExt` object being viewed or edited. Not reactive. Even on list or creation forms, it contains the last viewed/edited item.

📌 Example:
```kotlin
val currentDoc = vm.anyItem as DocUtilityChargeExt
```

The `Ext` version always contains a `.link` to the original Room entity.

---

### `getField(fieldName: String): String`
Returns the string representation of a field value on the form. Only makes sense during add/edit forms.

- If the field is a reference — returns the ID.
- If it's a date or datetime — returns the value in milliseconds.
- If the field doesn't exist — returns `null`.

📌 Example:
```kotlin
val descr = viewModel.getField("describe")
```

All values are stored as `String` and must be cast as needed.

---

### `updateField(fieldName: String, value: Any)`
Sets a value in the form. If it's a reference field, it resolves the linked entity and updates the display.

---

### `stateFlow: StateFlow<T?>`
Contains the current entity being edited or viewed. **Reactive**: when it changes, the UI updates automatically.

---

### `flowList: Flow<List<T?>>`
Reactive list of base entities being displayed in list forms.

---

### `stateFlowExt: StateFlow<T_EXT?>`
Like `stateFlow`, but contains the extended entity (with linked objects instead of IDs).

---

### `flowListExt: Flow<List<T_EXT>>`
Like `flowList`, but holds extended entities.

---

### `lastActionCount: StateFlow<Int>`
Tracks how many records were modified by actions like `insert`, `update`, or `delete`.

---

### `lastInsertedId: StateFlow<Long>`
Stores the ID of the last inserted or updated entity.

---

### `myClass: KClass<T>`
Reflective class reference to the managed entity type.

---

### `tableName: String`
Name of the database table being managed.

---

### `formData: Map<String, String>`
Reactive map of form field values. Automatically updates on edit. May differ from entity/stateFlow data until saved.

---

## ⚙️ Common Functions of the ViewModel

The following methods are available to all ViewModels extending the base implementation.

### `suspend fun insert(item: T)`
Inserts a new entity. Updates `lastInsertedId`, refreshes `stateFlowExt`, and resets the global modification flag.

---

### `suspend fun simpleInsert(item: T)`
Performs insert without touching `stateFlowExt` or `lastInsertedId`. Useful for background or batch operations.

---

### `suspend fun update(item: T)`
Updates an entity in the database. Also refreshes `stateFlowExt` and updates `lastActionCount`.

---

### `suspend fun delete(item: T)`
Deletes an entity and refreshes both `flowList` and `flowListExt`.

---

### `fun refreshAll()`
Refreshes the base entity list.

---

### `fun refreshAllExt()`
Refreshes the extended entity list.

---

### `suspend fun insertOrUpdate(item: T)`
Inserts if `id == 0`, updates otherwise. Updates `stateFlowExt` and `lastInsertedId`.

---

### `fun insertExt(item: T_EXT)`
Inserts an extended entity and refreshes the extended state.

---

### `fun updateExt(item: T_EXT)`
Updates an extended entity and refreshes the extended state.

---

### `fun saveForm()`
Updates the current entity from `formData` and persists it via `insertOrUpdate()`.

---

### `fun updateField(field: String, value: Any, modify: Boolean = true)`
Sets the field value in `formData`. Sets the global `isModified` flag if `modify = true`.

---

### `fun getField(field: String): Any?`
Returns the string value of a field from `formData`, or `""` if missing.

---

### `fun initializeForm(fields: List<String>)`
Initializes `formData` with a set of fields, each set to an empty string.

---

### `fun validateField(fieldName: String): Boolean`
Validates a single field using rules from `fieldDescriptions`. Updates the `errors` map.

---

### `fun validateForm(): Boolean`
Validates the entire form. Fills the `errors` map with any issues.

---

### `fun updateView(value: Long?)` / `fun updateView()`
Forces UI refresh. Increments a counter to trigger recomposition.

---

### `fun checkExist(id: Long)`
Checks whether a record exists in the database. Result is placed in `check`.

---

### `fun setList(list: List<T>)` / `fun setListExt(list: List<T_EXT>)`
Directly sets the displayed list of entities.

---

## 🧱 Additional Fields

- `formValidator`: Validates form fields.
- `errors`: Map of current validation errors.
- `fieldDescriptions`: Metadata about each form field.
- `isDataRefreshed`: Indicates if `refreshAllExt()` has finished.
- `viewCounter`: Counter used for manual recomposition.
- `filter`: Filter object passed to repository.
