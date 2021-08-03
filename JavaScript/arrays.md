# **[JavaScript](./index.md) - Массивы**

```js
const maze =
`.....w
..w...
......`;

console.log(maze.split('\n').map(record => record.split('')));

[ [ '.', '.', '.', '.', '.', 'w' ], 
  [ '.', '.', 'w', '.', '.', '.' ], 
  [ '.', '.', '.', '.', '.', '.' ] ]
```
