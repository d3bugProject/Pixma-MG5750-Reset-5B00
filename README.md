# Canon Pixma MG5750 - Guide de déblocage Erreur 5B00 / 1700 (Reset Absorbeur d'encre)
# Canon Pixma MG5750 - Waste Ink Absorber Counter Reset Guide (Error 5B00 / 1700)

[![Canon](https://img.shields.io/badge/Model-Canon%20Pixma%20MG5750-red.svg)](https://www.canon.fr)
[![Firmware](https://img.shields.io/badge/Firmware-EUR%20V2.040%20(Tested)-blue.svg)](#)
[![ServiceTool](https://img.shields.io/badge/Working%20Tool-ServiceTool%20v4906-success.svg)](#)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](#)

---

## 🇫🇷 Français

Ce dépôt contient la solution complète, vérifiée et **100% gratuite** pour résoudre l'erreur **5B00** (ou 1700 / "L'absorbeur d'encre est plein") sur l'imprimante multifonction **Canon Pixma MG5750** (série MG5700), testée avec succès sur le firmware **EUR V2.040**.

### ⚠️ Pourquoi cette solution est spéciale ?
1. **Les outils payants (ex: WIC Reset)** refusent la clé gratuite `trial` sur les modèles Canon récents et obligent à payer 7 à 10 €.
2. **Les versions récentes de Service Tool (ex: v5103)** renvoient l'**Erreur 006** sur le firmware V2.040 de la MG5750 car Canon a durci les sécurités EEPROM.
3. **La version qui fonctionne parfaitement est `ServiceTool_v4906`** fournie dans ce dépôt !

---

### 📋 Prérequis
* Un **PC Windows** (Windows 10 ou 11 recommandé).
* Un **câble USB** reliant l'imprimante au PC (le Wi-Fi ne fonctionne pas pour cette procédure).
* **2 ou 3 feuilles de papier standard** chargées dans la cassette inférieure de l'imprimante.

---

### 🛠️ Guide pas-à-pas

#### Étape 1 : Passer l'imprimante en « Mode Service »
1. Éteignez l'imprimante (laissez le câble d'alimentation branché au secteur).
2. Maintenez enfoncé le bouton **Stop** (le cercle rouge avec le triangle inversé).
3. Tout en maintenant *Stop*, maintenez enfoncé le bouton **Power** (Marche/Arrêt).
4. Relâchez **Stop**, mais **gardez le bouton Power enfoncé**.
5. Tout en gardant *Power* enfoncé, appuyez **6 fois d'affilée** sur le bouton **Stop** (un rythme régulier : 1, 2, 3, 4, 5, 6).
6. Relâchez enfin le bouton **Power**.
7. La LED d'alimentation blanche va clignoter pendant que les mécanismes s'initialisent, puis va devenir **blanche fixe**. L'écran de l'imprimante reste **éteint / noir** : c'est normal, l'imprimante est en **Mode Service**.

---

#### Étape 2 : Le piège du port USB sous Windows (Résolution Erreur 006)
Sous Windows 10/11, lorsque l'imprimante passe en Mode Service, Windows la réassigne souvent à un nouveau port virtuel (souvent `USB006`), alors que l'imprimante enregistrée dans la file d'attente pointe vers l'ancien port (ex: `USB002`).

Pour corriger cela automatiquement, ouvrez **PowerShell en administrateur** et exécutez :
```powershell
Set-Printer -Name "Canon MG5700 series" -PortName "USB006"
```
*(Si votre port est différent, vérifiez-le avec `Get-PnpDevice | Where-Object { $_.FriendlyName -match "Canon" }`).*

---

#### Étape 3 : Vérifier le pourcentage d'encre usagée (`D=...`)
1. **Chargez impérativement du papier** dans le bac inférieur.
2. Faites un clic droit sur **`ServiceTool_v4906.exe`** > **Exécuter en tant qu'administrateur**.
3. Dans l'onglet **Main**, cliquez sur le bouton **EEPROM** (ou **Test Print**).
4. Une page de diagnostic s'imprime.
5. 🔍 **Regardez la 2ème ligne de la feuille imprimée :**
   - Vous y trouverez l'indication **`D=...`** (par exemple : `D=100.4`).
   - **`D` représente le pourcentage de saturation du réservoir d'encre usagée !** (À 100%, l'erreur 5B00 se déclenche).

---

#### Étape 4 : Remise à zéro du compteur (Reset 5B00)
1. Toujours dans **`ServiceTool_v4906.exe`**, onglet **Main**.
2. Dans la section **Clear Ink Counter** (ou *Ink Absorber Counter*) :
   - Assurez-vous que le menu déroulant **Absorber** est réglé sur **Main**.
   - Cliquez sur le bouton **`Set`**.
3. Une boîte de dialogue apparaît avec le message :
   > **`A function was finished`**
4. Cliquez sur **OK** et fermez le logiciel.

---

#### Étape 5 : Redémarrage
1. Éteignez l'imprimante avec le bouton **Power**.
2. Débranchez la prise électrique de l'imprimante pendant **15 à 20 secondes**.
3. Rebranchez et rallumez l'imprimante normalement.
4. L'écran LCD s'allume, le voyant est vert/blanc stable : **l'erreur 5B00 a totalement disparu !**
*(Si vous refaites un test print, la deuxième ligne indiquera désormais `D=000.0`).*

---

> [!WARNING] Précautions physiques
> La réinitialisation logicielle remet le compteur interne à zéro, mais elle ne vide pas physiquement les feutres absorbants situés au fond du châssis. Après plus de 10 000 impressions, surveillez d'éventuelles coulures sous l'imprimante ou envisagez de nettoyer les tampons de feutre si nécessaire.

---
---

## 🇬🇧 English

This repository provides the complete, tested, and **100% free** solution to fix the Canon **Error 5B00** (or 1700 / "Waste ink absorber is full") on the **Canon Pixma MG5750** (MG5700 series), successfully verified on firmware **EUR V2.040**.

### ⚠️ Why this fix is important
1. **Commercial tools (e.g., WIC Reset)** do not support free `TRIAL` keys on modern Canon models and charge 7–10 € per reset.
2. **Newer Canon Service Tool iterations (e.g., v5103)** fail with **Error 006** on firmware V2.040 due to EEPROM write restrictions.
3. **The working version is `ServiceTool_v4906`**, included directly in this repository!

---

### 📋 Prerequisites
* A **Windows PC** (Windows 10 or 11).
* A **USB cable** directly connecting the printer to the PC (Wi-Fi cannot be used for service mode operations).
* **2–3 sheets of plain paper** loaded in the lower paper cassette.

---

### 🛠️ Step-by-Step Instructions

#### Step 1: Put the Printer into "Service Mode"
1. Turn off the printer (leave the power cord plugged into the electrical outlet).
2. Press and hold the **Stop** button (triangle inside a circle).
3. While continuing to hold *Stop*, press and hold the **Power** button.
4. Release the **Stop** button, but **keep holding the Power button down**.
5. While holding *Power*, press the **Stop** button **6 times sequentially** (steady rhythm: 1, 2, 3, 4, 5, 6).
6. Release the **Power** button.
7. The white power LED will blink as internal mechanisms initialize, then become **solid white**. The LCD screen will remain **black / turned off**. This is expected: the printer is in **Service Mode**.

---

#### Step 2: The Windows USB Port Assignment Fix (Avoid Error 006)
On Windows 10/11, switching to Service Mode often assigns the printer to a new virtual port (e.g., `USB006`), whereas the existing Windows print queue still points to the previous port (e.g., `USB002`).

To quickly rebind the printer to the active service port, run **PowerShell as Administrator**:
```powershell
Set-Printer -Name "Canon MG5700 series" -PortName "USB006"
```

---

#### Step 3: Check Waste Ink Counter Percentage (`D=...`)
1. **Ensure paper is loaded** in the paper cassette.
2. Right-click **`ServiceTool_v4906.exe`** > **Run as administrator**.
3. Under the **Main** tab, click **EEPROM** (or **Test Print**).
4. The printer will feed and print a diagnostic sheet.
5. 🔍 **Look at the 2nd line of the printed page:**
   - Look for the value **`D=...`** (e.g., `D=100.4`).
   - **`D` represents the exact waste ink counter percentage!** (The 5B00 error triggers as soon as `D` reaches `100.0`).

---

#### Step 4: Reset the Waste Ink Counter
1. In **`ServiceTool_v4906.exe`**, stay on the **Main** tab.
2. Under **Clear Ink Counter** (or *Ink Absorber Counter*):
   - Make sure **Absorber** is set to **Main**.
   - Click the **`Set`** button next to it.
3. A confirmation dialog will pop up stating:
   > **`A function was finished`**
4. Click **OK** and close the application.

---

#### Step 5: Power Cycle & Restart
1. Turn off the printer by pressing the **Power** button.
2. Unplug the power cable for **15 to 20 seconds**.
3. Plug the power cable back in and power on the printer normally.
4. The LCD screen turns on normally, and **Error 5B00 is completely resolved!**
*(If you print another diagnostic sheet, the 2nd line will now show `D=000.0`).*

---

> [!WARNING] Hardware Note
> This software reset clears the electronic lock, but it does not physically empty or clean the absorbent felt pads inside the base of the printer. If your printer has logged over 10,000–15,000 pages, inspect or clean the pads to prevent ink overflow over time.

---

### 📦 Files Included
* **`ServiceTool_v4906.exe`**: Official Canon technician adjustment program compatible with MG5750 (Firmware V2.040).
* **`README.md`**: Complete documentation in French and English.
