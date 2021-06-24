# 🤞 IndexUpdate - transaction system, memo and time-travelling
Solving dependency problems (hell of dependencies). Improved caching as a consequence of application performance. It becomes much easier to manage the application. Index update is a replacement for `redux`, `react hooks`, `mobx`, `effector` and other libraries. `IndexUpdate` pattern is a cross-platform business solution.

### Simple React example
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

### Simple Caching data / Use as Effect dependency
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
