# Firefox New Tab: Pinned Shortcuts Only

A custom `userContent.css` snippet for Firefox that completely hides unpinned (history-based) top sites on the New Tab page, keeping only your manually pinned shortcuts and a perfectly aligned "+" button. 

## Why use this?
By default, Firefox automatically fills any empty slots in your New Tab shortcuts grid with your recent browsing history. If you want a clean, minimalistic, and privacy-friendly New Tab page with just a few specific shortcuts—without installing heavy third-party extensions that override the entire page—this native CSS tweak is the perfect solution.

## Features
* **Zero Extensions:** Uses Firefox's native UI customization engine.
* **Privacy Focused:** Prevents recently visited sites from flashing on your screen when you open a new tab.

## Installation

1. **Enable custom stylesheets in Firefox:**
   * Type `about:config` in the URL bar and press Enter (accept the risk warning).
   * Search for `toolkit.legacyUserProfileCustomizations.stylesheets`.
   * Double-click it to change its value to **`true`**.

2. **Locate your Firefox Profile folder:**
   * Type `about:support` in the URL bar and press Enter.
   * Look for the **Profile Folder** (or Profile Directory) row and click the **Open Folder** button.

3. **Create the `chrome` folder and CSS file:**
   * In the folder that just opened, create a new directory named exactly `chrome` (lowercase).
   * Inside the `chrome` folder, create a new text file and name it `userContent.css`. *(Note: Ensure your OS isn't hiding file extensions. It must not be named `userContent.css.txt`)*.

4. **Add the code:**
   * Open `userContent.css` with any text editor, paste the CSS code provided in this repository, and save the file.

5. **Apply the changes:**
   * Completely close and reopen Firefox. Pin your favorite sites, and watch the history tiles disappear!

## How it works (Under the Hood)
Recent versions of Firefox use a dynamic DOM structure for the New Tab page. The "Add Shortcut" (`+`) button is not a standalone placeholder; it is actually injected directly into the HTML of the *last* history tile in the grid. 

This CSS snippet utilizes the CSS `:has()` pseudo-class to accurately filter and format grid elements without breaking the layout:
* It looks for the iron-clad `data-l10n-id="topsite-label-pinned"` attribute to identify and protect your manually pinned sites.
* It completely removes (`display: none`) any standard history tiles that lack both a pin and the `.add-button` class.
* For the specific history tile holding the `.add-button`, it hides the inner logo and title of the history site, revealing the hidden `+` button and using Flexbox to center it perfectly in the remaining grid cell.

## Troubleshooting
* **Everything disappeared!** You need to have at least one site pinned manually for the layout to anchor properly. Pin a site by hovering over a tile, clicking the three dots, and selecting "Pin". Restart the browser, and it should work.
* **No changes applied after restart.** Double-check that `toolkit.legacyUserProfileCustomizations.stylesheets` is set to `true` in `about:config`, and verify that your folder is named `chrome` and placed directly inside the active Profile Folder.