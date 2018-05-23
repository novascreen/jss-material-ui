# jss-material-ui
Provide seamless components styling to material-ui

# Introduction
Material-ui 1.0 is a great react library, but its css to jss styling could be enhanced.


# Drawback of the styling provided by material-ui

* doesn't support props
* Styles are applied globally resulting to a lot of warning for the styles not maching the processed component


# The solutions until now to resolve these problems
Some suggest to use styled libraries like styled-component, glamorous, emotion, ... to resove these problems

They resolve it, but two new problems arrive: 

* stylesheet priorisation. 
* two css engines on the system which provide more complexity for the app


# A new small styled libray
So I decided to develop a library with the folowing objective:

* use material-ui styling system, so compatibiity is 100%
* more component oriented
* provide props


# A little sample

## without props


```js
import style from 'jss-material-ui'

// a container style
const ContainerRoot = style(Paper)({
  containerRoot: {
    width: '100%',
    marginTop: 3,
    overflowX: 'auto'
  }
})

// container use
<ContainerRoot />
```

The first style is always applied to the styled component, ```containerRoot``` on the sample.
If you don't have style to pass to the component, you can write 

```js
root: {}
```

You can pass styles to subcomponents. In that case  ```classes``` props must be transmit to the subcomponents. material-ui do that for of of them: header of a table for example. else you'll have to do it.

```js
import style from 'jss-material-ui'

// a container style
const STable = style(Table)((theme, props) => {
  root: {},
  theader: {
    visibility: 'hidden',
  },
  tbody: {
    height: props.height
  }
})
```


## with props

```js
import style from 'styled'
import TableCell from '@material-ui/core/TableCell'

const CaloriesCell = style(TableCell)((theme, {calories}) => ({
  calories: {
    fontWeight: calories > 300 ? 700 : undefined,
    backgroundColor: calories > 300 ? '#ff0000' : calories < 160 ? '#00FF00' : undefined
  }
}))

// use
<CaloriesCell calories={n.calories} numeric>{n.calories}</CaloriesCell>
```

![Result](./stories/jss.png)




## Custom props

Its also possible to use custom props

```js
style(TableCell, {
     myCustomProps1,
     myCustomProps2
   })
   ((theme, {calories})
```


## Class inherithance

If a child B of a component A has for className :

```js
<A>
   <B className={classes.classB} />
</A>
```

Its possible to write that:

```js
const SA = style(A)((theme, props) => ({
  styleForA: {
    ...
  },
  classB: {
    ...
  }
}))
```

The style specified in the ```classB``` object will be applied to B class component.
Check ```stories/SimpleTableInherit.js```


## more samples

Check ./stories directory for complete sample files.

New samples files will arrive soon.
Keep in mind the styling system is compatible with material-ui styling

New samples will come soon.
