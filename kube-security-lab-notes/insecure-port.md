- docker exec -it client /bin/bash
- nmap 172.18.0.3

- port 2379 (etcd client)
- port 2380 (etcd server)
- port 6443 (sun-sr-https)
- port 8080 (http-proxy)
- 10250 (?)
- 10251 (?)
- 10252 (apollo relay)
- 10256 (?)

as you can see, just about everyport is exposed. exposed to the internet I suppose, since this is just a regular port scan
that can be coming from anywhere...

What do I want? I want the root ca... As i have HEARD that this is the key to persistent access ;)

where does that live...
