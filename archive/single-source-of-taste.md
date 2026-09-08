# **The Architecture of Judgment: Design Systems as the Single Source of Taste**

> A companion and counterpart to *[Design Systems: Single Source of Truth](https://github.com/ds1/design-token-context-model/wiki/Design-Systems_-Single-Source-of-Truth)*. That document asked where the **truth** of a product lives and how to keep it from drifting. This one asks the question the last few years have made urgent: now that anyone can build almost anything, where does its **taste** live, who owns it, and how do we keep *that* from drifting.

---

## Chapter 1: The Second Ontological Crisis

The Single Source of Truth argument began from a chasm: the distance between what a product was meant to be (the "envisioned reality" in Figma) and what it actually became (the "executed reality" in code). Truth was bifurcated. A hex value lived in a design file and again, by hand, in a stylesheet, and the two drifted. The design system was the connective tissue that normalized this duplication into a single mastered value, referenced everywhere and copied nowhere.

That crisis assumed a specific scarcity: **execution was expensive**. Turning intent into working software took engineers, time, and translation, and every translation was lossy. The whole apparatus of tokens, pipelines, and handoff existed to protect a costly, error-prone crossing from design to code.

That scarcity has collapsed. When a designer, a product manager, or a founder can describe an interface and have a machine render production-plausible code in seconds, execution stops being the bottleneck. The crossing from intent to artifact is nearly free and nearly instant. Building is democratized.

This does not end the crisis. It relocates it. When anything can be built, the binding question is no longer *can we build it correctly* but *should this exist, and is it any good*. The scarce quantity is no longer execution. It is **judgment**: the standard that separates the worth-building from the merely buildable.

So a product again exists in two realities, but the pair has changed:

- The **generable reality**: the effectively infinite set of things that can now be produced on demand, cheaply, by humans and machines alike.
- The **worth-building reality**: the small, governed subset of those things that meet a standard, that cohere, that a discerning owner would actually ship.

The gap between them is not the fidelity gap. It is the **discernment gap**. And just as the fidelity gap was bridged by normalizing truth, the discernment gap is bridged by normalizing **taste**: making the standard explicit, mastered in one place, referenced by every maker rather than re-invented by each one.

This document argues that the mature design system is no longer only a Single Source of Truth for values. It is becoming a **Single Source of Taste**: the connective tissue that negotiates not what a product *is* but what it *should be*, and that gives the people who hold that standard, the designers, a governed place to keep it.

### 1.1 Truth Was Split Between Two Files. Taste Is Split Between Every Head.

The truth problem was tractable because both copies of the truth were written down. The hex value existed in the design file and in the stylesheet; you could diff them. The failure mode of taste is worse, because taste has historically been **tacit**. It lives in the senior designer's eye, in the reviewer's flinch at a wrong radius, in the thousand micro-decisions that never became a value in any file. It is the least normalized asset an organization owns.

In the era of expensive execution, this was survivable. The bottleneck of implementation acted as an accidental quality gate: few things got built, and a small circle of skilled people built them, so their taste propagated by proximity. Democratized building removes that gate. Now many people and many models produce artifacts quickly, none of them with automatic access to the standard. Taste that lives only in heads cannot govern a system that now generates faster than any head can review.

The Single Source of Taste is the project of moving taste out of heads and into a mastered, referenceable, versioned form, for the same reason SSOT moved truth out of stylesheets: **an asset that is duplicated tacitly across many minds will drift**, and drift at machine speed is drift you cannot catch by hand.

---

## Chapter 2: The Epistemology of Taste

SSOT borrowed its rigor from database theory: normalization, DRY, CQRS. Those principles are not decoration; they are the reason a single source of *anything* holds. Taste earns the right to be called a "source" only if it can adopt the same discipline. It can.

### 2.1 Normalization, Applied to Judgment

Normalization eliminates redundancy by storing each fact once and referencing it everywhere. Applied to values, this turned `#007BFF` scattered across fifty files into one `brand.primary` referenced fifty times.

Applied to judgment, normalization means: **each aesthetic decision is made once, recorded, and referenced, never re-litigated ad hoc.** The decision "our primary action color should read as confident, not playful, and resolves to this blue at this contrast in this context" is a unit of taste. Stored once and referenced, it governs every button any maker produces. Re-decided in every new screen by every new contributor, it is guaranteed to fragment.

The taste equivalent of a denormalized database is the organization where every team invents its own spacing rhythm, its own motion feel, its own idea of "clean," because the standard was never written where they could reference it. This is not a style problem. It is a **data integrity failure in the judgment layer**, and it produces the same symptom SSOT was built to kill: drift.

### 2.2 DRY Becomes "Do Not Re-Decide"

The Do Not Repeat Yourself doctrine holds that any fact expressed in two places will eventually disagree. Its taste analogue: **any judgment re-derived in two places will eventually diverge.** When two designers, or two prompts, or a designer and a model each independently decide what "premium" means for the same product, the two premiums drift apart exactly as two copies of a hex value do.

The structural enforcement of DRY for taste is the same as for truth: centralize the decision, reference it downstream. The downstream consumers change, though. They are no longer only CSS files and iOS resources. They are **generators**: the AI tools, the junior builders, the non-designers now empowered to ship. Each of them treats the Single Source of Taste the way a microservice treats an API: it requests the current standard and conforms to it, rather than inventing one.

### 2.3 CQRS: Designers Write Taste, Makers Read It

Command Query Responsibility Segregation separates the model that **writes** information from the model that **reads** it. SSOT mapped this cleanly: the system designer writes the token definition (command); the application reads compiled variables (query); a pipeline reconciles them so the read side always reflects the write side.

The Single Source of Taste inherits this shape and sharpens who sits on each side:

- **The command side is the designer.** Taste is authored where taste is formed: in the visual medium, by the people with the eye. This is the write model. It is the act of deciding.
- **The query side is every maker**, human or machine, who now produces artifacts. They read taste as a set of constraints and resolve their output against it. This is the read model. It is the act of generating.
- **The reconciliation mechanism is the sync tooling** that keeps the authored standard and the consumed constraints from diverging, the same role Style Dictionary played for values.

The consequence is the crux of the whole reframe. In the SSOT world, the design tool was upstream of engineering but subordinate to it: design produced a *specification* that code was the *truth* of. In the CQRS-of-taste world, the designer is not producing a spec for someone else to make real. The designer is authoring the **write model of the standard itself**, and the makers, including the machines, are read replicas. Design moves from supplier to source.

---

## Chapter 3: The Atom of Taste Is a Policy, Not a Value

SSOT located its atomic unit in the design token: the smallest normalized unit of visual truth, `blue.500 = #3b82f6`. This is correct and insufficient for taste, because **taste is not a value. Taste is contextual judgment, and contextual judgment is a policy.**

This is where the coordinate model developed elsewhere in this repository does the load-bearing work. Its central claim is that *[a token is not a value; it is a policy that maps a context coordinate to a value](https://github.com/ds1/design-token-context-model/wiki/context-as-coordinate-system-thesis)*. `color.surface.default` does not "store white." It answers a question: *what should this surface be for this user, in this theme, at this density, at this elevation, under this accessibility need*. Resolution is policy evaluation over a point in a many-dimensioned context space.

Taste has exactly this shape, and only this shape explains why taste resists being written down. A rule like "use blue" is not taste; it is a value, and values feel arbitrary because they are context-free. Real taste is the governed resolution: *confident blue in the marketing hero at full contrast, but never that same blue on a disabled control, and a quieter blue in the dense data table, and a different weighting entirely under forced-colors.* Taste is the policy that produces the **right perceptual outcome for this agent in this context**, and the thing a discerning designer actually knows is the policy, not any one of its outputs.

This yields three properties that let taste behave like an engineered source rather than a vibe.

### 3.1 The Taste Tiers

The three-tier token taxonomy (primitive, semantic, component) maps onto taste with the semantic layer, again, as the crux.

| Tier | In Truth (SSOT) | In Taste (SSOTaste) |
| :--- | :--- | :--- |
| **Primitive** | The raw palette of available values (`blue.500`). | The **vocabulary of the possible**: the full range a system *could* express. Context-free, judgment-free. |
| **Semantic** | The decision that binds a value to an intent (`action.primary → blue.500`). | The **seat of taste**: the governed decision about what a thing should mean and how it should feel. This is where judgment lives. |
| **Component / Instance** | The application of a decision to a specific element. | The **exercise of taste**: a maker resolving a specific artifact against the standard. |

As in SSOT, the semantic tier is where the leverage is. It is the indirection layer that lets the standard shift by context (a "premium" that resolves one way for the enterprise brand and another for the consumer one) while the makers downstream keep referencing the same stable name. Taste is authored at the semantic tier and *resolved* at the component tier, which is precisely why a good design system lets a mediocre maker produce tasteful output: the maker exercises taste they did not have to originate.

### 3.2 Taste Becomes Testable

Because a policy encodes an *intended outcome* rather than an arbitrary value, its resolution can be checked against the intent. The coordinate thesis already argues this for tokens: `contrast.high` is correct not when it returns the specified value but when it **achieves WCAG AAA for the target population**. Taste inherits this. A taste policy states a behavioral intent ("this should read as calm," "this should feel responsive, not frantic"), and while the softest edges of aesthetic judgment stay human, large parts become measurable: contrast ratios, target sizes, motion thresholds, rhythm consistency, adherence to the governed scale. The parts of taste that were pure assertion become **assertions with acceptance criteria**. That is what makes taste governable rather than merely opinionated.

### 3.3 Taste Is Agent-Relative

The coordinate model's most subtle move is that resolution depends not only on environment but on the **agent**: a hover style is meaningless without a pointer, a P3 color unachievable on an sRGB panel, a 12px label illegible to a low-vision user. Taste is agent-relative in the same way. The tasteful decision is not "the beautiful thing in the abstract" but "the right thing *for this person, on this device, with these needs*." This is why accessibility sits at the top of the resolution precedence: an inaccessible interface is not a matter of taste one may debate, it is a policy that fails its intent for a class of agents. Good taste, formalized, subsumes accessibility rather than trading against it.

---

## Chapter 4: The Great Divide, Revisited and Dissolved

SSOT catalogued three architectures and treated the choice among them as an open, contested question:

- **Design-First** (Figma is master): high designer autonomy, but "Figma isn't production" and lacks version control, so engineering distrusts it.
- **Code-First** (Git is master): strong version control, "code is the only truth," but it disenfranchises designers and reduces them to filers of requests.
- **Middleware** (a synced JSON file is master): the bi-directional compromise, at the cost of sync complexity.

The entire debate turned on a single asymmetry: **code had governance rigor and design did not.** Git gave code branching, review, history, rollback, and bounded blast radius. Design tools gave visual fluency and nothing to audit. So even advocates of design-first conceded the master copy to code, because you cannot make a *source of truth* out of a medium that cannot show its history or gate its changes. Design won the argument about *where decisions originate* and lost the argument about *where they are mastered*, every time.

Two changes settle the question, and they settle it in design's favor.

First, **democratized building removes code's claim to primacy.** "Code is the only truth" was persuasive when code was the scarce, skilled, canonical artifact. When code is generated on demand from intent, it becomes the *read replica*, abundant and disposable, and the scarce canonical artifact moves upstream to the judgment that decides which generation to keep. You do not master your source of truth in the cheapest, most reproducible layer. You master it in the layer that holds the decision.

Second, **tooling closes design's rigor gap.** This is GitFig's actual contribution, read at the level of theory rather than features. A Figma-to-GitHub sync that carries branches, commits, pull requests, change detection, conflict guards, full history, and multi-mode variable resolution does not merely export tokens. It **grants the design surface the exact governance properties whose absence was the only serious argument against design-first.** Once the designer can branch a standard, open it for review, see its diff, trace its history, and know the blast radius of a change, from inside the design tool, Figma stops being "a simulation" and becomes a governed source. The codebase, as the framing of this exploration puts it, can now stay *true* in Figma, because the design tool has borrowed the discipline that made code trustworthy.

With those two changes, the trilemma collapses. Design-First is no longer a preference to be defended against engineering skepticism. It is the **only coherent place to master taste**, because taste originates in design and design now has the governance to hold it. The middleware compromise, JSON-in-Git as the real master with a design GUI bolted on, was a concession extracted by the rigor gap. Close the gap and the concession is unnecessary: the design surface itself, backed by Git, is the master, and the repository is its versioned, distributable projection.

| Architecture | Under SSOT (truth) | Under SSOTaste (taste) |
| :--- | :--- | :--- |
| **Design-First** | Contested. High autonomy, weak governance, "not production." | **The default.** Taste originates here; Git-backed sync supplies the governance that was missing. |
| **Code-First** | The safe institutional choice; "code is truth." | Demoted. Generated code is the read replica; mastering taste in it inverts source and copy. |
| **Middleware** | The mature compromise. | Unnecessary once the design surface itself is Git-governed. The repo is a projection, not the master. |

---

## Chapter 5: The Political Economy of Taste

SSOT observed that establishing a source of truth is as much a governance problem as a technical one, and prescribed a **federal model**: design owns the "what," engineering owns the "how," both own the shared taxonomy. The Single Source of Taste keeps the federal instinct but shifts its center of gravity.

### 5.1 The Balance of Ownership Tilts Toward Design

In the truth regime, the federation was near-symmetric because both sides held something scarce: design held intent, engineering held the ability to realize it. Democratized building erodes the second scarcity. When realization is cheap and largely automated, the "how" commoditizes, and the federation re-weights toward whoever holds the "what" and the standard. That is design.

This is not a claim that engineering disappears. Someone still owns the pipeline, the resolution algorithm, the correctness of the sync, the infrastructure that makes taste enforceable at scale, and that ownership is real and rising in leverage. It is a claim that the **decision rights** over the product's standard consolidate with the discipline that produces judgment, because judgment is now the bottleneck. The design system stops being a service department that translates decisions made elsewhere and becomes the **governing body of the standard everyone else generates against.**

### 5.2 The Design Technologist Becomes the Taste Steward

SSOT named an emerging role: the Design Technologist, the "custodian of the truth" who maintained the pipeline and arbitrated naming. The Single Source of Taste elevates and renames the function. The **Taste Steward** owns the standard as an asset: which decisions are canonical, when an exception has become a pattern worth promoting to a policy, when a policy has decayed and must be revised, and how the standard is versioned so that changing it does not silently break the fleet of makers, human and machine, resolving against it. The custodian of truth guarded consistency of values. The steward of taste guards **coherence of judgment**, which is harder, because its violations are not `#fff` where `#eee` was expected, but the slow entropy of a product that stops feeling like itself.

### 5.3 Versioning the Standard

SSOT adapted Semantic Versioning to tokens: renaming a token is a breaking MAJOR change, adding one is a MINOR feature, tweaking a value is a PATCH. Taste needs the same discipline, because a source of taste that cannot version itself cannot evolve without chaos.

- **MAJOR**: a change to the standard that invalidates existing conforming work. Redefining what "primary action" should feel like, retiring a governed context type, changing a precedence rule. Every maker's prior output may now be off-standard.
- **MINOR**: extending the standard. A new governed context type (`kiosk`, `editorial-reading`), a new sanctioned brand, a newly promoted pattern. Existing work stays valid; new capability is available.
- **PATCH**: refining a resolution without changing intent. Nudging a value to better hit the perceptual outcome the policy always aimed for.

Versioned taste is what lets the standard be both **stable enough to reference** and **alive enough to improve**, the same balance SemVer struck for truth. And the Git-backed design surface from Chapter 4 is what makes this more than an analogy: a taste change can literally be a branch, a pull request, a reviewed and dated commit against the standard.

---

## Chapter 6: The Operational Reality

SSOT is actualized by a transformation pipeline: Style Dictionary takes the JSON truth and compiles it into platform realities (CSS, Swift, XML), so a single mastered value propagates without manual re-entry. The Single Source of Taste needs two pipelines, and both now exist in recognizable form.

### 6.1 The Resolution Engine Is the Compiler of Taste

Style Dictionary flattens and transforms values. Its analogue for taste is the **resolution algorithm** of the coordinate model: the deterministic, total, monotonic, composable procedure that takes a context coordinate and a policy and returns the value the policy prescribes. This is the compiler that turns a *standard* into a *specific correct output* for a specific agent and context. Where Style Dictionary answers "what is this value on iOS," the resolution engine answers "what does the standard require *here*," which is the machine form of taste. The design-token-context-model in this repository, its 12 categories, 93 dimensions, precedence order, named context types, and resolution algorithm, is precisely an attempt to make that compiler real: to render taste computable without rendering it flat.

### 6.2 The Sync Layer Keeps Taste True in Both Homes

The second pipeline is the bi-directional bridge between where taste is authored (the visual surface) and where it is stored and distributed (the repository). This is GitFig's role, and its bi-directionality is essential rather than incidental. A one-way export makes design a supplier again: it emits a spec and loses control of it. Bi-directional sync, with the change detection, conflict guards, and per-mode resolution that v1.4 carries, means the standard has **one identity in two homes**: editable with a designer's fluency in Figma, auditable with an engineer's rigor in Git, and reconciled so the two never silently disagree. That is the operational precondition for design to *hold* the source of taste rather than merely originate it.

### 6.3 The Read Replicas Are Now Generators

The final and newest link: the consumers. Under SSOT, the read side was compiled files consumed by a build. Under SSOTaste, the read side increasingly includes **generative systems** that produce novel artifacts. Feeding the standard to them is not a distribution problem but a *conditioning* problem: the design system becomes the constraint set, the context, the guardrail that shapes what the generators are allowed to produce. The SSOT document anticipated exactly this in its final chapter, observing that in an AI-driven future "the design system becomes a set of constraints fed into the AI to ensure the generated output adheres to the brand." The Single Source of Taste is the name for that constraint set once we take it seriously as the primary artifact rather than a byproduct of the token files.

---

## Chapter 7: Philosophical Divergences

### 7.1 Source of Taste versus Source of Standard

SSOT's most sophisticated turn was to concede that "truth" is too static a word: what actually needs centralizing is not a frozen truth but the **source of change**, the governed process by which a modification is proposed, approved, and propagated. Figma was recast as the source of *intent*, code as the source of *execution*, and the truth as the *governed link between them*.

Taste deserves the same refinement. The Single Source of Taste is not a monument to one person's fixed preferences, that would be a style guide, and style guides rot. It is better understood as the **single source of standard**: the governed process by which a new aesthetic judgment is proposed, reviewed against the existing standard, promoted or rejected, versioned, and propagated to every maker. The value of centralizing taste lies less in freezing a look than in owning the **mechanism of aesthetic change**, so the standard can move deliberately instead of drifting accidentally. This is why the Git-backed design surface matters at the level of philosophy and not only tooling: it turns "changing our taste" from a diffuse cultural event into a reviewable, revertible, attributable act.

### 7.2 The Death of the Brief

SSOT foresaw the "death of handoff": when AI generates production code directly from design intent, the lossy handoff from design to engineering vanishes, and a hybrid role, the SSOT text calls it the "Tastemaker-Maker", emerges to manifest vision directly into the medium.

The Single Source of Taste completes that thought from the other end. If handoff dies because the *maker* absorbs the engineer, then the **brief** dies because the *maker* absorbs the requester. The old division of labor, one party specifies taste and another executes it, dissolves when execution is free. What remains is a single figure who both holds the standard and produces against it, and whose scarce contribution is entirely the former. In a world where everyone can make, the tastemaker is not the person who *can* build. It is the person whose judgment decides what is **worth** building and whether the built thing is good. The Single Source of Taste is the infrastructure that lets that judgment scale past the reach of any single eye, by giving it, at last, a place to live outside the head that formed it.

### 7.3 Is Code the Only Truth? Is Taste Even Real?

The staunchest SSOT camp insisted "code is the only truth": documentation is a lie because it is not executable, Figma is a lie because it is a simulation, only the running artifact affects the user. The symmetric skepticism about taste is that it is *not real*, merely subjective, unownable, impossible to normalize, and therefore ineligible to be a "source" of anything.

The answer is the same shape as SSOT's answer to the code purists. Code without design intent is directionless: it is the *how* with no *why*. Likewise, taste treated as ineffable is not humility, it is abdication, and it is exactly the abdication democratized building can no longer afford. The claim of this document is not that all taste is reducible to rules. It is that **enough of taste can be made explicit, contextual, testable, and versioned** to serve as a governed source, and that the residue which stays human, the genuine judgment at the edges, is precisely the scarce asset worth building the whole apparatus to protect and propagate. When execution was scarce, code was the truth worth mastering. Now that execution is abundant, **taste is the scarcity, and the scarce thing is the thing you master.**

---

## Chapter 8: Conclusion, The Asymptotic Pursuit of Discernment

The Single Source of Truth was an asymptote: a perfect alignment of intent and execution that real organizations approach but never reach, and the value lay in the pursuit, in the patterns (normalization, DRY, versioning, automated transformation) that made the pursuit survivable at scale.

The Single Source of Taste is an asymptote of the next order. Perfect, fully-captured, machine-resolvable taste is not achievable and probably not desirable, because the human residue is the point. But the pursuit is now the decisive one. When building was hard, aligning intent and execution was the work, and the design system was the operating system for **truth**. Now that building is easy, aligning generation and judgment is the work, and the design system becomes the operating system for **taste**: the place where a standard is authored by the people with the eye, governed with the rigor once reserved for code, resolved into specific correct outputs by a deterministic engine, and fed as constraint to a growing fleet of makers, human and machine, who can all now build but cannot, on their own, discern.

The same disciplines carry across. Normalize the decision. Do not re-decide. Separate authoring from consumption. Version the standard. Automate the propagation. What changes is the noun. SSOT normalized the truth so that a product could be built consistently. SSOTaste normalizes the taste so that, in a world where a product can be built by anyone in an afternoon, it is still built **well**, and so that the discipline which owns "well", design, finally has a source worthy of the name.

Truth answered: *is it correct?* Taste answers the question that correctness never could and that abundance has made supreme: *is it good, and should it exist at all?* The design system, having spent a decade becoming the single source of the first answer, is now becoming the single source of the second.
