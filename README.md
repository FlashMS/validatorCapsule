# Todd Wolf Project — Recruiter Showcase

## Overview
This project demonstrates modular app deployment, validator capsules, and symbolic registries built for both recruiters and market‑facing clarity. It compresses months of iteration into a clean capsule: homepage exposure, validator fingerprint, and registry overlays.

## Journey
- **Local Dev → Git + CLI**: capsule folders, shell triggers  
- **Azure App Service**: immutable config traps, TLS binding complexity  
- **Render & Railway**: cold starts, tunnel fallout, DNS ambiguity  
- **Azure Container Apps**: solved ingress, DNS, and cert binding with shell‑grade commands. Apex + www certs, `_dnsauth` TXT validation, and SNI binding finally brought the homepage live  

## The Azure Wall
Azure CLI enforced a circular dependency:
- `--certificate` is mandatory for `az containerapp hostname bind`  
- A cert requires a bound domain  
- No bypass via dummy app, REST patch, or ARM  

**Escape strategy:** inject a dummy app with full container definition, domain binding, cert creation, and explicit `dependsOn`.

## Capsules Included
- `index.html` → homepage capsule  
- `Dockerfile` → container definition  
- `capsule.json` → capsule metadata  
- `validator/fingerprint.json` → validator overlay  

## Command Capsules
```powershell
az containerapp env certificate create `
  --resource-group GravityBinaryRG `
  --name gravitybinary-env-eastus `
  --certificate-name vscgravity-com-root-cert `
  --hostname vscgravity.com `
  --validation-method TXT
