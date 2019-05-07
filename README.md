# autossh-tunnel-systemd
A very very very light script to create and run a permanent SSH tunnel via serveo.net using systemd.
Not to mention this is only usable for systemd provided kernels.

## Usage

    USAGE: ./autotunnel [-h/--help] alias-name local-port remote-port
    DESCRIPTION :
	    -h/--help			Display this helper
	    alias-name			The alias you want to give to your tunnel
	    local-port			The targeted local port for your tunnel
	    remote-port			The targeted remote port for your tunnel

	The script must be run under root or sudo permisions.

## Serveo Documentation Extracts
### How does it work?
Serveo is an SSH server just for remote port forwarding. When a user connects to Serveo, they get a public URL that anybody can use to connect to their localhost server.  
### SSH forwarding

Request forwarding for port 22, and serveo.net will act as a jump host, allowing you to conveniently SSH into your machine (a unique alias is required):

Then you can establish an SSH connection using serveo.net as an intermediary like this:

> ssh -J serveo.net user@myalias

The -J option was introduced in the OpenSSH client version 7.3. If you have an older client, you can use the ProxyCommand option instead:

> ssh  **-o ProxyCommand="ssh -W myalias:22 serveo.net"**  user@myalias

### Generic TCP forwarding

If you request a port other than 80, 443, or 22, raw TCP traffic will be forwarded. (In this case, there's no way to route connections based on hostname, and the alias, if specifed, will be ignored.)
