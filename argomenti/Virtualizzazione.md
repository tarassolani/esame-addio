Materie: [[Sistemi e Reti]]

# Virtualizzazione
### Server Virtualization
La **virtualizzazione dei server** permette di creare su un singolo server più **macchine virtuali**, in contemporanea e che condividono le risorse della stessa macchina fisica, su cui vengono eseguiti diversi sistemi operativi e applicativi client, che funzionano come se fossero ognuno un proprio server dedicato.
	Esempio: un'azienda con **3 server fisici** (web, posta elettronica e database) può consolidare tutti questi in **1 unico server fisico** con **3 macchine virtuali**, riducendo i costi hardware e semplificando la gestione.
	Esempio pratico: Citrix XenServer, piattaforma di virtualizzazione che usa l'hypervisor Xen, bare-metal.
Di fatto, sul **sistema operativo host** (ospitante) vengono create una serie di partizioni entro cui poter eseguire più **sistemi operativi guest** (ospiti) senza conflitti.
###### Vantaggi
- Costi bassi
- Delega di cura tecnica e sicurezza del server fisico alla società che fornisce il servizio
- Separazione tra gli ambienti occupati da aziende che affittano lo stesso servizio
###### Svantaggi
- Mancanza di una macchina fisica a uso esclusivo come server
- Possibili problemi legati allo scarso setup di uno degli utenti presenti sul server virtuale
- Garanzia delle prestazioni (dipende dalla capacità di dividere il carico di lavoro tra gli utenti)

#### Virtualizzazione hardware
Si possono creare e gestire macchine virtuali (VM) per simulare l'hardware fisico, grazie ad un hypervisor che può essere di 2 tipi: ^e58fb2
- **Hypervisor di tipo 1 (bare-metal):** Funzionano direttamente sull'hardware fisico, senza bisogno di un sistema operativo host. Usati spesso in ambienti server e data center per la loro efficienza e prestazioni elevate.
	Esempio: azienda che ha un server fisico con risorse (memoria, CPU) significative
- **Hypervisor di tipo 2 (hosted):** Funzionano sopra un sistema operativo host, comunemente usati per scenari di test e sviluppo.
	Esempio: uno sviluppatore crea una VM Ubuntu Linux per sviluppare un'applicazione, su un sistema operativo host Windows con VMware Workstation.
	Esempi di hypervisor: VMware Workstation, Oracle VirtualBox, Parallels.
Il vantaggio del **bare-metal** è l'efficienza dell'utilizzo delle risorse hardware.
Il vantaggio del **hosted** è la semplicità di installazione.

#### Virtualizzazione con Container
A differenza della virtualizzazione tradizionale, che crea macchine virtuali complete con OS separati, la virtualizzazione con container sfrutta il kernel del sistema operativo host creando ambienti isolati (container). È una tecnica leggera che offre prestazioni quasi native, poiché elimina la necessità di hypervisor e OS guest completi.
I container sono isolati l'uno dall'altro e dal OS host, con un proprio filesystem e spazio dei processi, ma condividono il kernel, il che rende più efficiente l'uso delle risorse hardware. Inoltre, sono noti per la portabilità e per la velocità di avvio (dato che non c'è bisogno di avviare un OS completo).
**Componenti**:
- **Namespaces:** forniscono l'isolamento (PID namespace isola i processi, NET namespace isola le risorse di rete, USER namespace isola utenti, ecc.)
- **Control groups (cgroups):** limitano e monitorano le risorse (CPU, memoria) utilizzate dai container, allocando risorse specifiche ad ognuno.
- **SELinux (Security-Enhanced Linux), o AppArmor**: meccanismo di sicurezza che limita le operazioni che un container può eseguire.
Diversi container su più host possono essere gestiti tramite strumenti di orchestrazione, come **Docker Swarm** (integrato in Docker), o **Kubernets** (piattaforma open source sviluppata originariamente da Google).
Esempi di utilizzo:
	Un team di sviluppo crea container per ogni microservizio di un'applicazione;
	Si usano container per eseguire vecchie applicazioni (legacy) su hardware moderno;
	L'esecuzione di un programma sviluppato viene garantita se si fa uso di container (dato che dispositivi diversi dal nostro potrebbero eseguire il programma in modi diversi, oppure non essere compatibili).
	
