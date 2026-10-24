# Copilot instructions

## Project structure

- This repository contains two independent entry points: `main.go` is a minimal Go command-line program, and `index.html` is the standalone Órbita space-exploration quiz. The Go program does not serve or generate the web page.
- The quiz is intentionally self-contained: its HTML, CSS, question data, and browser-side JavaScript live in `index.html`. It runs directly as a local file and has no web build step or runtime dependencies.
- The Go module is declared in `go.mod` and targets Go 1.27.1. Module dependencies are recorded in `go.sum`.

## Build, test, and lint

- Run the Go program: `go run .`
- Build all Go packages: `go build ./...`
- Run Go tests: `go test ./...`
- Run one Go test by name: `go test . -run '^TestName$'` (when tests exist; put them in `*_test.go` files).
- Run Go's static checks: `go vet ./...`
- Format Go source: `gofmt -w main.go`
- There are no repository-specific web build, test, or lint commands. Preview the quiz by opening `index.html` in a browser; verify interactive behavior in the browser.

## Code conventions

- Keep the quiz offline and dependency-free. Add questions to the `questions` array in `index.html`; each entry supplies its prompt, four options, zero-based correct-answer index, and explanation.
- Keep quiz state and UI behavior in the existing page script, and derive progress and results from the question list rather than duplicating its length.
- Preserve the page's semantic and keyboard behavior: native buttons for choices and actions, visible keyboard focus, arrow-key choice navigation, announced feedback/progress, and focus transfer when advancing or restarting.
- Keep visual changes consistent with the CSS custom properties and `prefers-color-scheme` themes. Respect `prefers-reduced-motion` for animations, including decorative effects.
