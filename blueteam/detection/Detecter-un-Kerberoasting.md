# Détecter un Kerberoasting

> Article de démonstration.

| Source | Événement | Indice |
|---|---|---|
| Contrôleur de domaine | 4769 | `TicketEncryptionType = 0x17` |
| Contrôleur de domaine | 4769 | Beaucoup de SPN demandés par un même compte en peu de temps |

## Requête Splunk
```spl
index=wineventlog EventCode=4769 Ticket_Encryption_Type=0x17 Service_Name!="*$"
| stats dc(Service_Name) as spn_count by Account_Name, Client_Address
| where spn_count > 5
```

- [x] Activer l'audit « Kerberos Service Ticket Operations »
- [ ] Créer un compte honeypot avec un SPN
