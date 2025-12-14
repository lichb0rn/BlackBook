---
up:
  - "[[Golang]]"
related: "[[Concurrency]]"
created: 2025-05-08
---
Допустим нам нужно написать функцию, которая будет вызывать две сервиса, собирать от них данные и отправлять в третий. Весь процесс должен занять не более 50мс.

Пример на [[Golang]]:
```go
func GatherAndProcess(ctx context.Context, data Input) (COut, error) {
	ctx, cancel := context.WithTimeout(ctx, 50*time.Millisecond)
	defer cancel()
	
	ab := newAbProcessor()
	ab.start(ctx, data)
	inputC, err := ab.wait(ctx)
	if err != nil {
		return COut{}, err
	}

	c := newCProcessor()
	c.start(ctx, inputC)
	out, err := c.wait(ctx)
	return out, err
}
```

`A` и `B` - условные названия сервисов, которые мы вызываем параллельно.

```go
type abProcessor struct {
	outA chan aOut
	outB chan bOut
	errs chan error
}

func newABProcessor() *abProcessor {
	return &abProcessor{
		outA: make(chan aOut, 1)
		outB: make(chan bOut, 1)
		errs: make(chan error, 2)
	}
}

func (p *abProcessor) start(ctx context.Context, data Input) {
	go func() {
		aOut, err := getResultA(ctx, data.A)
		if err != nil {
			p.errs <- err
			return
		}
		p.outA <- aOut
	}()
	
	go func() {
		bOut, err := getResultB(ctx, data.B)
		if err != nil {
			p.errs <- err
			return
		}
		p.outB <- bOut
	}()
}

func (p *abProcessor) wait(ctx context.Context) (cIn, error) {
	var cData cIn
	for count := 0; count < 2; count++ {
		select {
		case a := <-p.outA:
			cData.a = a
		case b := <-p.outB:
			cData.b = b
		case err := <-p.errs:
			return cIn{}, err
		case <-ctx.Done():
			return cIn{}, ctx.Err()
		}
	}
	return cData, nil
}```

И код `cProcessor`:
```go
type cProcessor struct {
	outC chan COut
	errs chan error
}

func newCProcessor() *cProcessor {
	return &cProcessor{
		outC: make(chan COut, 1),
		errs: make(chan error, 1),
	}
}

func (p *cProcessor) start(ctx context.Context, inputC cIn) {
	go func() {
		cOut, err := getResultC(ctx, inputC)
		if err != nil {
			p.errs <- err
			return
		}
		p.outC <- cOut
	}()
}

func (p *cProcessor) wait(ctx context.Context) (COut, error) {
	select {
		case out := <-p.outC:
			return out, nil
		case err := <-p.errs:
			return COut{}, err
		case <-ctx.Done():
			return COut{}, ctx.Err()
	}
}
```

