# Italy Property Finance Planner

A personal property-search planner for Fabio & Andrea, from Mestre to Treviso. A single interactive page: no installation, account, database or build step needed.

## 1. Open and test on your Mac

1. Unzip the download. Keep the `italy-property-finance-planner` folder somewhere easy to find, such as Documents.
2. Open Visual Studio Code. Choose **File → Open Folder…** and select that folder.
3. In Finder, right-click `index.html` → **Open With → Safari** (or Chrome). The calculator works directly from the file, even offline.
4. Try changing **ING valuation** from `165000` to `155000`. Estimated cash remaining should change from **€13,706** to **€4,330** with the other defaults unchanged.
5. Tap an ⓘ button to read an explanation. Press Escape or Close explanation to return. Use **Reset example** to restore all values and clear checklist ticks.
6. Choose **Print / Save PDF**, then choose **PDF → Save as PDF** in your Mac print dialog to keep your scenario. Your inputs and checklist are not saved after reloading. No financial inputs are transmitted by the calculator.

## 2. Create a GitHub repository and upload

The easiest first upload is through GitHub in your browser; no Terminal commands are needed.

1. Sign into your GitHub account. Click **+ → New repository**.
2. Name it `italy-property-finance-planner`.
3. Choose **Public** for the straightforward free GitHub Pages route. The source and default example figures will be visible to anyone. Review them before publishing; do not add documents, account details or private information.
4. Select **Add a README file**, then **Create repository**. This normally creates the `main` branch; check the branch selector says `main`.
5. Click **Add file → Upload files**. Drag `index.html` and `README.md` from inside your local folder into the upload area. This replaces GitHub’s starter README.
6. Also upload `.gitignore`: press **Command–Shift–.** in Finder to show hidden files, then drag it in. It is useful housekeeping, but not required for the site to run.
7. Enter a message such as `Add property finance planner` and click **Commit changes** to commit to `main`.
8. Check that `index.html` is visible at the top level beside `README.md`. Do not upload the ZIP or a surrounding folder.

## 3. Enable the live website

1. In your repository, open **Settings → Pages** (under Code and automation).
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select branch **main**, folder **/ (root)**, then **Save**.
4. Wait a few minutes. Refresh this Settings page and click **Visit site** when it appears.
5. Your address will usually be `https://BRAUTECH.github.io/Italy-Property-Financial-Planner/`.
6. Open that address on your iPhone or Android phone. It remains interactive: all calculations run in the browser.

Official guide: [Configure a GitHub Pages publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## 4. Update later

1. Edit `index.html` in VS Code, press **Command–S**, then refresh the local browser page to test.
2. Open your GitHub repository → **Add file → Upload files**. Upload the updated `index.html` at the top level again, and commit the change to `main`.
3. GitHub Pages rebuilds automatically. Wait for the deployment to finish, then refresh the live site. Use **Command–Shift–R** in Chrome if you still see the old version.

For this simple workflow, keep your local folder as the master copy. If you edit a file on GitHub, download that version before your next local edit. No Git or VS Code extensions are required.

## Troubleshooting

- **404 / site not found:** allow several minutes; confirm Pages uses `main` and `/ (root)`, and the filename is exactly `index.html` in the repository root, not inside another folder.
- **Only a README appears:** `index.html` is missing or in the wrong folder.
- **No main branch to select:** finish the first commit, check the repository branch name, then return to Pages.
- **Pages options unavailable:** check repository visibility and your GitHub plan/organisation policy. Public repositories are the simplest route.
- **Deployment failed:** open the repository’s **Actions** tab and inspect the Pages deployment. Check that GitHub Actions is enabled for the repository.
- **Old version:** wait for Actions to finish and hard-refresh; confirm you updated `main`.
- **Numbers do not update:** enable JavaScript, open the actual HTML in a browser rather than Finder Quick Look, and reload. There are no external scripts to install.
- **Input is adjusted:** blank/invalid values use the original default; out-of-range values are bounded on leaving the field. Years are rounded to whole years. An explanation appears above the inputs.
- **Disabled field:** perizia is waived in the qualifying energy scenario; rendita is unused for VAT sales; the editable prima-casa substitute rate is unused when prima casa is No. Values are retained when switching back.
- **Saving a PDF:** print after choosing your scenario. Check print preview, paper size and scale; browser print layouts can vary.

## Model and limits

The acquisition calculations are preserved from the uploaded `Italy_Property_Finance_Planner_Fabio_Andrea.html`:

- Mortgage = lower of price and valuation × selected LTV, capped by income pre-approval. LTV input is limited to 95%; that cap does not establish eligibility or an actual lender offer.
- Equity = price minus mortgage. Valuation gap = positive difference between price and valuation. The gap is not added again to equity.
- Private/VAT-exempt purchase assumes the prezzo-valore method is applicable. Prima casa uses rendita × 1.05 × 110, then 2% registration tax (minimum €1,000), plus €100 fixed taxes. The non-prima comparison uses ×120 and 9%, with the same minimum and fixed taxes.
- VAT-sale comparison uses 4% with prima casa or 10% without, plus €600 fixed taxes. Luxury VAT and special cases are not modelled.
- Agency = price × commission × 1.22. Other entered costs are added once. Notary/technical estimates should include their VAT and expenses, excluding taxes already modelled.
- Mortgage substitute tax uses the editable prima-casa rate (default 0.25%), or 2% without prima casa.
- Energy B/A-or-better uses max(0, standard TAN − energy discount), and €0 perizia. Default 3.50% minus 0.20 percentage points gives 3.30%. C–G/unknown uses standard TAN and the retained editable perizia fee. Avoid entering an already energy-discounted rate as standard TAN.
- Monthly payment uses the standard amortising loan formula and full term. Zero TAN uses loan ÷ number of months. Rate changes, insurance and recurring ownership costs are excluded.
- The signal retains the original rules: red when remaining cash is negative; amber below €5,000 remaining or above €10,000 valuation gap; green otherwise. It is a cash-screening signal, not an affordability assessment or recommendation to buy.

Defaults are planning assumptions, not current quotes. Confirm eligibility, tax treatment, APE, bank fees, disbursement timing and final terms with ING, Nicoleta and your notary. The original €950 processing and €300 perizia assumptions are retained and editable.

References checked for the upgrade on 18 September 2026: [ING energy benefits](https://www.ing.it/faq/mutuo/ing-offre-un-mutuo-green.html), [ING mortgage information](https://www.ing.it/mutuo-arancio/mutuo-on-line.html), [Agenzia delle Entrate purchase guide](https://www1.agenziaentrate.gov.it/web_app_entrate/guida_acquisto_casa.html). These pages may change; the planner does not fetch live rates or tax rules.

## Verification

The finished JavaScript passed executable tests in a Node.js DOM test harness. HTML IDs, field labels, help targets, script references and responsive/print CSS were checked. Browser rendering tests could not run: automated Chrome was blocked by the environment, and the preview tool rejected local-file URLs. Visual layout, actual touch sizing, native dialog keyboard behaviour and PDF pagination still need a manual browser check.

| Price | Valuation | Mortgage | Cash required | Cash remaining |
|---|---|---|---|---|
| €165,000 | €165,000 | €155,100 | €23,294 | €13,706 |
| €165,000 | €155,000 | €145,700 | €32,670 | €4,330 |
| €165,000 | €150,000 | €141,000 | €37,359 | −€359 |

These are rounded results with original cost defaults, private seller, prima casa, 94% LTV and qualifying energy. The new effective TAN is 3.30%; rate changes affect monthly repayment, not acquisition cash.

Passed executable checks cover VAT/private and prima-casa branches, minimum registration tax, approval and LTV caps, zero interest/valuation, energy fee retention, invalid/blank/negative input handling, all 29 help handlers, focus-return handler and checklist/reset. Static checks confirm responsive breakpoints, 16px input fonts, 44px help buttons, 48px financial controls and print rules. A browser test script was prepared, but did not execute because the browser could not launch. No build tooling is needed to use or publish the project.

Manual check before publication: resize your browser to phone width (320–390px) and tablet width, confirm there is no horizontal scrolling, open and close help with keyboard and touch, check the printed preview, and test on your actual phone.
