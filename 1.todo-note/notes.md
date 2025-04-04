### ✅ **Zustand Notes & Common Doubts**

#### **1️⃣ Zustand Updates & Shallow Copy**

- Zustand updates the state **immutably** by creating a **shallow copy** of the previous state.
- Example:

```typescript
set((state) => ({ notes: [...state.notes, newNote] }));`

    -   `notes: [...state.notes, newNote]` creates a **new array** (shallow copy).

    -   The previous `notes` array is discarded.
```

#### **2️⃣ Zustand & Deep Copy**

- Zustand **does not automatically deep copy** objects inside arrays.
- If a **nested object** inside the state is updated, a **shallow copy of that object** must be created manually.
- Example:

```jsx
updateNote: (id, updatedNote) => set((state) => ({ notes: state.notes.map((note) =>
          note.id === id ? { ...note, ...updatedNote } : note
        ),
      }));`
    -   `{ ...note, ...updatedNote }` ensures a new object is created.
```

#### **3️⃣ Difference in State Update Approach**

- **`addNote` returns a new array** (i.e., it replaces `notes`).
- **`updateNote` returns a new array** where only the modified note is updated.
- **✅ Solution**: Always return a **new reference** when updating state.

#### **4️⃣ Event Handler Binding in Buttons**

`onClick={() => handleEditNote(note)}`

✅ **Most common approach**
Calls `handleEditNote(note)` only when clicked.

`onClick={handleEditNote}`

❌ Incorrect if `handleEditNote` needs parameters.

`onClick={handleEditNote()}`

❌ **Wrong unless `handleEditNote` returns another function**. Calls it immediately during render.

`onClick={handleEditNote(note)}`
(if `handleEditNote` is a HOF)

✅ Works if `handleEditNote` is a **higher-order function** returning another function.

---
