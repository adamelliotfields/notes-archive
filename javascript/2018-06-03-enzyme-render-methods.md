# Enzyme Render Methods
> :calendar: _June 3, 2018_

This is a table I put together to document which methods are available on the `wrapper` returned
from the `shallow` and `mount` render methods.

### Shallow vs Mount

Shallow renders the outer-most component only, so it's very fast. Use this to unit-test individual
components.

```javascript
const Divider = ({ children }) => <div>{children}</div>;
const Heading = ({ text }) => <h1>{text}</h1>;

const wrapper = shallow(
  <Divider>
    <Heading text='hello world' />
  </Divider>
);

console.log(wrapper.debug());
```

```html
<div>
  <Heading text='hello world' />
</div>
```

Mount actually mounts the component to the DOM, so it renders the entire component tree, and you can
also spy on lifecycle methods.

```javascript
const Divider = ({ children }) => <div>{children}</div>;
const Heading = ({ text }) => <h1>{text}</h1>;

const wrapper = mount(
  <Divider>
    <Heading text='hello world' />
  </Divider>
);

console.log(wrapper.debug());
```

```html
<Divider>
  <div>
    <Heading text='hello world'>
      <h1>hello world</h1>
    </Heading>
  </div>
</Divider>
```

### Methods

| **API**                       | [`shallow`](http://airbnb.io/enzyme/docs/api/shallow.html) | [`mount`](http://airbnb.io/enzyme/docs/api/mount.html) |
|-------------------------------|------------------------------------------------------------|--------------------------------------------------------|
| `at`                          | :white_check_mark:                                         | :white_check_mark:                                     |
| `childAt`                     | :white_check_mark:                                         | :white_check_mark:                                     |
| `children`                    | :white_check_mark:                                         | :white_check_mark:                                     |
| `closest`                     | :white_check_mark:                                         | :white_check_mark:                                     |
| `contains`                    | :white_check_mark:                                         | :white_check_mark:                                     |
| `containsAllMatchingElements` | :white_check_mark:                                         | :white_check_mark:                                     |
| `containsAnyMatchingElements` | :white_check_mark:                                         | :white_check_mark:                                     |
| `containsMatchingElement`     | :white_check_mark:                                         | :white_check_mark:                                     |
| `context`                     | :white_check_mark:                                         | :white_check_mark:                                     |
| `debug`                       | :white_check_mark:                                         | :white_check_mark:                                     |
| `detach`                      |                                                            | :white_check_mark:                                     |
| `dive`                        | :white_check_mark:                                         |                                                        |
| `equals`                      | :white_check_mark:                                         |                                                        |
| `every`                       | :white_check_mark:                                         | :white_check_mark:                                     |
| `everyWhere`                  | :white_check_mark:                                         | :white_check_mark:                                     |
| `exists`                      | :white_check_mark:                                         | :white_check_mark:                                     |
| `filter`                      | :white_check_mark:                                         | :white_check_mark:                                     |
| `filterWhere`                 | :white_check_mark:                                         | :white_check_mark:                                     |
| `find`                        | :white_check_mark:                                         | :white_check_mark:                                     |
| `findWhere`                   | :white_check_mark:                                         | :white_check_mark:                                     |
| `first`                       | :white_check_mark:                                         | :white_check_mark:                                     |
| `forEach`                     | :white_check_mark:                                         | :white_check_mark:                                     |
| `get`                         | :white_check_mark:                                         | :white_check_mark:                                     |
| `hasClass`                    | :white_check_mark:                                         | :white_check_mark:                                     |
| `html`                        | :white_check_mark:                                         | :white_check_mark:                                     |
| `instance`                    | :white_check_mark:                                         | :white_check_mark:                                     |
| `is`                          | :white_check_mark:                                         | :white_check_mark:                                     |
| `isEmpty`                     | :white_check_mark:                                         | :white_check_mark:                                     |
| `key`                         | :white_check_mark:                                         | :white_check_mark:                                     |
| `last`                        | :white_check_mark:                                         | :white_check_mark:                                     |
| `map`                         | :white_check_mark:                                         | :white_check_mark:                                     |
| `matchesElement`              | :white_check_mark:                                         | :white_check_mark:                                     |
| `mount`                       |                                                            | :white_check_mark:                                     |
| `name`                        | :white_check_mark:                                         | :white_check_mark:                                     |
| `not`                         | :white_check_mark:                                         | :white_check_mark:                                     |
| `parent`                      | :white_check_mark:                                         | :white_check_mark:                                     |
| `parents`                     | :white_check_mark:                                         | :white_check_mark:                                     |
| `prop`                        | :white_check_mark:                                         | :white_check_mark:                                     |
| `props`                       | :white_check_mark:                                         | :white_check_mark:                                     |
| `reduce`                      | :white_check_mark:                                         | :white_check_mark:                                     |
| `reduceRight`                 | :white_check_mark:                                         | :white_check_mark:                                     |
| `ref`                         |                                                            | :white_check_mark:                                     |
| `render`                      | :white_check_mark:                                         | :white_check_mark:                                     |
| `setContext`                  | :white_check_mark:                                         | :white_check_mark:                                     |
| `setProps`                    | :white_check_mark:                                         | :white_check_mark:                                     |
| `setState`                    | :white_check_mark:                                         | :white_check_mark:                                     |
| `shallow`                     | :white_check_mark:                                         |                                                        |
| `simulate`                    | :white_check_mark:                                         | :white_check_mark:                                     |
| `slice`                       | :white_check_mark:                                         | :white_check_mark:                                     |
| `some`                        | :white_check_mark:                                         | :white_check_mark:                                     |
| `someWhere`                   | :white_check_mark:                                         | :white_check_mark:                                     |
| `state`                       | :white_check_mark:                                         | :white_check_mark:                                     |
| `tap`                         | :white_check_mark:                                         | :white_check_mark:                                     |
| `text`                        | :white_check_mark:                                         | :white_check_mark:                                     |
| `type`                        | :white_check_mark:                                         | :white_check_mark:                                     |
| `unmount`                     | :white_check_mark:                                         | :white_check_mark:                                     |
| `update`                      | :white_check_mark:                                         | :white_check_mark:                                     |
