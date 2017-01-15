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
