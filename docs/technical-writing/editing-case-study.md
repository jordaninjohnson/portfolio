# Editing case study: make troubleshooting instructions usable

**Status:** Synthetic classroom-style demonstration, drafted with ChatGPT on October 13, 2026. The “before” passage is **invented for this exercise**; it is not an archived original by Jordan or a client. The proposed edits do **not** demonstrate Jordan's unaided editing ability.

**Audience:** New users of an older Node.js README generator and developers supporting them.

## Synthetic starting passage (not a historical document)

> If it doesn't create your README, just run the generator again. It's pretty simple and should work without a network. You can change the license and it always makes the correct badge. Run the tests if you're unsure. The file is recreated each time so you don't need to check old output. You can hide your photo if you say no.

## Proposed revision: general user

Before retrying, open `Assets/README.md` and check whether any content was already added. The generator **appends** its output, so repeated successful runs can leave duplicate sections. This program contacts GitHub to look up the username and avatar, which means it needs network access. If nothing was written, verify the GitHub username and check for a request error in the terminal. Treat license badges and the profile image as items to review manually. The current `npm test` command is a placeholder, not an automated validation step.

## Adaptation for a technical reader

The source calls `axios.get('https://api.github.com/users/' + username)` and performs `fs.appendFileSync('./Assets/README.md', ...)` calls only in the success callback. Before rerunning, inspect the fixed output path for partial or duplicate content; the implementation has no truncation step. `package.json` maps `npm test` to a deliberate error exit. The photo answer is prompted for but not consulted before avatar output. Badge generation explicitly branches on the MIT license string; inspect other-license output rather than assuming correct handling.

## Editorial decisions

| Issue in the synthetic draft | Proposed correction | Reader benefit |
| --- | --- | --- |
| “Just run again” | Check output first; append behavior may duplicate content | Prevents avoidable cleanup |
| “Works without a network” | Explain the GitHub public API call | Adds a missing prerequisite |
| “Always makes the correct badge” | Qualify MIT-specific code path | Removes an unsupported guarantee |
| “Run the tests” | State the actual placeholder test script | Avoids false test assurance |
| “File is recreated” | Identify append-only implementation | Matches inspected behavior |
| “Hide your photo” | Flag ignored photo-choice input | Protects expectation and privacy |

**Evidence:** [`index.js` source](https://github.com/jordaninjohnson/ReadMe-Generator/blob/master/index.js), [`package.json`](https://github.com/jordaninjohnson/ReadMe-Generator/blob/master/package.json).

**What Jordan should verify:** Read the source and explain each correction in his own words. Rewrite one passage independently and preserve drafts for comparison. No program run or real-world editorial outcome is claimed.
