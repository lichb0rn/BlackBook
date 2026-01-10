---
created: 2024-03-15
aliases:
  - action slot for React Component
tags:
  - "#type/snippet"
source: "[[FSD - Полный Курс]]"
---
```ts
<TaskItem
  key={task.id}
  title={task.title}
  actions={
	<>
	  <ToggleTaskCheckbox
		value={task.done}
		onToggle={toggleCheckTask.bind(null, task.id)}
	  />
	  <DeleteTaskButton onClick={removeTask.bind(null, task.id)} />
	  {renderOwnerSelect({
		ownerId: task.ownerId,
		onChangeOwnerId: updateOwner.bind(null, task.id),
	  })}
	</>
  }
/>
```

```ts
import { ReactNode } from "react";

export const TaskItem = ({
  title,
  actions,
}: {
  title: string;
  actions: ReactNode;
}) => {
  return (
    <div style={{ display: "flex", gap: "10px", padding: "10px" }}>
      {actions}
      <div>{title}</div>
    </div>
  );
};
```