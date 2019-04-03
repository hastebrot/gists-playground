## m001. Pure components

#### `file-0.js`

```js
import React, { Fragment, useEffect, useState } from "react"

export default () => {
  return (
    <Fragment>
      <StatefulClassComponent />
      <StatefulFunctionalComponent />
    </Fragment>
  )
}
```

#### `file-1.js`

```js
export class ClassComponent extends React.Component {
  render() {
    console.log("render:", this.props.name, this.props.value)
    return <div>{this.props.value}</div>
  }
}

export class PureClassComponent extends React.PureComponent {
  render() {
    console.log("render:", this.props.name, this.props.value)
    return <div>{this.props.value}</div>
  }
}

export class StatefulClassComponent extends React.Component {
  state = {
    fastValue: "a",
    slowValue: "z",
  }

  componentDidMount() {
    this.setState(state => ({ ...state, fastValue: "aaa" }))
  }

  render() {
    return (
      <Fragment>
        <ClassComponent name="class-fast" value={this.state.fastValue} />
        <ClassComponent name="class-slow" value={this.state.slowValue} />
        <PureClassComponent
          name="pureclass-fast"
          value={this.state.fastValue}
        />
        <PureClassComponent
          name="pureclass-slow"
          value={this.state.slowValue}
        />
      </Fragment>
    )
  }
}
```

#### `file-2.js`

```js
export const FunctionalComponent = props => {
  console.log("render:", props.name, props.value)
  return <div>{props.value}</div>
}

export const PureFunctionalComponent = React.memo(props => {
  console.log("render:", props.name, props.value)
  return <div>{props.value}</div>
})

export const StatefulFunctionalComponent = props => {
  const [fastValue, setFastValue] = useState("a")
  const [slowValue, setSlowValue] = useState("z")

  useEffect(() => {
    setFastValue("aaa")
  }, [])

  return (
    <Fragment>
      <FunctionalComponent name="fun-fast" value={fastValue} />
      <FunctionalComponent name="fun-slow" value={slowValue} />
      <PureFunctionalComponent name="purefun-fast" value={fastValue} />
      <PureFunctionalComponent name="purefun-slow" value={slowValue} />
    </Fragment>
  )
}
```
