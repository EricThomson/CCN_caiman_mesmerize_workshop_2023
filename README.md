# CCN January 2023 Workshop

Materials for the workshop on CaImAn and Mesmerize for Calcium & Voltage Imaging. This repo currently only includes installation instructions but we will fill it in with more materials as the workshop approaches.

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

These are end-user instructions, they might look daunting but we have tried to describe each step in detail. Please post an issue on the appropriate repo or send a message on Slack. If you are interested in development see the devmode instructions on the respective repositories.

We recommend installing the `mesmerize-core` conda package which gives you everything that you need, including `caiman`. `fastplotlib` is installed separately but that is relatively trivial.

[**Note: If you haven't already done so please acquaint yourself with virtual environments**](https://www.freecodecamp.org/news/why-you-need-python-environments-and-how-to-manage-them-with-conda-85f155f4353c/)

**Note: The workshop will use the new `mesmerize-core` package, and not the old Mesmerize desktop application which is now legacy software. `mesmerize-core` is not backwards compatible so you will need to install `mesmerize-core`**

1. Install Anaconda if you already don't have it. You can find official instructions on the Anaconda website. A few important notes:
    - On Windows and Mac if you use the graphical installer make sure you choose to install *"Just Me"* and not a system install.
    - On Linux you can probably accept the default `PREFIX` to install to your user home directory, do not perform a system install.
  
1. Install `mamba` into your base environment. Skip this step if you have `mamba`. This step may take 10 minutes and display several messages like "Solving environment: failed with..." but it should eventually install `mamba`.

```bash
conda install -c conda-forge mamba

# if conda is behaving slow, this command can sometimes help
conda clean -a
```

**Important note: Sometimes conda or mamba will get stuck at a step, such as creating an environment or installing a package. Pressing `Enter` on your keyboard can sometimes help it continue when it pauses.**

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

If you continue to have issues with this step, please post an issue on the [`CaImAn` github](https://github.com/flatironinstitute/CaImAn) or post in the `#caiman` channel on slack.

5. Run `ipython` and verify that `caiman` and `mesmerize_core` are installed:

```python
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

7. If you have C compilers installed on your system we recommend installing `simplejpeg`. This is usually easier on Linux & Mac than on Windows. If you cannot install `simplejpeg` don't worry, it will just make `fastplotlib` slightly less fast.

8. Install Vulkan drivers for your GPU (this includes GPUs that are commonly integrated within CPUs).
    - Windows: Vulkan drivers should be installed by default so you shouldn't have to do anything, if you can run the first few cells of the `fastplotlib` `simple.ipynb` example you're good to go!
    - Mac uses Metal instead of Vulkan, which should also be installed by default so you don't have to do anything!
    - Linxu: This is the one time where you need to do more work on Linux :D . See the [`fastplotlib` repo](https://github.com/kushalkolar/fastplotlib#linux) for instructions.

9. Finally we recommend trying to run the simplest demo notebook for each library:
    - `fastplotlib`: https://github.com/kushalkolar/fastplotlib/blob/master/examples/simple.ipynb
    - `caiman`: https://github.com/flatironinstitute/CaImAn/blob/master/demos/notebooks/demo_pipeline.ipynb
    - `mesmerize-core`: https://github.com/flatironinstitute/CaImAn/blob/master/demos/notebooks/demo_pipeline.ipynb

You can either clone each repo to try out the demo notebooks or download the repo as a zip file:
https://github.com/kushalkolar/fastplotlib/archive/refs/heads/master.zip
https://github.com/flatironinstitute/CaImAn/archive/refs/heads/master.zip
https://github.com/nel-lab/mesmerize-core/archive/refs/heads/master.zip
