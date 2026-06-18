# Kuza Kazi Control Panel — Setup Guide

**Read the part with your name. Do only that part.**

This is a slider panel that lives inside Excel and drives the Kuza Kazi model. You move sliders, it
updates the model and recalculates. The model file is **locked so no one can break it** — the panel is
the only way to change anything.

**The three of you:**
- **Greg** (Greg@digittal.io, Digittal account) — does a one-time setup, then installs.
- **Barry** (barry@digittal.io, Digittal account) — installs.
- **Marlyn** (personal Microsoft 365 account) — installs; her steps differ slightly and are spelled out.

**Two files matter:**
- `Kuza_Kazi_OptionA_locked.xlsx` — the model. Everyone opens this.
- `manifest.xml` — the small file that tells Excel about the panel. Whoever installs needs this.

---

## PART 1 — GREG ONLY, ONCE  (about 15 minutes)

The panel is a small web page, so it has to live at a web address that everyone's Excel can reach.
The easiest free option is GitHub Pages.

1. Go to **github.com** and sign in (make a free account if you don't have one).
2. Click **New** to create a repository. Name it `kuza-kazi-panel`. Choose **Public**. Click **Create repository**.
3. Click **Add file -> Upload files**. From the add-in zip, drag in `taskpane.html`, `commands.html`,
   and the whole `assets` folder. Click **Commit changes**.
4. Click **Settings** (top of the repo) -> **Pages** (left menu). Under **Build and deployment**, set
   **Source** to **Deploy from a branch**, **Branch** to `main`, folder `/ (root)`. Click **Save**.
5. Wait about a minute. Your web address is now:
   `https://YOUR-GITHUB-USERNAME.github.io/kuza-kazi-panel`
   Check it works: open `https://YOUR-GITHUB-USERNAME.github.io/kuza-kazi-panel/taskpane.html` in a
   browser. You should see the panel. It will say "not in Excel" — that's expected here.

Now put that address into the manifest:

6. Open `manifest.xml` in a plain text editor (Notepad on Windows, TextEdit on Mac).
7. Use **Find & Replace**. Replace **every** `__BASE_URL__` (there are 9) with your address from step 5,
   with **no slash at the end**. So replace
   `__BASE_URL__`  with  `https://YOUR-GITHUB-USERNAME.github.io/kuza-kazi-panel`  -> **Replace All**.
8. **Save** the file.

**Then send two files to Barry and Marlyn:** the edited `manifest.xml` and
`Kuza_Kazi_OptionA_locked.xlsx`. Email, Teams, shared drive — however you like.

---

## PART 2 — INSTALL THE PANEL

Find your name.

### Greg & Barry (Digittal accounts) — easiest: Greg pushes it to both of you

Because you're on the company's Microsoft 365, Greg can install the panel for **both** of you at once
from the admin center. Barry then does nothing.

**Greg does this once:**
1. Go to **admin.microsoft.com** and sign in as Greg@digittal.io.
2. Left menu: **Settings -> Integrated apps**.
3. Click **Upload custom apps**.
4. App type: **Office add-in**. Choose **Upload manifest file (.xml) from device** and pick the edited
   `manifest.xml`.
5. Assign it to **Greg@digittal.io** and **barry@digittal.io** (or choose "Entire organization").
6. **Accept permissions -> Finish deployment.**

It appears in both of your desktop Excels automatically — usually within minutes, occasionally up to a
day the first time. **Then just close and reopen Excel.** A **Kuza Kazi** button appears on the **Home** tab.

> If Greg is not an admin, or step 3 (**Upload custom apps**) is missing or greyed out, both of you use
> **Manual install** below instead.

### Marlyn (personal account) — manual install

Personal accounts don't have the admin push, so you install it yourself using **Manual install** below.
The web option is the quickest.

---

## MANUAL INSTALL

(For Marlyn, and for Greg/Barry if the admin push isn't available to them.)
You only need the `manifest.xml` file for this. Pick one of the two ways.

### Quickest — Excel in a web browser (about 2 minutes, any computer)

1. Go to **excel.office.com** and sign in.
2. Open **Kuza_Kazi_OptionA_locked.xlsx**. (If it's not there yet, upload it to your OneDrive first,
   then click it to open.)
3. Click the **Insert** tab -> **Add-ins**. In the window that opens, if you don't see an upload
   option, click **More Settings**, then click **Upload My Add-in**.
4. Click **Browse**, choose `manifest.xml`, click **Upload**.
5. A **Kuza Kazi** button appears. Done.

> This remembers the panel for **that browser only**. If you clear your browser history or use a
> different browser, just upload `manifest.xml` again the same way.

### Permanent — the installed Excel app

**On a Mac:**
1. Open **Finder**. Press **Command + Shift + G**.
2. Paste this exactly and press Enter:
   `~/Library/Containers/com.microsoft.Excel/Data/Documents/wef`
   (If there's no `wef` folder, go to the `Documents` folder above it, make a new folder named exactly
   `wef`, then open it.)
3. Copy `manifest.xml` into that folder.
4. **Quit Excel completely** and reopen it.
5. **Kuza Kazi** appears on the **Home** tab (or under **Insert -> Add-ins -> My Add-ins**).

**On Windows:**
1. Put `manifest.xml` in a folder, for example `Documents\kuza-manifest`.
2. Right-click that folder -> **Properties** -> **Sharing** tab -> **Share...** -> add yourself ->
   **Share** -> note the path it shows (it looks like `\\YOUR-PC\kuza-manifest`) -> **Done** -> **Close**.
3. Open Excel -> **File -> Options -> Trust Center -> Trust Center Settings -> Trusted Add-in Catalogs**.
4. Paste that `\\YOUR-PC\...` path into the **Catalog Url** box -> **Add catalog** -> tick
   **Show in Menu** -> **OK** -> **OK**.
5. **Close Excel completely** and reopen it.
6. **Home** tab -> **Add-ins -> More Add-ins** -> click **SHARED FOLDER** at the top -> select
   **Kuza Kazi Control Panel** -> **Add**.

---

## PART 3 — USING IT  (everyone)

1. Open **Kuza_Kazi_OptionA_locked.xlsx**.
2. **Home** tab -> **Kuza Kazi -> Control Panel**. The panel opens on the right.
3. It loads the model's current numbers. Move a slider or pick a curve shape — the panel updates as you
   drag, and when you **let go**, it writes the value into the model and recalculates.
4. The three boxes at the top (Pessimistic / Conservative / Optimistic 5-year totals) update after each
   change.
5. To set the detailed per-stream numbers, open the **Calibration** section, pick a scenario, and type
   into the grid.
6. **Read from Excel** reloads the model's current values into the panel. **Reset to defaults** puts
   every input back to neutral.

You can't break the model by using it — every formula is locked, and the panel does the unlocking and
re-locking for you behind the scenes.

---

## IF SOMETHING DOESN'T WORK

- **No "Kuza Kazi" button after installing** — close Excel completely and reopen. For the admin push,
  give it a few minutes (up to a day the very first time).
- **Panel is blank or just spinning** — the web address isn't reachable. Greg: open your
  `.../taskpane.html` address in a browser; if it doesn't load, recheck Part 1 steps 4-5 and that all 9
  `__BASE_URL__` were replaced.
- **"Couldn't reach the workbook"** — make sure `Kuza_Kazi_OptionA_locked.xlsx` is the workbook you're
  actually clicked into, then press **Read from Excel** in the panel.
- **(Digittal accounts) "Upload My Add-in" is missing or greyed out** — your admin has turned off
  personal add-ins. Use the admin push in Part 2 instead, or ask IT to allow custom add-ins.
- **Sliders move but the sheet doesn't change** — you've got a different workbook open. Open the locked
  model and press **Read from Excel**.

---

## FOR GREG — editing the model yourself

The workbook is locked so the others can't break it. To edit it (for example, recalibrating on the
Inputs sheet): **Review -> Unprotect Sheet** (there's no password), make your changes, then
**Review -> Protect Sheet** again. Or keep your own unlocked master copy and re-send the locked one when
you publish updates. The lock is passwordless, which stops accidental edits. If you want to stop someone
deliberately unprotecting it, say so and I'll add a password the panel knows.

---

### Technical notes (reference)
- The panel writes to the **Control Panel** sheet and reads totals from **Summary 5-stream**; those
  sheet names must stay as they are.
- In the add-in zip: `taskpane.html` (the whole panel), `commands.html` (a required stub — keep it),
  `manifest.xml`, and the `assets` icons. Only `manifest.xml` is installed into Excel; the rest is
  served from Greg's web address.
- The add-in is identical on Windows and Mac; the only thing that differs is how you install it, above.
