```sh
panic: runtime error: invalid memory address or nil pointer dereference
[signal SIGSEGV: segmentation violation code=0x1 addr=0x0 pc=0x55822f]

goroutine 65 [running]:
triage/internal/emcparser/vnxetype.(*SefParser).merge(0x7f2a60?, 0xc0001d3200, 0xc00006c3c0)

/app/internal/emcparser/vnxetype/sef-parser.go:97 +0x1ef
triage/internal/emcparser/vnxetype.(*SefParser).wait(0xc00000e138, {0x8f9640, 0xc00028a2a0})

/app/internal/emcparser/vnxetype/sef-parser.go:78 +0x325
triage/internal/emcparser/vnxetype.Parser.Parse({}, {0x8f9640, 0xc00028a2a0}, {0xc0000e6000, 0x39})
/app/internal/emcparser/vnxetype/parser.go:19 +0xe5

triage/internal/emcparser.(*parser).Parse(0xc000182970, {0x8f9640, 0xc00028a2a0}, {0xc0000e6000, 0x39}, {0xc000098780, 0x8})
/app/internal/emcparser/parser.go:77 +0x497

triage/internal/worker.(*Worker).Process(0xc0001d2ea0, {0x8f9598, 0xc000092cc0}, {{0xc00008e090, 0x24}, {0x3d198fc, 0xee03a6353, 0x0}, {0xc000098762, 0xb}, ...})
/app/internal/worker/worker.go:85 +0x2b1

triage/internal/handler/rabbitmq.(*Consumer).worker(0xc0001910c0, {0x8f95d0?, 0xc0002920a0?}, 0xc00028e540)
/app/internal/handler/rabbitmq/consumer.go:151 +0x2ff
created by triage/internal/handler/rabbitmq.(*Consumer).StartConsumer in goroutine 46
/app/internal/handler/rabbitmq/consumer.go:129 +0x316
```

Падает на логе Unity: `Unity_300_service_data_CKM00174500653_2025-08-22_07_40_07.tar`