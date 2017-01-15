# ducks-helpers
Utils for ducks in redux

Api is not stable. You can use some ideas in your projects.
`constants()` - generates constants, however if `~` sign presents at the beginning then extra sufixes will be generated

```
import {constants} from 'ducks-helpers'
```

```
export const TYPE = constants('module-name/namespace', [
	'~GET_NOTE', //it will create GET_NOTE, GET_NOTE_LOADING, ...
	'NORMAL_ACTION' //it will create only itself
])
```

```
import {actions} from 'ducks-helpers'
export const ACTION = actions(TYPE)
//it will create getNote, getNoteLoading using redux-actions
```


```
import {loading, success, error} from 'ducks-helpers'

//if you have
const INITIAL_STATE = {
    loading: false,
    error: null,
    payload: {} //- then you can simplify reducer
}


export default function reducer(state = INITIAL_STATE, action = {}) {
	switch (action.type) {
		// do reducer stuff
		case TYPE.GET_NOTES:
			return loading(state,action)
		case TYPE.GET_NOTES_SUCCESS:
			return success(state,action)
		case TYPE.GET_NOTES_ERROR:
			return error(state, action)
```
