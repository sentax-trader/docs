
# log
logs are one of the most important things with development and debugging. easily log anything with `log()` function.
### example:
- ```log('hello mars!')```
- ```log(7)```
- ```log(x)```


# define
define sxcript type and define some `interProps`
### example:
- ```define('indicator')```
- ```define('condition')```
- ```define('indicator',{drawSection:'subWindow'})```
- ```define('indicator',{drawSection:'overlay'})```
- ```define('pattern')```

# Include
includes prebuilt tools to your sxcript
```Include(string name)```

### name struct :
- name of entity as string
- lib://[`lib name`]
### example :
 - ```const ohlc = Include('OHLC')```
 - ```const ta = Include('lib://ta')```
 - ```const plot = Include('Plot')```
 
 ** [linkTo] defines.md/include entities


# Import
import other sxcipts into your sxcript and use them results.\
`Import(string url)`\
## url protocols
struct = `[storage type]://[id or alias]`
- storage types: `st` as user storage, and `sst` as global secure storage
- you may not have `sst` access in some cases

 ### examples:
 - ```const RSI = await Import('sst://@indicator/rsi')```
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
`Input(any defaultValue, string title, string type,[meta])`

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
this is refereced to currently running sxcript and contains some sort of details and methods

## this.onInit(`Function` callback)
this callback runs when:
- timeFrame changes
- selected pair changes
- any input has been changed
### example:
- `this.onInit(()=>{ this.ready(buffer) })`

## this.ready(`Buffer` buffer)
every sxcipt should emit its own ready state with `this.ready` method.
 
## this.onReady(`Function` callback)
after callcing `this.ready` ,`onReady` event would be handled and accessible via `onReady` event

### example:
- `this.onReady(()=>{})`

# OHLC
any market data would be available with `OHLC` struct.
### entities
- `length`
- `pair`
- `tf`
### example
- `ohlc.pair`
- `ohlc.length`
### entities per index:
- `open`
- `high`
- `low`
- `close`
- `volume`
- `date`
### example:
- `ohlc[1].open`
- `ohlc[10].close`

**data sort is reversed (`0` is newer index)
# Plot
plot allows your sxcript to interact with chart, and draw `lines`, `bars`,`shapes` and `fill` them with colors.  

plot object is available after `Include`

`const plot = Include('Plot')` 
## Plot.series(`Buffer buffer`,[object props])
draw lines with `series`
### example:
- `plot.series(buffer,{lineMode:'Dot'})`
- `plot.series(buffer,{color:'red'})`
- `plot.series(buffer,{color:'#FF0000',lineMode:'Dot'})`

### props:
- `string` lineMode [linkTo]line mode types
- `string` color [linkTo]color mode types

## Plot.bars(`Buffer buffer`,[Buffer buffer2,object props])
drawing bars are available with `bars`
### example:
- `plot.bars(buffer,{color:'pink'})`
- `plot.bars(buffer1,buffer2,{color:'red'})`
- `plot.bars(buffer1,buffer2)`

### props:
- `string` color [linkTo]color mode types
## Plot.fill(`Buffer buffer`,[Buffer buffer2,object props])
`fill` between one or two points with defined color
### example: 
- `plot.fill(buffer,{color:'red'})`
- `plot.fill(buffer1, buffer2,{color:'red'})`

** if second buffer was not defined, `0` would be used by default as second buffer
### props:
- `string` color [linkTo]color mode types

## Plot.shape(`String shape`,`Buffer buffer`,[object props])
plotting shapes on the chart with `shape` method
[linkTo]available shapes
### example:
- `plot.shape('circle',buffer)`

### props:
- `string` color [linkTo]color mode types

