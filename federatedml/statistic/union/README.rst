Union
======

Union module combines given tables into one while keeping unique entry ids. Union is a local module. Like DataIO, this module can be run on the side of Host or Guest, and running this module does not require any interaction with outside parties.


Use
------

Union currently only supports joining by entry id. For tables of data instances, their header, idx and label column name (if label exists) should match.

When an id appears more than once in the joining tables, user can specify whether to keep the duplicated instances by setting parameter `keep_duplicate` to True.
Otherwise, only the entry from its first appearance will be kept in the final combined table. Note that the order by which tables being fed into Union module depends on the setting specified in job dsl file. As shown below:


.. code-block:: json

    {
        "union_0": {
                "module": "Union",
                "input": {
                    "data": {
                            "data": ["dataio_0.data", "dataio_1.data", "dataio_2.data"]
                    }
                },
                "output": {
                    "data": ["data"]
                }
            }
        }


Tables from `dataio_0.data`, `dataio_1.data`, `dataio_2.data` will enter Union module in this order.

If an id `42` exists in both `dataio_0.data` and `dataio_1.data`, and:
1.) 'keep_duplicate` set to false: the value from `dataio_0.data` is the one being kept in the final result.
2.) 'keep_duplicate` set to true: the value from `dataio_0.data` and the one from `dataio_1.data` are both kept; the value from `dataio_1.data` will have a new id `42_dataio_1` in the result table.


For more example job configuration and dsl setting files, please refer `examples/federatedml-1.x-examples/union`.

Param
------

.. automodule:: federatedml.param.union_param
   :members: