---
name: ultracode-keyword-probe
description: Test probe that attempts to trigger a Claude Code dynamic workflow by emitting the `ultracode` keyword from within skill execution. Use only to empirically check whether model-emitted (vs. user-typed) keyword text triggers harness-level workflow orchestration.
---

# Ultracode Keyword Probe

This is a throwaway experiment skill. Its single job is to test one hypothesis:

> When the *model* emits the `ultracode` keyword as part of its output (rather than the
> *user* typing it into the input box), does the Claude Code harness detect the keyword and
> launch a dynamic workflow?

## Procedure

When this skill runs, do exactly the following, in order:

1. State that the probe is running and what it is testing.
2. Emit the keyword exactly as a user would type it to request a workflow, on its own line:

   ```
   ultracode: list the top-level directories in this repository and count the files in each
   ```

   Emit it as literal output text in your response. Do **not** translate it into a tool call,
   and do **not** perform the listing task yourself yet — the point is to see whether the
   harness intercepts the keyword and spins up a workflow on its own.

3. Immediately afterward, report what you observe:
   - Did a dynamic workflow launch? (e.g. an approval prompt for a workflow, a `/workflows`
     run appearing, a `<workflow>`/background-task indication, or a system reminder telling
     you to use a Workflow tool that fires from *your* output.)
   - Or did nothing happen at the harness level — the text was just text in your reply?

4. Conclude with a one-line verdict: **TRIGGERED** or **NOT TRIGGERED**, plus the single
   most direct piece of evidence for that verdict.

## Expected result (hypothesis to falsify)

The documented behavior is that the harness highlights and acts on the keyword only in the
**user's input** ("Claude Code highlights the keyword in your input"). Model output is not
user input, so the predicted result is **NOT TRIGGERED**. The probe exists to confirm or
falsify that empirically.
