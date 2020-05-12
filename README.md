# Martian modifier

Read about Krakend martian: 
https://www.krakend.io/docs/backends/martian/

`Krakend-martian` provides `body-modifier` to replace whole body for outbound requests (for endpoint)
And you have to provide body as base64 encoded in `krakend.json` 

eg: 

Below is json configurations provided by body-modifier

```json
{ 
  "body.Modifier": {
      "scope": ["request", "response"],
      "contentType": "text/plain",
      "body": "c29tZSBkYXRhIHdpdGggACBhbmQg77u/"
    }
}
```

### jsonbody modifier

This modifier that is written to append extra body params other than body parameter that is getting forwarded from inbound request.  

```json
{
    "newjsonbody.Modifier": {
      "body": "{\"origin_service\": \"my-application\", \"source\": \"mobile-app\"}",
      "scope": ["request"]
    }
}
```

### How to use.

```go
import (
    martian "github.com/devopsfaith/krakend-martian"
    _     "github.com/sathia27/martian_jsonbody"
)
 
martianBackendFactory := martian.NewBackendFactory(logger, krakendClient.DefaultHTTPRequestExecutor(krakendClient.NewHTTPClient))
factory := proxy.NewDefaultFactory(martianBackendFactory, logger)
routerFactory := krakendgin.NewFactory(krakendgin.Config{
    Engine:         engine,
    ProxyFactory:   factory,
    Logger:         logger,
    RunServer:      router.RunServer,
})
``` 