# IndexUpdate - transaction system, memo and time-travelling

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
``
