# PM2

## Install

You have to get installed **node** previously. The -g option tells npm to install the module globally, so that it's available system-wide.

```shell
sudo npm install -g pm2
```

Once this is installed, check the installed path as:

```shell
whereis pm2
```

```shell
pm2: /opt/node/bin/pm2 /opt/node/lib/node_modules/pm2/bin/pm2
```

Now, we need to add this path in startup bash script. Add add the following line anywhere in `$HOME/.bashrc` or `$HOME/.zshrc` file.

```shell
nano $HOME/.bashrc
```

```shell
export PATH=$PATH:/home/ec2-user/.nvm/versions/node/v16.15.1/bin/pm2
```

Now restart the bash script as follows:

```shell
source ~/.bashrc
```

Check the status of pm2

```shell
pm2 status
```

## Commands

**Start**

```shell
pm2 start build/dist/src/index.js --name <app_name>
```

**Save**

```shell
pm2 save -f
```

**Logs**

```shell
pm2 logs <app_name> --lines 153
```

**Status**

```shell
pm2 status <app_name>
```
