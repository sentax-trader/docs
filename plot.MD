# Overview

# Plot
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

