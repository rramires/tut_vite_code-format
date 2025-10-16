# Tutorial Vite + Code Format

Tutorial to configure:  
Vite + Eslint, Prettier, and Organize Imports to format code.

---

### Instalação e configuração do Vite

1 - Instale o Vite:

[Vite Guide](https://vite.dev/guide/)

- Obs: Caso antes já tenha um arquivo README, a instalação vai sobrescrever. Então faça backup antes ou volte a versão dele com usando o git.

```sh
pnpm create vite .
```

Siga o passo a passo, no meu caso, já tem arquivos no projeto então vou mandar ignorar. E vou usar React + TypeScript
(Use as setas para mudar de opção)

1. ✔ Ignore files and continue
2. ✔ React
3. ✔ TypeScript
4. ✗ Use rolldown-vite
5. ✔ Install with pnpm and start now?

2 - Caso tenha optado por não instalar no wizard, instale as dependências e rode o projeto:

```sh
pnpm install
pnpm dev
```

3 - Caso queira trocar a porta, adicione no **vite.config.ts**:

```js
export default defineConfig({
	// adicione
	server: {
		port: 3001,
	},
	//
	plugins: [react()],
})
```

---

### Limpando o projeto padrão

1 - Exclua todos os arquivos .css e .svg

```sh
// remover
public/vite.svg
src/assets/react.svg
// remover
App.css
index.css
```

2 - Remova os imports desnecessários de **main.tsx**:

```js
// remover
import './index.css'
```

3 - Remova os imports e códigos desnecessários de **App.tsx**:

```js
// remover
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'
// remover
const [count, setCount] = useState(0)
// remover todo HTML do return (...)
```

4 - Adicione apenas um Hello World no return do **App.tsx**, ficando apenas:

```html
<>
    <h1>Hello World !!!</h1>
</>
```

4 - Mude para a exportação direta do módulo, ficando:

```js
// adicione export
export function App() {
	return (
		<>
			<h1>Hello World !!!</h1>
		</>
	)
}
// remova
// export default App
```

- Vai dar erro de importação no **main.tsx**

6 - Corrija a importação no **main.tsx**, adicionando chaves { }:

```js
// mudar de
// import App from './App.tsx'
// para
import { App } from './App.tsx'
```

7 - Comente a linha do Favicon no **index.html**:

```html
<!-- <link rel="icon" type="image/svg+xml" href="favicon.svg" /> -->
```

- Com isso, o projeto está limpo, pronto para ser organizado ao seu critério e exibindo apenas um **Hello World !!!** na página inicial.

8 - Rode com:

```sh
pnpm dev
```

---

### Instalação e configuração do Prettier

1 - Instale o Prettier:

[Prettier Install](https://prettier.io/docs/install)

- Obs: O ESLint já vem por padrão instalado qdo instalamos o Vite.

```sh
pnpm add --save-dev --save-exact prettier
```

2 - Crie o arquivo de exclusão **.prettierignore** e adicione:  
[Ignoring Code](https://prettier.io/docs/ignore)

```ini
# Dist Folder
dist
```

3 - Crie o arquivo de configuração do Prettier, **.prettierrc.json** contendo:  
[Prettier Options](https://prettier.io/docs/options)

- Minha configuração:  
  **printWidth=80** - Largura máxima de uma linha (quebra após passar)  
  **endOfLine="lf"** - Quebra de linha, "lf" padrão unix  
  **singleQuote=true** - Aspas simples  
  **jsxSingleQuote=true** - Aspas simples no jsx também  
  **quoteProps="as-needed"** - Usa aspas nas propriedases, só quando necessário  
  **semi=false** - Sem ponto e virgula  
  **useTabs=true** - Usar tabs em vez de espaços para indentação  
  **tabWidth=4** - Tab equvalente a 4 espaços  
  **arrowParens="always"** - Sempre usa parenteses nas Arrow Functions

```json
{
	"printWidth": 80,
	"endOfLine": "lf",
	"singleQuote": true,
	"jsxSingleQuote": true,
	"quoteProps": "as-needed",
	"semi": false,
	"useTabs": true,
	"tabWidth": 4,
	"arrowParens": "always"
}
```

- Atenção! Para funcionar deve estar marcado a opção do Prettier no VSCode requireConfig = true

Para habilitar via interface vá na Engrenagem > Settings e busque por **Prettier: Require Config**  
Marque a caixa de seleção e REINICIE o VSCode.

Para verificar/adicionar no **settings.json**.

```json
"prettier.requireConfig": true,
```

É essa linha que é adicionada ao clicar na caixa de seleção.

4 - Para que funcione ao salvar o arquivo ou no autoSave, adicione também no **settings.json**:

```js
// Verifique se existe:
"editor.formatOnSave": true
// Se não funcionar nos	.tsx, tente adicionar
"[typescriptreact]": {
    "editor.formatOnSave": true
},
```

Reinicie o VSCode.

5 - Caso queira, crie os comandos na sessão de **scripts** do **package.json**:

```json
"scripts": {
  "check": "prettier --check \"src/**/*.ts*\"",
  "format": "prettier --write \"src/**/*.ts*\""
}
```

Testando. Vá no **App.tsx** e **main.tsx** e volte aspas duplas e ponto e vírgula.

Verificar:

```sh
pnpm check
```

Corrigir:

```sh
pnpm format
```

---
