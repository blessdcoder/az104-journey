# Lab 01: ARM Templates

**Module:** Deploy Azure infrastructure by using JSON ARM templates
**Domain:** Manage Azure identities and governance
**Date completed:** 13 November 2026

## Goal
Write an ARM template that deploys a storage account, then make it reusable by adding a parameter for the name.

## What I did
1. Created `azuredeploy.json` with an empty template and deployed it to `rg-az104-lab`.
2. Added a storage account resource, hardcoded its name and SKU.
3. Added a `storageName` parameter and deployed with `--parameters storageName=...`.
4. Added parameters and outputs as covered in the module.

## Problems I hit
- **Subscription not found** on `az storage account check-name`. Fixed by re-signing in and using the Default Directory tenant.
- **Invalid storage name** when braces `{}` were copied into the parameter value. Fixed by removing them.
- **Wrong command** when a line was missing the second dash in `--template-file`. Fixed by re-running the full command.

## Parameter test and revert
- Deployed with `storageSKU=Standard_GRS` to check that the SKU parameter changes the account. It updated the existing account instead of creating a new one.
- Redeployed with `storageSKU=Standard_LRS` to return the account to the template's default and keep costs low.
- Confirmed the SKU with `az storage account show`.

## Key takeaways
- Parameters let one template deploy different values without editing the file.
- Git tracks files, not folders; `.gitkeep` keeps empty folders in the repo.

## Files
- Template: `infra/arm/azuredeploy.json`
- Screenshots: `docs/screenshots/` (add after cropping out subscription IDs and email)