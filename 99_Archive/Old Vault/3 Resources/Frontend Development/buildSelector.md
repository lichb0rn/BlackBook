---
tags:
  - resource
  - type/snippet
area: "[[Web Development]]"
---
Удобный builder [[Redux useSelect|селекторов]]  на [[TypeScript]] в [[React]]-приложении

```typescript
import { StateSchema } from '@/app/providers/StoreProvider';
import { useSelector } from 'react-redux';

type Selector<T> = (state: StateSchema) => T;
type Result<T> = [() => T, Selector<T>];

export function buildSelector<T>(selector: Selector<T>): Result<T> {
  const useSelectorHook = () => {
    return useSelector(selector);
  };

  return [useSelectorHook, selector];
}
```

source: [[Ulbi Продвинутый React]]