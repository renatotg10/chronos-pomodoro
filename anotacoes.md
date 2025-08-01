# Anotações

---

## 📁 `.vscode/settings.json` – Explicação das Configurações

Esse arquivo armazena configurações específicas do VS Code para o projeto atual.
Ele personaliza tanto o comportamento visual quanto ferramentas de formatação e
lint.

### 🎨 Aparência e Editor

```json
"window.zoomLevel": 0
```

- Nível de zoom da interface do VS Code. `0` é o padrão.

```json
"breadcrumbs.enabled": false
```

- Desativa a "trilha de navegação" (breadcrumbs) no topo do editor.

```json
"editor.fontSize": 14,
"debug.console.fontSize": 14,
"terminal.integrated.fontSize": 14
```

- Tamanho da fonte no editor, console de debug e terminal.

```json
"editor.glyphMargin": false
```

- Esconde a margem da esquerda que exibe ícones de depuração.

```json
"workbench.activityBar.location": "default"
```

- Mantém a barra lateral esquerda na posição padrão.

```json
"editor.lineNumbers": "on"
```

- Exibe os números das linhas no editor.

```json
"files.eol": "\n"
```

- Final de linha será sempre **LF**, usado em Linux/macOS. Evita problemas com
  Git e compatibilidade.

---

### 🛠️ Formatação e Lint

```json
"editor.defaultFormatter": "esbenp.prettier-vscode"
```

- Define o Prettier como formatador padrão de código.

```json
"editor.formatOnSave": true
```

- O código será formatado automaticamente ao salvar (`Ctrl+S`).

```json
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": "explicit"
}
```

- Aplica correções automáticas do ESLint ao salvar, apenas se forem ações
  explicitamente definidas.

---

### 📦 Formatação por tipo de arquivo

Cada bloco abaixo define que o **Prettier** será o formatador padrão para os
respectivos tipos de arquivos:

```json
"[javascript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[typescript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[xml]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[svg]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[html]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

---

### ✅ Resumo

Essa configuração garante que:

- O código será **padronizado** e **formatado automaticamente** com Prettier.
- O ESLint aplicará **correções automáticas** ao salvar.
- O ambiente de desenvolvimento no VS Code estará limpo, legível e otimizado.

---

## 🛠️ `.prettierrc.json` – Configurações do Prettier

Este arquivo define as regras de formatação automática do Prettier, uma
ferramenta que ajuda a manter o código limpo e consistente.

---

### Explicação de cada configuração

```json
"arrowParens": "avoid"
```

- Evita parênteses em funções arrow com um único parâmetro. Exemplo:

  ```js
  x => x + 1;
  ```

  ao invés de

  ```js
  x => x + 1;
  ```

```json
"bracketSpacing": true
```

- Adiciona espaços entre chaves em objetos. Exemplo: `{ foo: bar }` em vez de
  `{foo:bar}`.

```json
"htmlWhitespaceSensitivity": "css"
```

- O Prettier respeita as regras de espaçamento do CSS dentro do HTML, ajustando
  o espaçamento conforme o estilo CSS aplicado.

```json
"insertPragma": false
```

- Não insere automaticamente o comentário `@format` no topo dos arquivos.

```json
"jsxBracketSameLine": false
```

- Coloca o fechamento do JSX (`>`) em uma linha separada, para melhor
  legibilidade.

```json
"jsxSingleQuote": true
```

- Usa aspas simples (`'`) em vez de aspas duplas (`"`) em arquivos JSX. Exemplo:
  `<div className='minha-classe'>`.

```json
"printWidth": 80
```

- Limita o comprimento da linha para 80 caracteres antes de quebrar o código
  para a próxima linha.

```json
"proseWrap": "always"
```

- Quebra sempre o texto em Markdown (prose), facilitando a leitura e revisão.

```json
"quoteProps": "as-needed"
```

- Usa aspas em propriedades de objetos somente quando necessário. Exemplo:

  ```js
  { foo: 1 } // sem aspas
  { "foo-bar": 2 } // com aspas, pois contém traço
  ```

```json
"requirePragma": false
```

- Não exige comentário `@format` para formatar o arquivo.

```json
"semi": true
```

- Sempre adiciona ponto e vírgula no final das instruções.

```json
"singleQuote": true
```

- Usa aspas simples em vez de aspas duplas no JavaScript.

```json
"tabWidth": 2
```

- Define que cada indentação tem 2 espaços.

```json
"trailingComma": "all"
```

- Adiciona vírgula no final de objetos, arrays e parâmetros multilinha (isso
  facilita diffs e manutenção).

```json
"useTabs": false
```

- Usa espaços para indentação, não tabulações.

---

### ✅ Resumo

Essas configurações garantem que o código seja:

- Consistente, com aspas simples e indentação de 2 espaços.
- Legível, com largura máxima de 80 caracteres.
- Fácil de manter, com vírgulas finais em listas multilinha.
- Ajustado para JSX com aspas simples e fechamento de tags em linha separada.

---

Claro! Aqui está a explicação detalhada do seu arquivo `eslint.config.js`,
pronta para adicionar no seu `anotacoes.md`:

---

## 🛠️ `eslint.config.js` – Configuração do ESLint para TypeScript e React

Este arquivo configura o ESLint, que é uma ferramenta para verificar problemas
no código e impor boas práticas.

---

### Importações e Utilitários

```js
import js from '@eslint/js';
import globals from 'globals';
import reactHooks from 'eslint-plugin-react-hooks';
import reactRefresh from 'eslint-plugin-react-refresh';
import tseslint from 'typescript-eslint';
import { globalIgnores } from 'eslint/config';
```

- Importa módulos oficiais e plugins para configurar regras para JavaScript,
  TypeScript, React Hooks e integração com React Refresh.
- `globals` contém variáveis globais padrão para ambientes como navegador
  (`window`, `document`, etc).
- `globalIgnores` permite ignorar pastas inteiras, como a pasta `dist` de build.

---

### Exportação da Configuração

```js
export default tseslint.config([
  globalIgnores(['dist']),
  {
    files: ['**/*.{ts,tsx}'],
    extends: [
      js.configs.recommended,
      tseslint.configs.recommended,
      reactHooks.configs['recommended-latest'],
      reactRefresh.configs.vite,
    ],
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
    },
  },
]);
```

- Usa `typescript-eslint` para configurar o ESLint com foco em TypeScript.
- **Ignora a pasta `dist`** — arquivos gerados na build não são analisados.
- Aplica regras **somente nos arquivos `.ts` e `.tsx`** (TypeScript e React com
  TypeScript).
- Extende várias configurações recomendadas para:

  - **JavaScript padrão** (regras gerais).
  - **TypeScript** (regras específicas para TS).
  - **React Hooks** (regras para o uso correto de hooks).
  - **React Refresh com Vite** (suporte para atualização rápida em dev).

- Define a versão do ECMAScript como 2020, que permite usar recursos modernos do
  JS.
- Reconhece variáveis globais do ambiente **browser** (ex.: `window`,
  `document`).

---

### ✅ Resumo

Esse arquivo garante que o ESLint:

- Analise e aplique regras modernas para TypeScript e React.
- Respeite boas práticas específicas para hooks do React.
- Ignore arquivos gerados no build.
- Use configurações compatíveis com seu ambiente de desenvolvimento (Vite,
  navegador, ES2020).

---

## 📦 `package.json` – Explicação das Configurações

O arquivo `package.json` define as **informações do projeto**, os **scripts de
execução** e as **dependências** que serão usadas no seu app React (neste caso,
um projeto chamado `chronos-pomodoro`).

---

### 🏷️ Informações Básicas

```json
"name": "chronos-pomodoro"
```

- Nome do projeto.

```json
"private": true
```

- Impede que o projeto seja publicado no **npm** acidentalmente.

```json
"version": "0.0.0"
```

- Versão inicial do projeto. Pode ser usada em builds e CI.

```json
"type": "module"
```

- Define que o projeto usa **ES Modules** (import/export), e não `require()` do
  CommonJS.

---

### 🛠️ Scripts

Bloco `"scripts"` define comandos que podem ser executados com `npm run`:

```json
"dev": "vite"
```

- Inicia o servidor de desenvolvimento com **Vite** (rápido e com hot-reload).

```json
"build": "tsc -b && vite build"
```

- Compila os arquivos com **TypeScript (`tsc`)** e depois gera os arquivos
  otimizados para produção com `vite build`.

```json
"lint": "eslint ."
```

- Executa o **ESLint** na raiz do projeto (e em subpastas), verificando o código
  em busca de problemas.

```json
"preview": "vite preview"
```

- Visualiza a versão **já construída** do projeto localmente, como se estivesse
  em produção.

---

### 📦 Dependências

Instaladas com `npm install` (ou `npm install nome-pacote`) e necessárias **em
tempo de execução**:

```json
"react": "^19.1.0",
"react-dom": "^19.1.0"
```

- Bibliotecas principais do **React 19**: `react` (componentes) e `react-dom`
  (integração com a DOM).

---

### 🔧 DevDependencies

Usadas **somente em desenvolvimento**, para ferramentas e configurações:

```json
"@vitejs/plugin-react-swc"
```

- Plugin para o Vite suportar React com o compilador **SWC** (mais rápido que
  Babel).

```json
"vite"
```

- Bundler moderno para desenvolvimento e build do projeto (substitui Webpack).

```json
"typescript"
```

- Suporte à linguagem **TypeScript**.

```json
"@types/react", "@types/react-dom"
```

- Tipagens do React, necessárias para TypeScript.

```json
"eslint"
```

- Ferramenta de análise estática para identificar erros e padrões no código.

```json
"@eslint/js", "typescript-eslint"
```

- Integração do ESLint com JavaScript padrão e TypeScript.

```json
"eslint-plugin-react-hooks"
```

- Regras específicas para hooks do React (`useEffect`, `useState`, etc.).

```json
"eslint-plugin-react-refresh"
```

- Suporte ao **Fast Refresh** do React (atualização instantânea de componentes
  no dev).

```json
"globals"
```

- Define variáveis globais usadas por ESLint, como `window`, `console`, etc.

---

### ✅ Resumo

O `package.json`:

- Organiza e documenta as **dependências** do projeto.
- Define os **scripts** de desenvolvimento e build.
- Garante que o ambiente está padronizado e automatizado.

---

## 📄 `package-lock.json` – Para que serve?

O `package-lock.json` é um arquivo **gerado automaticamente pelo npm** (Node
Package Manager) toda vez que você instala dependências no seu projeto com
`npm install`.

---

### Função principal

- **Garantir que todas as pessoas (ou servidores) que instalarem o projeto terão
  exatamente as mesmas versões das dependências instaladas.** Mesmo que o
  `package.json` defina versões usando `^` ou `~` (que permitem atualizar para
  versões mais novas), o `package-lock.json` "trava" as versões exatas usadas
  naquele momento.

---

### Benefícios

- Evita bugs e inconsistências causadas por versões diferentes das bibliotecas.
- Garante reprodutibilidade e estabilidade no ambiente de desenvolvimento, teste
  e produção.
- Acelera instalações futuras, pois o npm sabe exatamente quais versões baixar.
- Contém não só as versões das dependências diretas, mas também das dependências
  **indiretas** (dependências das dependências).

---

### Importante

- Não deve ser editado manualmente.
- Sempre que alguém clonar seu projeto, deve rodar `npm install` para instalar
  as versões exatas do `package-lock.json`.
- O `package-lock.json` funciona junto com o `package.json` — o primeiro “trava”
  as versões, o segundo descreve as dependências em geral.

---

### Resumo rápido

| Arquivo             | Função                                         |
| ------------------- | ---------------------------------------------- |
| `package.json`      | Lista as dependências do projeto               |
| `package-lock.json` | Trava versões exatas e dependências recursivas |

---

## 📂 `node_modules` – O que é e para que serve?

A pasta `node_modules` é criada automaticamente pelo **npm** (ou yarn) quando
você instala as dependências do seu projeto usando comandos como `npm install`.

---

### Função principal

- Armazena **todos os pacotes (bibliotecas) que seu projeto usa**, incluindo as
  dependências diretas (listadas no `package.json`) e todas as dependências
  delas (dependências indiretas).
- Contém o código-fonte das bibliotecas para que seu projeto possa importar e
  executar.

---

### Como funciona?

- Quando você roda `npm install`, o npm lê o `package.json` e o
  `package-lock.json` para baixar as versões exatas das bibliotecas.
- Depois, coloca tudo dentro da pasta `node_modules`.
- O seu código (por exemplo, um `import React from 'react'`) vai buscar o React
  dentro dessa pasta.

---

### Por que a pasta pode ser tão grande?

- Porque cada pacote pode ter várias dependências.
- Cada uma dessas dependências pode ter outras dependências (cadeia de
  dependências).
- Assim, a árvore de dependências pode crescer bastante.

---

### Considerações importantes

- **Nunca envie a pasta `node_modules` para o controle de versão (ex: Git).**
  Por isso existe o `.gitignore`.
- Se alguém clona seu projeto, basta rodar `npm install` para baixar tudo de
  novo.
- Às vezes, se algo der errado com as dependências, você pode deletar essa pasta
  e rodar `npm install` novamente para restaurar.

---

### Resumo rápido

| Item           | Função                                              |
| -------------- | --------------------------------------------------- |
| `node_modules` | Armazena todos os pacotes/bibliotecas do projeto    |
| `npm install`  | Baixa e instala os pacotes dentro do `node_modules` |

---

## ⚙️ `tsconfig.app.json` – Configurações do compilador TypeScript para o projeto React

Esse arquivo define as opções usadas pelo compilador TypeScript (`tsc`) para
interpretar, verificar e compilar seu código `.ts` e `.tsx` no projeto.

---

### Explicação dos principais campos

```json
"tsBuildInfoFile": "./node_modules/.tmp/tsconfig.app.tsbuildinfo"
```

- Arquivo que armazena informações para acelerar builds incrementais (para
  compilar mais rápido ao recompilar).

```json
"target": "ES2022"
```

- Define a versão do JavaScript que será gerada após compilação. Aqui, é o
  padrão ES2022, que suporta recursos modernos.

```json
"useDefineForClassFields": true
```

- Usa a semântica do `define` para campos de classe (atual padrão mais alinhado
  com o comportamento JS moderno).

```json
"lib": ["ES2022", "DOM", "DOM.Iterable"]
```

- Define as bibliotecas padrão que o compilador deve incluir. Inclui APIs do
  ES2022 e do DOM para manipulação de elementos HTML e iteráveis.

```json
"module": "ESNext"
```

- Define o sistema de módulos usado no código gerado. `ESNext` é o mais moderno,
  usando `import`/`export`.

```json
"skipLibCheck": true
```

- Ignora a checagem de tipos em arquivos de declaração `.d.ts` das bibliotecas,
  acelerando a compilação.

---

### Configurações para bundlers modernos (como Vite)

```json
"moduleResolution": "bundler"
```

- Resolva módulos pensando em bundlers (Vite, Webpack), melhor para projetos
  modernos.

```json
"allowImportingTsExtensions": true
```

- Permite importar arquivos TypeScript com extensão explícita `.ts` ou `.tsx`.

```json
"verbatimModuleSyntax": true
```

- Mantém a sintaxe original de módulos sem alterações, útil para bundlers.

```json
"moduleDetection": "force"
```

- Força o compilador a detectar módulos mesmo em casos ambíguos.

```json
"noEmit": true
```

- Não gera arquivos `.js` (porque a build real é feita pelo Vite).

```json
"jsx": "react-jsx"
```

- Usa o novo transformador JSX automático para React 17+, sem necessidade de
  importar `React` manualmente.

---

### Configurações de Linting e Verificação Rigorosa

```json
"strict": true
```

- Ativa modo estrito, com várias verificações rigorosas de tipos.

```json
"noUnusedLocals": true,
"noUnusedParameters": true,
```

- Gera erros se houver variáveis ou parâmetros não usados.

```json
"erasableSyntaxOnly": true,
```

- Aplica verificações somente a sintaxes que podem ser removidas pelo
  compilador.

```json
"noFallthroughCasesInSwitch": true,
```

- Evita que casos `switch` caiam “acidentalmente” para o próximo caso sem
  `break`.

```json
"noUncheckedSideEffectImports": true
```

- Evita importar módulos que possam ter efeitos colaterais não verificados.

---

### Inclusão de arquivos

```json
"include": ["src"]
```

- Define que o compilador deve considerar apenas arquivos dentro da pasta `src`.

---

### ✅ Resumo

Esse arquivo configura o TypeScript para:

- Compilar para JavaScript moderno (ES2022) com módulos ESNext.
- Usar recursos específicos para bundlers modernos como Vite.
- Garantir código mais seguro e limpo com verificações estritas.
- Não gerar arquivos JS diretamente (build final é feita pelo Vite).
- Trabalhar com JSX no estilo React 17+ de forma automática.

---

## ⚙️ `tsconfig.json` – Arquivo de referência para configurações TypeScript

Esse arquivo é uma espécie de **configuração raiz** que indica outros arquivos
de configuração do TypeScript para o projeto.

---

### Estrutura e significado

```json
"files": []
```

- Não especifica arquivos diretamente neste arquivo, ou seja, ele não compila
  nada por si só.

```json
"references": [
  { "path": "./tsconfig.app.json" },
  { "path": "./tsconfig.node.json" }
]
```

- Define referências para outros projetos TypeScript (arquivos de configuração),
  que serão usados em conjunto.
- Isso permite usar o recurso de **builds incrementais e dependentes** do
  TypeScript (comando `tsc --build`).
- Aqui, indica que o projeto depende das configurações definidas em
  `tsconfig.app.json` e `tsconfig.node.json`.

---

### Para que serve?

- Facilita o gerenciamento de projetos maiores que podem ter múltiplos
  "subprojetos" ou configurações distintas.
- Permite que o TypeScript compile cada parte separadamente, mantendo controle
  das dependências.
- Melhora o desempenho do build em projetos complexos.

---

### Exemplo no seu caso

- `tsconfig.app.json`: Configura o compilador para o código da aplicação React.
- `tsconfig.node.json`: Provavelmente configura o compilador para código que
  roda no Node.js (por exemplo, scripts de build ou servidores).

---

### ✅ Resumo rápido

| Campo        | Função                                       |
| ------------ | -------------------------------------------- |
| `files`      | Lista de arquivos para compilar (vazio aqui) |
| `references` | Referências para outros arquivos `tsconfig`  |

---

## ⚙️ `tsconfig.node.json` – Configurações TypeScript para código Node.js (ex.: scripts e configuração)

Este arquivo configura o compilador TypeScript para arquivos que rodam no
ambiente **Node.js**, como configurações, scripts auxiliares e ferramentas (ex.:
`vite.config.ts`).

---

### Principais opções e explicações

```json
"tsBuildInfoFile": "./node_modules/.tmp/tsconfig.node.tsbuildinfo"
```

- Arquivo usado para acelerar builds incrementais.

```json
"target": "ES2023"
```

- Versão do JavaScript alvo (mais moderna que ES2022), com recursos atuais do
  JS.

```json
"lib": ["ES2023"]
```

- Bibliotecas usadas na compilação, aqui só a padrão ES2023 (sem DOM, porque é
  código Node).

```json
"module": "ESNext"
```

- Sistema de módulos moderno (`import`/`export`).

```json
"skipLibCheck": true
```

- Ignora checagem de tipos em declarações de bibliotecas para acelerar
  compilação.

---

### Configurações para bundler e resolução de módulos

```json
"moduleResolution": "bundler"
```

- Otimiza resolução de módulos para bundlers modernos.

```json
"allowImportingTsExtensions": true
```

- Permite importar arquivos TypeScript com extensões explícitas.

```json
"verbatimModuleSyntax": true
```

- Mantém a sintaxe original do módulo sem alteração.

```json
"moduleDetection": "force"
```

- Força detecção de módulos mesmo em casos ambíguos.

```json
"noEmit": true
```

- Não gera arquivos `.js` (compilação real feita por bundler ou runtime).

---

### Verificações rigorosas de código (linting)

```json
"strict": true,
"noUnusedLocals": true,
"noUnusedParameters": true,
"erasableSyntaxOnly": true,
"noFallthroughCasesInSwitch": true,
"noUncheckedSideEffectImports": true
```

- Ativa checagens rigorosas para evitar erros comuns, variáveis não usadas, e
  outros problemas.

---

### Inclusão de arquivos

```json
"include": ["vite.config.ts"]
```

- Aplica a compilação e verificação somente no arquivo `vite.config.ts`, que é a
  configuração do Vite em TypeScript.

---

### ✅ Resumo

Esse arquivo é específico para configurar o TypeScript para:

- Código que roda no Node.js, com suporte a recursos modernos do ES2023.
- Garantir qualidade e segurança no código de configuração.
- Otimizar resolução e bundling.
- Focar somente no arquivo `vite.config.ts`.

---

## ⚙️ `vite.config.ts` – Configuração do Vite para o projeto React

Este arquivo configura o **Vite**, que é o bundler e servidor de desenvolvimento
usado no projeto. O arquivo está em TypeScript (`.ts`).

---

### Explicação do conteúdo

```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react-swc';
```

- Importa a função `defineConfig` para ajudar a escrever a configuração com
  autocompletar e tipos.
- Importa o plugin React para Vite, usando o compilador SWC (mais rápido que
  Babel).

---

### Exportação da configuração

```ts
export default defineConfig({
  plugins: [react()],
});
```

- Exporta a configuração padrão do Vite.
- O plugin React é ativado para que o Vite possa processar arquivos React
  (`.jsx`/`.tsx`), incluindo suporte a Fast Refresh e compilação eficiente.

---

### Resumo

Esse arquivo é bem simples, e serve para:

- Configurar o Vite para trabalhar com React usando SWC, garantindo rapidez e
  suporte às funcionalidades modernas.
- Permitir que o servidor de desenvolvimento e o build processem corretamente os
  arquivos React.

---

## 🚫 `.gitignore` – Para que serve e explicação do conteúdo

O arquivo `.gitignore` é usado para dizer ao **Git** quais arquivos ou pastas
**não devem ser incluídos** no controle de versão.

---

### Por que usar `.gitignore`?

- Evita subir para o repositório arquivos que não são necessários para o
  código-fonte, como arquivos temporários, logs, dependências, builds,
  configurações locais.
- Mantém o repositório limpo e menor.
- Protege informações sensíveis que podem estar em arquivos locais.

---

### Explicação das regras no seu arquivo

```gitignore
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
pnpm-debug.log*
lerna-debug.log*
```

- Ignora pastas e arquivos de log que são gerados durante a execução e depuração
  do projeto.

```gitignore
node_modules
```

- Ignora a pasta `node_modules`, que contém dependências instaladas localmente.

```gitignore
dist
dist-ssr
```

- Ignora pastas de build (arquivos gerados para produção).

```gitignore
*.local
```

- Ignora arquivos com a extensão `.local`, geralmente usados para configurações
  locais.

```gitignore
# Editor directories and files
!.vscode/extensions.json
.idea
.DS_Store
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?
```

- Ignora arquivos e pastas específicas de editores e sistemas operacionais,
  como:

  - `.idea` (JetBrains IDEs),
  - `.DS_Store` (macOS),
  - arquivos do Visual Studio (`*.suo`, `*.sln`, etc),
  - arquivos temporários e de configuração.

- A exceção `!.vscode/extensions.json` significa que esse arquivo específico
  dentro da pasta `.vscode` **não** será ignorado (é comitado).

---

### ✅ Resumo

O `.gitignore` serve para:

- Evitar subir arquivos inúteis ou temporários.
- Manter o repositório limpo e focado no código.
- Proteger configurações locais e sensíveis.

---

## 📁 Pastas e Arquivos Básicos do Projeto React

### 1. `public/`

- Pasta onde ficam arquivos estáticos que **não passam por processamento do
  bundler** (Vite, Webpack).
- Exemplo: imagens, ícones, `favicon.ico`, arquivos HTML base, fontes.
- O conteúdo aqui é copiado **direto para a pasta final de build**, mantendo os
  mesmos caminhos.
- Serve para arquivos que precisam estar acessíveis diretamente, sem
  transformação.

---

### 2. `src/`

- Pasta principal onde fica o **código-fonte da aplicação React**.
- Contém os componentes React, estilos, arquivos TypeScript/JavaScript, assets
  que precisam ser processados.
- É onde você vai passar a maior parte do tempo escrevendo seu app.

---

### 3. `index.html`

- Arquivo HTML base que o Vite usa para servir sua aplicação.
- Contém a estrutura básica da página, com a div raiz (geralmente
  `<div id="root"></div>`) onde o React vai montar a interface.
- Pode conter links para favicons, fontes externas, meta tags, etc.
- O Vite injeta automaticamente o bundle JavaScript nesse arquivo no momento do
  build.

---

### 4. `README.md`

- Arquivo texto escrito em Markdown que explica o projeto.
- Geralmente contém:

  - O que é o projeto,
  - Como instalar e rodar,
  - Tecnologias usadas,
  - Como contribuir,
  - Licença,
  - Informações importantes para outros desenvolvedores.

- Serve como documentação inicial do projeto.

---

### ✅ Resumo rápido

| Item         | Função                                  |
| ------------ | --------------------------------------- |
| `public/`    | Arquivos estáticos servidos direto      |
| `src/`       | Código-fonte React e assets processados |
| `index.html` | Página HTML base da aplicação React     |
| `README.md`  | Documentação e instruções do projeto    |

---
