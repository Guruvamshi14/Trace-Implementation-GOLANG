
## Intialisation of Trace's and Span's in HTTP handlers

Execute the command in you termimal

```
go get go.opentelemetry.io/otel
```
Include this command in HTTP handlers at top of the file

```
import "go.opentelemetry.io/otel"
```

Intialisation of Trace Function

```
tracer := otel.Tracer("Handler-Name")
```

Span Tag (Create a parent Span)
```
ctx, parentSpan := tracer.Start(r.Context(), "Handler-Name")
defer parentSpan.End()
```

Child span(ctx is passed as parameter, so that every span will have same trace ID)
```
_, span1 := tracer.Start(ctx, "span-name1")
defer span1.End()
_, span2 := tracer.Start(ctx, "span-name2")
defer span2.End()
```

## Docker Command  to Export the Telemetry-data to Jeager

```
docker run --rm --name jaeger \
  -e COLLECTOR_ZIPKIN_HTTP_PORT=9411 \
  -p 16686:16686 \
  -p 4318:4318 \
  jaegertracing/all-in-one:1.56

```

## Compile 
```
go build .
```

## Run
```
go run .
```

## Reference 
If you have any doubts about initializing a trace or span, you can refer to the mini project on tracing in Go.

[GOLANG Mini Project](https://github.com/Guruvamshi14/GOLANG-Mini-Project-trace-Application)

