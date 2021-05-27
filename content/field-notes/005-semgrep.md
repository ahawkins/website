---
title: "Semgrep"
slug: 5
author: "Adam Hawkins"
date: 2021-05-26T22:07:56-10:00
summary: Semgrep is great. Try it!
---

I started using [semgrep][] on a work project. I initially learned
about the project through HN. The project looked great so I filed it
under "tools to use when the time comes". Well the time came. Here are
my initial thoughts in preparation for writing a guide.

My use case was detecting jest `expect` calls that would be replaced
by a custom matcher. Here is the backstory. The codebase makes calls
to the [Slack BlockKit API][blockkit]. This results in large complex objects in
HTTP requests. Different blocks have their own validations too such as
"this field only accepts these values", or "this field must be less
than X characters" etc. The test suite did not capture 100% of these
requirements. The result was tests would pass but then fail in
production due to some unknown API constraint or other contractor
error. This had happened before, so I updated the relevant test, then
continued work.

The problem with that approach is it's a local fix to that specific
block in that specific test. The same issue may be present in other
API calls but there's no way to know without adding more `expect`
calls. I decided to write a custom jest matcher that encapsulated
checks for "should match contract" that supersede the other calls.

I figured `semgrep` would work well enough for this. I could write
rules to match lines that I should change. Then run `semgrep` to find
tests to refactor, then repeat until `semgrep` passed. That worked
well.

Here's an example:

The test have a lot of code like this:

```javascript
expect(message.blocks[0]).toHaveProperty("type", "section");
// check required text.type
expect(message.blocks[0]).toHaveProperty("text.type", "mrkdwn");
// check required text.text present
expect(message.blocks[0]).toHaveProperty("text.text");

// continue to make specific expectations on property values
```

These three lines are coarse contract testing. They are repeated
_a lot_ in the codebase. I'd guess it's in the hundreds. I want all
those replaced with something like:

```javascript
// One custom matcher that checks the block is compliant with the
// "section" API spec
expect(message.blocks[0]).toBeSection();
```

Now the test suite can add more checks to `toBeSection()` and now more
repeated code. All that's left is to identify all the call sites.
`semgrep` is great for this.

I initially wrote a rule to find all `toHaveProperty("type", "section")` calls. Then I learned I could generalize it to find common
_sequences_ of code. Check this out.

```yaml
- id: expect.slack.block.manual-matcher
  languages:
    - javascript
  message: |
    Use our custom Slack Block matchers instead of these checks.

    The custom matchers encapsulate all theses expectations.
    They also check that the Block objects are API compliant.
    That means their shape is checked and other semantics like
    length of certain attributes, expected values of attributes,
    and other contraints imposed by the Slack API.

    Our matchers are

    - `toBeSection()`
    - `toBeHeader()`
    - `toBeContext()`
    - `toBeButton()`

    Etc, etc. There is a matcher for all different types of Slack Blocks.
  severity: ERROR
  pattern-either:
    # For blocks with text
    - pattern: |
        $EXPECT.toHaveProperty("type", "...")
        $EXPECT.toHaveProperty("text.type", "...")
        $EXPECT.toHaveProperty("text.text")
      # For blocks that forgot to check text.type
    - pattern: |
        $EXPECT.toHaveProperty("type", "...")
        $EXPECT.toHaveProperty("text.text")
      # For blocks that forgot to check text.text
    - pattern: |
        $EXPECT.toHaveProperty("type", "...")
        $EXPECT.toHaveProperty("text.type", "...")
      # For "context" blocks
    - pattern: |
        $EXPECT.toHaveProperty("type", "...")
        $EXPECT.toHaveProperty("elements")
```

I'm not going to go deep into the pattern rules right now but I think
it's clear enough what's going on. `$EXPECT` is a placeholder for
anything with the `.toHaveProperty` method called. `"..."` means any
string. This allowed me generalize pattern for common object "shape"
expectations.

This is just the beginning of my `semgrep` practice. This small
experiment taught me that it is a useful tool and definitely deserves
a spot in my workflow. I can't wait to add this to my precommit
`lint-staged` hook.

The second learning is that Semgrep has an `--autofix` option. **Do
not use this**. It's not reliable enough yet. Consider this alpha
level.

Lastly, it could be faster. It could be too slow to run on entire
codebases during precommit. Luckily it can be limited to specific
files on the CLI. Even so, it could be faster. Hopefully the team
makes performance improvements in the future.

Regardless of all this, I'm stoked to keep practicing with semgrep to
see how and where it can improve my workflow. You should try it.

[semgrep]: https://semgrep.dev
[blockkit]: https://api.slack.com/reference/block-kit/blocks
