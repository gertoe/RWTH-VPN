# RWTH-VPN
This repository provides a workaround for automating the login process
connecting to the RWTH Aachen Cisco Anyconnect VPN server using the official
Cisco Anyconnect client.

Due to a "recent" configuration change in the VPN server configuration, the
previous openconnect-based workaround does not work anymore, and the official
Cisco client must be used.

## Prerequisites
You need to install the official Cisco Anyconnect VPN client distributed, e.g.,
by the RWTH Aachen University. Ensure that the `vpnagentd` daemon is running,
otherwise the Anyconnect client will be unable to establish a connection. See
the Anyconnect documentation for further details.

In order to connect with the provided script/templates, you must initially
connect to the VPN server by entering your credentials manually. For some
reason, the available groups and protocols as described below cannot be
discovered by the client without an interactive login attempt.

Please configure the provided scripts and templates (see below) according to
your requirements.

## Login Automation
Basically, the workaround for login automation consists of two parts: one
credential file and a wrapper script piping the connect commands into the
Anyconnect client CLI.

The _credential_ file has the following structure:
```
connect vpn.rwth-aachen.de (<VPN PROTOCOL>)
RWTH-VPN (<GROUP>)
<YOUR TIM ID>
<YOUR VPN PASSWORD>
[blank]
```
where `<VPN PROTOCOL>` can be configured `SSLVPN` or `IPsec`, and `<GROUP>`
selected from `Full Tunnel` or `Split Tunnel`, respectively.

The wrapper script is for sole convenience and executes:
```
/path/to/your/cisco/anyconnect/bin/vpn -s < credential_file
```

## Disconnecting from the VPN server
Either disconnect by `/path/to/your/cisco/anyconnect/bin/vpn disconnect` or use
the provided disconnect wrapper for convenience.

# NOTE: DO NOT SHARE YOUR CREDENTIALS AND STORE THEM AT A SAFE LOCATION!
__Ensure that the credential file can only be accessed by yourself!__
Secure your file, e.g., with `chmod 600` and take additional safety measures!

