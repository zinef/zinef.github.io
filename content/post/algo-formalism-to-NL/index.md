---
title: "From Algorithms to Prompts: Did We Just Loop Back or Level Up?"
description: "A deep dive into why algorithms were formalized to escape natural language ambiguity, and how LLMs bring natural language back as an interface for problem solving."
slug: algorithms-to-prompts-llms
date: 2025-08-19
image: turing-m.jpeg
categories:
    - Artificial Intelligence
    - Computer Science
    - History of Computing
tags:
    - Algorithms
    - Turing
    - Church
    - Computability
    - Formalism
    - Natural Language Interfaces
    - Large Language Models
    - Agents
    - Problem Solving
    - Programming Abstractions
---

A century ago we invented *formal* ways to describe computations precisely because everyday language was too squishy. Now we’re steering powerful systems with… everyday language. Is that progress or a regression?

Short answer: it’s a step sideways and up. We didn’t abandon formalism, we pushed it down a layer. Natural language is becoming the interface, while the machinery underneath is getting more formal (APIs, schemas, tools, verifiers). Below I’ll unpack why the algorithmic formalists did what they did, how LLMs change the surface of programming, and when “English as glue” is a good idea or a trap.

## Why formalize algorithms in the first place ?

Early 20th-century logicians tried to pin down what it means to compute at all. David Hilbert’s program asked whether there was a mechanical procedure to decide the truth of any statement in first-order logic (the Entscheidungsproblem). Alonzo Church (lambda calculus) and Alan Turing (Turing machines) independently answered no, but their negative answers gave us something priceless: precise models of effective procedure, what we now call algorithms. Their work, together with Post and Kleene, forms the backbone of the Church - Turing thesis and computability theory.

From there, computer science doubled down on precision inside programming, not just in computability theory:

- **Syntax** got formal grammars (e.g., Backus–Naur Form) to define languages unambiguously, famously in the ALGOL 60 report.
- **Semantics and correctness** got axioms and proofs (e.g., Hoare logic), and structured programming discouraged ambiguous control flow.

The point was never to avoid natural language in discourse, but to ensure that what the *machine* sees is crisp, verifiable, and composable.

## So why are we “back” to natural language now?

Because LLMs made natural language an effective **specification medium** for many tasks. A good prompt can compress years of prior work : data, code, papers … into a short instruction that selects and adapts knowledge. But crucially, recent LLM apps don’t stop at plain text:

- **Function/Tool calling** turns a sentence into a typed API call with guaranteed structure. What the user says is fuzzy, what the system executes is precise.
- **Agents + tools** (search, code execution, calculators, retrievers) let models plan in language but act through formal interfaces.
- **Structured outputs** (JSON Schema) and **constrained decoding** force the model to emit data that matches a schema exactly, bridging natural prompts with machine-checkable results.

In other words, we use natural language for **intent capture** and **explanation**, then immediately re-enter formal territory for **execution** and **interoperability**.

## Are we undoing the original reasons for formalism?

No. We’re relocating formalism to the seams where it matters.

- **Ambiguity control** moved from the user’s prompt to the **contracts at the boundary** (schemas, types, tools). With structured outputs and grammar-constrained decoding, you can make the generator respect your formal spec while still letting users speak freely.
- **Verification** is increasingly externalized: the model proposes, specialized solvers/checkers verify. This reflects a broader trend: treat the LLM as a parser/planner and let formal tools enforce correctness downstream.
- **Proven limits** still apply. Church-Turing didn’t go away, undecidability and incompleteness still constrain what any program or model can guarantee. The practical response is to bound the problem and add safeguards, not to hope that prose resolves impossibility.

Think of LLMs as stochastic compilers **from intent to actions**. We’re not programming in English, we’re **using English to drive formal systems**.

## When is natural language a good “programming layer”?

**Great for:**

- **Exploration & orchestration.** “Summarize these docs, extract entities, then call the CRM API.” The natural language plan can be translated to tool calls with structured outputs so the rest of your stack stays typed.
- **End-user customization.** Users don’t want DSLs, they want results. NL prompts make power accessible, while your app constrains what can actually happen via tools and schemas.

**Risky for:**

- **High-assurance logic.** Dijkstra warned in 1978 against “natural language programming” because ambiguity clashes with the precision that programs require. The warning is still relevant unless you couple NL with formal constraints and verification.

A pragmatic pattern is: **Prompt → Plan → Structured Calls → Verify → Persist**. The prompt is the human-friendly layer, everything after is formal and testable.

## LLMs reuse existing knowledge, prompts just query it

LLMs are trained on existing artifacts. At inference time they compose and contextualize that knowledge. Tool use and retrieval make this even clearer: the model plans in language but leans on external knowledge bases or APIs for facts and effects. Recent surveys of LLM-based agents document this emerging architecture, language for reasoning and coordination, tools for ground truth and action.

## But didn’t people try “English-like programming” before?

Yes, COBOL’s Englishy syntax, HyperTalk, Inform 7, and decades of “natural language programming” experiments. The enduring critique, again from Dijkstra, is that surface readability doesn’t buy you **semantic guarantees**. What’s new now isn’t Englishy syntax, it’s **learning-based intent capture + formal execution layers**. The shift is closer to Andrej Karpathy’s “Software 2.0” idea, specifying behavior via data and learned models instead of only handwritten rules, now extended with a natural language interface on top.

## A sober take: is this a step up?

Yes, with guardrails. We improved the human-computer interface without discarding the computer’s need for formality. The socio-technical win is accessibility and speed, the technical debt is that ambiguity and hallucination creep back in unless you constrain, ground, and verify. The state of the art is actively addressing this with structured outputs, grammar-constrained decoding, and agent frameworks that keep LLMs honest by delegating to formal tools.

## Further reading & references

- **Why formalize algorithms / historical roots.**
    Stanford Encyclopedia entries on the Church-Turing Thesis and Computability, Turing (1936) and Church (1936) on the Entscheidungsproblem. [plato.stanford.edu](https://plato.stanford.edu/entries/church-turing/), [dl.acm.org](https://dl.acm.org/doi/10.1145/360303.360308)

- **Language design and correctness.**
    ALGOL 60 report (BNF for syntax), Hoare’s “An Axiomatic Basis for Computer Programming”, Dijkstra’s “Go To Statement Considered Harmful.” [mass:werk – media environments](https://www.masswerk.at/algol60/report.htm),[eli-project.sourceforge.net](https://eli-project.sourceforge.net/a60_html/a60.html), [homepages.cwi.nl](https://homepages.cwi.nl/~storm/teaching/reader/Dijkstra68.pdf)

- **Natural language programming debate.**
    Dijkstra’s *On the foolishness of “natural language programming”* (1978/79), The New Yorker’s “What if natural language replaced programming?” for a modern cultural view. [cs.utexas.edu](https://www.cs.utexas.edu/~EWD/ewd06xx/EWD667.PDF)

- **LLMs as planners with tools.**
    ReAct (reasoning+acting) and Toolformer (teaching models to use tools), surveys of LLM-based agents. [arXiv](https://arxiv.org/pdf/2210.03629), [openai.com](https://openai.com/index/function-calling-and-other-api-updates/)

- **Bridging NL to formal outputs.**
    OpenAI structured outputs (JSON Schema adherence) and research on constrained/grammar-guided decoding. [openai.com](https://openai.com/index/introducing-structured-outputs-in-the-api/), [arXiv](https://arxiv.org/html/2403.06988v1), [aclanthology.org](https://aclanthology.org/2025.acl-industry.34.pdf)