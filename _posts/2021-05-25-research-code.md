---
layout: post
title: "Writing Code for (Machine Learning) Research"
date: 2021-05-25
description: "Lessons from 3 years of computational science"
giscus_comments: true
toc:
  sidebar: left
tags: artificial-intelligence
citation: true
---

Writing code is an essential task in much of today's scientific research. In fields such as astronomy, chemistry, economics, and sociology, scientists are writing code in languages such as MATLAB, Python, R, and Fortran to perform simulations and analyze experimental results. These scientists, however, have minimal training as software engineers. The codebase is often nothing more than a disorganized collection of scripts, sometimes not even under source control. No doubt much contemporary research is bottlenecked by poor code quality. While scientists would be well served to read a software engineering book or two, writing code for business is not like writing code for research.

The problems, constraints, and therefore solutions are different. Business code is expected to run for years, sometimes continuously, serving up to billions of users. The code will be updated throughout its lifetime. Research code is run primarily by its author, secondarily by others who wish to build on the author's work. Thus, the best research code can be easily adapted into unrelated projects. In contrast, many software engineering design patterns seek to hide implementations behind various interfaces. Business code is expected to run on a variety of standard hardware without change in behavior. Research code often runs in unusual specialized environments such as supercomputers or embedded devices.

I have spent the last 3 years doing machine learning research, where code is both a tool and the artifact being studied. After 3 years, you tend to notice what works and what doesn't. Here is my advice.

## 1. Use Python

Python has the most extensive ecosystem of scientific packages and tools, too numerous to list here. Some are widely known, like [NumPy](https://numpy.org/) (linear algebra) or [Pandas](https://pandas.pydata.org/) (dataframes), but many are field specific, like [Astropy](https://www.astropy.org/) (astronomy). Many libraries are Python exclusives, such as the 3 previously mentioned. Others, such as [PyTorch](https://pytorch.org/) or [Tensorflow](https://www.tensorflow.org/) have frontends in other languages, but these are not as complete as the Python interface. Beyond the deep pool of great packages are tools like [Jupyter](https://www.jupyter.org/) or the VSCode [Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python) that make programming and viewing results easy.

The language itself has a concise syntax that prevents unnecessary keystrokes by the programmer. This dramatically reduces the time needed to complete first drafts of programs. Just compare the length of Hello World programs between Python, C++, and Java—the 3 most common introductory programming languages. Python's version is only one line compared to the 5+ lines needed by C++ and Java. In C++, printing to the screen requires an include (import) statement[^1]. Compared to specialized scientific languages like MATLAB or R, Python has the advantage of being a general purpose programming language. Python can be used for your machine learning or computational biology research, but it can also be used to download files off the internet or set up a website with the same ease.

```python
print('Hello World!')
```

```c++
#include <iostream>

int main() {
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```

```java
public class HelloWorld {

    public static void main(str[] args) {
        System.out.println("Hello World!");
    }
}
```

When should Python not be used? Often for certain applications, certain languages must be used.

- Interactive educational web apps: JavaScript
- Utilizing Nvidia GPU kernels for machine learning: C++ and CUDA
- Mobile apps: Swift for iOS and Java/Kotlin for Android (unless you use a cross-platform UI framework like React Native or Flutter)
- Climate change simulations on supercomputers: Fortran

High performance code, in general, should not be written in Python. Python is an interpreted language; each line is processed right before it runs. This precludes a number of optimizations that can be made in compiled languages. Because the compiler can see the entire file, it can perform a number of optimizations to make it run faster or consume less memory. Furthermore, Python has a Global Interpreter Lock which prevents multi-threading. While there has been discussion about its removal, that is unlikely to happen.

> Unfortunately, since the GIL exists, other features have grown to depend on the guarantees that it enforces. This makes it hard to remove the GIL without breaking many official and unofficial Python packages and modules.

## 2. Track Dependencies

Nearly every program relies on code authored by external parties. These are **dependencies**. Importantly, changes to dependencies can break your code. This is unlikely for many of the older, more popular packages. NumPy is not going to suddenly change how `np.array` works. But for younger packages, instability should be expected. A machine learning example is [torchtext](https://pytorch.org/text/stable/index.html) which migrated its datasets from subclassing `torchtext.data.Dataset` in version 0.8 to subclassing `torch.utils.data.Dataset` in version 0.9. After upgrading torchtext, much of my NLP code crashed in the process.

The solution is to specify the compatible versions of your dependencies. For Python programs, this can be done in a `requirements.txt` file. These packages and their versions can be installed in a new environment with a single command. An **environment** is an isolated set of dependencies which can be swapped in or out for different projects.

```python
torch==1.7.0
torchvision==0.8.0
torchaudio==0.7.0
torchtext==0.8.0
```

```bash
pip install -r requirements.txt
```

## 3. Use Hydra

At least in machine learning, computational experiments may contain a number of hyperparameters[^2] that influence the result. Some may be experimental hyperparameters such as the choice of model or learning algorithm which vary for the sake of comparison. Others, such as the learning rate, may need to be tuned to the correct value for the experiment to work. Researchers are interested in the result under the best-case value for these parameters. Tracking which trials used what parameter values can be tricky when launching them in batches across multiple machines. [Hydra](https://hydra.cc/) solves this problem.

{% include figure.liquid path="https://hydra.cc/img/logo.svg" class="img-fluid" %}

Using Hydra is as simple as inserting a single decorator around your `main` function. Hydra will create a config object from a group of YAML files accessible inside `main`. Hyperparameters can be accessed as object properties: `cfg.prop1`, `cfg.prop2`, etc. Parameter values can be overridden by in the command line using the syntax `prop1=value1 prop2=value2` when the program is launched. This makes it easy to, say, start several experiments using different learning rates. This config object can be passed to different functions in classes as one argument, irrespective of the number of hyperparameters they access.

Each program run creates a new folder `outputs/yyyy-MM-dd/hh-mm-ss` (date and time of launch) that becomes the current working directory. Plots, tables, and data saved to relative paths (those not starting with ~, /, or C:/ on Windows) will be placed inside this new folder. Inside, Hydra will save a copy of your config object as `config.yaml` and create a `main.log` file. Loggers are automatically configured to write to this file.

```python
import hydra
import logging
import os

log = logging.getLogger(__name__)  # __name__ is the name of the module

@hydra.main(config_path='config_folder', config_name='config_file.yaml')
def main(cfg):
    function_which_uses_2_properties(cfg)
    print(os.getcwd())  # current working directory is outputs/yyyy-MM-dd
    log.info("Writing INFO level message to main.log")
```

## 4. Document But Don't Test

In Python and most programming languages, allow explanatory comments to be placed beside confusing code. A special type of comment is a **doc comment** placed above a class/function definition. In Python, these are triple-quote strings, hence the name **docstring**, which go below the class/function definition. Docstring provide invaluable context to other researchers looking to build on top of your work. Others will need to understand the inner workings of your code before they can modify it. Docstrings also jog the memory when you revisit your code in the future as a stranger.

Docstrings can be formatted however, but I prefer to use [Google's docstring style](https://github.com/google/styleguide/blob/gh-pages/pyguide.md#38-comments-and-docstrings). The first section is reserved for a description of the class/function; succeeding sections provide more information about arguments, return values, exceptions, and properties. If you use VSCode, I recommend installing the [Python Docstring Generator](https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring) extension which can create a docstring template upon typing `"""`. VSCode will display the docstring when hovering over a function call.

```python
def function(arg1, arg2):
    """[summary]

    Args:
        arg1 (type): [description]
        arg2 (typd): [description]

    Returns:
        [description]

    Raises:
        [exception]: [description]
    """
```

While it's it important to write docstrings, writing unit/integration tests are a waste of time. The test code will call sections of the source code to check its correctness. Usually, the author of the section will write the tests. This doubles the effort required to implement a certain feature. That may already be a dealbreaker but, since research is a messy process of diving into the unknown, research code has a short lifetime. There is no point writing tests for code which might be abandoned or revised in a few days. Moreover, the presence of bugs is not necessarily a problem. Research code is often narrow in scope, not designed to work without flaw in every circumstance.

## 5. Release Your Code

Whenever possible, code should be made public. The code to generate the plots are as important as the plots themselves. If the latter can be included in a publication, the former can be distributed as well. In many cases, such as in machine learning, the code itself is the labor of your research, developing this algorithm that does $X$ or solves $Y$. To withhold the code is like a withholding a proof in to a theorem. Stating that a statement is proven is not as interesting as the actual mechanics of proving it. Such a central artifact should be shared. There is also a more selfish motive for open sourcing code. Other researcher using it will cite your papers.

## See Also

- <https://da-data.blogspot.com/2016/04/stealing-googles-coding-practices-for.html>
- <https://github.com/allenai/writing-code-for-nlp-research-emnlp2018/>

---

[^1]: You can use `printf` to output the console, but it is not recommended over using `std::cout`.
[^2]: Machine learning models contain a number of parameters which are adjusted during training. The hyper in hyperparameter distinguishes values, like learning rate, which do not change over the course of training from model parameters.
