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
