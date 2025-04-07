
# Trace Implementation GOLANG




## Content
- Importing the Trace package from GitHub
- Intialise the Trace function(StartTracing()) in Main function
- Intialisation of Trace's and Span's in HTTP Handlers

## Importing the Trace package from GitHub

Create go mod file (It Contains all dependencies)

```
go mod init <your-folder>
```

Execute the below command in you termimal

```
go get github.com/Guruvamshi14/Trace-Implementation-GOLANG
```
Include this command in main function
```
import trace "github.com/Guruvamshi14/Trace-Implementation-GOLANG"
```
## Intialise the Trace function (Start-Tracing) in Main Function

Include this in Mian function

```
tp, err := trace.StartTracing()
	if err != nil {
		log.Fatalf("failed to initialize tracing: %v", err)
	}
	defer func() {
		if err := tp.Shutdown(context.Background()); err != nil {
			log.Fatalf("failed to shutdown tracer provider: %v", err)
		}
	}()

```

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

## compile 
```
go build .
```

## run
```
go run .
```

## Reference 
If you have any doubts about initializing a trace or span, you can refer to the mini project on tracing in Go.

[GOLANG Mini Project](https://github.com/Guruvamshi14/GOLANG-Mini-Project-trace-Application)
