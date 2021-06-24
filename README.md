# 🤞 IndexUpdate - transaction system, memo and time-travelling
Solving dependency problems (hell of dependencies). Improved caching as a consequence of application performance. It becomes much easier to manage the application. Index update is a replacement for `redux`, `react hooks`, `mobx`, `effector` and other libraries. `IndexUpdate` pattern is a cross-platform business solution.

## Problem: 
As a new version of react becomes available, it becomes more and more difficult to manage state. The developer should focus on many variables in their order when it is possible to encapsulate all the logic in `indexUpdate`. So here is `React hook dependency hell`:
```tsx
// Very Bad 📛
import React, { useState, useCallback } from "react";
import debounce from "lodash/debounce";

const App = () => {
  const [value, setValue] = useState("");
  const [dbValue, saveToDb] = useState(""); // would be an API call normally

  const debouncedSave = useCallback(
    debounce(nextValue => saveToDb(nextValue), 1000),
    [debounce, saveToDb]
  );

  const handleChange = useCallback(
    event => {
      const { value: nextValue } = event.target;
      setValue(nextValue);
      debouncedSave(nextValue);
    },
    [debouncedSave, setValue]
  );

  return (
    <main>
      <h1>Blog</h1>
      <textarea value={value} onChange={handleChange} rows={5} cols={50} />
      <section className="panels">
        <div>
          <h2>Editor (Client)</h2>
          {value}
        </div>
        <div>
          <h2>Saved (DB)</h2>
          {dbValue}
        </div>
      </section>
    </main>
  );
};
```

```tsx
// Good 👍
import React, { useState, useCallback } from "react";
import debounce from "lodash/debounce";
import { useIndexUpdate } from "@indexUpdate/react";

const App = () => {
  const [indexUpdate, setIndexUpdate] = useIndexUpdate();
  const [value, setValue] = useState("");
  const [dbValue, saveToDb] = useState(""); // would be an API call normally

  const debouncedSave = useCallback(
    debounce(nextValue => saveToDb(nextValue), 1000),
    [indexUpdate]
  );

  const handleChange = useCallback(
    event => {
      const { value: nextValue } = event.target;
      setValue(nextValue);
      debouncedSave(nextValue);
      setIndexUpdate(indexUpdate);
    },
    [indexUpdate]
  );

  return (
    <main>
      <h1>Blog</h1>
      <textarea value={value} onChange={handleChange} rows={5} cols={50} />
      <section className="panels">
        <div>
          <h2>Editor (Client)</h2>
          {value}
        </div>
        <div>
          <h2>Saved (DB)</h2>
          {dbValue}
        </div>
      </section>
    </main>
  );
};
```


## Simple React example
```tsx
const App = () => {
  const { index, makeTransaction } = useIndexUpdate();
  return (
    <button onClick={() => makeTransaction()} type="button">
        current value is {index}
    </button>
  )
};
```

## Simple Caching data / Use as Effect dependency
```tsx
const App = () => {
  const { index, makeTransaction } = useIndexUpdate();
  React.useEffect(() => { 
     // Your Side Effect
  }, [index);
  return (
    <button onClick={() => makeTransaction()} type="button">
        current value is {index}
    </button>
  )
};
```

### FAQ
- #### Does it support `Angular`, `Vue`, `VanillaJS`?
Not yet, but it will added in future (`@indexUpdate/angular`, `@indexUpdate/angular`)
- #### How fast is it? 
Very fast
- #### Does `@indexUpdate/react` support `React classes`?
Yes, it does.
- #### Does `@indexUpdate/react` exist? 
No, it doesn't

