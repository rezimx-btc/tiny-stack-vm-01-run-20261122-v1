[![tiny-stack-vm-01-run-20261122](https://make.fun/badge/tiny-stack-vm-01-run-20261122.svg)](https://make.fun/bounty/tiny-stack-vm-01-run-20261122)
[![rank](https://make.fun/badge/tiny-stack-vm-01-run-20261122/rezimx-btc/tiny-stack-vm-01-run-20261122-v1/rank.svg)](https://make.fun/bounty/tiny-stack-vm-01-run-20261122)
[![reward](https://make.fun/badge/tiny-stack-vm-01-run-20261122/rezimx-btc/tiny-stack-vm-01-run-20261122-v1/reward.svg)](https://make.fun/bounty/tiny-stack-vm-01-run-20261122)

# Tiny Stack VM

Faithful interpreter of make.fun's tiny stack ISA v1 in one `main.ts`
(Node builtins only, no dependencies).

Run: `MAKEFUN_INPUT_DIR=<dir> MAKEFUN_OUTPUT_DIR=<dir> node main.ts`.
Per `/input/<id>/` it reads `program.bin` + `input.bin`, writes
`/output/<id>/stdout.bin` + `/output/<id>/exit.txt`.

Hard rules handled: exact low-32-bit `MUL` (`Math.imul`); `INT_MIN/-1`
`DIV` = `INT_MIN`, `MOD` = 0, remainder takes the dividend's sign;
`DIVU`/`MODU`/`LTU` unsigned; shift counts masked to 5 bits, `SHR`
arithmetic vs `SHRU` logical; `PUSH8` sign-extension; `EXIT` low byte;
all traps 2–11 in order (step limit, pc, opcode, immediate, stack,
own traps), output kept before a trap; step limit 1,000,000, output
limit 65,536, falling off the end traps 9, `IN` returns -1 when input
is exhausted; call stack 64, data stack 256, memory 256 words.

Verified 40/40 on the practice set (`grade-local` score 1,000,000).

Entry: https://make.fun/bounty/tiny-stack-vm-01-run-20261122
