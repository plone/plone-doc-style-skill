# Diataxis framework

Read this before writing a tutorial or an explanation, when a page seems to need two quadrants, or when auditing existing pages for mixed content.

## Contents

- The two axes
- Tutorials (learning-oriented)
- How-to guides (task-oriented)
- Reference (information-oriented)
- Explanation (understanding-oriented)
- Diataxis decision matrix

Plone organizes documentation using the Diataxis framework (<https://diataxis.fr/>).
Content is classified by what the reader needs. User role plays no part.
**Each page must belong to exactly one quadrant.**

## The two axes

|                        | Acquisition (study/learning) | Application (work/doing) |
|------------------------|------------------------------|--------------------------|
| **Action (practical)** | Tutorial                     | How-to guide             |
| **Cognition (theory)** | Explanation                  | Reference                |

- **Axis 1, action versus cognition:** practical doing versus theoretical knowing.
- **Axis 2, acquisition versus application:** learning a skill versus applying a skill at work.

Crossing these boundaries is the single most common documentation failure.
Every piece you write must sit cleanly in one quadrant.

## Tutorials (learning-oriented)

**Purpose:** A guided lesson where a beginner acquires skills by doing.
The stated goal (build X) differs from the real goal (learn skills A, B, C).

**Analogy:** Teaching a child to cook. The dish is the vehicle. Knife skills, timing, and food safety are the actual learning outcomes.

### Essential properties

- **Meaningful**: gives a genuine sense of achievement.
- **Successful**: every learner must be able to complete it.
- **Logical**: follows a sensible learning progression.
- **Usefully complete**: covers all necessary actions, concepts, and tools the learner needs.

### What to DO

1. **Do not try to teach.** Provide experiences that produce learning. Trust the process.
2. **Show the destination up front.** "In this tutorial we will build a custom content type that..."
3. **Deliver visible results at every step.** Each action produces output the learner can see and verify.
4. **Maintain a narrative of expectations.** "You will notice that the page now shows..." / "The terminal should output..."
5. **Point out what to observe.** Learners need prompting: "Notice that the URL has changed."
6. **Target the feeling of doing.** Cultivate the pleasurable, confident rhythm of skilled practice.
7. **Use strategic repetition.** Repeat important steps so they become familiar.
8. **Stay concrete.** Move from one concrete action to the next. Never abstract.
9. **Aspire to perfect reliability.** The tutorial must work for every user, every time. Eliminate environmental surprises.

### What NOT to do (anti-patterns)

- **No abstraction or generalization.** Stay concrete and particular.
- **No explanation.** A tutorial is NOT the place for explanation. Keep it to the bare minimum needed to proceed. Link elsewhere for depth.
- **No choices or alternatives.** One path, one outcome. Eliminate options.
- **No information overload.** Ruthlessly cut anything non-essential.

### Language patterns

- First-person plural: "We will create...", "Let's check..."
- Imperative + unambiguous: "First, do x. Now, do y."
- Narrative cues: "Notice that...", "Remember that...", "You should see..."
- Celebrate accomplishment: "You have now built a working content type."

### Quick test

Ask: "Does this follow one guaranteed-safe path that a beginner can complete?"
If yes -> Tutorial.

## How-to guides (task-oriented)

**Purpose:** Directions guiding a competent user through a real-world problem toward a specific result.

**Analogy:** A recipe. Professional cooks use recipes not because they lack skill, but for precision. Recipes define outcomes, address questions, exclude teaching, and focus on execution.

### Essential properties

- **Problem-centered**: it starts from the reader's goal, never from the tool.
- **Action only**: no teaching, no explanation.
- **Adaptable** to real-world variations (forking paths, multiple entry/exit points).
- **Practically useful** over exhaustively complete.

### What to DO

1. **Title states the goal.** Write "How to integrate application performance monitoring". A title like "Application performance monitoring" only names a topic.
2. **Open with purpose.** "This guide shows you how to..."
3. **Assume competence.** The reader knows what they want. Show them how to get it.
4. **Provide action and only action.** Every sentence moves toward the result.
5. **Use conditional imperatives.** "If you want x, do y."
6. **Handle real-world complexity.** Multiple valid approaches, branching conditions, edge cases.
7. **Link, don't embed.** "Refer to the X reference for a complete list of options."

### What NOT to do (anti-patterns)

- **No teaching or conceptual context** (link to Explanation).
- **No reference material inline** (link to Reference).
- **No exhaustive completeness**: usability beats comprehensiveness.
- **No tool-oriented framing** divorced from user goals.

### Language patterns

- "This guide shows you how to..."
- "If you want x, do y. To do z instead, see {ref}`other-guide`."
- "Refer to {ref}`reference-section` for the complete option list."

### Quick test

Ask: "Does this solve a specific real-world problem for someone who already has the skill?"
If yes -> How-to guide.

## Reference (information-oriented)

**Purpose:** Accurate, complete, austere technical description of the machinery. Facts only.

**Analogy:** A map. It describes the territory without telling you where to go.

### Essential properties

- **Accurate**: no ambiguity, no doubt.
- **Complete**: covers everything the user might need to look up.
- **Consistent**: uses standard, repeatable patterns throughout.
- **Structurally aligned**: mirrors the product's own structure (modules, classes, config keys).

### What to DO

1. **Describe, and only describe.** Neutral, objective, factual.
2. **Adopt standard patterns.** Tables, definition lists, consistent formats. Every entry looks the same.
3. **Mirror the code structure.** If the product has modules A, B, C, the reference has sections A, B, C.
4. **Provide terse examples.** Illustrate, but do not instruct.
5. **Be wholly authoritative.** State facts with certainty.
6. **Use mandatory language.** "You must use X. You must not apply Y unless Z. Never do W."
7. **Include warnings where appropriate.**

### What NOT to do (anti-patterns)

- **No instruction** (that is a How-to).
- **No explanation, opinion, or discussion** (that is Explanation).
- **No stylistic variation**: consistency is paramount.
- **No marketing claims or speculation.**
- **Auto-generated docs alone are not sufficient**: curate and organize them.

### Language patterns

- Declarative facts: "The `timeout` parameter accepts an integer in seconds."
- Mandatory: "You must use X. You must not apply Y unless Z."
- Lists, tables, definition lists for structured data.

### Quick test

Ask: "Is this boring, unmemorable, and purely factual?" (That is good. It means it is Reference.)

## Explanation (understanding-oriented)

**Purpose:** Discursive, reflective treatment that deepens understanding through context and connections. The only docs you can read "in the bath."

### Essential properties

- **Connective**: links ideas, shows relationships, illuminates the bigger picture.
- **Contextual**: history, design decisions, constraints, trade-offs.
- **Opinionated**: may weigh alternatives and express judgment.
- **Bounded**: establishes scope and stays within it.

### What to DO

1. **Make connections.** Relate topics to each other, even beyond the immediate subject.
2. **Provide context.** History, design decisions, technical constraints, "why it is this way."
3. **Frame as "about" topics.** Titles should accept an implicit "About..." prefix. E.g., "About user authentication."
4. **Discuss the bigger picture.** Alternatives, choices, trade-offs, possibilities.
5. **Acknowledge opinion and perspective.** Weigh alternatives and counter-examples.
6. **Unfold internal secrets.** Illuminate *why* something works the way it does.

### What NOT to do (anti-patterns)

- **No instruction** (that drifts into How-to territory).
- **No lists of facts** (that is Reference).
- **No encyclopedic sprawl**: keep reasonable boundaries.
- **No scattering**: consolidate explanatory material rather than sprinkling it through other pages.

### Language patterns

- "The reason for x is because historically, y..."
- "W is better than z, because..."
- "An x is analogous to w... However..."
- "Some users prefer w (because z). This can be effective, but consider..."

### Quick test

Ask: "Could you read this in the bath and find it enlightening?"
If yes -> Explanation.

## Diataxis decision matrix

When classifying or writing content, use this:

| Question | If yes... |
|----------|-----------|
| Follows one guaranteed-safe path for a beginner? | **Tutorial** |
| Solves a specific real-world problem? | **How-to guide** |
| Boring, factual, structured like the code? | **Reference** |
| Illuminating, discursive, readable away from keyboard? | **Explanation** |
| Is it for someone *learning*? | Tutorial or Explanation |
| Is it for someone *working*? | How-to or Reference |
| Is it *practical* (doing)? | Tutorial or How-to |
| Is it *theoretical* (knowing)? | Explanation or Reference |
