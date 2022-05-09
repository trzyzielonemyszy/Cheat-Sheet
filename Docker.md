**Docker compose**

`docker volume rm $(docker volume ls -q) ` usuwa wszystkie volumy

`docker image rm $(docker image ls -q) ` usuwa wszystkie obrazy

`docker container inspect --format '{{ .NetworkSettings.IPAddress }}' <container  name> ` wyswietla ip contanera

`docker container inspect --format '{{ .NetworkSettings.Ports }}' <container  name>` wyswietla porty contanera
`docker ps --format '{{.Image}}' ` listuje właczone kontenery wypisujac tylko image

`docker ps --format '{{.Names}}'` listuje włączone konrtenery, tylko nazwy
