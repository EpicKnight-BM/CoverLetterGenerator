# Cover Letter Generator

A meta-prompt that turns Claude into an interviewer, which builds a personal, fact-checked **cover-letter-writing Claude Skill** for you.

## What this actually is

[`cover-letter-generator-prompt.md`](cover-letter-generator-prompt.md) is not a skill itself. It's a prompt you hand to Claude, and when you do, Claude:

1. Interviews you about your CV, projects, GitHub/portfolio, and past cover letters.
2. Shows you its reading of your evidence and lets you correct it.
3. Runs an "honest calibration" pass to sort your skills into tiers (solid / real-but-junior / exposure-only) and pin down what you can and can't defend in an interview.
4. Maps your strongest evidence to the different role types you apply for.
5. Captures your writing voice, language preferences, and (optionally) a PDF letter design.
6. Produces a **fact sheet**, the single source of truth for every claim the skill is allowed to make, and lets you correct it before anything else is written.
7. Writes a single-file `SKILL.md` (interview steps + fact sheet + an optional PDF renderer appendix) that you can save as a real Claude Skill.
8. Test-drives the new skill on a real job ad and asks: *would you actually send this letter?*
9. Walks you through saving the skill for whichever Claude surface you use (claude.ai, Cowork, or Claude Code).

## Why the fact sheet matters

The core idea: a cover-letter generator that can invent plausible-sounding claims about you is worse than useless. It produces confident, generic praise that falls apart under interview questions. This process forces every claim in your future cover letters to trace back to something you actually said was true and defensible, with ownership, status (finished/in-progress/abandoned), and tier of expertise all made explicit up front.

## Privacy

This interview asks for personal, detailed information about your CV, work history, and projects. That data goes to Anthropic as part of your conversation, and by default Anthropic may use conversations to help improve its models unless you turn that off. You can disable it in Settings > Privacy on claude.ai (look for an option like "Help improve Claude" or "Improve the model for everyone"), or in the equivalent data controls setting for whichever Claude surface you're using. Check the setting before you run the interview if you'd rather your data not be used that way.

Separately: this prompt file is just a file. Running it doesn't send anything back to the creator, including the author of this repository. Your answers stay between you and Claude (and Anthropic, per the setting above); no third party sees them.

## How to use it

1. Open a conversation with Claude (claude.ai, Claude Code, or Cowork). Cowork is preferred, since it can save the resulting skill directly at the account level.
2. Attach `cover-letter-generator-prompt.md` to your first message (the file is long, so attaching it is more reliable than copy-pasting).
3. Have ready (all optional, but the more you bring the better): your CV, one or two past cover letters/application emails, links to your GitHub/portfolio/projects, and, if handy, a job ad you're already looking at.
4. Set aside roughly 15 to 30 minutes for the interview. You can stop and resume within the same conversation.
5. Follow the phases as Claude walks through them: read, calibrate, correct, and finally review the generated `SKILL.md`.
6. Save the resulting skill using the instructions Claude gives you for your specific Claude surface.

## Output

The end result is a `SKILL.md` file containing:

- Interview and drafting logic for letters, application emails, and application-form answers.
- A **fact sheet** of your real, verified experience, the only source the skill is allowed to draw claims from.
- (Optional) A Python/Playwright renderer that turns a letter JSON into a styled, one-page A4 PDF.

This skill file is meant to be reused across your entire job search, not regenerated per application. You update its fact sheet as you finish new projects or change roles, and it drafts every future letter from there.

## What the finished skill does

Once saved, the `SKILL.md` is what you actually use for each application. Give it a company name and a job ad (pasted text or a link), and it:

- Asks a single round of quick questions: letter, email, or form box; which language, if more than one was built in; a form field's exact wording and character limit, if relevant.
- Researches the role and the company: reads the ad closely, and finds one or two genuinely specific things about the company worth mentioning (no generic praise).
- Picks the strongest true overlaps between the ad and your fact sheet, following the "default lead by role type" table built during setup, and is honest about it when an ad asks for something you don't have.
- Drafts strictly from the fact sheet: your voice, your verified projects, your calibrated skill tiers. It cannot invent experience or round up a claim you flagged as unverifiable.
- Delivers the right format for the job: a 350-450 word letter, a 200-300 word email, or a 150-250 word form answer, each with the correct structure, salutation rules, and length for that format.
- If the PDF renderer was set up, turns the letter into a styled one-page A4 PDF using the look you chose during setup, refusing to render if a banned character or phrase slipped in.
- Runs a final judgment-level check before handing anything over, tailored to your specific risk areas (ownership mix-ups, name spelling, language consistency, and so on).
- Keeps its own fact sheet honest over time: it notices when the "last confirmed accurate" date is stale and asks what's changed, and it accepts direct updates ("I finished the X project", "add the Y certification") without needing a job ad in sight, always re-running the same ownership/depth calibration questions before adding anything new.
