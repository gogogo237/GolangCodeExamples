When you write your own package, and want to import it locally. Here is the method you will use. Let's illustrate how to do it in an example.
The folder directory is like this:
```shell
main.go
treesort
	|____sort.go

```
Package main import ./treesort. It want to import locally created package. We run the source code with:
```shell
go mod init
go build
```
the following error occurs:
```shell
main.go:4:2: local import "./treesort" in non-local package
```
Why? the *treesort* package is obviously here in a directory. And the import ./treesort command seems right. What's wrong?
We modify import ./treesort to import treesort, deleting ./ and we use this command to update our go.mod:
```shell
go mod edit -replace treesort=./treesort
cd treesort
go mod int
cd ..
go get treesort
go build
```
As you can see, the code build successfully!