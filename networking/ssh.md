# SSH

- Usually port 22

## Enumeration

- We need to keep notes of the ssh version
- We can try to ssh to our target `ssh IP-ADD`. In our example we get this  
![image](https://user-images.githubusercontent.com/96747355/175833787-a2b8bcbd-05a9-4ecb-ac37-b584c896253c.png)  
- For this error we can try this `ssh 10.0.2.4 -oKexAlgorithms=+diffie-hellman-group1-sha1 `  
![image](https://user-images.githubusercontent.com/96747355/175834000-bc2e9cbe-5949-4836-88d7-c9d399f95054.png)  
- For this error we can try this `ssh 10.0.2.4 -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa `  
![image](https://user-images.githubusercontent.com/96747355/175834033-1c9a18f8-bb6f-4961-bbc1-3550da4dba45.png)  
- Finally for this error we can use this and will try to connect `ssh 10.0.2.4 -oKexAlgorithms=+diffie-hellman-group1-sha1 -oHostKeyAlgorithms=+ssh-rsa -c aes128-cbc`
- `nmap -p22 TARGET-IP --script ssh-auth-methods --script-args="ssh.user=username"` will show authentication methods (requires a username).  
See output example

```bash
PORT   STATE SERVICE
22/tcp open  ssh
| ssh-auth-methods: 
|   Supported authentication methods: 
|_    publickey
```

- `nmap -p22 TARGET-IP --script ssh-hostkey --script-args ssh_hostkey=full`
See output example

```bash
PORT   STATE SERVICE
22/tcp open  ssh
| ssh-hostkey: 
|   ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDMCwfnXf0WI8xwEChpVHr9JZNlgJxXnGbrVM7TkTx2Kh+bnYBwtuZrIBj7zD+LNRqIOHPMmDCZuVHOONRX9qauAq46EtCYBN35NtCtQnBRGPMC8fVxPk6KORkrWJ2J5c/crYnNCbVOt55fad739S1fYs35+X2As5/bR+F6zfnpsTMvNSiXzzJRb4C/W4PcQ9T3Az7knI+8oyP4WsbUN3l2KOq+QsWscv5Ida+ZTR7DJIbfFs/fdsPzJsLJsONsjOwyOmWsge/nik2zMRkuIUgrYco8MtPoKKfXohpFffUm4dx0I54wv9GiIHRjEEx3przciF6XvPq/2uPWhi1wpn9R
|   ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBJjL31haOqBjuQ4XE/yrVby9ygrWlBMaGhxa2gzUau6Oxqp+Lomi72wf/KQ1/FPwG8qFGM0mJxTFKnwj/Ez5Ok0=
|_  ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAII61CNVnXxys5WNU/Q2WShh2JKJb3Pd1sPItUTK144ZJ
```

- `nmap -p22 TARGET-IP --script ssh2-enum-algos `

## Password spray or bruteforce

- `hydra -L users.txt -P passwords.txt TARGET-IP -t 4 ssh`

## Connect to ssh server

- `ssh username@IP-TARGET` 

## Resources

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/pentesting-ssh" %} Pentesting SSH - Hacktricks {% endembed %}  