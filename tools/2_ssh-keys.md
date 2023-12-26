# 🔑 SSH Keys

## Intro
An _SSH key_ is an access credential in the [SSH protocol](https://www.ssh.com/ssh/protocol/). Its function is similar to that of user names and passwords, but the keys are primarily used for automated processes and for implementing single sign-on by system administrators and power users.

Public key cryptography is a method of encrypting or signing data with two different keys and making one of the keys, the public key, available for anyone to use. The other key is known as the private key. Data encrypted with the public key can only be decrypted with the private key.

![[Pasted image 20231226112616.png]]
https://101blockchains.com/private-key-vs-public-key/
## Generate SSH keys

```shell
ls -al ~/.ssh
```

```shell
ssh-keygen -t ed25519 -C "alejandromartinezcornes@gmail.com"
```

```shell
eval "$(ssh-agent -s)"
```

```shell
ssh-add ~/.ssh/id_ed25519
```

```shell
chmod 600 ~/.ssh/id_ed25519 && chmod 600 ~/.ssh/id_ed25519.pub
```

```shell
cat ~/.ssh/id_ed25519.pub
```

## Change ssh key

_ssh_-_agent_ es un manejador de claves para SSH, es decir, mantiene las claves privadas en memoria, descifradas y listas para usarse. Si tienes multiples claves ssh en tu sistema, a la hora de realizar alguna operación con las mismas, querrás cambiar que clave estás usando.

https://superuser.com/questions/357602/use-a-specified-key-from-ssh-agent
