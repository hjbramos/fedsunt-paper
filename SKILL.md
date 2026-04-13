---
name: NASP Paper and Rebuttal Letter
description: Copilot instructions for the NASP (Network Slice as a Service Platform) revised paper (JNCA) and its rebuttal letter.
---

# Copilot Instructions for "NASP Paper and Rebuttal Letter"

This workspace contains the LaTeX source for a research paper (Elsevier JNCA) and its rebuttal letter.

## Project Structure & Context

*   **Revised-Paper-NASP/**: Main revised manuscript.
    *   **Root**: `main.tex` (elsarticle class, `5p,times,twocolumn,authoryear`). Do not add content here; use `Sections/`.
    *   **Sections**: `Sections/*.tex`. Content is split as:
        *   `0-acronym-list.tex` — Acronym definitions (`\acrodef`)
        *   `1-introduction.tex`
        *   `2-background.tex`
        *   `3-related-works.tex`
        *   `4-proposal.tex`
        *   `5-prototype.tex`
        *   `6-evaluation-methodology.tex`
        *   `7-results.tex`
        *   `8-conclusion.tex`
    *   **Figures**: `Figures/`
    *   **Bib**: `ref.bib` (author-year style, `elsarticle-harv`).
*   **Letter-NASP/**: Response to reviewers.
    *   **Root**: `main.tex` (exam class, `answers,11pt,table`).
    *   **Tables**: `Tables/*.tex` — standalone table files included in responses.
    *   **Figures**: `Figures/`
    *   **Bib**: `biblio.bib`.
    *   **Acronyms**: `acronyms.tex`.
*   **reviewers_comments.md**: Summary of reviewer comments and required changes.

## Critical Conventions

### 1. Source Editing (Strict)
*   **Sentence Breaking**: End EVERY sentence with a newline. No exceptions.
    *   *Bad*: `The system is efficient. It uses AI.`
    *   *Good*:
        ```latex
        The system is efficient.
        It uses AI.
        ```
*   **Revisions**: Mark changed text in the **paper** with `\textcolor{blue}{...}` to reflect the resubmission status.
*   **Math**: Use standard LaTeX math. Units via standard SI formatting.
*   **Avoid Em-Dashes (Ligatures & Unicode)**: Do not use `---` or the Unicode character `—` (em-dash) for parenthetical breaks; prefer commas or separate sentences to maintain a formal IEEE tone.
*   **Avoid Excessive Hyphens**: Avoid parenthetical dashes (e.g., `word -- explanation -- word`) and complex compound adjectives. Use commas or rephrase for clarity.

### 2. Acronyms
*   **Rule**: NEVER hardcode an acronym. Always check the acronym list (`0-acronym-list.tex` in paper, `acronyms.tex` in letter).
*   **Usage**:
    *   `\ac{ID}` for singular (outputs "Full Name (FN)" on first use, "FN" after).
    *   `\acp{ID}` for plural.
    *   `\acf{ID}` to force full expansion.
*   **Common IDs**: `\ac{NASP}`, `\ac{CSMF}`, `\ac{NSMF}`, `\ac{NSSMF}`, `\ac{NSI}`, `\ac{NSSI}`, `\ac{E2E}`, `\ac{3GPP}`, `\ac{ETSI}`, `\ac{ZSM}`, `\ac{URLLC}`, `\ac{eMBB}`, `\ac{mMTC}`, `\ac{SDN}`, `\ac{NFV}`, `\ac{K8s}`, `\ac{ONOS}`, `\ac{UE}`, `\ac{QoS}`, `\ac{SLA}`, `\ac{O-RAN}`, `\ac{5GC}`, `\ac{RAN}`, `\ac{TN}`, `\ac{CN}`.

### 3. Rebuttal Letter Format
*   **Prevent Duplication**: Always check if the question was already answered to a previous reviewer. If so, reference that previous response rather than answering it from scratch again.
*   Each reviewer comment uses the `exam` class `questions` environment:
    ```latex
    \question \textit{``[Original reviewer comment]''}

    \begin{solution}
    [Response text — explanation and justification]
    \end{solution}

    \begin{evidence}
    [Corresponding manuscript changes — quoted revised text]
    \end{evidence}
    ```
*   Questions auto-label as **Q1, Q2, …**; solutions as **R1, R2, …**.
*   Custom commands: `\blue{...}` for blue text, `\LetterSection{num}{title}` for section headings.
*   Tables can be included from `Tables/` via `\input{Tables/filename}`.

### 4. Terminology
*   **NASP**: Network Slice as a Service Platform.
*   **CSMF → NSMF → NSSMF**: Hierarchical management chain.
*   **Shared slice**: An eMBB-type slice that reuses existing control-plane NFs for best-case provisioning measurement.
*   **Tone**: Technical, focused on *experimental validation* and *standards compliance* (3GPP, ETSI ZSM, GSMA GST).

### 5. Build & Workflow
*   **Build Tool**: `latexmk`.
*   **Commands**:
    *   Paper: `latexmk -pdf -pvc -interaction=nonstopmode main.tex` (from `Revised-Paper-NASP/`)
    *   Letter: `latexmk -pdf -pvc -interaction=nonstopmode main.tex` (from `Letter-NASP/`)
*   **Clean**: `latexmk -c`

## Integration
*   **Figures**: Referenced as `Figure~\ref{fig:label}`. Files in `Figures/`.
*   **Tables**: Referenced as `Table~\ref{tab:label}`. Standalone files in `Tables/` (letter) or inline (paper).
*   **Citations**: `\cite{key}` or `\citep{key}` (author-year).
*   **Cross-refs**: `Section~\ref{sec:label}`.
*   **Code Listings**: Use `listings` package with `language=json` for schemas (configured in letter `main.tex`).

## Key Files to Reference
*   [0-acronym-list.tex](Revised-Paper-NASP/Sections/0-acronym-list.tex) — Paper acronym definitions.
*   [acronyms.tex](Letter-NASP/acronyms.tex) — Letter acronym definitions.
*   [reviewers_comments.md](reviewers_comments.md) — Reviewer change tracker.
*   [7-results.tex](Revised-Paper-NASP/Sections/7-results.tex) — Section to split into subsections (Reviewer 1.4).
*   [table_related_works.tex](Letter-NASP/Tables/table_related_works.tex) — Related-work comparison table.
