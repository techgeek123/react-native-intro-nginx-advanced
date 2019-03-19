# Load balancing and reverse proxy

## Related Content
This content should be short and ideally restricted to this challenge

## Release 0
You might be having several node web applications lying around. Run 4 of them in several ports.
Ex:
1. A hello world program that runs at `localhost:80`
2. A cube timer app runs at `localhost:3001`
3. An ecommerce website runs at `localhost:4444`
4. A pokemon application runs at `localhost:3000`


## Release 1
Learn about [Hosts file](https://en.wikipedia.org/wiki/Hosts_file)
Here's an article on [How to edit Hosts file on Mac](https://www.imore.com/how-edit-your-macs-hosts-file-and-why-you-would-want)
Add some hosts on your system to be used with above sites
Ex: hello.local, cubetimer.dev, myshop.local, pokemon.go etc

All the hosts now point to the home ip 127.0.0.1

## Release 2
Use `proxy_pass` to pass the request from each of the above domains to respective servers.

i.e. When a user opens `http://pokemon.go` in the browser, it should immediately show the content from `localhost:3000` which is running a node server with pokemon application.


## Release 3
Configure your nginx setup to serve the static sites directly. And pass the remaining requests onto the respective server port so that they can be processed by node server.
