# protobuf

Common protobuf files that should be available in every service.

Unfortunately, currently with go modules and the protc compiler, there is no easy way (that I've found) to include the correct version of these files from their packages. For now, we are stuck copying these to the services.

## Setting up a project

1. Create a folder in your project with the same name as the project (e.g., call the folder `wheelhouse` if your project name is `wheelhouse`).
2. Copy these files to that folder.
3. Create a `swagger` folder in your project root and copy the contents of the `swagger` folder here to that one.
3. Create a `proto.go` file that looks like the following:

```go
package wheelhouse

//go:generate protoc -I./ -I../ ./domain_model.proto --gogoslick_out=plugins=grpc:./ --swagger_out=../swagger/ --grpc-gateway_out=./
//go:generate protoc -I./ -I../ ./$$SERVICE$$.proto --gogoslick_out=plugins=grpc:./ --swagger_out=../swagger/ --grpc-gateway_out=./
```

Typically you should put entity messages in `domain_model.proto`, and then have separate `proto` files for each service and its required `Request`/`Response` messages.

