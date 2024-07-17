# Setup
- use python 3.9.19
- after installing torch you get this error:
```bash
ERROR - main.py - 2024-07-17 10:26:28,456 - Traceback (most recent call last):
  File "/home/nisar2/projects/ddim/main.py", line 224, in main
    runner.train()
  File "/home/nisar2/projects/ddim/runners/diffusion.py", line 101, in train
    dataset, test_dataset = get_dataset(args, config)
  File "/home/nisar2/projects/ddim/datasets/__init__.py", line 69, in get_dataset
    dataset = CelebA(
  File "/home/nisar2/projects/ddim/datasets/celeba.py", line 56, in __init__
    super(CelebA, self).__init__(root)
  File "/home/nisar2/projects/ddim/datasets/vision.py", line 10, in __init__
    if isinstance(root, torch._six.string_classes):
  File "/home/nisar2/anaconda3/envs/ddim/lib/python3.9/site-packages/torch/__init__.py", line 2005, in __getattr__
    raise AttributeError(f"module '{__name__}' has no attribute '{name}'")
AttributeError: module 'torch' has no attribute '_six'
```
to fix this, change the following in `datasets/vision.py` from this:
```python
if isinstance(root, str):
    root = os.path.expanduser(root)
self.root = root
```
to this:
```python
if isinstance(root, str):
    root = os.path.expanduser(root)
self.root = root
```