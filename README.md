# ResetReady

A portable Windows app to **pack your essentials, reset Windows, and unpack them**. Version 0.5.3, built for your Zen / games / Nord / Windhawk setup.

## New in 0.5.3

Fixed the extra navbar outline during mouse selection: keyboard focus uses a separate keyboard-only dashed indicator, while the glass fill and border travel together as one selection capsule.

## New in 0.5.2

Both navbar states now share a 64-pixel height and 32-pixel outer corner radius. Compact mode retains its 116-pixel width; only the width changes during expansion. Status clearance stays consistent.

## New in 0.5.1

The floating navbar is smaller: 420 × 64 expanded and 116 × 44 collapsed. Icons, labels, selection spacing and status clearance were adjusted to match.

## New in 0.5

- The progress pill is hidden at startup and while idle. Operation progress stays visible while busy; completion, cancellation or stopped-operation messages dismiss after five seconds, with hover pausing dismissal. Title and action text now share a vertical center. Activity remains accessible from **Settings → Storage → Activity**.
- Navigation uses neutral silver/graphite glass in both themes, independently of the yellow page accent. The glow is removed. A live blurred sample of the content sits beneath neutral material layers, a fine rim and a translucent selection capsule. This is an original WPF interpretation of Liquid Glass, not Apple's native renderer or an imported Figma component.
- Content fills the viewport through the bottom of the window and scrolls behind the floating navbar. Bottom clearance lives at the end of the content, so the final actions can scroll fully into view. The game table's viewport follows the window height instead of its previous fixed 430-pixel limit; virtualization is retained.
- Downward scrolling collapses the navbar into a small active-tab capsule at the lower left. Scroll upward, hover over it, or tap it to expand all tabs. Navigation remains available by keyboard. Reduced visual effects removes the motion and live blur while preserving the compact behavior.
- New generated archive-and-recovery icon, packaged at 16, 24, 32, 48, 64, 128 and 256 pixels for Windows. The source PNG and the built-in image_gen prompt are under `assets`; `Build-Icon.ps1` encodes the Windows ICO without installing any dependencies.

## New in 0.4

- Bundled Inter and Inter Display typography, with a bright yellow accent, warm gold links and softer yellow surfaces in both themes. The fonts load from the app folder; no system font installation is needed. Keep the `fonts` folder beside the executable. The original font license is included there.
- Scrolling reverses immediately from the current position, with shorter easing and Windows' configured wheel-line count. Nested panes retain their own scrolling.
- **Games → Library** now has a **Pack** toggle for each game. Choices persist across scans and restarts. **Select all / Select none** affect the currently filtered rows. Custom save folders share the selection in Pack. Read-only archive views show what was actually saved, including **Excluded** entries.
- Exclusions reach the game engine: packing performs a fresh preview, then passes only eligible selected titles using UTF-8 standard input. Unicode names and large libraries do not need one enormous command line. A completely excluded library never falls back to backing up everything. Ludusavi's disabled entries remain disabled, and unsupported games still need custom folders.
- Home shows the next action, selected save size, destination, reinstall count, latest created pack and reset checks. **Open & verify** opens the latest pack in Restore. Cloud upload remains a manual check. Packs created before this version are not automatically discovered as the latest pack; open them in Restore.
- **Windows → Clean setup** prepares a reviewable preset: PowerToys, 11 optional bundled-app removals and nine quieter defaults. This button selects choices; **Review & apply** displays the exact plan before running it. PowerToys is also selected by default in the reinstall list. Terminal and 7-Zip are optional. Existing tools are kept rather than reinstalled.
- New per-user policy choices turn off diagnostic-based suggestions, promotional Spotlight notifications and third-party Spotlight suggestions. They require Pro, Enterprise or Education and are skipped on Home. Previous setting values are retained for **Undo tweaks**. Organization policies and Windows versions can affect results.
- Windows setup also links directly to Startup, Notifications, Game capture, Default apps, Storage and Start settings for manual fine-tuning. Tool installation runs before the selected tweaks/removals; a failure can leave earlier steps applied. Undo restores tweaks, not removed apps or newly installed tools.

## New in 0.3

- Compact floating glass navbar with a sliding selection capsule. The sidebar and visible app branding are removed.
- Dark appearance, enabled by default. Switch between dark and light in **Settings → Appearance**; the choice is saved.
- Soft page crossfades, directional movement, button feedback and smooth mouse-wheel scrolling. Nested game lists scroll independently and hand off at their boundaries.
- Thin rounded scrollbars brighten and widen on hover. Horizontal scrollbar commands follow their orientation.
- Window controls sit at the top right. Maximizing respects the monitor's work area, including a taskbar at the top.
- **Reduce visual effects** switches to opaque navigation and disables these animations. Windows' animation preference is respected as well.

## New in 0.2.1

The interface now uses short labels, compact status summaries and fewer descriptions. Section info buttons reveal help on demand; row details appear in tooltips. Recovery notes are collapsed by default. Restore confirmations, reset acknowledgement, plaintext export warnings and failure/cancellation notices remain available at the relevant step. Backup and restore behavior is unchanged.

## New in 0.2

- A complete WPF interface redesign inspired by iOS 26 and Apple's Liquid Glass guidance: translucent floating navigation, light grouped content, pill controls, original vector icons, custom window controls, short page transitions and matching dialog sheets. This is a Windows implementation, not Apple's native rendering engine. Windows file choosers remain native. The Settings page offers reduced visual effects.
- A searchable **Games** library with **All**, **With saves** and **To check** filters. **Library** distinguishes **Not scanned**, **Save detected**, **No save detected**, **Skipped** and **Needs review**. Steam, Epic and GOG metadata is used where accessible, and supported saves discovered by Ludusavi are included even when their launcher isn't identified. A scan is read-only and may download the game engine's database. A missing match is not proof that no save exists.
- **Pack** lists the games actually recorded in the archive, with **Backed up** status, source, included file counts, sizes and save paths. Custom folders added with **Add saves** are listed separately as games. Packs created with 0.1 can still be opened; older game-engine reports are used when available, but old custom folders cannot be retrospectively classified as games.
- Readable operation progress shows the current stage, current file, bytes, file counts, phase percentage, measured throughput and approximate remaining time when enough data is available. Scans, password derivation and external engine work use an indeterminate indicator and elapsed time rather than an invented percentage. Different stages have their own percentages; the app does not claim a single overall percentage for work that cannot be measured. Technical logs are available through **Activity**.

To check coverage: **Games → Scan**. To see what was saved: create or open a verified pack, then **Games → Pack**. “Save detected” only describes local discovery; it never claims a backup has been created.

The packing, restore, installers, Nord handling and optional Windows changes remain available. The new archive metadata is compatible with the existing encryption format.

## Start

Extract the entire ResetReady folder, then double-click **ResetReady.exe**. Keep `ResetReady.exe.config` beside the executable and keep the `tools` and `fonts` folders. Windows 10/11 with .NET Framework 4.8 is required; no Python, Node, SDK, installer or subscription is needed. The bundled game engine targets x64 Windows.

Opening the app does not uninstall apps, apply tweaks, copy browser profiles or start a backup. It detects standard profile folders and available engines, and saves local preferences. Windows changes have their own review screen.

## Before resetting Windows

1. In **Settings**, choose **Scan saves**. Ludusavi is included. Check that the games you care about are present. Its GUI lets you configure extra game-library roots and custom games. The first scan may download its game database.
2. Close Zen, games, and Windhawk. In **Pack**, select the detected data you want. Zen is selected by default. Add missing game-save or settings folders with **Add saves** or **Add folder**.
3. Review the app installer list. Zen, NordPass, NordVPN, Windhawk and PowerToys are selected by default; Steam is optional. Add other essentials by their exact WinGet package ID. Only selected apps are offered for reinstalling; this does not bundle their program files.
4. Optionally export a NordPass CSV yourself using NordPass Settings → Import and Export, then attach it with **Attach export**. The app does not interact with your password manager or ask for your master password. You can instead rely on your synced vault and sign in again after reinstalling.
5. Write down NordVPN preferences in **Recovery notes**: preferred location, auto-connect, kill-switch choices and split-tunneling rules. Do not put passwords or recovery codes in these notes. Recognized local NordVPN preference files are also offered as reference snapshots when found.
6. Choose a `.rrpack` filename in a cloud-synced folder, or save locally and upload it yourself. Use a new backup password of at least 12 characters, repeat it, and create the pack. There is no password recovery.
7. After the app verifies the pack, open **Restore**, select the pack, and verify it again. Inspect the file inventory and the **Games → Pack** list. A verified file proves that the archive is intact, not that every game or account was covered.
8. Keep a copy of this entire app folder and the pack outside the disk that will be reset. Wait until the cloud provider confirms the upload has completed. Make sure you can access that cloud account and your backup password after the reset.

This is an early working version. Test your important data before using it as the only copy for a reset. The app does not perform the Windows reset.

## After resetting Windows

1. Download your pack and extract this entire app folder. Start ResetReady and verify the pack under **Restore**.
2. Use **Install selected** to download current versions through WinGet's community catalog. Microsoft's App Installer supplies WinGet; there is a link in Tools if it is missing. Installation can require internet access and normal publisher / administrator prompts. ResetReady does not bypass installer hash checks.
3. Close newly installed browsers and games. Choose the data to restore and review the destinations. Custom folders have editable destinations. Recovery notes and NordVPN references can be extracted to a folder you choose.
4. If game-library paths or drive letters changed, add game path redirects. Preview the game restore paths before restoring saves. The old Windows user folder is mapped to your current account automatically. Inspect saves outside your user folder carefully.
5. Restore the selected data. Existing files that are replaced are copied to a private local recovery folder first. New files are recorded in a journal. The app shows where recovery data is kept.
6. Start Zen. If it opens a fresh profile, use `about:profiles` to select the restored profile. External / nonstandard Zen profiles require the custom-folder route and manual profile registration; the app blocks an incomplete standard-profile backup when it detects that layout.
7. Sign in to NordPass and NordVPN yourself. Check vault sync. If you extracted a NordPass CSV, import it inside NordPass and remove the plaintext CSV yourself when finished. Reapply NordVPN preferences from the notes / reference snapshot. Launch each important game and check its save.

## What is preserved

| Essential | Handling and limits |
| --- | --- |
| Zen | Full standard `%APPDATA%\zen` profile tree, excluding caches, crash dumps and lock files. Includes profile data used for settings, extensions, bookmarks, tabs and spaces. Browser version changes and individual extensions can still need attention. |
| Other browsers | Detected standard Firefox, Chrome, Edge and Brave profiles can be selected. Windows-bound encrypted logins / cookies are not guaranteed to transfer after a reset. |
| Game saves | Ludusavi's configured game database, roots and enabled entries, plus your custom folder selections. The report records what the engine actually found. Unknown games, disabled entries, server-only saves, unusual launchers and nonstandard paths can need manual additions. |
| NordPass | Optional user-exported CSV inside the encrypted pack, plus a reinstall entry. CSV is not a complete backup of every vault item type; passkeys, attachments and some fields may be omitted. Synced-vault access and your recovery method still matter. |
| NordVPN | Reinstall entry, recovery notes, and recognized `user.config`, `settings.json`, or `settings.xml` files under standard local / roaming NordVPN folders when found. Logs, update folders and unrelated files are excluded. Snapshots extract for reference; automatic preference / session migration across versions is not implemented. |
| Windhawk | Recent versions: native CLI offline export/import. Older installed versions: mod binaries, mod sources and both Windhawk registry views. Close Windhawk for legacy operations. Legacy restore needs **Run as administrator**, and compatibility depends on Windhawk version and Windows architecture. Portable Windhawk requires selecting its native CLI; otherwise use custom folders and manual recovery. |
| Other essentials | Any selected folder, encrypted recovery notes, and selected WinGet app installer IDs. Files outside a selected folder are not implicitly included. Custom-folder symbolic links / junctions need their actual target folder selected separately. |

## Windows

This optional page lets you choose bundled apps such as Teams, Clipchamp, News, Weather, Solitaire, the Microsoft 365 hub, Outlook, Phone Link, Feedback Hub, Tips, Maps, To Do and the standalone Copilot app. Only the current account is targeted. Apps provisioned for future users are unchanged; Windows may bring apps back after upgrades. Windows can refuse removal of protected or managed packages.

Edge is sent to its **supported uninstaller**. Availability depends on Windows version and region. There is no forced deletion, region spoofing or removal of WebView2. If Windows refuses, the activity log says so and you can inspect Installed apps.

Optional user-level tweaks reduce suggestions, hide Widgets / Chat / search / Task View buttons, show file extensions and open Explorer to This PC. Additional policy choices reduce tailored and promotional suggestions on supported editions. Their previous registry values are saved before application. **Undo tweaks** restores a chosen history; it does not reinstall removed apps. Some changes need sign-out and can be overridden by Windows updates or organization policies. App removal can delete local app data, so pack essentials first.

Windows Update, Defender, Microsoft Store, drivers, WebView2 and gaming services are not removed or disabled by the catalog. This is a supported clutter-reduction profile, not a modified Windows installation image or a guarantee of the smallest possible OS footprint.

## Storage and recovery

- By default, local settings, engine downloads, temporary files and retained recovery data are under `%LOCALAPPDATA%\ResetReady`.
- `.rrpack` archives use a random salt and IV, AES-256-CBC encryption, HMAC-SHA-256 authentication, and PBKDF2-HMAC-SHA-256 with 600,000 iterations and independent encryption / authentication keys. This is a new, unaudited archive format, not a claim of an independent security review.
- Authentication is checked before decrypting. Verification then checks file hashes, sizes, archive paths and the manifest. ZIP traversal, alternate data streams, duplicate paths and Windows device aliases are rejected. Junctions and symlinks are blocked; Windows Cloud Files placeholders are recognized so synced folders can be used.
- Browser / custom data is streamed directly into the encrypted archive. Ludusavi output, native Windhawk exports and verification ZIPs use private temporary plaintext storage. Those temporary folders are removed after normal completion, error or cancellation. A forced shutdown can leave `temp\rr-work-*` folders; inspect and remove these yourself with the app closed. Deletion is normal filesystem deletion, not guaranteed secure erasure.
- Pre-restore copies are retained in `recovery\rr-work-*`. `file-changes.jsonl` maps original destinations to saved previous copies; an empty `previous` means a newly created file. Game restores additionally save the exact destination files reported by the engine to `game-files-before`, with `game-file-changes.jsonl` mapping them back, and create a Ludusavi safety backup for saves recognized by the current configuration. Older Windhawk registry recovery is JSON for manual recovery; native exports use Windhawk's own import.
- Restore and Windows changes are not all-or-nothing transactions. Cancel / external-tool failures can leave partial changes. Review the recovery folder and activity log before retrying. Keep sufficient free disk space for temporary verification, snapshots and previous data.
- The app has no telemetry, cloud credentials or automatic uploads. Internet use is for selected installers, optional engine setup and Ludusavi's database / normal engine behavior. Your cloud sync client manages uploading whichever finished pack you place in its folder.

## Source, build and validation

Source is in `src`. An optional `Build.ps1 -OutputDirectory <folder>` builds a separate copy when the current app is open. Run `Build.ps1` with Windows PowerShell or PowerShell to rebuild using the C# compiler included with .NET Framework. No NuGet packages or SDK installation is required. Keep the adjacent `.exe.config` file for .NET version and long-path settings.

`Test-UI.ps1` builds and runs 51 isolated appearance and scrolling regression checks in memory, including bundled font resolution, yellow control contrast and immediate upward reversals: repeated theme switches after template application, text and status contrast, reduced motion, horizontal scrollbar commands, nested scroll ownership and animation reset.

`Test.ps1` builds and runs 50 core, game and setup-plan checks, followed by real-Ludusavi integration checks against synthetic data in a newly created temporary directory. The tests exercise password / tamper rejection, path validation, preservation of overwritten files, Unicode and long paths, and actual game backup / preview / redirected restore. They do not apply live Windows tweaks or operate on your browser, password manager or actual games. Live Windows uninstalls, fresh-OS migrations and every Windhawk / NordVPN version have not been tested.

Advanced environment overrides: `RESETREADY_DATA` selects the app data directory; `RESETREADY_GAME_CONFIG` selects an existing Ludusavi configuration directory. Neither contains or supplies a backup password.

## Primary references

- [Apple: Tab bars](https://developer.apple.com/design/human-interface-guidelines/tab-bars)
- [Apple: Build a UIKit app with the new design](https://developer.apple.com/videos/play/wwdc2025/284/)
- [Supplied Figma UI kit](https://www.figma.com/community/file/1651309003795292092/ios-and-ipados-27): the community file could not be read through the research tool; navigation was developed from the supplied screenshots and Apple's published guidance.


- [Inter 4.1 and its font license](https://github.com/rsms/inter/releases/tag/v4.1)
- [Microsoft: Install PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/install)
- [Microsoft: Experience policy settings and registry mappings](https://learn.microsoft.com/en-us/windows/client-management/mdm/policy-csp-experience)
- [Microsoft: Windows Settings links](https://learn.microsoft.com/en-us/windows/apps/develop/launch/launch-settings)
- [Microsoft WinGet catalog: Windows Terminal](https://github.com/microsoft/winget-pkgs/tree/master/manifests/m/Microsoft/WindowsTerminal) and [7-Zip](https://github.com/microsoft/winget-pkgs/tree/master/manifests/7/7zip/7zip)


- [Zen profile location and guidance](https://docs.zen-browser.app/faq)
- [Ludusavi documentation](https://github.com/mtkennerly/ludusavi) and [CLI](https://github.com/mtkennerly/ludusavi/blob/master/docs/cli.md)
- [NordPass export instructions](https://support.nordpass.com/hc/en-us/articles/360007646477-How-to-export-passwords-from-NordPass)
- [Windhawk releases and native export/import support](https://github.com/ramensoftware/windhawk/releases)
- [Microsoft's WinGet documentation](https://learn.microsoft.com/windows/package-manager/winget/)
- [Microsoft's Edge policy / regional uninstall documentation](https://learn.microsoft.com/deployedge/microsoft-edge-update-policies)
- [Chromium credential protection](https://github.com/chromium/chromium/blob/main/docs/security/faq.md)
- [Apple's Liquid Glass materials guidance](https://developer.apple.com/design/human-interface-guidelines/materials)

See `THIRD-PARTY-NOTICES.txt` for the bundled game engine and its license archive.
