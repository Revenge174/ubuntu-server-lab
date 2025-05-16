# 🐧 Ubuntu Server Lab on Proxmox

Setup and configuration of an Ubuntu Server 22.04 LTS virtual machine within my home lab using Proxmox VE. Remote SSH access and a lightweight footprint were key goals.

---

## 📚 Language / Lingua

- 🇬🇧 [English version](#english-version)
- 🇮🇹 [Versione italiana](#versione-italiana)

---

## English Version

### 1. ISO Download

I downloaded the Ubuntu Server 22.04 LTS ISO from the official website:

👉 https://ubuntu.com/download/server

Then saved it locally for upload into Proxmox.

---

### 2. ISO Upload to Proxmox

From the Proxmox web interface:

- Navigate to `local` → **ISO Images**
- Click **Upload**, then select the ISO file previously downloaded

---

### 3. VM Creation in Proxmox

**Configuration used:**

- **Name:** `ubuntu-srv`
- **OS Type:** Linux, version 6.x - 2.6 Kernel
- **Disk:** 20 GB (SCSI)
- **CPU:** 2 cores
- **RAM:** 2 GB (2048 MB)
- **Network:** `vmbr0`, VirtIO model

VM creation completed by clicking **Finish**. Afterward, I started the VM and completed the installation process.

---

### 4. Ubuntu Server Installation

During installation:

- Language: English  
- Keyboard layout: Italian  
- Hostname: `ubuntu-srv`  
- User: created a personal account  
- SSH option: enabled  
- No additional software selected  

---

### 5. Post-Installation Configuration

After login via console or SSH:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install net-tools htop curl wget unzip git -y
sudo ufw allow OpenSSH
sudo ufw enable
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

---

### 6. Snapshot Creation

Steps:

1. Select VM `ubuntu-srv`  
2. Go to **Snapshot**  
3. Click **Take Snapshot**  
4. Fill in:
   - Name: `clean-install`
   - Description: Snapshot after base setup
   - Uncheck **Include RAM**
5. Save snapshot

---

### 7. Considerations

This VM is now ready for:

- Web hosting  
- Centralized logging  
- Security testing  
- Lab exercises

---

### 8. Next Steps

- Install Docker or Apache  
- Configure custom DNS/hostname  
- Add Windows VM or pfSense

---

### 9. About

Created by **Sebastiano Daniele Condorelli**  
LinkedIn: [www.linkedin.com/in/sebastianodanielecondorelli](https://www.linkedin.com/in/sebastianodanielecondorelli)  
2025

---

## Versione Italiana

# Installazione e configurazione Ubuntu Server su Proxmox

In questo report documento la creazione di una VM con Ubuntu Server 22.04 LTS all'interno del mio laboratorio casalingo basato su Proxmox. La macchina è stata configurata per essere leggera, accessibile da remoto tramite SSH, e pronta per installare altri servizi in futuro.

---

## 1. Scaricamento ISO

Ho scaricato l'immagine di Ubuntu Server 22.04 LTS dal sito ufficiale:

👉 https://ubuntu.com/download/server

L'ho salvata in locale per poi caricarla su Proxmox.

---

## 2. Upload ISO in Proxmox

Dall’interfaccia web di Proxmox:

- Nodo → `local` → `ISO Images`
- Clic su **Upload** e selezionata la ISO di Ubuntu appena scaricata

---

## 3. Creazione VM in Proxmox

### Impostazioni usate:

- **Name:** `ubuntu-srv`
- **OS Type:** Linux, versione 6.x - 2.6 Kernel
- **Disk:** 20 GB su SCSI
- **CPU:** 2 core
- **RAM:** 2 GB (2048 MB)
- **Rete:** `vmbr0`, modello VirtIO

La creazione è stata completata cliccando su **Finish**. Poi ho avviato la macchina e seguito l’installazione.

---

## 4. Installazione Ubuntu Server

Durante l’installazione:

- Lingua: English
- Layout tastiera: italiano
- Hostname: `ubuntu-srv`
- Utente: creato un account personale
- Opzione SSH: attivata
- Nessun software aggiuntivo selezionato

Dopo l’installazione, riavvio completato senza problemi.

---

## 5. Configurazione iniziale post-installazione

Dopo l'accesso via console (o SSH se già attivo), ho eseguito le seguenti configurazioni:

### Aggiornamento sistema:

```bash
sudo apt update && sudo apt upgrade -y
```

### Installazione pacchetti utili:

```bash
sudo apt install net-tools htop curl wget unzip git -y
```

### Attivazione firewall UFW e apertura porta SSH:

```bash
sudo ufw allow OpenSSH
sudo ufw enable
```

### Installazione di fail2ban per protezione SSH:

```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

---

## 6. Creazione snapshot (punto di ripristino)

Dopo aver completato installazione e configurazione iniziale, ho creato uno snapshot per avere un punto di partenza pulito.

### Come fare:

1. Seleziona la VM `ubuntu-srv` su Proxmox
2. Vai su **Snapshot**
3. Clicca su **Take Snapshot**
4. Compila:
   - **Name:** `clean-install`
   - **Description:** `Snapshot subito dopo installazione e configurazione iniziale`
   - Lascia **Include RAM** disattivo (non serve in questo caso)
5. Clicca su **Take Snapshot**

Lo snapshot viene creato in pochi secondi e permette di tornare indietro in caso di problemi futuri.

---

## 7. Considerazioni

La macchina Ubuntu è pronta e funzionante. Può essere gestita interamente via SSH e servirà come base per:
- Hosting web
- Logging centralizzato
- Prove di hardening
- Simulazioni di attacco/difesa nel laboratorio

---

## 8. Prossimi step

- Installare Docker o Apache
- Aggiungere DNS statico o hostname personalizzato
- Proseguire con VM Windows o pfSense nel lab

---

## 9. Info

Creato da  **Sebastiano Daniele Condorelli**  
LinkedIn: [www.linkedin.com/in/sebastianodanielecondorelli](https://www.linkedin.com/in/sebastianodanielecondorelli)  
2025
