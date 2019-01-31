.. lsst-task-topic:: lsst.verify.gen2tasks.MetricTask

.. currentmodule:: lsst.verify.gen2tasks

##################################
MetricTask (lsst.verify.gen2tasks)
##################################

``MetricTask`` is a base class for generating `lsst.verify.Measurement` given input data.
Each ``MetricTask`` class accepts specific type(s) of datasets and produces measurements for a specific metric or family of metrics.

While its API mirrors that of `~lsst.pipe.base.PipelineTask`, this version of ``MetricTask`` is designed to be used with the Gen 2 framework.

.. _lsst.verify.gen2tasks.MetricTask-api:

Python API summary
==================

.. lsst-task-api-summary:: lsst.verify.gen2tasks.MetricTask

.. _lsst.verify.gen2tasks.MetricTask-subtasks:

Retargetable subtasks
=====================

.. lsst-task-config-subtasks:: lsst.verify.gen2tasks.MetricTask

.. _lsst.verify.gen2tasks.MetricTask-configs:

Configuration fields
====================

.. lsst-task-config-fields:: lsst.verify.gen2tasks.MetricTask

.. _lsst.verify.gen2tasks.MetricTask-indepth:

In Depth
========

.. _lsst.verify.gen2tasks.MetricTask-indepth-subclassing:

Subclassing
-----------

``MetricTask`` is primarily customized using the `~MetricTask.run` or `~MetricTask.adaptArgsAndRun` methods.
Each subclass must also implement the `~MetricTask.getOutputMetricName` method.

The task config should use `lsst.pipe.base.InputDatasetConfig` to identify input datasets as if it were a `~lsst.pipe.base.PipelineTask`.
Only the ``name`` field is used in a Gen 2 context, but use of `~lsst.pipe.base.InputDatasetConfig` is expected to simplify the transition to Gen 3.

.. _lsst.verify.gen2tasks.MetricTask-indepth-register:

Registration
------------

The most common way to run ``MetricTask`` is as plugins to :lsst-task:`~lsst.verify.gen2tasks.MetricsControllerTask`.
Most ``MetricTask`` classes should use the `register` decorator to assign a plugin name.

Because of implementation limitations, each registered name may appear at most once in `MetricsControllerConfig`.
If you expect to need multiple instances of the same ``MetricTask`` class (typically when the same class can compute multiple metrics), it must have the `registerMultiple` decorator instead.