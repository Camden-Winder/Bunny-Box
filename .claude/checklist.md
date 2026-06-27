# Pre-flight Checklists

## Before Every Commit

- [ ] `bash -n Q2/install-bb-q2.sh` — no syntax errors
- [ ] If Max4 or Plus4 were touched: `bash -n Max4/install-bb-max4.sh` and `bash -n Plus4/install-bb-p4.sh`
- [ ] No raw `echo` used where `printf` is the established pattern
- [ ] Any config file that must survive Happy Hare's install is explicitly re-copied after `./install.sh` in the relevant install script

## Before Merging to main

- [ ] All shell scripts pass `bash -n`
- [ ] PR is not draft
- [ ] No unresolved merge conflicts
- [ ] PR description complete (no placeholder comments remaining)
