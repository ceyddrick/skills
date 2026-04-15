---
description: Draft an X (Twitter) post. Accepts a link, an idea, or text to share. Fetches context, proposes 2-3 draft variants matching the user's voice. Use when the user wants to write or improve a tweet.
allowed-tools: Read, Bash, WebFetch, WebSearch
argument-hint: "<URL, idea, or text to share>"
---

# X Post Writer

Draft X posts that sound like the user, not like a brand or an AI.

## Configure the voice

Before drafting, establish the voice profile. The user should describe (or store in a voice-profile.md file) the following:

- **Bio**: one-line description of who they are
- **Audience**: who they write for
- **Tone**: direct/conversational/formal/playful — pick the register
- **Language**: primary language, when (if ever) to mix in others
- **Posting patterns**: what types of posts they publish (opinions, article promos, event recaps, data observations, humor, etc.)
- **Opinions and beliefs**: recurring takes, stances, allergies
- **Vocabulary**: words they use, words they would never use
- **Banned words and phrases**: corporate speak, hashtags, emojis — whatever is off-limits

Use those settings to inform every draft. The examples below are illustrative; swap them for the user's actual preferences.

## Voice rules

### DO
- Write like you talk to a friend who works in the same field
- Start with a hook that stops the scroll (fact, tension, question, provocation)
- Have an opinion. "C'est cool mais..." is better than "Voici un outil interessant"
- Use short sentences. Break lines for rhythm.
- Use ASCII diagrams (box-drawing characters) when explaining a process or framework in long-form posts
- Tag companies and people when relevant (@AnthropicAI, @MistralAI, etc.)
- End with something memorable: a punchline, a question, a sharp observation
- Use "tu" when addressing the reader (if writing in French)
- Let humor come naturally, don't force it

### DON'T
- Never use hashtags (unless the voice profile says otherwise)
- Never use emojis (unless quoting someone)
- Never write corporate voice: "ravi de partager", "excited to announce", "stay tuned"
- Never start with "Je suis ravi", "Tres heureux", "Content de"
- Never use LinkedIn-speak: "Retour d'experience", "N'hesitez pas a"
- Never write threads longer than 3 tweets unless the content truly demands it
- Never add a CTA like "Partagez si vous etes d'accord"
- Never pad. If it fits in one tweet, don't stretch it to two.
- Never write generic openers: "Mon truc du moment", "Je voulais partager"

## Post formats

### 1. Article promo (link to your blog)

```
[Hook: problem or tension in 1-2 lines]
[Bridge: what the article solves, 1 line]

[URL]
```

Example (good):
> Tu as genere une app avec Claude Code. Ca tourne en local. Et maintenant ?
> "Push sur GitHub." Sauf que personne ne t'a jamais explique ce que ca veut dire et le concept associe. Github pour les non-devs, explique.
> [link]

Rules for article promos:
- Open with the READER's problem, not "j'ai ecrit un article"
- The link should feel like the answer, not the point
- One tweet max. No thread for promos.

### 2. Opinion / reaction

```
[What happened or what you saw, 1 line]
[Your take, 2-3 lines. Be specific.]
[Optional: punchline or question]
```

Example (good):
> C'est cool ce que @MistralAI fait avec son text-to-speech. Mais des que la demo passe en francais... pourquoi cet accent toujours bizarre ?
> Ca fait des annees que le TTS galere avec le francais. Oui, l'anglais a plus de data, mais on a aussi largement de quoi faire en FR.
> C'est plus un manque de moyens. C'est un manque de priorite, surtout pour une societe basee a... Paris. Cocorico, zut alors.

Rules:
- Lead with the thing, not your feelings about the thing
- Critique is fine. Be fair but direct.
- Tag the company/person when critiquing (shows confidence)

### 3. Event recap

```
[What you did / saw, 1 line]
[One specific takeaway or moment, 1-2 lines]
[Tag people you met / organizers]
[Optional: photos]
```

Rules:
- Be generous with tags and credit
- One concrete detail beats a generic "c'etait genial"
- Photos boost engagement massively

### 4. Data / observation

```
[Numbers or facts, raw]
[Your interpretation, 1-2 lines]
[Optional: provocative conclusion]
```

Rules:
- Let the data do the heavy lifting
- Your take should add something the numbers don't say on their own
- Comparisons and timelines work well

### 5. Personal / humor

```
[Setup]
[Punchline or unexpected twist]
[Optional: photo]
```

Rules:
- Keep it short. Humor dies in long posts.
- Self-deprecating > bragging
- Photo of friends/situation makes it land better

### 6. Long-form / essay

For deeper takes that need more than a tweet. Think mini-blog-post in the feed.

Structure:
- **Hook** (1-2 lines): tension, surprising fact, or contrarian claim
- **Setup** (2-3 lines): context, why this matters now
- **Sections** (2-3 blocks): each with a clear point. Problem/reality/lesson works well.
- **Optional: ASCII diagram**: a simple box-drawing visual that summarizes the argument. Max 40 chars wide. This is a real differentiator in the feed.
- **Uncomfortable truth** (1-2 lines): the thing nobody wants to say
- **Payoff** (1-2 lines): sharp conclusion, callback to hook, or actionable takeaway

Example ASCII diagram:
```
Before:
  idea -> tweet -> silence

After:
  idea -> data -> angle
          |
        draft -> unslop -> post
          |
        engagement <- reply
```

Rules for long-form:
- Only use this format when the content genuinely needs 500+ characters
- Every section must earn its place. If a section can be cut without losing meaning, cut it.
- The ASCII diagram is optional but powerful. Use it when explaining a process, comparison, or before/after.
- Run an unslop mental pass before finalizing: no AI vocabulary, no filler transitions, no generic conclusions
- Keep the voice throughout: direct, opinionated, conversational

## Workflow

### 1. Parse input

- **URL**: fetch the content with WebFetch, extract the key message
- **Idea/text**: work directly with it
- **No argument**: ask what the user wants to post about

### 2. Analyze

- What type of post is this? (article promo, opinion, event, data, humor, long-form)
- What's the hook? What stops someone from scrolling?
- Who should be tagged?
- Is there a contrarian angle or a non-obvious take?
- Check the voice profile for beliefs and tone settings to inform the angle

### 3. Draft

Produce **2-3 variants**, each with a different angle or format:

```
---
**Option 1** (format: [type]) — [X characters]
[draft]

**Option 2** (format: [type]) — [X characters]
[draft]

**Option 3** (format: [type]) — [X characters]
[draft]
---

Laquelle tu preferes ? Je peux ajuster.
```

Rules for drafts:
- Each variant should feel different, not just be a rewording
- Show character count (280 char limit for single tweet, but X allows longer posts)
- For longer posts (>280 chars), indicate where the fold would be
- If the content works as a single tweet, prefer that over a long post
- Always write with proper accents in the target language

### 4. Iterate

If the user picks one and wants changes, refine. Don't restart from scratch.

## Quality checklist

Before presenting drafts, verify:
- [ ] Would the user actually say this out loud to a friend?
- [ ] Does the first line make you want to read the rest?
- [ ] Is there an opinion or a point of view? (not just information)
- [ ] No hashtags, no emojis, no corporate speak?
- [ ] Proper accents throughout?
- [ ] Relevant @mentions included?
- [ ] Under 280 chars if it works as a single tweet?

## Anti-patterns

- Never produce a single "perfect" draft. Always give options.
- Never write a post that could come from any generic tech account
- Never use the word "partage" as in "je partage cet article"
- Never write "Petit thread sur..." or "Thread interessant sur..."
- Never add "Qu'en pensez-vous ?" at the end (engagement bait)
- Never write in a language the user didn't ask for
- Never write long-form just to seem thorough. If the take fits in a tweet, tweet it.
