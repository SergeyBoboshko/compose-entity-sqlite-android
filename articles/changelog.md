# Version 1.0.27 – Breaking annotation renaming (16.07.2025)

## ⚠️ Breaking Changes

This version introduces **new, cleaner naming** for all core annotations in the `ComposeEntity` framework.  
Old annotations are now **officially deprecated** and will cause **compilation errors**.

This change improves consistency, clarity, and better reflects the naming style of the framework going forward.

### 🔁 Renamed Annotations

| Old Annotation             | New Annotation            |
|----------------------------|----------------------------|
| `@ObjectGeneratorCE`       | `@CeGenerator`             |
| `@DatabaseVersion`         | `@CeDatabaseVersion`       |
| `@DatabaseMigration`       | `@CeManualMigration`       |
| `@MigrationEntityCE`       | `@CeMigrationEntity`       |
| `@FormFieldCE`             | `@CeField`                 |
| `@DocumentDescriberCE`     | `@CeDocumentDescriber`     |

### ❗ Compilation Errors

If you try to use a deprecated annotation, you will see a **compiler error** like this: Annotation @ObjectGeneratorCE is deprecated. Use @CeGenerator instead.


### ✅ How to Fix

Simply replace all occurrences of deprecated annotations in your code with the corresponding new ones (see the table above).  
No behavioral changes were made — only annotation names were updated.

---

## 🆕 New Additions

- Added new official annotations with `Ce*` prefix:  
  - `@CeGenerator`, `@CeField`, `@CeDatabaseVersion`, `@CeManualMigration`, `@CeMigrationEntity`, etc.
- Introduced `@CeFree`, `@CeReport`, `@CeAutoMigration` for advanced use cases.

## 🔍 Notes

- Deprecated annotations remain in the codebase only to provide meaningful error messages.
- Deprecated annotations will be **fully removed in a future release**.


