## Getting Started

### Install the handler

We first need to serve the probing HTTP handler.

```go
    http.HandleFunc("/health", probing.NewHandler())
    err := http.ListenAndServe(":12345", nil)
	if err != nil {
		log.Fatal("ListenAndServe: ", err)
	}
```

### Start to probe

Now we can start to probe the endpoint.

``` go
    id := "example"
    probingInterval = 5 * time.Second
    url := "http://example.com:12345/health"
    p.AddHTTP(id, probingInterval, url)

	time.Sleep(13 * time.Millisecond)
	status, err := p.Status(id)
    fmt.Printf("Total Probing: %d, Total Loss: %d, Estimated RTT: %v, Estimated Clock Difference: %v", status.Total(), status.Loss(), status.SRTT(), status.ClockDiff())
```

### TODOs:

- TCP probing
- UDP probing
- Gossip based probing
- More accurate RTT estimation
- More accurate Clock difference estimation
- Use a clock interface rather than the real clock
