# Understanding Control Level in Jetpack Compose: Why Compose Entity Makes Sense

My experience working with Compose Entity and Jetpack Compose revealed one thing: **Compose gives developers a level of control that no visual form builder provides**.

## 1. Visual form builders: limited to events
In most visual systems (Oracle Forms, 1C, SAP, or drag-and-drop Android builders), the developer only works with events:

- Before opening a form  
- While opening a form  
- On editing  

They do not give access to what happens **inside the rendering of each element**. You can only react to the form’s state, but not manage the rendering process at a low or even medium level.

## 2. Jetpack Compose: declarative control
Jetpack Compose allows you to **declare what happens inside the form and its elements**:

- You work at a high level of abstraction: you describe the UI declaratively, but still have access to the whole rendering process.  
- It is not low-level like DOS or Assembly, but also not limited to event hooks like visual form builders.  
- You can create custom Composables, manage state, observe data flows, and still remain in a safe, high-level context.

## 3. Compose Entity: simplification without losing control
In Compose Entity, I moved part of the event handling and logic into abstractions:

- The developer does not need to see the internal mechanisms of SQLite, DAO, ViewModel, or standard forms, unless they want to.  
- It’s still possible to customize Composables and access state inside the form.  
- This makes it possible to quickly test an idea without losing declarative control.

## Conclusion
The control level in Jetpack Compose makes it possible to **combine the simplicity of visual forms with the flexibility of the declarative approach**. Compose Entity is a way to keep things convenient for the developer, hiding unnecessary internals, while still giving access to what really matters: the rendering process and element states.
