---
tags:
  - resource
  - type/snippet
area: "[[OLD/2 Areas/Web Development]]"
---
Builder [[Redux slice|слайсов]] в [[React]]-приложении

```typescript
import {
  CreateSliceOptions,
  SliceCaseReducers,
  SliceSelectors,
  bindActionCreators,
  createSlice,
} from '@reduxjs/toolkit';
import { useMemo } from 'react';
import { useDispatch } from 'react-redux';

export function buildSlice<
  State,
  CaseReducers extends SliceCaseReducers<State%3E,
  Name extends string,
  Selectors extends SliceSelectors<State>,
  ReducerPath extends string = Name,
>(options: CreateSliceOptions<State, CaseReducers, Name, ReducerPath, Selectors>) {
  const slice = createSlice(options);

  const useActions = (): typeof slice.actions => {
    const dispatch = useDispatch();

    return useMemo(() => bindActionCreators(
	    slice.actions, 
	    dispatch
	), [dispatch]);
  };

  return {
    ...slice,
    useActions,
  };
}
```