# Accuracy-review demonstration: evaluate a synthetic technical answer

**Scenario:** Someone asks how to run the public [ReadMe-Generator](https://github.com/jordaninjohnson/ReadMe-Generator) project.  
**Status:** Independent portfolio practice exercise about a **synthetic** response. This is **not** Handshake AI assessment content and not client work. The scenario, response, rubric, and feedback were drafted with ChatGPT. Jordan must independently evaluate and explain them before representing this as his work.

## Synthetic response under review

> “Download the app, run `npm install`, then run `node index.js`. It works offline and replaces your old README every time. Answer no to the profile picture prompt to exclude your photo. Any license will automatically get the right badge. Use `npm test` to run the automated checks. Your README will be pure Markdown.”

## Evidence-grounded review

| Claim | Finding | Evidence and impact |
| --- | --- | --- |
| `npm install` then `node index.js` | **Supported as documented instructions; not runtime-verified** | The project [README](https://github.com/jordaninjohnson/ReadMe-Generator/blob/master/README.md) specifies both commands |
| “Works offline” | **Unsupported / contradicted by code** | [`index.js`](https://github.com/jordaninjohnson/ReadMe-Generator/blob/master/index.js) requests a GitHub user through Axios before writing |
| “Replaces your old README” | **False** | `fs.appendFileSync` appends to `./Assets/README.md`; duplicate sections are possible |
| Photo answer disables avatar | **False** | The script asks for `photo` but later writes `res.data.avatar_url` unconditionally |
| Any license gets correct badge | **False as a guarantee** | The MIT-specific badge assignment does not establish correct behavior for other licenses |
| `npm test` runs automated checks | **False** | [`package.json`](https://github.com/jordaninjohnson/ReadMe-Generator/blob/master/package.json) has a placeholder failing test script |
| Output is pure Markdown | **Misleading** | The program calls `md.render` and writes HTML fragments inside a `README.md` file |

## Rubric

Score each dimension **0 = misleading/missing**, **1 = partially adequate**, **2 = accurate/actionable**, for a maximum of 10 points.

| Dimension | Score for synthetic answer | Justification |
| --- | ---: | --- |
| Factual accuracy | 0 | Five strong claims conflict with source inspection |
| Verifiability and citations | 0 | No file or code references supplied |
| Prerequisites and reproducibility | 1 | Commands supplied; GitHub API dependency omitted |
| Audience clarity and task relevance | 1 | Concise setup, but dangerous assurances |
| Security, limitations and uncertainty | 0 | No disclosure of test, output, or privacy limitations |
| **Total** | **2 / 10** | **Not publishable without substantial correction** |

## Actionable reviewer feedback

Keep the two documented setup commands, but add that the program needs network access for its GitHub user request. Warn that it appends to a fixed output file, so users should inspect or back up existing content before rerunning. Explain that the photo-choice prompt is not enforced by the inspected implementation and that users should review email, avatar, and license output before sharing. Remove the automated-testing claim; the test script is a placeholder. Note that the `.md` file contains HTML fragments. Label execution status as **not tested**.

**Uncertainty:** Source review establishes what the checked-in code attempts; it does not establish successful installation, actual output, runtime compatibility, or production security. Those require recorded execution in a disposable environment.

**Reference materials:** [Source code](https://github.com/jordaninjohnson/ReadMe-Generator/blob/master/index.js), [Project README](https://github.com/jordaninjohnson/ReadMe-Generator/blob/master/README.md), [Package metadata](https://github.com/jordaninjohnson/ReadMe-Generator/blob/master/package.json).

**Personal verification still required:** Independently identify at least one missed flaw, reconsider the scoring, and write a corrected 150–250 word answer without AI if using this to demonstrate unaided ability.
