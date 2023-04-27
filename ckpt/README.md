# How to use pre-trained models

One can load a pre-trained model for fine-tuning or testing as follows:

```python
from src.trainers import TransformLearning

# create args parser and link to Lightning trainer:
parser = argparse.ArgumentParser(description="demo")
parser = Trainer.add_argparse_args(parser)

# extract args from config file and add to parser:
config = yaml_config_hook("some_config.yaml")
for key, value in config.items():
    parser.add_argument(f"--{key}", default=value, type=type(value))
args = parser.parse_args()

# set random seed if selected:
if args.seed:
    pl.seed_everything(args.seed, workers=True)

encoder = ... # PyTorch nn.Module
ckpt_path = "ckpt/s4_trans.ckpt"
model = TransformLearning.load_from_checkpoint(ckpt_path, encoder)
```