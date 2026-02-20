# Phase 1: Breaking the Sequoia Gatekeeper (VMware Fusion)

## The Controversy: UTM vs. VMware on M4
Many users default to **UTM** on Apple Silicon because it "just works." However, for a professional lab, **VMware Fusion** offers superior hardware acceleration and network bridging—if you can get it to launch. On macOS Sequoia 15.6, the GUI installer is functionally broken for most users.

## Trials and Tribulations
- **Setback 1:** Drag-and-drop install failed. Double-clicking the app resulted in "File does not exist" errors.
- **Setback 2:** Gatekeeper Quarantine. macOS flagged the Broadcom binaries, preventing the app from executing its internal library.
- **Setback 3:** Missing Helper Tools. The GUI could not request the necessary root permissions to talk to the M4's virtualization engine.

## The CLI Solution (The "Magic" Commands)
We bypassed the GUI entirely using these terminal commands to "force-bless" the hypervisor:

1. **Remove the Quarantine Flag:**
   `sudo xattr -r -d com.apple.quarantine "/Applications/VMware Fusion.app"`
2. **Fix Internal Permissions:**
   `sudo chmod +x "/Applications/VMware Fusion.app/Contents/Library/Initialize VMware Fusion.tool"`
3. **Manual Kernel Initialization:**
   `sudo "/Applications/VMware Fusion.app/Contents/Library/Initialize VMware Fusion.tool" set`

**Outcome:** Hypervisor services stabilized. VMware Fusion is now natively operational on M4 Silicon.
