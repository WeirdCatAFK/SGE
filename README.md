# Standard Generated English

Standard Generated English (SGE) is a writing standard for text that AI agents write. It is also a Claude Code skill and a checker that applies the standard.

SGE keeps text short, literal and plain. A person or another agent must read each sentence in one way only. SGE also limits code comments to a short file header and short doc comments.

## What the checker examines

- Markdown: sentence length, passive voice, semicolons, words to avoid, bold body text, separators, emoji and other decoration.
- Words to avoid: formal words, words that LLMs overuse, claims with no source, and leftover chatbot phrases. The list has 154 entries.
- Code: the comments in `.js`, `.jsx`, `.mjs`, `.cjs`, `.ts`, `.tsx` and `.py` files. The checker permits one file header of 3 lines or less, and doc comments of 5 lines or less directly above the code.

`rules.md` lists each rule and its severity.

## Install

Clone the repository into the Claude Code skills folder:

```bash
git clone https://github.com/WeirdCatAFK/SGE ~/.claude/skills/standard-generated-english
```

Claude Code then loads the skill in all your projects. The checker needs Python 3.8 or later and no other packages. The tests ran on Python 3.14.

## Use

Run the checker on files:

```bash
python -I ~/.claude/skills/standard-generated-english/scripts/sge_check.py README.md src/app.ts
```

Run it on the changed files of a git repository:

```bash
git ls-files -m -o --exclude-standard -z -- '*.md' '*.py' '*.js' '*.jsx' '*.mjs' '*.cjs' '*.ts' '*.tsx' | xargs -0 -r python -I ~/.claude/skills/standard-generated-english/scripts/sge_check.py
```

Options:

| Option              | Effect                                                       |
| ------------------- | ------------------------------------------------------------ |
| `--json`          | Prints the result as JSON, with only the sentences that fail |
| `--glossary PATH` | Permits the technical terms in a JSON list                   |
| `--disable RULES` | Turns off the rules in a comma-separated list                |
| `--selftest`      | Runs the built-in tests                                      |

## Verdicts

| Verdict               | Condition                  | Exit code |
| --------------------- | -------------------------- | --------- |
| compliant             | No findings                | 0         |
| minimal not compliant | Only minor findings        | 1         |
| not compliant         | One or more major findings | 3         |

Exit code 2 means a usage error.

## Credits

The checker started as a fork of `ste-lint.py` from the asd-ste100 skill by Dustin Yuchen Teng. `LICENSE-ste-lint` holds its MIT license. SGE is a separate standard. It does not copy ASD-STE100 or its dictionary, and it does not claim compliance with ASD-STE100.

The words that LLMs overuse come from Juzek and Ward, `Why Does ChatGPT "Delve" So Much?` (COLING 2025), and from the Wikipedia guide "Signs of AI writing".

## License

MIT. See `LICENSE`.
