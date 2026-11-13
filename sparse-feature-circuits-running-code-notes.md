Cloned the repository from https://github.com/saprmarks/feature-circuits/tree/main

Installing packages with Python 3.13 failed (some Numpy library install conflict).

Installing packages with Python 3.11 seems to work for now.

Need Jupyter notebooks to run the code:
- Make a new branch
- Add `jupyter` to the requirements

Open the `experiments/bib_shift.ipynb` Jupyter notebook and start running each cell in order. Changes:
- Error: trying to get access to a gated repo (gemma-2-2b). Let's use Pythia instead since I want to just test it out anyway.
- Error: since I'm using a Mac I need to use `mps` as the device rather that CUDA
- Use layer 4 for Pythia rather than 22 (from the paper)

Error when training probes:
```
AttributeError: 'GPTNeoXForCausalLM' object has no attribute 'model'
```
Fix: change `acts` in `collect_activations` to:
```
acts = model.gpt_neox.layers[layer].output[0]
```

Error when training probes:
```
IndexError: Above exception when execution Node: 'getitem_0' in Graph: '14169918224'
```
Fix: unclear!