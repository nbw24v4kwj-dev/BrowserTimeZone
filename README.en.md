# Browser Time Zone

[简体中文](README.md) · **English**

Set an IANA time zone for websites in Chrome, such as `Asia/Shanghai`, `America/New_York`, or `Europe/London`. When the override is on, new pages use the saved time zone, including daylight saving rules for the date in question. The selected time zone and on/off setting persist in your Chrome profile across restarts.

Features include Chinese city search, favorites and recent zones, per-website rules, page consistency checks, multi-zone comparisons at a UTC date, and JSON settings backups. The toolbar ON/OFF badge shows the master switch. Check the popup for the current page's actual results.

This project is supported by [XOProxy](https://www.xoproxy.com/?utm_source=TimeZonePlugin), a **residential proxy network for global businesses** offering dynamic and static proxies.

## Install and use

This public repository currently contains product and usage documentation only. Earlier source files, source tags, and installation packages containing unminified code have been withdrawn. Any future public downloads will contain verified distribution builds. GitHub's automatic “Source code” archives contain documentation only and cannot be installed as an extension.

1. Use Chrome 138 or later. Once an official `browser-timezone.zip` distribution is available, extract it to a permanent folder.
2. Open `chrome://extensions`, turn on **Developer mode**, and click **Load unpacked**. Select the extracted folder that contains `manifest.json`.
3. Click the extension icon in the toolbar to open Browser Time Zone. Saving a time zone for the first time turns on the override. The extension applies it to sites allowed by Chrome's **Site access** settings.
4. Turn off **Time zone override** to restore the system time zone in open web pages without reloading them. The saved selection stays available. **Clear time zone** also restores the system time zone and removes the saved selection.
5. Reload open pages after turning the override back on or switching to another time zone.

Website rules match exact hostnames by default for HTTP and HTTPS across all ports. Select **Include all subdomains** to apply a rule for `antom.com` to every level below it, including `xx.antom.com` and `a.b.antom.com`. Set the scope with the checkbox. Existing rules keep their exact hostname match. IP addresses use exact matching.

More specific host rules take priority. For example, set Hong Kong time for `antom.com` and all its subdomains, then give `pay.antom.com` its own system time zone rule. Frames follow their own host rules. Unmatched hosts use the default zone, and the master switch controls all overrides. After removing a subdomain rule, reload the page to use a matching parent rule, or the default zone when no rule matches.

When the current website has a rule, the top preview shows that rule's time zone and local time, and its rule editor appears first. The default time zone is labeled separately and applies to unmatched websites. Reload open pages after saving a rule.

Click **Edit** beside a saved rule to change its hostname, time zone or system time zone mode, and subdomain scope, then select **Save changes** to update the original rule. **Cancel editing** discards unsaved changes. If a renamed hostname already has a rule, the popup reports the conflict and keeps both original rules.

City names such as “纽约”, “倫敦”, and “上海” resolve to IANA time zones. Save up to 12 favorites and keep 6 recent zones. The comparison date is entered in UTC, and each result uses the daylight saving rules for that instant.

The default shortcuts are `Alt+Shift+T` to toggle the override and `Alt+Shift+N` to enable and select the next favorite. Change the keys at `chrome://extensions/shortcuts`. Importing JSON first shows a preview. Applying it replaces the default zone, website rules, favorites, history, and interface language.

To update an existing installation, replace the files in the original extension folder and click **Reload** on `chrome://extensions`. Using the same folder keeps the saved time zone. Refresh pages that were open before the update once so the new version can restore their system time zone in place.

The popup follows Chrome's interface language by default. It supports English, Simplified Chinese, Traditional Chinese, Spanish, Russian, and Vietnamese, and uses English for other Chrome languages. It remembers your language choice. Select **Chrome language** to follow Chrome again. The XOProxy link in the popup opens the sponsor's website in a new tab with the fixed `utm_source=TimeZonePlugin` parameter.

## Check the current page

1. Save your time zone and reload the website.
2. Open the extension popup and select **Check again** under **Current page**.
3. Compare the expected and observed time zones. The result also reports interfaces that disagree or documents that need a reload.

The check follows each document's website rule. Frames with an uncertain initiating origin are marked unverifiable, and workers are outside the check scope. Check again after a page reload or navigation.

## Where it applies

The extension changes the default JavaScript time zone on HTTP and HTTPS pages it can access, including same-origin and cross-origin iframes. Chrome also matches related documents such as `srcdoc`, `data:`, and `blob:` using the initiating origin. A script that reads the initial `about:blank` window synchronously can still see the system time zone.

Chrome's built-in pages, the Chrome Web Store, dedicated workers (including module workers), shared workers, service workers, and worklets retain their original time zones. Sites can still specify a time zone explicitly or choose one based on your IP address or account settings. Chrome's native parsing behavior can still apply to some uncommon date strings. Historical dates can use a GMT offset label from Intl in the parenthetical part of the Date string.

After turning on the override or switching zones, reload open pages to apply the new setting to the document and its frames. Until reload, open documents can keep their previous zone while newly loaded frames use the new setting. Turning off the override restores date methods and the default zone for new formatters in accessible active documents. Existing formatters keep their original zone. A page restored from Chrome's back/forward cache may need a refresh.

The extension uses Chrome's content script API to apply the time zone before page scripts run in matching documents. Time zone scripts ship with the extension, and your time zone and language preferences are stored in the current Chrome profile. The system clock, operating-system time zone, and existing Date timestamps keep their original values.

Development source submissions are not accepted in this public repository.

## License

Copyright © 2026 nbw24v4kwj-dev. Previously published source versions were licensed under the [GNU General Public License v3.0 only (GPL-3.0-only)](LICENSE). Withdrawing those files does not revoke existing licenses.

The time zone catalog uses IANA time zone identifiers and ICU compatibility aliases. [IANA Time Zone Database](https://www.iana.org/time-zones)
