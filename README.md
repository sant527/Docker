# Docker

## How to build a docker image from Dockerfile

```
docker build -t "archlinux/testing:latest" .
```
options
```
-t, --tag list                Name and optionally a tag in the 'name:tag' format
```

## how to run a docker image

```
docker run \
    --rm \
    -it \
    -e LISTEN_PORT=6924 \
    -p 6992:6992 \
    -u 0 \
    --workdir /etc/openvpn/ \
    -v localdirector/filename:dockerdir/filename \
    -v localdirector:dockerdir \
    --name archtesting \
    archlinux/testing:latest
```

options
```
--rm                             Automatically remove the container when it exits
-i, --interactive                    Keep STDIN open even if not attached
-t, --tty                            Allocate a pseudo-TTY
-e, --env list                       Set environment variables
-p, --publish list                   Publish a container's port(s) to the host
-u, --user string                    Username or UID (format: <name|uid>[:<group|gid>])
-w, --workdir string                 Working directory inside the container
-v, --volume list                    Bind mount a volume
--name string                    Assign a name to the container
```

## how to execute some command on a running docker container
```
docker exec -it -u 0 -w /root archtesting bash
```

options
```
-i, --interactive          Keep STDIN open even if not attached
-t, --tty                  Allocate a pseudo-TTY
-w, --workdir string       Working directory inside the container
-u, --user string          Username or UID (format: <name|uid>[:<group|gid>])
```

## how to see the ip and current geographic location
```
curl ipinfo.io/$(curl ifconfig.me)
```

## configuring ssh without need to login with password
ssh should be installed in the docker and also at the entry point one should start sshd by

```
/usr/sbin/sshd &&
```

on the host run

```
IP_ADDRESS=$(docker inspect -f "{{ .NetworkSettings.IPAddress }}" archtesting)
echo $IP_ADDRESS
ssh -i '/home/user/.ssh/id_rsa2' "root@${IP_ADDRESS}"
```
If It will say that remove from known_hosts
```
vi .ssh/known_hosts # and remove the line with the IP_ADDRESS
```

then again run
```
ssh -i '/home/user/.ssh/id_rsa2' "root@${IP_ADDRESS}"
```

Now we can connect the docker using ssh


## How to check images

```
docker image ls
```

## remove dangling images

```
docker image prune
```


## how to stop and remove all containers
```
docker stop $(docker ps -a -q) 
docker rm $(docker ps -a -q)
```

## How to attach to detached container
```
docker attach delugevpn
```

## view list of containers

```
docker container ls
```

