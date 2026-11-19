# Contributing / Как допринасяме

## Branches / Клонове

- Never commit directly to `main`. / Никога не записваме директно в `main`.
- One branch per issue, named `<type>/t<NN>-<short-name>`, e.g. `docs/t03-service`, `fix/t14-revert-port`. / Един клон за всяка задача.
- Types: `docs`, `feat`, `fix`, `chore`, `test`.
- Delete the branch after the merge. / Клонът се трие след сливането.

## Commits / Комити

- Format: `<type>: <what changed>` in the imperative, e.g. `docs: add glossary terms`. / Формат: `<тип>: <какво се промени>`.
- First line at most 72 characters. / Първият ред е до 72 знака.
- One logical change per commit. / Една логическа промяна в комит.
- Reference the issue in the body: `Closes #12`. / В тялото се посочва задачата.

## Pull requests / Заявки за сливане

- Every change reaches `main` only through a pull request. / Всяка промяна влиза в `main` само чрез PR.
- Fill in the PR template and link the issue with `Closes #NN`. / Попълва се шаблонът и се свързва задачата.
- At least 1 approval from a code owner; the author does not merge without it. / Поне 1 одобрение от code owner.
- Keep the history linear: merge with **Squash and merge** or **Rebase and merge**. / Историята е линейна.
- Resolve conflicts locally on your branch, not in `main`. / Конфликтите се решават локално в клона.

Branching strategy: GitHub Flow. We agreed on it over trunk-based: short feature branches with a reviewed PR into a protected `main` fit a small team, and `main` is always releasable.
