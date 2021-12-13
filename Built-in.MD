


# Include
includes prebuilt tools to your sxcript
`Include(string name)`
### example :
 - `const ohlc = Include('OHLC')`
 - `const ta = Include('lib://ta')`
 - `const plot = Include('Plot')`


# Import
import other sxcipts into your sxcript and use them results.\
`Import(string url)`\
## url protocols
struct = `[storage type]://[id or alias]`
- storage types: `st` as user storage, and `sst` as global secure storage
- you may not have `sst` access in some cases

 ### examples:
 - `const RSI = await Import('sst://@indicator/rsi')`
 - `const myCustom = await Import('st://6060d571eefefd13e8fe6beb')`
# Buffer
buffers are the only way that you could interact with chart or other sxcripts
### example:
- `const buffer = Buffer('myBuffer')`
## Buffer.set(`array` data)
set data into the buffer
- data should be an array
- **use `update` method for update `one` key in buffer
### example:
- `buffer.set([1,2,3,4])`
## Buffer.get(`int` key)
returns buffer value with the given key
### example:
- `buffer.get(10)`
## Buffer.update(`int` key,`any` value)
updates buffer key with the given value
### example:
- `buffer.update(10,1.681541)`
## Buffer.fit(`OHLC` ohlc)
buffers are forced to be in the same size of the ohlc data.
fit method helps you to keep your buffer fitted with given ohlc object.

# Input
Inputs are the variable that are accepts changes from outside of the sxcript.\
`Buffer(any defaultValue, string title, string type,[meta])`

** [linkTo] available input types
### example:
- `const period = Buffer(14,'Period','number')`

## Input.set(`any` data,[`object` props])
set given value into the input
- data type should be same as defined type
- **use `update` method for update `one` key in buffer
### example:
- `input.set(7)`
- `input.set('high',{rerun:false})`

** setting an input will take effect by `reIniting` the sxcript. setting `rerun` prop will override this action
## Input.bind(`Input` input)
binds an input to another input.
changing first input will change second input automatically.
### example:
- `input.bind(input2)`
# this


