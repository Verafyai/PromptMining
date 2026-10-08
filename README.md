# Prompt Mining: Generative Chains

Interactive, single-file browser demos exploring what happens when generative AI becomes part of a blockchain: models as the key to a chain, mining by generating art, open math problems as puzzles, and living cellular automata grown from language.

The demos accompany two essays by Rex St. John (ironchef):

- *Generative AI Blockchains are Coming, And They Will Blow Your Mind* (Medium, Feb 2023)
- *Generative Blockchains* (Medium, Oct 2023)

> **These are concept demos, not production systems.** Every model, network, prover and result shown is simulated in the browser. Nothing here is connected to a real blockchain.

## The demos

| Demo | Idea | Docs |
|---|---|---|
| [Artwork Chain](demos/artwork-chain.html) | Each block is a painting generated from a verse plus the previous block's hash. Only the exact model can verify the chain. | [docs](docs/artwork-chain.md) |
| [Prompt Mining](demos/prompt-mining.html) | Proof of Generation: miners race to find the secret prompt that reproduces a broadcast hash. | [docs](docs/prompt-mining.md) |
| [Request for Art](demos/request-for-art.html) | The mining race as a scatter plot: near-misses gather toward the center, only an exact match solves. | [docs](docs/request-for-art.md) |
| [Proof Chain](demos/proof-chain.html) | Challenge Vaults: open Erdős problems stated in Lean, minted by whoever submits a proof the kernel accepts. | [docs](docs/proof-chain.md) |
| [Living Rules](demos/living-rules.html) | Lenia-style cellular automata, with an evolutionary search that finds rules that come alive. | [docs](docs/living-rules.md) |
| [Bloom Chain](demos/bloom-chain.html) | Type a prompt; Claude sketches it as living tissue and each new prompt evolves the scene, link by link. | [docs](docs/bloom-chain.md) |

## Running them

Each demo is one self-contained HTML file with no build step and no dependencies beyond Google Fonts.

```bash
git clone https://github.com/Verafyai/PromptMining.git
cd PromptMining
python3 -m http.server 8000
# open http://localhost:8000/demos/
```

Opening the files directly (`file://`) also works in most browsers. Living Rules and Bloom Chain need **WebGL 2** with floating-point render targets (any current Chrome, Firefox, Safari or Edge on a machine with a GPU).

## The thread running through them

1. **The model is the key.** A generative model's output depends on its exact weights. Store the hash of an output on-chain and only the exact model can reproduce it. Artwork Chain shows a fine-tuned "knockoff" failing verification.
2. **Generation as work.** Prompt Mining and Request for Art turn that into a mining race. They also show the idea's central weakness: real models are noisy, so the right prompt can still miss the hash.
3. **Swap the noisy model for a perfect checker.** Proof Chain replaces image models with the Lean theorem prover, whose kernel gives an exact yes or no. Verification is solved; scheduling is not, since nobody can predict when an open problem falls.
4. **Intelligence at every scale.** Living Rules and Bloom Chain move from chains of blocks to grids of cells, where one local rule produces structure at many scales, and a language model decides what gets grown.

See [docs/concepts.md](docs/concepts.md) for the design reasoning, including where each idea holds up and where it breaks.

## Repository layout

```
demos/   the six standalone HTML demos
docs/    one page per demo, plus the concepts overview
```

## License

MIT. See [LICENSE](LICENSE).
