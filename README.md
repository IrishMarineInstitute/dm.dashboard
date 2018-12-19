# dm.dashboardon cluster02:/home/opsuser/apps/dashboard
docker build -t 127.0.0.1:5000/dashboard .
docker push 127.0.0.1:5000/dashboard
docker service create --name dashboard --label traefik.port=80 --label traefik.domain=sysadmin.dm.marine.ie --network traefik-net 127.0.0.1:5000/dashboard:latest
# to update need to run docker pull command on each of the swarm nodes:
docker pull 127.0.0.1:5000/dashboard:latest
# Then do an update:
docker service update --force --image 127.0.0.1:5000/dashboard:latest dashboard
