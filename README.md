# react-opentracing

Trace the React lifecycle methods of the wrapped component and gain insights on where the performance bottlenecks in your application are.

## Requirements

- The [Opentracing client](https://github.com/opentracing/opentracing-javascript) needs set up. Tracer implementations you may use:
  - [costacruise/zipkin-javascript-opentracing](https://github.com/costacruise/zipkin-javascript-opentracing)
- The global tracer needs to be set with `opentracing.initGlobalTracer`, this one will be used.

## Usage


```js
import React from 'react';
import traceComponentLifecycle from 'react-opentracing';

class Example extends React.Component {
  constructor(props) {
    super(props);
    // Logic
  }

  componentDidMount() {
    // Logic
  }
  
  componentWillUpdate(){
    // Logic
  }
  
  componentDidUpdate(){
    // Logic
  }

  componentWillUnmount() {
    // Logic
  }

  render() {
    // Logic
  }
}

export default traceComponentLifecycle({
  name: 'MyExampleComponent',
  track: [
    'constuctor',
    'mount',
    'update',
    'render',
    'unmount',
  ],
})(Example);
```

### Configuration

- **name**(*string*): the prefix for the spanName
- **track**(*Array<string>*): opt-in in what to trace specifically
  - **constructor**, **mount**, **unmount**, **render**: tracks time from start to end that the function takes
  - **update**: tracks time from beginning of `componentWillUpdate` to the end of `componentDidUpdate`
  
## Contributing

Please see the [contribution guide](./CONTRIBUTING.md)
