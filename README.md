# CCN January 2023 Workshop

Materials for the workshop on CaImAn and Mesmerize for Calcium & Voltage Imaging.

This workshop will cover the following topics:

1. [`fastplotlib`](https://github.com/kushalkolar/fastplotlib) for very fast interactive visualization of large datasets in notebooks.
2. Preprocessing of calcium imaging data
3. Various [`CaImAn`](https://github.com/flatironinstitute/CaImAn) algorithms including:
  - NoRMCorre motion correction
  - CNMF(E) - Constrained Non-negative Matrix Factorization for source separation and extraction
  - OnACID and FIOLA for online calcium imaging analysis
  - VolPy for voltage imaging analysis
4. [`mesmerize-core`](https://github.com/nel-lab/mesmerize-core) for parameter optimization and dataorganization of CaImAn algorithm outputs.
5. Postprocessing

# Installation instructions

These are end-user instructions. If you are interested in development see the devmode instructions on the respective repositories.

We recommend installing the `mesmerize-core` conda package which gives you everything that you need, including `caiman`. `fastplotlib` is installed separately but that is relatively trivial. [**If you haven't already done so please acquaint yourself with virtual environments**](https://www.freecodecamp.org/news/why-you-need-python-environments-and-how-to-manage-them-with-conda-85f155f4353c/)

1. Install Anaconda if you already don't have it. You can find official instructions on the Anaconda website. A few important notes:
    - On Windows and Mac if you use the graphical installer make sure you choose to install *"Just Me"* and not a system install.
    - On Linux you can probably accept the default `PREFIX` to install to your user home directory, do not perform a system install.
  
1. Install `mamba` into your base environment. Skip this step if you have `mamba`. This step may take 10 minutes and display several messages like "Solving environment: failed with..." but it should eventually install `mamba`.

```bash
conda install -c conda-forge mamba

# if conda is behaving slow, this command can sometimes help
conda clean -a
```

2. To create a new environment and install `mesmerize-core` into it do this:

```bash
mamba create -n mescore -c conda-forge mesmerize-core
```

`caiman` is a dependency of `mesmerize-core` so it will automatically grab `caiman` too

If you already have an environment with `caiman`:

```bash
mamba install -n name-of-env-with-caiman mesmerize-core
```

3. Activate environment. You can only use `mesmerize-core` in the environment that it's installed into.

```bash
mamba activate mescore
```

4. Install `caimanmanager`

```bash
caimanmanager.py install
```

The `caimanmanager.py` step may cause issues, especially on Windows. Assuming your anaconda is in your user directory a workaround is to call it using the full path:

```bash
python C:\Users\your-username\anaconda3\envs\your-env-name\bin\caimanmanager.py install
```

If you continue to have issues with this step, please post an issue on the caiman github or gitterpip install git+https://github.com/kushalkolar/fastplotlib.git: https://github.com/flatironinstitute/CaImAn/issues 

5. Run `ipython` and verify that `caiman` and `mesmerize_core` are installed:

```bash
# run in ipython
import caiman
import mesmerize_core
print(caiman.__version__)  # should be 1.9.13, anything over 1.9.10 is mostly fine for the workshop but we recommend 1.9.13
print(mesmerize_core.__version__)  # should be 0.1.0, make sure it's not the 0.1.0.b1 beta version
```

6. Install `fastplotlib` for visualization into the same environment (run this in the anaconda prompt, not ipython)

```bash
pip install git+https://github.com/kushalkolar/fastplotlib.git
```

If you don't have git installed you will need to install that first in the environment:

```bash
conda install git
```


