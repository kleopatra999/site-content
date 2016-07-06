+++
Categories = ["Learning"]
Tags = ["cayley", "graph", "library"]
date = "2016-07-04T01:25:28Z"
title = "Cayley as a Library"

+++

Currently, Cayley supports being used as a Go library for other projects. To use it in such a way, here's a quick example:

```go
package main

import (
  "log"

  "github.com/google/cayley"
)

func main() {
  store, err := cayley.NewMemoryGraph()
  if err != nil {
    log.Fatalln(err)
  }
  store.AddQuad(cayley.Quad("food", "is", "good", ""))
  p := cayley.StartPath(store, "food").Out("is")
  it := p.BuildIterator()
  for cayley.RawNext(it) {
    log.Println(store.NameOf(it.Result()))
  }
}
```

To use other backends, you can empty-import them, eg

```go
import _ "github.com/google/cayley/graph/bolt"
```

And use them with a call like

```go
import "github.com/google/cayley/graph"

func open() {
  // Initialize the database
  graph.InitQuadStore("bolt", path, nil)

  // Open and use the database
  cayley.NewGraph("bolt", path, nil)
}
```

----

Comments: https://discourse.cayley.io/t/quickstart-cayley-as-a-library/36
