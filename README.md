# job-search

A Claude-powered job hunt for Ziggy. Instead of a scraper that dumps everything, Claude searches the web
deeply, filters hard, scores what is left, finds a recruiter for the best ones, and helps tailor the CV.

## How it works
1. `config/profile.yaml` says what you want (seniority up to 4 years, location priority, job families).
2. `config/search-terms.md` lists titles, employers and job sources per family.
3. The `deep-job-search` skill runs the sweep and writes `results/YYYY-MM-DD-report.md` and updates `data/tracker.csv`.
4. The `tailor-cv` skill turns one posting plus `data/experience-bank.md` into a tailored CV, cover note and recruiter message.

## Using it
Open a Claude Code session on this repo and say:
- "Run the deep job search" for a full sweep.
- "Tailor my CV for <link>" for one application.
- "Update the tracker: I applied to X" to keep status current.

## Files you edit yourself
- `config/profile.yaml`: change rules and priorities any time.
- `data/experience-bank.md`: the more you put here, the better the tailoring. Fill the TODOs.
- `data/tracker.csv`: change `status` (new, applied, interview, rejected, offer, skip).

## Notes
- The cloud session can search and read the web but cannot run a classic scraper. Claude does the searching itself.
- Claude never applies, sends messages, or makes accounts for you. It prepares drafts; you send.
- Recruiter details come only from public professional sources, with a confidence level. Nothing is guessed silently.
