# Contributing

- Nothing about us without us: disabled users take part in design, not only testing.
- Definition of done for every story: works with at least two input methods (or documents why not), passes CI on all supported OSes, passes the app's own accessibility checklist (contrast, focus order, target size, reduced motion), documented in the user guide, tried by at least one disabled tester before release.
- Any new third-party component, model or dataset must be added to `docs/licences/THIRD_PARTY.md` with its licence and redistribution terms.
- OS-specific code only in `adapters/`. No component other than `core/` may inject input.
