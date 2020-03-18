# Jimo React Hooks

Collection of some react hooks

[![CI](https://github.com/jimengio/jimo-hooks/workflows/CI/badge.svg?branch=master)](https://github.com/jimengio/jimo-hooks/actions?query=workflow%3ACI)
[![npm](https://img.shields.io/npm/v/@jimengio/jimo-hooks.svg)](https://www.npmjs.com/package/@jimengio/jimo-hooks)
[![GitHub license](https://img.shields.io/github/license/jimengio/jimo-hooks)](https://github.com/jimengio/jimo-hooks/blob/master/LICENSE)

## Usage

### Installation

```shell
yarn add @jimengio/jimo-hooks
```

## Hooks

- [useAsyncClick](###useAsyncClick)
- [useDebounce](###useDebounce)
- [useDebouncedCallback](###useDebouncedCallback)
- [useDebouncedClick](###useDebouncedClick)
- [useDeepCompareCache](###useDeepCompareCache)
- [useDeepEffect](###useDeepEffect)

### useAsyncClick

Click event with `loading`

| option    | type     | default | explain        |
| --------- | -------- | ------- | -------------- |
| asyncFunc | function |         | async function |

```tsx
import { useAsyncClick } from "@react-cmpt/hooks";

const asyncFn = async () => {
  // do something
};

const Demo = () => {
  const [clickEvent, loading] = useAsyncClick(asyncFn);

  return <Button loading={loading} click={clickEvent} />;
};
```

### useDebounce

| option  | type   | default | explain |
| ------- | ------ | ------- | ------- |
| value   | any    |         |         |
| delay   | number |         |         |
| options | Object |         |         |

options:

| option     | type     | default | explain                                                                                                                          |
| ---------- | -------- | ------- | -------------------------------------------------------------------------------------------------------------------------------- |
| maxWait    | number   |         | Describes the maximum time func is allowed to be delayed before it's invoked                                                     |
| leading    | boolean  |         | This param will execute the function once immediately when called. Subsequent calls will be debounced until the timeout expires. |
| equalityFn | function |         | Comparator function which shows if timeout should be started                                                                     |

> [more options](https://github.com/xnimorz/use-debounce#options)

```tsx
import { useDebounce } from "@react-cmpt/hooks";

const Demo = () => {
  const [text, setText] = useState("hello");
  const [value] = useDebounce(text, 1000);

  return (
    <div>
      <input
        defaultValue={"hello"}
        onChange={e => {
          setText(e.target.value);
        }}
      />
      <p>Actual value: {text}</p>
      <p>Debounce value: {value}</p>
    </div>
  );
};
```

### useDebouncedCallback

| option   | type     | default | explain |
| -------- | -------- | ------- | ------- |
| callback | function |         |         |
| delay    | number   |         |         |
| options  | Object   |         |         |

```tsx
import { useDebouncedCallback } from "@react-cmpt/hooks";

const Demo = () => {
  const [value, setValue] = useState();
  // Debounce callback
  const [debouncedCallback] = useDebouncedCallback(
    // function
    value => {
      setValue(value);
    },
    // delay in ms
    1000
  );

  return (
    <div>
      <input onChange={e => debouncedCallback(e.target.value)} />
      <p>Debounced value: {value}</p>
    </div>
  );
};
```

### useDebouncedClick

Click event with `loading` and `debounce`

| option    | type     | default | explain                             |
| --------- | -------- | ------- | ----------------------------------- |
| asyncFunc | function |         | async function                      |
| delay     | number   | 300     | useDebouncedCallbackArgs["delay"]   |
| options   | Object   |         | useDebouncedCallbackArgs["options"] |

```tsx
import { useDebouncedClick } from "@react-cmpt/hooks";

const asyncFn = async () => {
  // do something
};

const Demo = () => {
  const [clickEvent, loading] = useDebounceClick(asyncFn);

  return <Button loading={loading} click={clickEvent} />;
};
```

### useDeepCompareCache

| option | type | default | explain |
| ------ | ---- | ------- | ------- |
| value  | any  |         |         |

```tsx
import { useDeepCompareCache } from "@react-cmpt/hooks";

const obj1 = { a: 1, b: { b1: 2 } };
const obj2 = { a: 1, b: { b1: 2 } };

const Demo = () => {
  const obj = useDeepCompareCache(obj1);
  console.log(obj === obj1); // true
  console.log(obj === obj2); // true

  // ...
};
```

### useDeepEffect

Deep comparison React.useEffect

| option | type     | default | explain                                                                 |
| ------ | -------- | ------- | ----------------------------------------------------------------------- |
| effect | function |         | Imperative function that can return a cleanup function                  |
| deps   | Array    |         | If present, effect will only activate if the values in the list change. |

```tsx
import { useDeepEffect } from "@react-cmpt/hooks";

const Demo = ({ value: Object }) => {
  useDeepEffect(() => {
    // do something
  }, [value]);

  // ...
};
```

## Dependencies

- [lodash.isequal](https://github.com/lodash/lodash)
- [use-debounce](https://github.com/xnimorz/use-debounce)

## Dev

```shell
# build package
yarn build

# tests
yarn test

# lint
yarn lint
```

## License

[MIT](./LICENSE)
