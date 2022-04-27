# tor-hidden-ssh
ssh available as a hidden service accessible only through the Tor network

It is relatively easy to make your SSH server available as a hidden service accessible only through the Tor network. There are several reasons you might want to do this.

- You can access your server anonymously.
- You can access your server from the open internet even if it is hidden behind a firewall and it has a dynamically assigned IP address.

The downside to using the Tor network to access your server is that the network is not particularly fast.

# Prerequisites
- Ubuntu 20.04 (Server)(Recommended)
- Ubuntu 20.04 (Client)

# Server

Install Tor

```
sudo apt update
sudo apt install tor
```

```
sudo nano /etc/tor/torrc
```

```
HiddenServiceDir /var/lib/tor/hidden/
HiddenServicePort 22
```

Restart Tor service

```
sudo systemctl restart tor
```

Get onion address:

```
cat /var/lib/tor/hidden/hostname
```

You might want to close port 22 since you will be connecting through Tor and change to password authentication

```
sudo nano /etc/ssh/sshd_config
```

```
...
ListenAddress 127.0.0.1
...
PasswordAuthentication yes
```

Restart ssh service

```
sudo systemctl restart ssh
```

# Client

Update apt index and install tor

```
sudo apt update
sudo apt install tor
```

# Connect

```
torify ssh <USERNAME>@<ONION_ADDRESS>
```
