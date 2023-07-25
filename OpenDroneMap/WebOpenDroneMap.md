# Instalando
Segundo [manual de instalação](https://docs.opendronemap.org/installation/#linux), É necessário ter [[Docker-compose]] instalado!

Clone do github:
```
git clone https://github.com/OpenDroneMap/WebODM
```

# Executando

```
cd WebODM
./webodm.sh start
```

```
# Restart WebODM (useful if things get stuck)
$ ./webodm.sh restart

# Reset the admin user's password if you forget it
$ ./webodm.sh resetadminpassword newpass

# Update everything to the latest version
$ ./webodm.sh update

# Store processing results in the specified folder instead of the default location (inside docker)
$ ./webodm.sh restart --media-dir /path/to/webodm_results

# See all options
$ ./webodm.sh --help
```
