.. _customize-datagrids-extensions-export:

Export Extension
================

This extension provides a functionality to export grid rows. This allows you to export rows from all pages. The exported data will be the same as on a grid, including filters and sorting.

Configuration
-------------

To enable export functionality you just need to add `export` option to a configuration of your grid. For example:

.. code-block:: yaml


    datagrids:
        accounts-grid:
            ...
            options:
                export: true


After that `Export` button will be displayed in the top left corner of a grid. To export grid data, users need to click this button and select the format of exporting data (currently only CSV format is implemented).

If you need to allow to export grid data in other formats, you need to configure your grid properly. For example, to allow export data in CSV and PDF formats you can use the following configuration:

.. code-block:: yaml


    datagrids:
        my-grid:
            ...
            options:
                export:
                    csv: { label: oro.grid.export.csv }
                    pdf: { label: acme.grid.export.pdf }


You also need to implement and register a writer for the new export format. To register a writer in dependency container, use the following naming convention: ``oro_importexport.writer.echo.[format]``. So, a writer for PDF should be registerd as ``oro_importexport.writer.echo.pdf``.

You can use |existing CSV writer| as an example for your writer.

There is also the ability to influence performance by changing the value of the grid export page size in the configuration. This will allow you to change the number of queries to the database. But keep in mind that increasing the size of the batch increases memory consumption.

.. code-block:: yaml


    datagrids:
        my-grid:
            ...
            options:
                export:
                    csv:
                        label: oro.grid.export.csv
                        page_size: 500

.. include:: /include/include-links-dev.rst
   :start-after: begin