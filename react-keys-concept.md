# React Controlled vs Uncontrolled Components

Understanding the difference between **controlled** and **uncontrolled** inputs in React is crucial for avoiding tricky bugs (especially with `defaultValue` and index keys).

---

## ✅ Controlled Component

- React **reuses the same DOM node** if the key is the same.
- But since you pass a **`value` prop**, React **always updates the DOM’s `value` property** during render.
- Result: Even if React reuses the wrong `<input>` node (like when using `index` keys), the text inside the input is corrected to match your state.
- **Always in sync with React state.**

### Example (Controlled)
```jsx
import { useState } from "react";

function ControlledExample() {
  const [fruits, setFruits] = useState(["Apple", "Banana"]);

  const handleAddFruit = () => {
    setFruits((prev) => ["Orange", ...prev]); // prepend new fruit
  };

  return (
    <div>
      <h3>Controlled (Safe)</h3>
      {fruits.map((fruit, index) => (
        <input
          key={index}
          value={fruit}   // React controls the value
          readOnly        // no user editing here
        />
      ))}
      <button onClick={handleAddFruit}>Add Fruit</button>
    </div>
  );
}

export default ControlledExample;

***************************************************************************************************************************************************************

import { useState } from "react";

function UncontrolledExample() {
  const [fruits, setFruits] = useState(["Apple", "Banana"]);

  const handleAddFruit = () => {
    setFruits((prev) => ["Orange", ...prev]); // prepend new fruit
  };

  return (
    <div>
      <h3>Uncontrolled (Buggy)</h3>
      {fruits.map((fruit, index) => (
        <input
          key={index}
          defaultValue={fruit}  // initial value only
        />
      ))}
      <button onClick={handleAddFruit}>Add Fruit</button>
    </div>
  );
}

export default UncontrolledExample;
