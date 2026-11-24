---
name: job-application-pack
description: Turn a saved job description into a full application pack: fit check, tailored CV, note or portal answers, and a ChatGPT review prompt. Use when Tom names a company whose JD is in JD_Inbox.
---

# Job application pack

Use when Tom names a company (for example "Setel") whose job description (JD) is saved in JD_Inbox and he wants to apply. Output: a fit verdict, a tailored CV, any extras the application needs, a review prompt, and everything filed in one folder.

This skill holds the workflow only. Facts live in `career-master`. CV rules live in the Project instructions. Never copy either into this skill or into a CV from memory.

## 0. Preconditions (stop and tell Tom if any fails)

1. Run inside the Project "My CV". Outside it, stop and ask Tom to open the Project.
2. Read from the Project: the Project instructions, the latest `career-master_vX_Y.md`, `cv-head-of-product_vX_Y.md` and `cv-review-notes_vX_Y.md`.
3. The folder must be connected: `/Users/tlozza/Library/Mobile Documents/com~apple~CloudDocs/MyDocuments/CV`. If not, ask Tom to add it (+ menu, "Add folder"). Do not fall back silently to the Project alone.
4. Source of truth: the Project. The folder is a synced mirror (see step 12). Never edit the master only in the folder.

Folder layout (under the CV folder): `JD_Inbox/`, `JD_Inbox/_skipped/`, `Applications/<Company> - <Role>/`, `Archive/`. The master, main CV and review notes sit in the folder root.

## 1. Intake

1. List `JD_Inbox/`. Match Tom's company name to file names, ignoring case. If several files match (for example two roles at one company), read all of them. If none or an unclear match, ask which file.
2. Read the JD (md, txt, pdf or screenshot). LinkedIn pages cannot be fetched: if only a link exists, ask Tom to paste the text, or search for the employer's own careers page.
3. Record: posting date or age, whether it still looks open, pay if stated, required years, location and work-mode rule, languages, company size.
4. If there are two roles at one company, ask which is the primary role. Name the folder, CV and note after it.

## 2. Normalise file names

1. JD files: `jd-<company>-<role>_vX_Y.md`. All lowercase. Underscores join words within a part; hyphens separate parts. Keep the existing version if the file has one; otherwise v0_1.
2. Rename in place in `JD_Inbox/` if wrong. Do not move yet.

## 3. Fit check

1. Apply the hard gates (location, level, years, right to work) using the job-scan config and master.
2. Map each key requirement to evidence in the master, with section numbers, or mark it "gap". Be honest about gaps (for example years asked versus years held).
3. Score fit 1 to 5. Give a verdict: apply / apply with a stated gap / skip. Challenge poor fits. Label each judgement as fact, assumption or suggestion.
4. Check consistency of the role with Tom's targets (Head or Director of Product, scale-up Chief Product Officer).

## 4. Gate 1 (Tom decides)

1. Present the fit check, numbered. State the Definition of Done (DoD) in a few lines (see below). Ask at most three questions, only if the answers change the work: borderline verdict, primary role, unclear extras.
2. Wait for Tom's go. If Tom says skip: move the JD(s) to `JD_Inbox/_skipped/`, add the reason to the file name or a one-line note, and stop.
3. After the go, work autonomously to the DoD. Ask mid-way only if blocked or a wrong guess would be costly or hard to reverse.

Standing DoD: CV passes the checks in step 7; every figure traces to the master; extras exist if the application needs them; ChatGPT review prompt written; all files named and filed; open decisions listed.

## 5. Extras

1. Decide with Tom what the application needs: cover letter, short note, portal answers, or nothing. Past packs used a note (Setel) and a cover letter plus two character-limited portal answers (DKSH).
2. Count characters for portal answers with code, not by eye. Flag en dashes, which some forms count as more than one character.

## 6. Build

1. CV: built only from the master and the JD. Follow the Project instructions in full (hard rules, writing style, ATS format, two pages). Never use [CONFIRM] facts.
2. File names: `cv-<company>-<role>_v0_1.md`, plus `note-` or `application-` files for extras. Put a comment at the top: source versions (master, main CV), JD file name, what changed from the main CV, gaps deliberately not claimed, and "draft - Tom to review before sending".
3. If tailoring needs a fact the master lacks: ask Tom, update the master first (new minor version), then the CV. A CV never leads the master.
4. Mirror JD keywords only where true. Never stuff keywords.

## 7. Check

1. Hard-rule check against the Project instructions (names, reasons for leaving, confidential items, titles, Crux8 dates, overclaiming wording).
2. Every figure traces to the master. Dates, titles and figures are consistent with LinkedIn and the Crux8 collateral; list every conflict.
3. Render the PDF and confirm two pages or fewer, single column, no tables, standard headings.
4. Markdown tables: same cell count in every row.

## 8. Review prompt (always)

1. Write `review-prompt-<company>-<role>_v0_1.md`: a ready-to-paste ChatGPT prompt containing the JD, the CV and any extras. Ask for numbered findings covering errors, omissions, weak assumptions, contradictions, overclaiming, keyword fit against the JD, and alternatives, each marked fact or opinion, with a severity.
2. The prompt must not name anything the hard rules forbid (no former ventures, employers Tom does not mention, reasons for leaving, or people). Describe them generically: "do not suggest adding any former venture, any reason for leaving, or anyone's name."
3. Add a Gemini prompt only for a top-priority role, or when Claude and ChatGPT disagree on something that matters. Say why the third opinion is worth the effort.

## 9. Processing review feedback

When Tom pastes reviewer feedback: sort each point as accept / reject / needs Tom's decision, with a one-line reason. Apply accepted points only. Raise the version. List new inconsistencies instead of silently fixing them.

## 10. Gate 2 (Tom decides)

1. Tom approves: v0_x becomes v1_0.
2. Export PDFs with no version numbers: `Thomas_Lozza_CV_<Company>.pdf`, `Thomas_Lozza_Cover_Letter_<Company>.pdf`, `Thomas_Lozza_Note_<Company>.pdf`.

## 11. File away

1. Create `Applications/<Company> - <Role>/`. Move the JD file(s) from `JD_Inbox/` into it. Do this when the pack is complete; do not wait for Tom's approval.
2. Save the CV, extras, review prompt and PDFs there. When a file gets a new version, move the previous version to the CV folder's `Archive/`.
3. Save the same drafts to the Project, following the Project's rule that only the latest version of each file is kept.

## 12. Mirror to the folder

1. Whenever the master, main CV or review notes get a new version: write the latest to the folder root and move the previous version to `Archive/`. The Project copy is written first.
2. Before overwriting, check the folder copy. If it is newer, or has a higher version, than the Project copy, stop and ask Tom.
3. If the folder is not connected, skip, say so, and catch up on the next run.

## 13. Log

When Tom confirms he has sent the application, add a row to the Google Sheet "Crux8 outreach starter kit" (applications tab): company, role, date, CV version sent, status, follow-up date. Read the sheet's headers and conventions first. Never send or apply on Tom's behalf, and never log before Tom confirms.

## 14. Hand-off

Finish with a short numbered summary: verdict, files created and where, review prompt location, open decisions, and one suggested next step. Interview preparation is a separate, optional follow-on; offer it only when asked.

## Style

UK English. Spell out abbreviations on first use, then the abbreviation in brackets. Plain, short sentences. Number points (A.1, A.2). Change only what Tom asked; list side effects instead of fixing them silently.
