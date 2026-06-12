# 🦜 Generative Deep Learning - 2nd Edition Codebase

A fork of the official code repository for the second edition of the O'Reilly book *Generative Deep Learning: Teaching Machines to Paint, Write, Compose and Play*.
Modified for native use on Apple Silicon Macs (M-series) with Metal GPU acceleration.

[O'Reilly link](https://www.oreilly.com/library/view/generative-deep-learning/9781098134174/)

[Amazon US link](https://www.amazon.com/Generative-Deep-Learning-Teaching-Machines/dp/1098134184/)

<img src="img/book_cover.png" width="300px">

## 📖 Book Chapters

Below is an outline of the book chapters:

*Part I: Introduction to Generative Deep Learning*

1. Generative Modeling
2. Deep Learning

*Part II: Methods*

3. Variational Autoencoders
4. Generative Adversarial Networks
5. Autoregressive Models
6. Normalizing Flows
7. Energy-Based Models
8. Diffusion Models

*Part III: Applications*

9. Transformers
10. Advanced GANs
11. Music Generation
12. World Models
13. Multimodal Models
14. Conclusion

## 🌟 Star History

<img src="https://api.star-history.com/svg?repos=davidADSP/Generative_Deep_Learning_2nd_Edition&type=Date" width="500px">

## 🚀 Getting Started (Apple Silicon)

> **Note:** The original codebase was designed for Docker. This fork runs natively on Apple Silicon (M1/M2/M3/M5) using a Python virtual environment, giving you Metal GPU acceleration without any container overhead.

### Prerequisites

- [pyenv](https://github.com/pyenv/pyenv) — to manage Python versions
- [VSCode](https://code.visualstudio.com/) with the Python and Jupyter extensions

### Kaggle API

To download some of the datasets for the book, you will need a Kaggle account and an API token:

1. Sign up for a [Kaggle account](https://www.kaggle.com).
2. Go to the 'Account' tab of your user profile.
3. Select 'Create API Token'. This will trigger the download of `kaggle.json`, a file containing your API credentials.

### The .env file

Create a file called `.env` in the root directory with the following values (replacing the Kaggle credentials with those from your `kaggle.json`):

```
JUPYTER_PORT=8888
TENSORBOARD_PORT=6006
KAGGLE_USERNAME=<your_kaggle_username>
KAGGLE_KEY=<your_kaggle_key>
```

### Python setup

**1. Install Python 3.11 via pyenv**

`tensorflow-macos` requires Python 3.11:

```bash
pyenv install 3.11.9
pyenv local 3.11.9
```

**2. Create and activate a virtual environment**

```bash
python -m venv .venv
source .venv/bin/activate
```

**3. Install TensorFlow with Metal GPU support**

Install the Apple Silicon TensorFlow stack first, before the rest of the requirements, so pip resolves dependencies correctly:

```bash
pip install --upgrade pip
pip install tensorflow-macos tensorflow-metal
```

**4. Install the remaining dependencies**

```bash
pip install -r requirements.txt
```

**5. Register the virtual environment as a Jupyter kernel**

```bash
pip install ipykernel
python -m ipykernel install --user --name=gdl --display-name "GDL (Python 3.11)"
```

**6. Add the repo root to the Python path**

The notebooks import from the `notebooks/` package using the repo root as the base. Register it with the venv:

```bash
echo "$(pwd)" >> .venv/lib/python3.11/site-packages/gdl.pth
```

### Verify GPU access

```bash
python
```

```python
import tensorflow as tf
print(tf.__version__)
print(tf.config.list_physical_devices('GPU'))
```

You should see a `PhysicalDevice` with `device_type='GPU'` listed. This confirms Metal acceleration is active.

### Running notebooks

Open the repo in VSCode and select the **GDL (Python 3.11)** kernel from the kernel picker when opening any notebook. Notebooks are in the `/notebooks` folder, organised by chapter and example.

Alternatively, launch JupyterLab in the browser:

```bash
jupyter lab
```

## 🏞️ Downloading data

The codebase includes a data downloader script. Run the following from the repo root, choosing one of the named datasets:

```bash
bash scripts/download.sh [faces, bricks, recipes, flowers, wines, cellosuites, chorales]
```

## 📈 TensorBoard

To monitor training, launch TensorBoard using the helper script:

- `<CHAPTER>` — e.g. `03_vae`
- `<EXAMPLE>` — e.g. `02_vae_fashion`

```bash
bash scripts/tensorboard.sh <CHAPTER> <EXAMPLE>
```

TensorBoard will be available at `http://localhost:6006`.

## ☁️ Using a cloud virtual machine

To set up a virtual machine with GPU in Google Cloud Platform, follow the instructions in the [Google Cloud README](./docs/googlecloud.md).

## 📦 Other resources

Some of the examples in this book are adapted from the excellent open source implementations available through the [Keras website](https://keras.io/examples/generative/). New models and examples are constantly being added there.