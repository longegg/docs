## Virtualbox / Linux

### Installer Virtualbox

Last ned Virtualbox og installer.
<https://www.virtualbox.org/>

### Last ned Linux ISO

Hvis Lubuntu, last ned her:
<https://lubuntu.net/downloads/>

Det kan være lurt å velge LTS-versjon for å sikre oppdaterte pakker gjennom PPA.

### Lag ny maskin i Virtualbox

- Gi maskinen et navn, velg operativsystem og versjon.
- 4096 MB RAM
- 20 GB Virtual Hard Drive. Fixed er raskere, men kanskje ikke nødvendig?

### Juster instillinger

- Øk RAM til skjermkort
- Øktil 2 kjerner prosessor
- Skru av Lyd hvis ikke trenger
- Skru på clipboard funksjonalitet

### Last inn ISO

- Settings > Storage > Trykk på ikon av CD
- Finn nedlastet ISO og trykk på OK

### Installer OS / Oppdater

Start maskinen. Følg instruksjoner for installering av OS.
Installer eventuelle oppdatering som dukker opp i OS.

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

### Nettverk 

#### Bridged

NB!: Problemer med denne hjemme (GET-boks DHCP klarer ikke tildele IP). Bruk metoden under.

I Virtualbox:
Høyreklikk på VM > Settings > Network > Enable Network Adapter > Attached To: Bridged Network adapter
Bruke WIFI enheten

#### NAT / Host Only

I VirtualBox. File > Host Network Manager > Opprett ny

- Configure Adapter Manually
- IPv4 Address: 192.168.2.1
- IPv4 Network Mask: 255.255.255.0
- Apply

Settings på VM. Network

Adapter 1: 
- Attached to: NAT

Adapter 2: 
- Attached to: Host-only Adapter
- Name: Velg den nye adapteren

I Lubuntu:

Åpne terminal:

```
ifconfig
```

Du skal se to adaptere. Den en kan ikke nås, den andre må få en Ipv4 adresse.

Åpne Network Connections (høyreklikk nettverksikon nede i høyre hjørne).

Velg riktig .. og Ipv4 Settings.
Legg til ny: 
- Address: 192.168.2.10
- Gateway: 192.168.2.1
- DNS Server: 8.8.8.8 (Google sin. Ikke nødvendig?)

Kjør ifconfig igjen. Må kanskje disconnect og connect nettverk.

Prøv å pinge fra Host og vice versa.


#### Open-SSH-Server

Inne i VM:

```
sudo apt-get install openssh-server -y
```

Og så kjør:

```
ifconfig
```

Bruk IP-addresse i windows for å koble til.

#### Guest -> Eksterne

Lag .ssh mappen under Home directory hvis den ikke finnes:

```
mkdir .ssh
```

Bruk SSH for å kopere over filer, typ:

```
scp config devbox:.ssh/
```

Fjern settinger i config-fil som ikke trenger å være der.

Sett riktig permissions i VM:

```
sudo chmod 600 ~/.ssh/id_rsa
sudo chmod 600 ~/.ssh/id_rsa.pub
```

Så bruk ssh-add for å legge til identity

```
ssh-add
```

## Emacs

### Lubuntu Bionic

```
sudo add-apt-repository ppa:kelleyk/emacs
sudo apt-get update
sudo apt install emacs26
```

### Lubuntu Cosmic (Nov. 2018)

Brukte disse som guide:
<https://www.gnu.org/software/emacs/manual/html_node/efaq/Installing-Emacs.html>
<http://ubuntuhandbook.org/index.php/2014/10/emacs-24-4-released-install-in-ubuntu-14-04/>

Hvis denne feilen dukker opp:
You must put some ‘source’ URIs in your sources.list

<https://techoverflow.net/2018/05/03/how-to-fix-apt-get-source-you-must-put-some-source-uris-in-your-sources-list/>

Men ikke ta med deb-scr som har med Canonical å gjøre!