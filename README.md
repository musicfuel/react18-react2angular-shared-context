# react2angular-shared-context

> Share context between React components in react2angular.
> <b>This version can be used with React 18</b>

[![NPM](https://img.shields.io/npm/v/react18-react2angular-shared-context.svg)](https://www.npmjs.com/package/react18-react2angular-shared-context) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

## Install

```bash
npm install --save react18-react2angular-shared-context
```

## Usage

```tsx
import { react2angular } from 'react2angular';
import React, { FunctionComponent } from 'react'
import { ProviderAbc, ConsumerAbc } from './context/abc'

import createSharedContext from 'react18-react2angular-shared-context'

// Root component with context providers
const Root: FunctionComponent<{foo: number}> = ({foo, children}) => (
  <ProviderAbc foo={foo}>
      {children}
  </ProviderAbc>
);

// Example component that consumes providers defined in Root component
const MyExample: FunctionComponent<{bar: string}> = ({bar}) => (
  <ConsumerAbc>
    {({a, b, c}) => <p>{bar} says: {a} x {b} = {c}</p>}
  </ConsumerAbc>
);

// Create shared context instance
const sharedContext = createSharedContext(Root);

// Define shared context component first
// This component can be optionally wrapped in react-hot-loader
angular
  .module('example')
  .component('sharedContextReact', react2angular(sharedContext.component, ['foo']));

// Wrap example component with shared context
// Do not wrap this component with react-hot-loader because the shared context instance will already handle this
angular
  .module('example')
  .component('myExampleReact', react2angular(sharedContext.use(MyExample), ['bar']));
```

## License

MIT © [https://github.com/musicfuel](https://github.com/musicfuel)
