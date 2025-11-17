---
up:
  - "[[Golang]]"
related: "[[json]]"
created: 2025-05-15
in:
  - "[[LexMechanica]]"
---
```go
package main

import (
	"encoding/json"
	"fmt"
	"strings"
	"time"
)

const input = `
{
  "id": "caa8ecf6-570c-45c9-82a4-368fd69f27c5",
  "request_time": "2025-05-15T06:35:51.374554177Z",
  "task_number": "TASK0913767",
  "device_type": "Unity",
  "result": {
    "info": {
      "platform_type": "Unity 380",
      "serial_number": "CKM01214305387",
      "mgmt_address": "192.168.194.103",
      "disk_count": 0,
      "hostname": "CKM01214305387"
    },
    "bbu": {
        "serial_number": "bbu1234",
        "status": "ok"
    }
  }
}
`

type Result struct {
	ParseRequest
	Result any
}

type ParseRequest struct {
	ID          string    `json:"id"`
	RequestTime time.Time `json:"request_time"`
	TaskNumber  string    `json:"task_number"`
	DeviceType  string    `json:"device_type"`
}

type Unity struct {
	Info ArrayInfo `json:"info"`
	BBU  BBU       `json:"bbu"`
}

type ArrayInfo struct {
	PlatformType string `json:"platform_type"`
	SerialNumber string `json:"serial_number"`
	MGMTAddress  string `json:"mgmt_address"`
	DiskCount    int    `json:"disk_count"`
	Hostname     string `json:"hostname"`
}

type BBU struct {
	SerialNumber string `json:"serial_number"`
	Status       string `json:"status"`
}

type ParseResult interface {
	Type() string
}

var kindHandlers = map[string]func() ParseResult{
	"unity": func() ParseResult { return &Unity{} },
}

func main() {
	var raw json.RawMessage
	r := Result{
		Result: &raw,
	}

	if err := json.Unmarshal([]byte(input), &r); err != nil {
		fmt.Println("error: %v", err)
	}

	deviceType := strings.ToLower(r.ParseRequest.DeviceType)
	if factory, ok := kindHandlers[deviceType]; ok {
		msg := factory()
		if err := json.Unmarshal(raw, &msg); err != nil {
			fmt.Println("error 2: ", err)
			return
		}
		r.Result = msg
		DoStuff(r)
	}
}

func DoStuff(r Result) {
	if t, ok := r.Result.(*Unity); ok {
		fmt.Println(t.Info)
		fmt.Println(t.BBU)
	}
}
```