# Code Style Guideline

<p align="center">
  <img src="https://media.giphy.com/media/26tn33aiTi1jkl6H6/giphy.gif">
</p>

- [Code Style Guideline](#code-style-guideline)
  - [Front end](#front-end)
    - [Get started](#get-started)
      - [For VSCode CLI](#for-vscode-cli)
      - [How to make VSCode format changed files on save](#how-to-make-vscode-format-changed-files-on-save)
    - [Naming](#naming)
    - [Project structure](#project-structure)
    - [Component](#component)
      - [Ordering (Top - Bottom)](#ordering-top---bottom)
      - [Exporting](#exporting)
    - [Storage management](#storage-management)
  - [Commenting](#commenting)
    - [TODO](#todo)
    - [Refactoring](#refactoring)
    - [Styling](#styling)
  - [Testing](#testing)
  - [Standpoint](#standpoint)
    - [Do not repeat yourself (DRY)](#do-not-repeat-yourself-dry)
    - [Do not use Magic Numbers](#do-not-use-magic-numbers)

## Front end

### Get started

Always use Typescript feature to prevent hidden bugs from Javascript.

If you are VSCode use, We suggest installing these following extensions and make the editor auto format after you saved

#### For VSCode CLI

```bash
code --install-extension esbenp.prettier-vscode
code --install-extension dbaeumer.vscode-eslint
code --install-extension styled-components.vscode-styled-components
```

#### How to make VSCode format changed files on save

1. Type shortcut **⌘ + shift + P**
2. Choose **Preferences: Open Settings (UI)*
3. Search by **Editor: Format On Save**
4. Check the checkbox

Finally, please make sure the VSCode configuration file (JSON) have configurations as below:

```json
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true
},
"[typescript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[typescriptreact]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[javascript]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
"[javascriptreact]": {
  "editor.defaultFormatter": "esbenp.prettier-vscode"
},
```

### Naming

Constant variables: **camelCase**

For **Boolean** variables should start with **is**, **has**, and **should**

For **Array** should use the **plural** noun

```ts
const tmnId = 'tmn.1234566789'
let count = 0

const isModalVisible = false
const hasValue = true
const shouldUpdate = false

const users = ['Dang', 'Dum']
const userDetail = {
  name: 'Tester',
  occupations: [
    'farmer',
    'investor'
  ]
}
```

For function please use **camelCase**, start with Verb, and only use [Arrow function](https://www.w3schools.com/js/js_arrow_function.asp)

For handler function should start with on

```ts
const calculateNumber = (firstInput: number, secondInput: number) => firstInput + secondInput

const onClose = () => ({})
const onSubmitComplete = () => ({})
```

For **Enumerate** please use **PascalCase**

```ts
enum ActionType = {
  Create = 1,
  Update = 2
}
```

For Type and Interface use **PascalCase** start with **I**

```ts
type IOccupation = 'business' | 'farmer' | 'other'

interface IComponentProps {
  title: string
  onClick: () => void
  onChange: (input: number) => void
}
```

For Component and Styled-Component please use **PascalCase**

```ts
const FundCard = ({ title, description }: IFundCard) => (
  <Container>
    ...
  </Container>
)

const Container = styled.div`
  border: 1px solid red;
`
```

For Page please add a **Page** suffix to our page component.

```ts
const PurchasePage = () => {
  return (...)
}

export default PurchasePage
```

### Project structure

The structure is based on [Next.js](https://nextjs.org/) framework.

```text
/public
    favicon.ico
/src
    /components
        /common
            /button
                /__tests__
                    Button.spec.tsx
                Button.tsx
        /auth
            /__tests__
                AuthForm.test.tsx
            AuthForm.tsx
        /[Name]
            [Name].tsx
            [Name].test.ts
    /hooks
    /types
    /utils
    /api
        /__tests__
            [HTTP_METHOD][Name]Api.spec.ts
        [HTTP_METHOD][Name]Api.ts
    /test
        /api
            authApi.spec.ts
        /pages
            index.test.tsx
    /pages
        /api
          /auth
              authApi.ts
        _app.tsx
        _document.tsx
        index.tsx
```

### Component

Use only **[Functional components](https://reactjs.org/docs/components-and-props.html#function-and-class-components)** with **[Hooks](https://reactjs.org/docs/hooks-intro.html)**

#### Ordering (Top - Bottom)

1. Dependencies importing part
2. Styled part
3. Interface and Type part
4. Component part
5. Exporting part

```ts
// /src/components/counter/Counter.tsx

import { useState } from 'react'
import styled from 'styled-components'

const CounterLabel = styled.span`
  font-size: 18px;
  font-weight: bold;
`

const Container = styled.div`
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
`

const SubContainer = styled.div`
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: row;
`

interface ICounterProps {
  title: string
}

const Counter = ({ title }: ICounterProps) => {
  const [count, setCount] = useState(0)

  return (
    <Container>
      <h3>{title}</h3>
      <CounterLabel>{count}</CounterLabel>
      <SubContainer>
        <button onClick={() => setCount(count + 1)}>Increase</button>
        <button onClick={() => setCount(count - 1)}>Decrease</button>
      </SubContainer>
    </Container>
  )
}

export default Counter
```

#### Exporting

If we want to export a single thing, use export default first. For many things use both export and export default.

```ts
export interface IExportingDetail {
  title: string
  index: number
}

const exportingDetail: IExportingDetail = {
  title: 'Hello',
  index: 0
}

export default exportingDetail
```

### Storage management

Please read the [Redux style guide](https://redux.js.org/style-guide/style-guide)

## Commenting

### TODO

If something needs to be changed or refactored later, add a `// TODO:` comment to indicate what the issue is.

### Refactoring

If you refactor code that has comments, please check afterward if the comments still make sense or need to be updated.

### Styling

No **!important** postfix, for more [information](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)

No need to create new **classname**, please use [styled-components](https://styled-components.com) instead. Except the [tailwindcss](https://tailwindcss.com)

## Testing

Paste every test file into `__tests__` folder at the sibling layer of the code.

```text
/src
    /components
        /button
            /__tests__
                Button.spec.tsx
            Button.tsx
    /apis
        /__tests__
            getUserStatus.spec.ts
        getUserStatus.ts
```

The testing structure and lifecycle must align with [Jest guideline](https://jestjs.io/docs/setup-teardown).

Naming of test cases should start with **should** because Jest implements it function to make everyone read easier. We read a test case below as **it clicking the purchase button normally**.

```ts
describe('purchase page', () => {
  beforeAll(() => {
    ...
  })
  
  afterEach(() => {
    ...
  })
  
  it('should clicking the purchase button normally', () => {
    ...
  });
});
```

## Standpoint

**Always separate Logic From Configuration**
Write code that is **reusable**, **scalable**, and **testable**.

### Do not repeat yourself (DRY)

- Do not copy code to another place.
- Avoid using the same string twice in a project.
- Move shared logic to a shared place.
- Make sure you do not have to adapt changes in multiple places.

### Do not use Magic Numbers

See [Magic number programming](https://en.wikipedia.org/wiki/Magic_number_(programming))
