# Colonial Collections: discovering changes to the data of a data provider

This is a demonstration of the 'change discovery' functionality of Colonial Collections. A [workflow](.github/workflows/process-changes.yaml) periodically checks whether the data of a data provider has changed, using its [IIIF Change Discovery endpoint](https://iiif.io/api/discovery/1.0/), and stores the current state of its data.

## Steps of the workflow

1. At a specified interval (e.g. once per hour, day or week), the workflow checks whether the data of the data provider has changed since the last time the workflow has run.
1. If so, it processes the changes of the data provider. Notably:
    1. It stores the resources that have been added or changed by the data provider
    1. It removes the resources that have been deleted by the data provider
1. It stores the latest state of the data in the `resources` directory in this Git repository. In addition, it stores the details of the run in the `runs` directory so that the workflow can use these on the next run.
1. It replaces the resources of the data provider in the [RDF store](https://colonial-heritage.triply.cc/data-hub-development/iiif-change-discovery-demo/graphs) of Colonial Collections by removing the resources that were stored in the previous run and by uploading the resources that have been stored in the current run.

## Example: Bodleian Libraries

This demonstration uses the [IIIF Change Discovery endpoint](https://iiif.bodleian.ox.ac.uk/iiif/activity/all-changes) of the [Bodleian Libraries](https://digital.bodleian.ox.ac.uk/). Please note that this data provider nor its data is a part of Colonial Collections - it's only used for demo purposes.
