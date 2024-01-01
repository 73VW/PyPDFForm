<p align="center"><img src="https://github.com/chinapandaman/PyPDFForm/raw/master/logo.png"></p>
<p align="center">
    <a href="https://github.com/chinapandaman/PyPDFForm/actions/workflows/python-black-isort.yml/badge.svg"><img src="https://github.com/chinapandaman/PyPDFForm/actions/workflows/python-black-isort.yml/badge.svg"></a>
    <a href="https://github.com/chinapandaman/PyPDFForm/actions/workflows/python-package.yml/badge.svg"><img src="https://github.com/chinapandaman/PyPDFForm/actions/workflows/python-package.yml/badge.svg"></a>
    <a href="https://codecov.io/gh/chinapandaman/PyPDFForm"><img src="https://codecov.io/gh/chinapandaman/PyPDFForm/branch/master/graph/badge.svg?token=CSRLN14IFE"></a>
    <a href="https://github.com/chinapandaman/PyPDFForm/actions/workflows/python-publish.yml/badge.svg"><img src="https://github.com/chinapandaman/PyPDFForm/actions/workflows/python-publish.yml/badge.svg"></a>
    <a href="https://pepy.tech/project/pypdfform"><img src="https://static.pepy.tech/personalized-badge/pypdfform?period=total&units=international_system&left_color=black&right_color=blue&left_text=Downloads"></a>
    <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-orange.svg"></a>
</p>

## Important API Changes

Happy new year fellow developers! We start the year 2024 with a new release of v1.4.0 and 
there are some important changes I'm making to the APIs of the library.

* The PDF object that gets instantiated is now `PyPDFForm.PdfWrapper`, changed from `PyPDFForm.PyPDFForm`.
* Form widgets are now accessed via the `PdfWrapper.widgets` attribute, changed from `PdfWrapper.elements`.
* The JSON schema of the form data is now accessed via a new attribute called `PdfWrapper.schema`, 
changed from the old method of `PdfWrapper.generate_schema()`.

All the old APIs will be persisted for half a year and then fully deprecated. Each of them 
will emit a `DeprecationWarning` when invoked, so it is advised that you make the switch before they are 
removed and start breaking your code.

Happy hacking!

## Introduction

PyPDFForm is a pure Python library for PDF form processing. 
It allows filling a PDF form programmatically by creating 
a Python dictionary with keys matching its annotated names 
for widgets like text fields and checkboxes. It also supports other functionalities such as 
drawing image and merging multiple PDFs together.

## Installing

Install using [pip](https://pip.pypa.io/en/stable/):

```shell script
pip install PyPDFForm
```

## Quick Example
![Check out the GitHub repository for a live demo if you can't see it here.](https://github.com/chinapandaman/PyPDFForm/raw/master/demo.gif)

A sample PDF form can be found [here](https://github.com/chinapandaman/PyPDFForm/raw/master/pdf_samples/sample_template.pdf). Download it and try:

```python
import os

from PyPDFForm import PdfWrapper

PATH_TO_DOWNLOADED_SAMPLE_PDF_FORM = os.path.join(
    os.path.expanduser("~/Downloads"), "sample_template.pdf"
)  # Change this to where you downloaded the sample PDF form

PATH_TO_FILLED_PDF_FORM = os.path.join(
    os.path.expanduser("~"), "output.pdf"
)  # Change this to where you wish to put your filled PDF form

with open(PATH_TO_FILLED_PDF_FORM, "wb+") as output:
    output.write(
        PdfWrapper(PATH_TO_DOWNLOADED_SAMPLE_PDF_FORM)
        .fill(
            {
                "test": "test_1",
                "check": True,
                "test_2": "test_2",
                "check_2": False,
                "test_3": "test_3",
                "check_3": True,
            },
        )
        .read()
    )
```

After running the above code snippet you can find `output.pdf` at the location you specified, 
and it should look like [this](https://github.com/chinapandaman/PyPDFForm/raw/master/pdf_samples/sample_filled.pdf).

## Documentation

[Examples](https://github.com/chinapandaman/PyPDFForm/blob/master/docs/examples.md)

## Public Speak

[Chicago Python User Group - Dec 14, 2023](https://youtu.be/8t1RdAKwr9w?si=TLgumBNXv9H8szSn)

## How to Contribute

It is difficult to make sure that the library supports all the PDF form creating tools out 
there. So if you run into a case where the library does not work for certain PDF forms created by certain tools, feel free to open an issue with the problematic PDF form attached. I will seek 
to make the library support the attached PDF form as well as the tool used to create it.
