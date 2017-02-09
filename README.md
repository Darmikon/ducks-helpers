# ducks-helpers
Utils for [ducks](https://github.com/erikras/ducks-modular-redux) in redux to create action types and actions creators

###Installation
```
npm i --save ducks-helpers
```

###`constants(namespace, actions)`
`constants()` - generates action types names
If `~` sign presents at the beginning of the string
then extra sufixes will be generated:
```
//SUFFIXES
[
    'LOADING',
    'PENDING',
    'SUCCESS',
    'ERROR',
    'FAILED',
    'CANCELED'
]
```

How to use:
```
import {constants} from 'ducks-helpers'
export const TYPE = constants('module-name/namespace', [
    '~ASYNC_ACTION',
    'SYNC_ACTION'
])
```

Result:
```
// with ~
// TYPE.ASYNC_ACTION === 'module-name/namespace/ASYNC_ACTION'
// TYPE.ASYNC_ACTION_SUCCESS === 'module-name/namespace/ASYNC_ACTION_SUCCESS'
//...
// TYPE.ASYNC_ACTION_CANCELED === 'module-name/namespace/ASYNC_ACTION_CANCELED'

// without ~
// TYPE.SYNC_ACTION === 'module-name/namespace/SYNC_ACTION'
```

Using handleActions() from [redux-actions](https://github.com/acdlite/redux-actions#handleactionsreducermap-defaultstate)
```
// reducer
export default handleActions({
    [TYPE.SYNC_ACTION]: (state, action) => state,
    [TYPE.ASYNC_ACTION]: (state, action) => state,
    [TYPE.ASYNC_ACTION_LOADING]: (state, action) => state,
    //... other suffixes also are available and can be used
    [TYPE.ASYNC_ACTION_SUCCESS]: (state, action) => state,
    [TYPE.ASYNC_ACTION_ERROR]: (state, action) => state,
}, {})
```


###`actions(types)`

`types` is an array of constants.
In case of using `~` sign at the beginning of action name
it will also create action creators with suffixes
`syncAction`,
`asyncAction`,
`asyncActionLoading`,
`asyncActionPending`,
`asyncActionCanceled`,
`asyncActionError`,
`asyncActionFailed`
using redux-actions:
```
import {actions} from 'ducks-helpers'
export const ACTION = actions(TYPE)
```

All action creators have been built now.
You can use any action creators in your container.

```
// container.js
import { ACTION } from '../duck'
...
@connect(
    ...,
    {
        asyncAction: ACTION.asyncAction
    }

)
...

componentWillMount(){
    this.props.asyncAction()
}

...
```