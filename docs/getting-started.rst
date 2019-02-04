***************************
Getting started
***************************

Requirements
============

First we need to install the requirements of the ``jwst`` package,
see `the JWST instructions
<https://github.com/spacetelescope/jwst/#installing-the-latest-development-version>`_,
reported here for convenience::

    conda create -n jwst_dev --only-deps --override-channels -c http://ssb.stsci.edu/astroconda-dev -c defaults python=3.6 jwst
    source activate jwst_dev

then we need to install the ``jwst`` package, in the future we will be able to use
the package released by Space Telescope, for now I have some minor modifications,
therefore you need to install my fork::

    git clone --branch iris_devel https://github.com/zonca/jwst
    cd jwst
    python setup.py install

Then you need to download the ``CRDS`` cache:

.. code-block:: bash

    git clone https://github.com/oirlab/tmt-crds-cache $HOME/crds_cache

the ``CRDS`` cache contains metadata for IRIS, the calibration files, flat fields,
and a set of rules_ on how to choose the right calibration file given a set of metadata,
you can browse the content on `Github <https://github.com/oirlab/tmt-crds-cache>`_.

.. _rules: https://github.com/oirlab/tmt-crds-cache/blob/master/mappings/tmt/tmt_iris_flat_0001.rmap

Finally, we need a custom version of the ``CRDS`` library that contains some modules specific to TMT::

    git clone https://github.com/oirlab/tmt-crds.git
    cd tmt-crds
    pip install .

Development install
===================

First fork the repository under your account on Github,
then clone your fork on your machine.

Then enter the root folder and create a development install
with::

  pip install -e .

Example pipeline
================

You can then run a example pipeline to subtract the background and apply flat-fielding
to a simple simulated observation of the imager::

    git clone https://github.com/oirlab/IRIS-data-reduction-tests
    cd IRIS-data-reduction-tests/201901_stpipe_iris_pipeline

then run the bash script ``run.sh``::

    bash run.sh

this will load the input files ``sci.fits`` and ``bg.fits``, retrieve a flat from the ``CRDS`` cache
and then perform the pipeline steps defined in the configuration file and output a reduced frame
in FITS format.