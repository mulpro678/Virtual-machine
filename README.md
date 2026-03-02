 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a/README.md b/README.md
new file mode 100644
index 0000000000000000000000000000000000000000..0beaedd153a1958a3fb6bb85fc6defbbb0d3f77c
--- /dev/null
+++ b/README.md
@@ -0,0 +1,42 @@
+# Virtual Machine Manager (EXE + Installer)
+
+This project provides a lightweight desktop **virtual machine manager** that can be packaged as a Windows `.exe` and distributed through an installer.
+
+## What it does
+
+- Lets you register VMs (name, disk, ISO, memory, CPUs)
+- Persists VM entries locally in `%USERPROFILE%\\.vm_manager\\vms.json`
+- Starts selected VMs through `qemu-system-x86_64`
+- Deletes VM entries from the manager list
+
+## Prerequisites
+
+- Python 3.11+
+- QEMU installed and available in `PATH`
+- For installer packaging: Inno Setup (ISCC)
+
+## Local run (dev)
+
+```powershell
+python vm_manager.py
+```
+
+## Build Windows EXE
+
+```powershell
+powershell -ExecutionPolicy Bypass -File scripts/build_installer.ps1
+```
+
+Output:
+- `dist/VirtualMachineManager.exe`
+
+## Build installer
+
+1. Open `installer/VirtualMachineManager.iss` in Inno Setup Compiler.
+2. Compile.
+3. Installer will be emitted to `dist-installer/VirtualMachineManagerSetup.exe`.
+
+## Notes
+
+- This is a manager UI/wrapper around QEMU command invocation. It does not include a hypervisor itself.
+- If hardware acceleration is not available, remove `-enable-kvm` from `vm_manager.py` for compatibility.
 
EOF
)
