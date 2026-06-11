# raven-prompt

Small interactive prompts for a terminal program: ask a question, confirm a
yes/no, or pick from a menu. The question is styled with raven-color, and the
answer interpreters are plain functions you can test on their own.

## Install

```toml
[dependencies]
"github.com/martian56/raven-prompt" = "0.1"
```

That pulls in raven-color too.

## Usage

```raven
import "github.com/martian56/raven-prompt" { ask, ask_default, confirm, select }

fun main() {
    let name = ask("What's your name")
    let env = ask_default("Environment", "production")
    if confirm("Deploy now", false) {
        let region = select("Region", ["us-east", "eu-west", "ap-south"])
        // region is the chosen 0-based index, or -1 if the answer wasn't valid
    }
}
```

Each prompt reads one line from standard input. On end of input (a pipe, or no
terminal) it returns the default instead of hanging: an empty string for `ask`,
the given default for `ask_default` and `confirm`, and -1 for `select`.

## The pieces

`ask(question)` and `ask_default(question, default)` collect free text.
`confirm(question, default)` is the yes/no prompt, where `y` or `yes` is true and
empty falls back to the default. `select(question, options)` prints a numbered
menu and gives you the chosen index.

The interpretation is split out so you can use or test it without any IO:
`yes_no(answer, default)` and `parse_choice(answer, count)` do the parsing, and
`prompt(question)` builds the styled prefix.

## License

MIT
