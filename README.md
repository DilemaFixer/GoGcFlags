# Go Flags

``-m`` - Escape analysis

```
go build -gcflags="-m" main.go
go build -gcflags="-m -m" main.go  # more details
```
will show 

```
./main.go:9:2: moved to heap: result
./main.go:12:13: make([]int, n) escapes to heap
```

``-S`` - Assembly code

``` 
go build -gcflags="-S" main.go
```
Shows the generated assembler - useful for understanding performance.

``-N -l`` - Disable optimization

```
go build -gcflags="-N -l" main.go
```
``-N`` - disable optimizations
``-l`` - disable inlining

## Base setup

```
# 1. Basic analysis
go build -gcflags="-m" main.go

# 2. If there are performance issues
go build -gcflags="-m -m -S" main.go > analysis.txt

# 3. Optimized assembly
go build -ldflags="-s -w" -gcflags="-B" main.go

# 4. Profiling
go test -bench=. -cpuprofile=cpu.prof
go tool pprof cpu.prof
```


