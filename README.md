About
=====

Go bindings to radix tree library for fast subnet (IPv4 and IPv6) lookups.

Usage example
=============
```go

package main

import (
    "github.com/thekvs/go-net-radix"

    "fmt"
    "log"
)

func main() {
    rtree, err := netradix.NewNetRadixTree()
    if err != nil {
        panic(err)
    }
    defer rtree.Close()

    if err = rtree.Add("217.72.192.0/20", "UDATA1"); err != nil {
        log.Fatal(err)
    }

    if err = rtree.Add("2001:220::/35", "UDATA2"); err != nil {
        log.Fatal(err)
    }

    var found bool
    var udata string

    found, udata, err = rtree.SearchBest("217.72.192.2")
    if err != nil {
        log.Fatal(err)
    }
    if found {
        fmt.Printf("found: %v\n", udata)
    }

    found, udata, err = rtree.SearchBest("2001:220::")
    if err != nil {
        log.Fatal(err)
    }
    if found {
        fmt.Printf("found: %v\n", udata)
    }

    if err = rtree.Remove("217.72.192.0/20"); err != nil {
        log.Fatal(err)
    }
}

```

Licensing
=========

All source code included in this distribution is covered by the MIT License found in the LICENSE file,
unless specifically stated otherwise within each file.
