## Virtualbox / Linux

### Installer Virtualbox

Last ned Virtualbox og installer.

### Last ned Linux ISO

Hvis Lubuntu, last ned her:
<https://lubuntu.net/downloads/>

### Lag ny maskin i Virtualbox

- Gi maskinen et navn, velg operativsystem og versjon.
- 4096 MB RAM
- 20 GB Virtual Hard Drive (Fixed er raskere)

### Last inn ISO

- Settings > Storage > Trykk på ikon av CD
- Finn nedlastet ISO og trykk på OK

### Installer OS

Start maskinen. Følg instruksjoner for installering av OS.

### Build-essential

Etter installasjon, åpne terminal og skriv:
sudo apt-get install build-essential

### Guest Additions

<https://askubuntu.com/questions/311161/how-to-install-guest-additions-in-lubuntu-13-04>

Inne i VM i terminal:
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install dkms

Reboot

I Virtualbox-vindu.
Devices > Insert Guest Additions CD Image (sjekk om den er mounted fra før i settings)

Finn ut hvor CD er mounted (bruk File Explorer) og naviger dit med Terminal.
Kjør denne filen:

```
sudo sh ./VBoxLinuxAdditions.run
```

### SSH tilgang

I Virtualbox:
Høyreklikk på VM > Settings > Network > Enable Network Adapter
Bruke WIFI enheten

Inne i VM:

```
sudo apt-get install openssh-server -y
```

Og så kjør:

```
ifconfig
```

Bruk IP-addresse i windows for å koble til.

Lag .ssh mappen under Home directory hvis den ikke finnes:

```
mkdir .ssh
```

Bruk SSH for å kopere over filer, typ:

```
scp config devbox:.ssh/
```

Sett riktig permissions i VM:

```
sudo chmod 600 ~/.ssh/id_rsa
sudo chmod 600 ~/.ssh/id_rsa.pub
```

Så bruk ssh-add for å legge til identity

```
ssh-add
```

## Emacs Lubuntu

sudo add-apt-repository ppa:kelleyk/emacs
sudo apt-get update
sudo apt install emacs26