# Cod

An unopinionated documentation generator.

<p align="center">
  <img src="http://i.imgur.com/Owgsb3R.jpg"/>
</p>

(NOTE: Cod is currently just a concept; development is in-progress)

### Concept/Example

Cod infers the structure and meaning of your documentation's tags as they are parsed,
allowing for an arbitrary structure.

```coffee
###
@Rectangle
  @extends Shape
  A four-sided shape with all right angles.
###
class Rectangle extends Shape
  ###
  @Rectangle:method area
    Get the area of this rectangle.
    @return
      The area of this rectangle.
      @type Number
  ###
  area: -> return @width * @height
  
###
@Rectangle:mixins Scalable
###
mixin(Rectangle, Scalable)

###
@Rectangle:mixins Movable
###
mixin(Rectangle, Movable)
```

```js
{
  "Rectangle": {
    "!body": "A four-sided shape with all right angles.",
    "extends": "Shape",
    "mixins": ["Scalable", "Movable"],
    "method": {
      "area": {
        "!body": "Get the area of this rectangle.",
        "return": {
          "!body": "The area of this rectangle.",
          "type": "Number"
        }
      }
    }
  },
  "Shape": /* ... */,
  "Scalable": /* ... */,
  "Movable": /* ... */
}
```

### How the structure is created.
```
@Rectangle
```

```js
{
  "Rectangle": true
}
```

-----

```
@Rectangle
  @extends Shape
  A four-sided shape with all right angles.
```

```js
{
  "Rectangle": {
    "!body": "A four-sided shape with all right angles."
    "extends": "Shape"
  }
}
```

-----

```
@Rectangle
  @extends Shape
  A four-sided shape with all right angles.

@Rectangle:method:area
```

```js
{
  "Rectangle": {
    "!body": "A four-sided shape with all right angles."
    "extends": "Shape",
    "method": {
      "area": true
    }
  }
}
```

-----


```
@Rectangle
  @extends Shape
  A four-sided shape with all right angles.

@Rectangle:method area
```

```js
{
  "Rectangle": {
    "!body": "A four-sided shape with all right angles."
    "extends": "Shape",
    "method": "area"
  }
}
```

-----

```
@Rectangle
  @extends Shape
  A four-sided shape with all right angles.

@Rectangle:method area
  Get the area of this rectangle.
  @return
    The area of this rectangle.
    @type Number

```

```js
{
  "Rectangle": {
    "!body": "A four-sided shape with all right angles."
    "extends": "Shape",
    "method": {
      "area": {
        "!body": "Get the area of this rectangle.",
        "return": {
          "!body": "The area of this rectangle.",
          "type": "Number"
        }
      }
    }
  }
}
```

-----

```
@Rectangle
  @extends Shape
  A four-sided shape with all right angles.

@Rectangle:method area
  Get the area of this rectangle.
  @return
    The area of this rectangle.
    @type Number

@Rectangle:mixin Scalable

```

```js
{
  "Rectangle": {
    "!body": "A four-sided shape with all right angles."
    "extends": "Shape",
    "method": {
      "area": {
        "!body": "Get the area of this rectangle.",
        "return": {
          "!body": "The area of this rectangle.",
          "type": "Number"
        }
      }
    },
    "mixin": "Scalable"
  }
}
```

-----

```
@Rectangle
  @extends Shape
  A four-sided shape with all right angles.

@Rectangle:method area
  Get the area of this rectangle.
  @return
    The area of this rectangle.
    @type Number

@Rectangle:mixin Scalable
@Rectangle:mixin Movable

```

```js
{
  "Rectangle": {
    "!body": "A four-sided shape with all right angles."
    "extends": "Shape",
    "method": {
      "area": {
        "!body": "Get the area of this rectangle.",
        "return": {
          "!body": "The area of this rectangle.",
          "type": "Number"
        }
      }
    },
    "mixin": ["Scalable", "Movable"]
  }
}
```
