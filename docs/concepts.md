# Concepts

This page explains the ideas behind the demos and is candid about which parts hold up.

## 1. The model is the key

A large generative model is a deterministic function of its weights, its input and its sampling settings. Fix all three and the output is reproducible byte for byte. Change any of them, even by fine-tuning a copy, and the output changes.

That gives a chain a new kind of key:

- A block stores a prompt, the previous block's hash and a **fingerprint** (hash) of the generated artifact.
- Anyone holding the canonical model can regenerate the artifact and check the fingerprint.
- Anyone without the exact model cannot produce artifacts the network accepts.

"Encryption" is the word the original essay used. Strictly, nothing is encrypted, because nothing is decrypted back to an original. A clearer description is **a hash only the exact model can reproduce**.

## 2. Proof of Generation

Bitcoin's proof of work spends compute on puzzles with no use of their own. Proof of Generation proposes spending it on generation instead:

1. A proposer picks a secret prompt, generates an artifact and broadcasts only its hash.
2. Miners generate candidates from guessed prompts and hash each one.
3. The first exact match wins and mints the artifact.

**Where it breaks:**

- **Determinism.** Production image models sample with noise. The right prompt usually yields a slightly different image and therefore a different hash. A real network would have to fix seeds, samplers and numeric precision across all hardware.
- **No partial credit.** A hash is all-or-nothing, so a near-miss is still a miss. Visual similarity does not help a miner.
- **Search space.** A three-word prompt space is tiny and enumerable. Large spaces make mining a lottery over language rather than useful work.

## 3. Challenge Vaults and the Proof Chain

Swapping the image model for the Lean theorem prover fixes verification: checking a proof is cheap, exact and objective. Each open problem becomes a vault:

- The Lean **statement** is hashed and locked into the vault, so nobody can claim it by proving an easier version.
- A submission passes only if the statement hash matches, no `sorry` remains, only the standard axioms (`propext`, `Classical.choice`, `Quot.sound`) are used, and the kernel type-checks the proof.
- The vault pays the bounty and records permanent credit.

**Why it is not proof of work.** Open problems have no difficulty adjustment, proof search rewards insight rather than random trials, a published proof can be copied and re-verified instantly (so it does not secure history), and the supply of problems is finite. The viable design lets an existing chain handle consensus and puts the vaults on top, with:

- **Commit-reveal** submissions to prevent front-running.
- A **challenge window** to catch misformalized statements before payout.
- A **difficulty ladder** of tractable goals (lemmas, unformalized known results) so contributors are rewarded between rare breakthroughs.

## 4. Cellular automata and fractal intelligence

Living Rules uses a continuous, multi-kernel automaton in the Lenia family. Every cell measures life in three rings around it and feeds each reading through a bell-shaped growth curve. Sensing at several distances at once is what produces structure at several scales: spots inside worms, worms inside colonies, membranes around colonies.

The automaton itself is not AI. AI enters in three possible places:

1. **As the rule:** neural cellular automata, where every cell runs a small trained network.
2. **As the judge:** a vision-language model scoring which simulations look alive or novel.
3. **As the designer:** a language model deciding what to grow.

Bloom Chain takes the third route: Claude turns a prompt into a sketch, assigns a living behavior to each part, and evolves the scene link by link, with each link's hash including the previous one.
