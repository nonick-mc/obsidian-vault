#RSC

ServerComponentではSuspenseとasync/awaitを用いて、データのストリーミングを行うことができる。以下は、ServerComponentを使用してTodoリストのデータを取得し、表示する例である。

```tsx
// page.tsx
import { Suspense } from "react";
import TodoList from "./todoList";

export default function Page() {
	return (
		<div>
			<h1>Todo</h1>
			{/* データの取得が完了するまでLoading...を表示 */}
			<Suspense fallback={<div>Loading...</div>}>
				<TodoList />
			</Suspense>
		</div>
	)
}
```

```tsx
// todoList.tsx
import { getTodos } from "./utils";

export default async function TodoList() {
	const todos = await getTodos();

	return (
		<div>
			{todos.map((todo, index) => (
				<div key={index}>{todo}</div>
			))}
		</div>
	)
}
```

ストリーミングを行うことで、データの取得を待たずにページ全体のレンダリングを行うことができ、ユーザーの待ち時間を短縮することができる。

データのストリーミングをClientComponentで行いたい場合、reactの[`use()`](https://ja.react.dev/reference/react/use)を使用する方法がある。`use()`は引数にPromiseを指定することができ、Promiseの結果を返り値として取り出すことができる