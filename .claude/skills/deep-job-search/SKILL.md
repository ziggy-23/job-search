---
name: deep-job-search
description: Run a deep job sweep for Ziggy across many boards and company career pages, filter and score results against config/profile.yaml, find the recruiter or hiring contact for each strong match, and update the tracker. Use when asked to find jobs, run the job search, sweep for postings, or find recruiters.
---

# Deep job search

Goal: surface postings Ziggy could realistically get and win, not everything that exists.
A short ranked list of good matches beats a long list of noise.

## Step 0. Load context (always)
1. Read `config/profile.yaml` (seniority rules, location tiers, families, deprioritise list).
2. Read `config/search-terms.md` (titles, employers, sources).
3. Read `data/tracker.csv` so you never re-report a job already in it (match on company + title, or URL).
4. Read `data/experience-bank.md` only if you also need to judge fit in detail.

## Step 1. Sweep (go wide, then deep)
Use WebSearch and WebFetch. The shell cannot reach job sites, so do not try curl or scripts.
- For each job family in profile.yaml, run several searches per title group and per location tier.
  Mix English and Spanish (and French for Paris).
- Hit the ATS-domain searches (greenhouse, lever, ashby, workable, smartrecruiters, personio): these hold many
  Barcelona postings that never reach the big boards.
- Check target-employer career pages directly for each family's employer list, not just search results.
- Fetch the actual posting page for every candidate. Titles lie. Read the requirements.
- Prefer postings under ~30 days old. Note posted date when visible; skip clearly expired ones.
- Search in parallel where you can (multiple independent searches in one step). If working at scale, you may
  hand one job family to a subagent each, but only when the user asked for a big sweep.

## Step 2. Filter (hard rules)
Drop a posting if any of these is true:
- Requires more than 4 years of experience (see profile.yaml). No years stated means KEEP.
- Title contains an excluded seniority word (senior, manager, head of, director, ...) UNLESS it is a
  genuine stretch worth trying. In that case keep it and label it STRETCH with one line on why.
- It is a deprioritised type (call centre, generic customer service, FMCG/on-trade, ETT/staffing sales, hospitality).
- Requires a language or work permit Ziggy lacks with no way around it (e.g. native German).
- Duplicate of something in the tracker.

Do NOT drop for: degree mentioned, missing a specific tool that is learnable in weeks, salary not posted.
Ziggy is happy to stretch into unfamiliar functions as long as he can credibly pitch it, so lean inclusive
on skills but strict on seniority and role type.

## Step 3. Score (0-100) and tier
Score = fit of function to Ziggy's story (40) + location tier (20) + seniority fit (15) + language bonus (10)
+ employer quality/brand and growth (10) + freshness (5).
Location points: tier1=20, tier2=17, tier3=13, tier4=10, tier5=8, tier6=4.
Label each result A (80+, apply this week), B (60-79, worth applying), C (40-59, backup).
Show only A and B in the main report. List C in the tracker only.

Reference for "what a great match looks like": Simon-Kucher Associate Consultant, Barcelona
(Ziggy already got an interview there). Similar: analytical, client-facing, strategy or research heavy,
international, entry to 3 years.

## Step 4. Recruiter and contact linking (for A and B roles)
For each A/B posting, find who to contact. Use only publicly available professional information.
1. Check the posting itself for a named recruiter or "contact" line (some, like Zurich's, are signed by the recruiter).
2. Search `"<company>" recruiter Barcelona`, `"<company>" talent acquisition Spain/EMEA`, and the LinkedIn public
   profile snippets that appear in search results. Prefer: named talent acquisition / recruiter for that office
   or business unit, then the hiring team lead if named in the posting, then a general careers email.
3. If the role is via an agency (Hays, Michael Page, Randstad, Talent Brand, ...), the agency consultant named on
   the posting is the contact.
4. Record: name, title, where you found it (URL), and confidence (high = named in posting or official page,
   medium = public LinkedIn snippet, low = guess).
5. NEVER invent a name or email address. If you cannot find one, write "not found" and suggest a search Ziggy
   can run himself. Do not guess email formats as if they were fact; if you suggest a pattern, label it a guess.
6. Do not gather personal details beyond professional role and public work contact. No personal emails, phone
   numbers of private individuals, or home information.

## Step 5. Write the outputs
1. Append every new posting (A, B and C) to `data/tracker.csv`. Columns are in that file's header.
   Status for new rows is `new`.
2. Write `results/YYYY-MM-DD-report.md` with:
   - one-paragraph summary (how many searched, kept, dropped and why in one line)
   - a table of A roles, then B roles: company, title, location (tier), posted, score, why it fits in one line,
     apply link, recruiter/contact + confidence
   - STRETCH roles in their own short section
   - "Companies worth watching" (employers that fit but have no open role now)
   - Any source that failed or looked blocked
3. Keep report language plain and short. No filler.
4. Commit results to git if asked. Never push anything the user has not asked to be pushed.

## Step 6. Offer next steps
End with: which 3 roles to apply to first, and offer to run the `tailor-cv` skill for any of them.

## Honesty rules
- Only report a role if you opened the posting or a reliable mirror of it. Never fabricate a posting, company,
  salary, deadline or recruiter.
- If a fetch is blocked (LinkedIn login walls are common), say so and use the search snippet, marked as unverified.
- Do not apply to jobs, message recruiters, or create accounts on Ziggy's behalf. Preparing drafts is fine.
  Sending anything needs Ziggy's explicit yes.
