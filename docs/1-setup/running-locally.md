

During the image build, Docker pulls in a [requirements.txt](../requirements.txt) file which lists the Python modules required to run the toolkit. These modules are automatically installed as the image is built. The requirements.txt file can also be used to create a [virtual Python environment](https://docs.python.org/3/tutorial/venv.html) on your local machine. When running the toolkit without using a container, it is recommended to create a virtual environment to prevent package versioning conflicts.

## Software requirements

We recommend using the Docker image to run the toolkit, but if you prefer you can run it locally.
If you chose to do so, you will need to have a modern Windows, Linux, or Mac computer with the software listed in the following table installed.

| Prerequisite | Minimum version
| :-           | :-
| Azure CLI    | 2.0.34
| Python       | 3.6 (3.7 not yet supported)

See [../requirements.txt] for Python package dependencies.