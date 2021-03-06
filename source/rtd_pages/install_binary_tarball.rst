:orphan:

.. _install-binary-tarball-guide:

Binary Tarball Download & Setup
===============================

The Electric Coin Company provides a binary tarball for download.

`Download Tarball for Debian Stretch v4.2.0 <https://z.cash/downloads/zcash-4.2.0-linux64-debian-stretch.tar.gz>`_

After downloading but before extracting, verify that the checksum of the tarball matches the hash below for the version of the binary you downloaded:

Debian Stretch:

.. code-block:: bash

   sha256sum zcash-4.2.0-linux64-debian-stretch.tar.gz

Result: ``386633ba5f740252830fab9f6dd6bc9cb31514357643b7a5caf11f5c4faa63af``

This checksum was generated from our gitian deterministic build process. `View all gitian signatures <https://github.com/zcash/gitian.sigs/tree/master>`_.

Once you've verified that it matches, extract the files and move the binaries into your executables $PATH: 

.. code-block:: bash

    tar -xvf zcash-4.2.0-linux64.tar.gz

    mv -t /usr/local/bin/ zcash-4.2.0/bin/*

Now that Zcash is installed, run this command to download the parameters used to create and verify shielded transactions:

.. code-block:: bash 

    zcash-fetch-params

Finally, `set up a configuration file <https://zcash.readthedocs.io/en/latest/rtd_pages/zcash_conf_guide.html>`_ (`~/.zcash/zcash.conf`) before runnning zcashd. It can be completely empty; it will then run with the default parameters.
