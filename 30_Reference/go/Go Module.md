
- Проекты в [[Golang]] называются [[Go Module|модулями]]
- Модуль - это исходники + зависимости
- Каждый модуль  имеет `go.mod` файл в корневой директории

Для инициализации модуля можно использовать команду:
```go
go mod init hello_world
```


## Dependency Management

- When a developer imports a package that is not already included in the project, the **build command** (go build or go test) causes Go to **automatically locate, download, and add that dependency to the go.mod file**. 
- This occurs when the build command is executed.  After that, this file functions as a **manifest, providing information about the particular versions** of each dependency that is utilized in the project.
- `go get <module-path>@<version`
