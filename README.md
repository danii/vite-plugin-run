<p align="center">
<h2 align="center">Runner plugin for Vite</h2>

<p align="center">
	<a href="https://github.com/innocenzi/vite-plugin-run/actions/workflows/test.yaml"><img alt="Status" src="https://github.com/innocenzi/vite-plugin-run/actions/workflows/test.yaml/badge.svg"></a>
	<span>&nbsp;</span>
	<a href="https://github.com/innocenzi/vite-plugin-run/releases"><img alt="version" src="https://img.shields.io/github/v/release/innocenzi/vite-plugin-run?include_prereleases&label=version&logo=github&logoColor=white"></a>
	<br />
	<br />
	<p align="center">
		A plugin for running commands when files change or when Vite starts.
	</p>
	<pre><div align="center">npm i -D vite-plugin-run</div></pre>
</p>

&nbsp;

## Usage

Install `vite-plugin-run` and add it to your Vite configuration:

```ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import laravel from 'vite-plugin-laravel'
import run from 'vite-plugin-run'

export default defineConfig({
	plugins: [
		laravel(),
		vue(),
		run([
			{
				startup: true,
				name: 'typescript transform',
				run: ['php', 'artisan', 'typescript:transform'],
				condition: (file) => file.includes('Data.php'),
			},
			{
				startup: true,
				name: 'build routes',
				run: ['php', 'artisan', 'routes:generate'],
				condition: (file) => file.includes('/routes/'),
			}
		]),
	],
})
```

When a file in your project changes, its path will be given as an argument to `condition`. If the function returns `true`, a shell command described by `run` will be executed.

&nbsp;

## Runner options

| Option          | Type                           | Description                                                                | Default  |
| --------------- | ------------------------------ | -------------------------------------------------------------------------- | -------- |
| `startup`       | `bool`                         | Whether the command should run when Vite starts                            | `false`  |
| `name`          | `string`                       | An identifier for the runner, used in logs                                 | Required |
| `condition`     | `() => boolean`                | A function that should return true for a file change to execute the runner | Required |
| `run`           | `() => string[]` or `string[]` | A command executed when a file changed and the condition matches           | Required |
| `onFileChanged` | `() =>void`                    | A callback executed when a file changed and the condition matches          | Required |
| `delay`         | `number`                       | Delay before the command is executed                                       | `50`     |

<p align="center">
	<br />
	<br />
	·
	<br />
	<br />
	<sub>Built with ❤︎ by <a href="https://github.com/enzoinnocenzi">Enzo Innocenzi</a>
</p>