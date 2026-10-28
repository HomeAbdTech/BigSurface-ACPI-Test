# BigSurface ACPI battery experiment — GitHub Actions

This package is **not a bootable EFI** and contains **no compiled driver**. It is a modified source snapshot based on the user's `BigSurface-dev.zip`, plus a GitHub Actions build workflow. The source was not proven to correspond to the installed BigSurface 1.1.0 binary.

## GitHub setup
1. Create a new private GitHub repository (or a dedicated experimental branch). Do **not** push these files into your working EFI repository.
2. On a computer with Git, clone the upstream BigSurface **dev** branch with its submodules:
   `git clone --branch dev --recurse-submodules https://github.com/Xiashangning/BigSurface.git BigSurface-ACPI-Test`
3. Compare the upstream checkout to the source in this package. The supplied source ZIP was dated August 2024 and may not match the current `dev` branch or the installed 1.1.0 binary. Do not blindly overwrite a different revision.
4. If it matches, copy these modified files into the cloned checkout:
   - `BigSurface/BigSurface.xcodeproj/project.pbxproj`
   - `BigSurface/BigSurface/Info.plist`
   - `.github/workflows/build-acpi-battery.yml`
5. Commit and push the experimental repository/branch. GitHub Actions > Build BigSurface (ACPI battery experiment) > Run workflow.
6. Download the `BigSurface-ACPI-Battery-EXPERIMENT-UNTESTED` artifact and inspect `bigsurface-build.log`, `binary-inspection.txt`, `battery-symbol-scan.txt` and the produced kext. A green build does **not** prove runtime compatibility.

## Safety
- Do **not** copy this archive directly into EFI.
- Do **not** enable SMCBatteryManager or replace BigSurface until build and compatibility checks are reviewed.
- Keep the full known-working EFI and recovery USB available.
- The workflow builds an unsigned x86_64 kext on GitHub macOS runners; it does not install anything.
- Build may fail due to Xcode/macOS SDK changes or submodule revisions; share the log for diagnosis.
