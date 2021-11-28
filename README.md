# observable-jupyter

Embed cells from [Observable](https://observablehq.com/) notebooks into Jupyter notebooks.

[View demo notebook on Colab](https://colab.research.google.com/drive/1t_wcE-NqoPO-dpnrB9VMQ0KUxR5e1rML?usp=sharing)

This library provides a simple way to embed cells and pass custom inputs values to them from Python code. For more complicated data flow in Jupyter notebooks, see the related library [observable-jupyter-widget](https://github.com/thomasballinger/observable-jupyter-widget) which uses the Jupyter Widget system to pass data back and forth between Python and JavaScript.

# Usage

To install the library, import the embed function, and embed the "graphic" cell from [this Observable notebook](https://observablehq.com/@mbostock/epicyclic-gearing):
~~~py
!pip install observable_jupyter
from observable_jupyter import embed
embed('@mbostock/epicyclic-gearing', cells=['graphic'], inputs={'speed': 0.2})
~~~

The simplest way to use `embed()` is to render an entire Observable notebook:
~~~py
embed('@d3/gallery')
~~~

You may want to swap in your own data into a D3 chart:
~~~py
import this
text = ''.join(this.d.get(l, l) for l in this.s)
embed('@d3/word-cloud', cells=['chart'], inputs={'source': text})
~~~

With multiple cells, you can embed interactive charts!
~~~py
embed(
    '@observablehq/visualize-a-data-frame-with-observable-in-jupyter,
    cells=['vegaPetalsWidget', 'viewof sepalLengthLimits', 'viewof sepalWidthLimits'],
)
~~~

Embedding specific cells with the cell keyword parameter of `embed([])` causes only these cells to be shown, but every cell still runs.

This behavior is slightly different than the Observable embed default.

## About this library

This library uses the APIs provided by [Observable](https://observablehq.com) to embed notebooks hosted on Observable in Jupyter.

The library was [developed at Observable](https://github.com/observablehq/observable-jupyter) but is now maintained by Thomas Ballinger.
All code added before Sept 2021 is copyright Observable.

## Development

See [ARCHITECTURE.md](./ARCHITECTURE.md) for an overview.

Because Python library includes JavaScript, you'll need node as well as Python to contribute to it.

The two JavaScript files included in an installed package iframe_bundle.js and wrapper_bundle.js are not saved in this repo.
They are generated by rollup, a JavaScript "bundler" that combines JavaScript source code
from files in the js folder and dependencies listed in [js/package.json](./js/package.json).

Installing the Python package with or `pip install -e .` will automatically run the bundler and produce these files.

