## m000. Subscribe to useState hooks

#### `file-0.js`

```js
import React, { Fragment, useState, useEffect } from "react"

// this is similar to react's render().
export default () => {
  const [state, setState] = useState({ count: 1 })

  // this is similar to react's componentDidMount().
  useEffect(() => {
    setState({ count: 2 })
    timeout(500, () => {
      setState({ count: 3 })
    })
  }, [])

  // this is similar to redux's store.subscribe(() => store.getState()).
  useEffect(() => {
    console.log("state changed:", state)
  }, [state])

  return <Fragment>{state.count}</Fragment>
}

const timeout = (durationMillis, action) => {
  return setTimeout(action, durationMillis)
}

// OUTPUTS:
// state changed: Object { count: 1 }
// state changed: Object { count: 2 }
// state changed: Object { count: 3 }
```
