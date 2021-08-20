# **[Vue 3](./index.md) - Composition API**

* Computed with get and set

```js
setup(props, context) {
	let val = computed({
		get: () => {
			return null;
		},
		set: (value) => {
			// code
		}
	});

	return { val };
}
```
