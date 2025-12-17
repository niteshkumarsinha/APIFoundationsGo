## Networking

When you have docker set up, we will need to create a network so the services that we’re going
to use can talk to each other. Creating a network is simple, all you need to do is run the following
command:

```bash
docker network create -d bridge --subnet 172.25.0.0/24 party
``` 

* This command will create a network named `party` on the specified subnet.
* All Docker containers which will run on this network will have connectivity to each other.
* That means that when we run our Go container, it will be able to connect to another Redis container on the same network.

### Setting up a runner for your Go Programs

To run your Go programs, you will need to have a runner set up. This is a simple process, all you need to do is run the following command:

```bash
docker run --net=party -p 8080:80 --rm=true -it -v `pwd`:/go/src/app -w /go/src/app golang go "$@"
```

Save this code snippet as the file ‘go’, make it executable and copy it to your execution path (usually
/usr/local/bin is reserved for things like this.

Let’s quickly go over the arguments provided:

* `--net=party` - runs the container on the shared network
* `-p` - network forwarding from host:8080 to container:80 (HTTP server)
* `--rm=true` - when the container stops, clean up after it (saves disk space)
* `-v` option - creates a volume from the current path (pwd) in the container
* `"$@"` - passes all arguments to go to the container application

Very simply, what this command does is run a Docker container in your current folder, execute the
go binary in the container, and clean up after itself when the program finishes.

Note: as we only expose the current working path to the container, it limits access to the host machine

* if you have code outside the current path, for example in “..” or “/usr/share”, this code will not be
available to the container.

An example of running go would be:

```bash
$ go version
```
>go version go1.6 linux/amd64

And, what we will do through most of this book is run the following command:

- compile and run Go program
```bash
$ go run [file]
```


```bash
$ go run hello_world.go
```
>Hello world!
