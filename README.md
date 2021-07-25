# micro-todo-app
micro-tiny-little todo list using vanilla web technologies (HTML, CSS, JS)

## it's so tiny that I'll put the whole source code here:

```html
	<html>
		<head>
			<style type="text/css">
				body {
					margin: 25% auto;
					width: 250px;
					padding: 10px;
					border: 1px solid black;
				}

				#dones {
					text-decoration: line-through;
				}

				li {
					cursor: pointer;
				}
			</style>
		</head>
		<body>
			<input id="text" type="text" placeholder="add some task" />
			<button id="add" type="button" onclick="add()">add</button>
			<p>todos</p>
			<ul id="todos"></ul>
			<p>dones</p>
			<ul id="dones"></ul>
		</body>
		<script type="text/javascript">
			let data = todos = dones = JSON.parse(localStorage.getItem('todos-data')) || [[], []];
			render()

			function add() { 
				const text = document.getElementById('text');
				data[0].push(text.value);
				text.value = '';
				render();
			}

			function render() {
				([todos, dones] = [document.getElementById('todos'), document.getElementById('dones')]) && (todos.innerHTML = dones.innerHTML = '') || data.forEach((d, _) => d.forEach((t, k) => {
					const li = document.createElement('li');
					((li.innerHTML = t) && (li.onclick = () => data[(!_ ? 1 : 0)].push(data[_].splice(k, 1)) && render()) && (!_ ? todos : dones).append(li));
				}))

				return !localStorage.setItem('todos-data', JSON.stringify(data))
			}
		</script>
	</html>
```
