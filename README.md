# model-decorator

<div align="center">

[![npm version](https://badge.fury.io/js/model-decorator.svg)](https://badge.fury.io/js/model-decorator)
[![dependencies Status](https://david-dm.org/d9767192/model-decorator/master/status.svg)](https://david-dm.org/d9767192/model-decorator/master)
[![devDependencies Status](https://david-dm.org/d9767192/model-decorator/master/dev-status.svg)](https://david-dm.org/d9767192/model-decorator/master?type=dev)
[![download](https://img.shields.io/npm/dt/model-decorator.svg?style=flat)](https://npmcharts.com/compare/model-decorator)
[![License](https://img.shields.io/npm/l/model-decorator.svg)](https://github.com/d9767192/model-decorator/blob/master/LICENSE)


</div>

> Better model, better life

The major mission of model-decorator is to solve the data validation problem. Validating input data from user has always been a challenging task for web developer. One way to achieve this goal is to write validation codes in business logic. However, it would make your codes more complex and hard to maintain. Another solution is to use some components which already implemented validation mechanism. This way would loss some elasticity (For example, styles, features limitation etc).

model-decorator offers a lightweight method to solve this problem. All you need to do is to write viewmodel with validation decorators. Besides, you have largely elasticity to decide how to show your error message and components.

## Installation

model-decorator is available from npm:

```npm install model-decorator --save```

## Usage

Here is a quick example to get you started, it's all you need:

View model construction
```javascript
import { DefineProps, Type, DisplayName, StringLen, BaseModel } from 'model-decorator';

class SimpleModel extends BaseModel {
  @DefineProps()
  @DisplayName('User Name: ')
  @Type(PropTypes.string, { errorMessage: 'Error type of name. It should be string' })
  @StringLen([, 5], { errorMessage: 'Exceed max length 5 of name' })
  name
}

export default SimpleModel;
```

In your component
```javascript
import { ViewModel } from 'model-decorator';

@ViewModel(SimpleModel)
class Answer extends Component {
  render() {
    const { name } = this.props.model;
    return (
      <div>
        <div>
          <label htmlFor="name">
            <span>{name.title}</span>
            <input name="name" value={name.val} readOnly />
            <span>{name.err}</span>
          </label>
        </div>
      </div>
    );
  }
}
```
That's all!

## Examples

You can find more examples in our demo pages: [Click Me](https://d9767192.github.io/model-decorator/dist/#/)

Furthermore, there is a codepen playground. You can try anything if you want: [Click Me](https://codepen.io/d9767192/pen/xWZYmN)

## Setting of ES7 Decorator

Because decorator is a modern feature in ES7, the browser compatibility is still not so powerful. Therefore, we need to turn to babel. In Babel 7, the decorator feature is the default plugin in stage-0. You will need to include it as:

.babelrc
```
{
  "presets": [
    "env",
    "stage-0"
  ]
}
```

Besides, we also need plugin `transform-decorators-legacy` to transfer `@` syntax (If you are wonder why it is legacy, you can check its repo and there is an explaination: [Click Me](https://github.com/loganfsmyth/babel-plugin-transform-decorators-legacy))

```
{
  "presets": [
    "env",
    "stage-0"
  ],
  "plugins": [
    "transform-decorators-legacy",
    "transform-class-properties"
  ]
}
```

* It should be noticed that `transform-decorators-legacy` must ahead of `transform-class-properties`

## Documentation

Check out our [Documentation page](https://github.com/d9767192/model-decorator/blob/master/docs/api.md)

## License

This project is licensed under the terms of the [MIT license](https://github.com/d9767192/model-decorator/blob/master/LICENSE)
