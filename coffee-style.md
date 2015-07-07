# FactoryX CoffeeScript Style guide


## Functions

Clean, concise, modular.

Should only have 1-3 arguments.

**Wrong:**
```coffee-script
test = (user, newAge, id, cb) ->
  # ...

```
**Right:**
```
test = (opts, cb) ->
  # ...

```

Reduce the number of variable created in a function by using coffee-script argument reducers:


**Wrong:**
```coffee-script
test = (args) ->
  res = args.res
  body = args.body

```

**Right**
```coffee-script
test = ({res, body}) ->

```

Function names should not be intensely long. Use the shortest name that fulfills the meaning.

Use `getUser` instead of `getOneUserProfile` and `getUsers` instead of `getAllUserProfiles`


**Use short returns**

**Wrong:**
```coffee-script
module.exports = (req, res, next) ->

  if req.user?
    # ... do something as user
  else if req.headers.admin is 'admin' and req.user?
    # ... do something as admin
  else
    next()
  next()

```

**Right**
```coffee-script
module.exports = (req, res, next) ->

  return next() unless req.user?
  if req.headers.admin is 'admin'
    # ... do something as admin
    return next()
  # ... do something as user
  next()

```

## Write clean functions

**Wrong:**
```coffee-script

module.exports = (type, opts, cb) ->

  if type is 'admin'
    data = # ... something
    return cb(null, data)

  if type is 'user'
    data = # ... something
    return cb(null, data)

  if type is 'moderator'
    data = # ... something
    return cb(null, data)

```

***Right***
```coffee-script
module.exports =
  admin: (opts, cb) ->
    # ...
  user: (opts, cb) ->
    # ...
  moderator: (opts, cb) ->
    # ...
```


## WIP
