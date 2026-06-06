---
description: Rewrite filter that strips AI slop patterns from text in English or French. Detects language automatically. Preserves ideas, logic, and argument. Use when the user wants to clean up AI-generated or AI-sounding text.
allowed-tools: Read, Bash
argument-hint: "<text, file path, or URL> [FR|EN]"
---

# Unslop — AI Writing Filter

Takes text and rewrites it to sound human. Does NOT change the ideas, argument, or logic. Changes only the phrasing and structure that marks it as AI-generated slop.

## Input

Accept text in any of these forms:
- Pasted directly as the argument
- A file path → read the file
- No argument → read from clipboard via `pbpaste`

This skill is the single source of truth for anti-slop rules. Other skills reference it instead of duplicating lists.

## Language detection

1. If the user passes `FR` or `EN` as an argument, use that language
2. Otherwise, detect from the text content
3. Apply the corresponding replacement table + shared structural rules

---

## ENGLISH — What to rewrite

### Hard replacements EN — always fix, no judgment needed

| Slop | Replace with |
|------|-------------|
| "delve into" | "look at", "dig into", "explore" |
| "unpack" (writing context) | "break down", "explain" |
| "navigate the complexities of" | say what's actually complex, or cut |
| "ever-changing landscape" | cut entirely or be specific |
| "the landscape of X" | cut or say what you mean |
| "synergies" | say specifically what combines and why |
| "leverage our learnings" | "use what we learned" |
| "leverage" (as verb) | "use" |
| "holistic approach" | say what you actually mean |
| "this underscores" / "this signals that" | state the actual opinion directly |
| "it's worth noting that" | just say the thing |
| "it bears mentioning" | just say it |
| "lean into" | say what you're actually doing |
| "foster a culture of" | be specific |
| "in an effort to" | "to" |
| "at the end of the day" | cut or rewrite the conclusion |
| "ultimately, the goal is" | cut — filler bow |
| "moving forward" | cut |
| "in conclusion" | cut |
| "as we navigate" | cut or rewrite |
| "actionable insights" | say the actual actions |
| "robust" (unless literally about software) | specific adjective or cut |
| "seamlessly" | cut |
| "game-changer" | cut or be specific |
| "paradigm shift" | cut or be specific |
| "let's dive in" | cut |
| "in today's world" / "in today's fast-paced" | cut |
| "cutting-edge" | cut or be specific |
| "groundbreaking" | cut or be specific |
| "revolutionize" | say what actually changes |
| "empower" | say what's enabled specifically |
| "harness the power of" | "use" |
| "unlock the potential" | say what becomes possible |
| "ecosystem" (unless literally biological) | say what you mean |
| "double down on" | "invest more in" or "focus on" |
| "north star" | "goal" or "priority" |
| "deep dive" | "detailed look" or cut |
| "key takeaways" | "what matters" or just list them |
| "at scale" (filler usage) | cut or specify the scale |

### Content patterns EN — rewrite when detected

| Pattern | What it looks like | Fix |
|---------|-------------------|-----|
| Significance Inflation | "stands as", "is a testament", "pivotal moment", "underscores its importance", "reflects broader", "setting the stage for", "indelible mark", "deeply rooted" | State the actual fact without inflating. Before: "This marked a pivotal moment in the evolution of digital marketing." After: "The company launched its first programmatic ad campaign in 2019." |
| Superficial -ing Analyses | "highlighting", "underscoring", "emphasizing", "ensuring", "reflecting", "symbolizing", "contributing to", "fostering", "showcasing" as filler depth | State the actual cause/effect. Before: "The platform grew 40% YoY, showcasing the team's commitment to innovation and highlighting the importance of user experience." After: "The platform grew 40% YoY. Most of that came from a single referral loop they built in Q2." |
| Promotional Language | "boasts a", "vibrant" (figurative), "rich" (figurative), "profound", "exemplifies", "commitment to", "must-visit" | Replace with specific facts/numbers. Before: "The company boasts a vibrant team with a profound commitment to delivering results." After: "The company has 45 employees. Revenue grew 32% last year." |
| Vague Attributions | "Industry reports", "Experts argue", "Some critics argue", "several sources" with no specific citation | Name the source or cut. Before: "Experts believe AI will transform the marketing landscape." After: "A 2024 Gartner survey found 67% of CMOs plan to increase AI spend next year." |
| Formulaic Challenges & Future | "Despite its X, faces challenges...", "Despite these challenges, continues to Y", "Future Outlook" sections | State what actually happened. Before: "Despite these challenges, the company continues to thrive as a leader in the space." After: "Customer churn hit 8% in Q3. They hired a retention team in October." |
| Copula Avoidance | "serves as", "stands as", "marks", "represents", "boasts", "features", "offers" instead of simple is/are/has | Use the simple verb. Before: "The newsletter serves as a valuable resource for marketers." After: "The newsletter is a resource for marketers. 12K subscribers open it weekly." |
| Rule of Three Overuse | Forcing ideas into groups of three. Triple adjectives, triple nouns, triple parallel clauses. | Just list what matters, even if it's two things or four. Before: "The event features keynote sessions, panel discussions, and networking opportunities." After: "The event has talks and panels. There's also time for networking between sessions." |
| Elegant Variation / Synonym Cycling | Excessive synonym substitution to avoid repeating a word. | Just use the same noun. Before: "The CEO shared his vision. The business leader outlined the strategy. The company head detailed the plan." After: "The CEO shared his vision and outlined the strategy." |
| False Ranges | "From X to Y" where X and Y aren't on a meaningful scale. | Just list the things. Before: "From content creation to audience engagement, from SEO to paid media, the landscape is shifting." After: "Content, SEO, and paid media are all changing. Here's what actually matters." |

### Structural patterns EN — always rewrite

- Em dash (—) as clause separator → rewrite as two sentences, or use a comma
- Paragraph openers: "Moreover," / "Furthermore," / "Additionally," / "That said," / "Importantly," / "Notably," / "Interestingly," → cut the opener, restructure
- "Not X, but Y" / "Instead of X, Y" forced negation → rewrite as positive statement
- Staccato triple repetitions: "not this, or this, or this" → rewrite plainly
- Excessive adverbs before weak verbs: "quietly underscores", "powerfully demonstrates", "fundamentally transforms" → strip adverb, strengthen verb if needed
- Corporate therapist voice: "lean into our strengths", "foster accountability", "empower our teams" → say what's actually happening
- Bold word: colon: explanation (the AI list format) → convert to prose or normal bullets
- Rhetorical question as section opener: "So what does this mean?" → cut, just answer
- Collaborative artifacts: "I hope this helps", "Of course!", "Certainly!", "Would you like...", "let me know", "here is a..." → cut entirely
- Knowledge-cutoff disclaimers: "As of [date]", "While specific details are limited", "based on available information" → cut entirely
- Sycophantic tone: "Great question!", "You're absolutely right!", "That's an excellent point!" → cut entirely
- Generic positive conclusions: "The future looks bright", "Exciting times lie ahead", "continues their journey toward excellence" → cut or rewrite with specifics

---

## FRENCH — What to rewrite

### Hard replacements FR — always fix, no judgment needed

| Slop                                          | Replace with                                            |
| --------------------------------------------- | ------------------------------------------------------- |
| "Il convient de noter que"                    | dire la chose directement                               |
| "Il est important de souligner que"           | dire la chose directement                               |
| "Il est a noter que"                          | couper, dire la chose                                   |
| "Force est de constater que"                  | dire le constat directement                             |
| "Il va sans dire que"                         | si ca va sans dire, ne pas le dire                      |
| "Dans un monde ou" / "A l'ere de"             | couper ou etre specifique                               |
| "Dans un contexte ou"                         | couper ou etre specifique                               |
| "N'hesitez pas a"                             | utiliser l'imperatif directement                        |
| "En effet" (ouverture de phrase)              | couper                                                  |
| "Par ailleurs" (transition molle)             | couper ou reformuler le lien logique                    |
| "De surcroit"                                 | couper                                                  |
| "Qui plus est"                                | couper                                                  |
| "En ce qui concerne"                          | "pour", "sur"                                           |
| "Dans le cadre de"                            | "pour", "pendant", ou etre specifique                   |
| "Mettre en lumiere"                           | "montrer"                                               |
| "Jouer un role cle" / "jouer un role crucial" | dire ce que ca fait concretement                        |
| "Au coeur de"                                 | etre specifique                                         |
| "S'inscrire dans une demarche de"             | dire ce qu'on fait                                      |
| "Constituer un levier"                        | dire ce que ca permet concretement                      |
| "Un enjeu majeur" / "un enjeu de taille"      | dire quel est l'enjeu concretement                      |
| "Incontournable"                              | dire pourquoi c'est important                           |
| "En somme" / "En definitive"                  | couper ou reformuler la conclusion                      |
| "A cet egard"                                 | couper                                                  |
| "Dans cette optique"                          | couper ou etre specifique                               |
| "Veritable" (intensifieur)                    | couper ("un veritable tournant" → dire ce qui a change) |
| "Bel et bien"                                 | couper                                                  |
| "Ni plus ni moins"                            | couper                                                  |
| "Tout un chacun"                              | "chacun", "tout le monde"                               |
| "Se positionner comme"                        | "etre", "devenir"                                       |
| "Accompagner le changement"                   | dire quel changement, comment                           |
| "Embarquer les equipes"                       | dire comment concretement                               |
| "Creer de la valeur"                          | dire quelle valeur                                      |
| "Monter en competences"                       | "apprendre", "se former a"                              |
| "Porter une vision"                           | dire la vision                                          |
| "L'avenir nous le dira"                       | couper — conclusion vide                                |
| "Seul le temps nous dira"                     | couper — conclusion vide                                |
| "A l'heure ou"                                | couper ou etre specifique                               |
| "Tant sur le plan X que sur le plan Y"        | simplifier                                              |
| "Permettre de" (surutilise)                   | verbe direct                                            |
| "Il est essentiel de"                         | dire ce qu'il faut faire                                |
| "Il apparait clairement que"                  | dire la chose                                           |
| "On ne peut que constater"                    | constater directement                                   |
| "Autant d'elements qui"                       | couper, lister les elements                             |
| "Un tournant decisif"                         | dire ce qui change et pourquoi                          |
| "Plus que jamais"                             | couper                                                  |

### Structural patterns FR — always rewrite

- Tiret cadratin (—) comme separateur de clause → reformuler en deux phrases, ou virgule
- Ouvertures de paragraphes : "Ainsi,", "Des lors,", "De plus,", "En outre,", "Par consequent,", "Toutefois,", "Neanmoins," → couper l'ouverture, restructurer
- Le pattern "X. Mais pas n'importe quel X." (emphase fragmentee) → reformuler en une phrase
- "Ce n'est pas X, c'est Y" (fausse opposition) → formuler positivement
- "Qu'il s'agisse de X, de Y ou de Z" (enumeration artificielle) → lister normalement ou reformuler
- Nominalisation excessive : "la mise en place de", "la prise en compte de", "l'accompagnement de" → utiliser le verbe directement
- Voix corporate therapeute : "accompagner", "embarquer", "federer", "porter un projet" → dire ce qui se passe concretement
- Format liste avec gras + deux-points + explication (format AI) → convertir en prose ou puces normales
- Question rhetorique en ouverture de section : "Alors, qu'en est-il ?" → couper, repondre directement
- Conclusion passe-partout applicable a n'importe quel sujet → reformuler avec du specifique ou couper

---

## Shared rules (both languages)

### Persistence — no filler drift

Once this skill is triggered in a conversation, the anti-slop filter stays active on EVERY following response, not just the first. It must not dilute or relax as the turns go on — active every response once triggered, no filler drift. Keep applying the full replacement tables and structural rules until the user explicitly says to stop.

### Slop patterns that need judgment — fix if present
- Conclusion that could apply to any company or topic → rewrite with something specific or cut
- Paragraph that sounds smart but can't be summarized in one sentence → rewrite for clarity
- Excessive hedging chains: "it could be argued that" / "on pourrait arguer que" → cut, state the point
- Paragraph that restates the previous one with different words → merge or cut

### What good human writing looks like
- Has opinions, not just reporting
- Varied sentence rhythm (short punches + longer explanatory ones)
- Specific details over vague claims
- Simple verbs (is, has, does) over elaborate constructions
- Acknowledges uncertainty or mixed feelings honestly
- First-person perspective when appropriate
- Concrete examples with names, dates, numbers
- Humor, edge, or personality when the register allows it

### What NOT to change
- The user's actual ideas, opinions, arguments, examples, data
- Sentence order and paragraph structure (unless a specific pattern above requires it)
- The user's voice and register (casual stays casual, formal stays formal)
- Technical terms and jargon that are accurate and necessary
- Short, direct sentences that are already clean
- Correct use of em dashes for parenthetical asides (only fix overuse as clause separators)

---

## Output Format

Produce output in exactly this order:

---

**Langue** : [FR/EN]
**Slop Score** : XX/100
*(90-100 = clean human writing, 70-89 = minor AI tells, 50-69 = obvious AI patterns, 0-49 = full AI output)*

**What was fixed** / **Ce qui a change** :
- [Brief list of specific changes. Quote original → replacement. Skip categories with no changes.]

---

[The full rewritten text. No commentary, no preamble. Just the clean text.]

---

## Scoring Guide

Start at 100. Deduct points for each pattern detected. Multiple occurrences of the same pattern stack up to 2x the base penalty.

| Category                                                                        | Penalty per occurrence |
| ------------------------------------------------------------------------------- | ---------------------- |
| Banned phrase (hard replacement table)                                          | -5                     |
| Content pattern (significance inflation, promotional, vague attributions, etc.) | -8                     |
| Structural pattern (em dash overuse, transition openers, etc.)                  | -5                     |
| Collaborative artifact / sycophantic tone / knowledge disclaimer                | -10                    |
| Filler conclusion or "sounds smart, means nothing" paragraph                    | -10                    |
| Generic positive conclusion                                                     | -10                    |

Score interpretation:
- **90-100**: Clean human writing. Ship it.
- **70-89**: Minor AI tells. Quick fixes needed.
- **50-69**: Obvious AI patterns. Significant rewrite needed.
- **0-49**: Reads like ChatGPT output. Full rewrite.
