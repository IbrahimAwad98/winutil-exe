# winutil-exe — regler

Detta repo bygger nattligen en exe av ChrisTitusTech/winutil (ps2exe) och
publicerar den som en GitHub Release. Se NOTICE — detta är en ompaketering,
inte originalprojektet.

## Regler

- Verifiera alltid `gh auth status` innan push.
- Aldrig `git push` utan mitt uttryckliga godkännande.
- Innan commit av workflow-ändringar: validera YAML-syntax lokalt.
- Ändra aldrig -noConsole-beslutet i `.github/workflows/build.yml` utan att
  först läsa kommentaren där om varför: -noConsole gör om Write-Host till
  MessageBox-popups och winutil skriver massor av status under körning.
- Inga hemligheter eller tokens i repot; workflowet använder `GITHUB_TOKEN`.
- Ikonen ligger i `assets/winutil.ico` och byts genom att ersätta filen —
  inte genom att ändra workflowet.

## Arkitektur

- `check`-jobbet körs på ubuntu-latest (1x-kostnad) och jämför upstream-tag
  mot vår senaste release; `build` (windows-latest, 2x-kostnad) körs bara när
  taggen är ny eller `force`-inputen är satt.
- Alla PowerShell-steg kör `shell: powershell` (5.1), inte pwsh — ps2exe är
  instabilt i PowerShell 7.
