Log [![GoDoc](https://godoc.org/github.com/raz-varren/log?status.svg)](https://godoc.org/github.com/raz-varren/log)
===

log is a more robust logging system that provides a standard logger, an ANSI color logger, and a JSON logger that all make use of log levels. This package used to exist under the [Sacrificial-Socket](https://github.com/raz-varren/sacrificial-socket) websocket package, but has since been broken out into it's own repository.

Examples
-----

#### Default Usage:
```go
package main

import "github.com/raz-varren/log"

func main(){
	log.Info.Println("white info log")
    log.Warn.Println("orange warn log")
    log.Err.Println("red error log")
    log.Debug.Println("blue debug log")
}
```

#### Change Default Logger:
```go
package main

import(
	"github.com/raz-varren/log"
   	"os"
)

func main(){
	//Some command consoles (like windows) can't use ANSI colors, 
    //or perhaps you want a different log level
    log.SetDefaultLogger(log.NewLogger(os.Stdout, log.LogLevelStd))
    
    log.Info.Println("plain info log")
    log.Warn.Println("plain warn log")
    log.Err.Println("plain error log")
    log.Debug.Println("no plain debug log")
}
```

#### Log to file:
```go
package main

import(
	"github.com/raz-varren/log"
	"os"
)

func main(){
	f, err := os.OpenFile("/tmp/test.log", os.O_WRONLY|os.O_CREATE|os.O_TRUNC, 0644)
	if err != nil {
		panic(err)
	}
	
	log.SetDefaultLogger(log.NewLogger(f, log.LogLevelDbg))
	log.Info.Println("file info log")
    log.Warn.Println("file warn log")
    log.Err.Println("file error log")
    log.Debug.Println("file debug log")
}
```
