Getting Started
===============

Running Locally
---------------

Glow requires Apache Spark 3.1.2.

.. tabs::

    .. tab:: Python

        If you don't have a local Apache Spark installation, you can install it from PyPI:

        .. code-block:: sh

          pip install pyspark==3.1.2

        or `download a specific distribution <https://spark.apache.org/downloads.html>`_.

        Install the Python frontend from pip:

        .. code-block:: sh

          pip install glow.py

        and then start the `Spark shell <http://spark.apache.org/docs/latest/rdd-programming-guide.html#using-the-shell>`_
        with the Glow maven package:

        .. code-block:: sh
          :substitutions:

          ./bin/pyspark --packages io.projectglow:glow-spark3_2.12:|mvn-version| --conf spark.hadoop.io.compression.codecs=io.projectglow.sql.util.BGZFCodec

        To start a Jupyter notebook instead of a shell:

        .. code-block:: sh
          :substitutions:

          PYSPARK_DRIVER_PYTHON=jupyter PYSPARK_DRIVER_PYTHON_OPTS=notebook ./bin/pyspark --packages io.projectglow:glow-spark3_2.12:|mvn-version| --conf spark.hadoop.io.compression.codecs=io.projectglow.sql.util.BGZFCodec

        And now your notebook is glowing! To access the Glow functions, you need to register them with the
        Spark session.

        .. invisible-code-block: python

          path = 'test-data/tabix-test-vcf/NA12878_21_10002403.vcf.gz'

        .. code-block:: python

          import glow
          spark = glow.register(spark)
          df = spark.read.format('vcf').load(path)

    .. tab:: Scala

        If you don't have a local Apache Spark installation,
        `download a specific distribution <https://spark.apache.org/downloads.html>`_.

        Start the `Spark shell <http://spark.apache.org/docs/latest/rdd-programming-guide.html#using-the-shell>`_
        with the Glow maven package:

        .. code-block:: sh
          :substitutions:

          ./bin/spark-shell --packages io.projectglow:glow-spark3_2.12:|mvn-version| --conf spark.hadoop.io.compression.codecs=io.projectglow.sql.util.BGZFCodec

        To access the Glow functions, you need to register them with the Spark session.

        .. code-block:: scala

          import io.projectglow.Glow
          val sess = Glow.register(spark)
          val df = sess.read.format("vcf").load(path)

Notebooks embedded in the docs
------------------------------

To demonstrate use cases of Glow, documentation pages are accompanied by embedded notebooks. Most code in these notebooks can be run on Spark and Glow alone, but functions such as ``display()`` or ``dbutils()`` are only available on Databricks. See :ref:`dbnotebooks` for more info.

Also note that the path to datasets used as example in these notebooks is usually a folder in ``/databricks-datasets/genomics/`` and should be replaced with the appropriate path based on your own folder structure.

Getting started on Databricks
-----------------------------

The Databricks documentation shows how to get started with Glow on **Amazon Web Services** (AWS - `docs <https://docs.databricks.com/applications/genomics/genomics-libraries/index.html>`_), **Microsoft Azure** (`docs <https://docs.microsoft.com/en-us/azure/databricks/applications/genomics/genomics-libraries/>`_) and **Google Cloud Platform** (GCP - `docs <https://docs.gcp.databricks.com/applications/genomics/genomics-libraries/index.html>`_). 
This documentation includes,
 
1. **cluster recommendations**
2. **how to install** 
	- Glow
	- Hail
	- The Variant Effect Predictor
	- DeepNull
        - Deep Variant
3. **how to develop automated production jobs**

Getting started on other cloud services
---------------------------------------

Please submit a pull request to add a guide for other cloud services.
