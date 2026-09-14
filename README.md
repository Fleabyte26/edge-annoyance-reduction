# Edge & OneDrive Annoyance Reduction

A safe, transparent PowerShell utility to permanently remove OneDrive persistence mechanisms, disable automated re-install triggers, and reclaim local user profile control.

## What This Script Does

1. **Pre-Flight Safety Check:** Audits Windows Known Folder Redirection (`User Shell Folders`) to prevent data loss if your Desktop, Documents, or Pictures are mapped to OneDrive.
2. **Kills Active Processes:** Terminates lingering background sync engines.
3. **Removes Scheduled Tasks:** Unregisters hidden OneDrive update tasks from Task Scheduler.
4. **Enforces GPO Hard-Stop:** Sets `DisableFileSyncNGSC = 1` under `HKLM\SOFTWARE\Policies\Microsoft\Windows\OneDrive` so Windows will not auto-deploy OneDrive in the background.
5. **Purges Active Setup Hooks:** Cleans out legacy registry keys that trigger silent re-installs on user login.
6. **Cleans Explorer Sidebar:** Hides orphaned OneDrive cloud icons from the File Explorer navigation pane.

## Usage

1. Open PowerShell with elevated privileges (**Run as Administrator**).
2. Clone or download `Remove-OneDrivePersistence.ps1`.
3. If script execution is restricted, temporarily permit it for the process:
   ```powershell
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass






Video Tutorial Outline
Title: How to Permanently Kill OneDrive (Without Breaking Your PC & Losing Files)

Tone: Candid, practical, technical deep-dive into persistence mechanisms.

Phase 1: The Trap (0:00 – 1:30)
Hook: Explain why clicking "Uninstall" on OneDrive is an illusion—it self-heals weeks later or after major Windows updates.

The Danger (Known Folder Move): Explain how Microsoft silently moves C:\Users\<Name>\Desktop into C:\Users\<Name>\OneDrive\Desktop. If an uninformed user rips out OneDrive without checking, their desktop icons and documents vanish, scaring them into thinking their PC is bricked.

Phase 2: The Persistence Vectors (1:30 – 3:30)
Visual Breakdown: Walk through how OneDrive hides across multiple layers:

User Run Keys: Standard startup triggers.

Active Setup (Installed Components): The legacy mechanism Windows uses to rebuild user profiles by re-running OneDriveSetup.exe behind the scenes.

Task Scheduler: The automated updater tasks that run silently under the user context.

Phase 3: The Safe Inspection (Pre-Check) (3:30 – 5:00)
Demonstrate how to check User Shell Folders via regedit or the script's built-in check.

Show viewers how to right-click Desktop / Documents > Properties > Location and ensure it says C:\Users\<User>\Desktop, not the OneDrive path.

Phase 4: Eradication via PowerShell (5:00 – 7:30)
Open PowerShell as Administrator.

Run the script step-by-step or as a unified tool from the Git repository.

Highlight the permanent blocker: DisableFileSyncNGSC = 1 in HKLM:\SOFTWARE\Policies\Microsoft\Windows\OneDrive (the Group Policy that prevents the background engine from reviving).

Phase 5: Verification & Wrap-up (7:30 – End)
Restart explorer.exe or log out/in.

Show that File Explorer is clean (no orphaned cloud folders in the sidebar), Task Scheduler is empty, and the PC maintains full local autonomy.
