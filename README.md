# Colonial Collections: discovering changes to the data of a data provider

This is a demonstration of the change discovery functionality of Colonial Collections. A [workflow](.github/workflows/create-graph.yaml) periodically checks whether the data of a data provider has changed, using its [IIIF Change Discovery endpoint](https://iiif.io/api/discovery/1.0/), and stores the current state of its data.

## Steps of the workflow

1. At a specified interval (e.g. once per hour, day or week), the workflow checks whether the data of the data provider has changed since the last time the workflow has run.
1. If so, it processes the changes of the data provider. Notably:
    1. It stores the resources that have been added or modified by the data provider
    1. It removes the resources that have been deleted by the data provider
1. It stores the latest state of the data in the [resources directory](./bodleian/resources/) in this repository. In addition, it stores the details of the run in a [data file](./bodleian/data/) so that the workflow can use this on the next run.

## Notes about the implementation

1. The workflow stores the resources of the data provider in files on the file system. This is a simple, low-cost, low-resource implementation. However, the workflow can be changed to allow for more advanced options, e.g. by using a triplestore as backend.
1. The workflow stores resources in the N-Triples serialization format, regardless of the format that the data provider uses for providing its data. N-Triples is both readable by humans and easy to process by machines.
1. The workflow uses Git when storing files. The use of a version control system makes it easy to detect changes between runs, e.g. to find out which resources have been added, modified or deleted.
1. The workflow ends when the (current state of the) resources of the data provider have been stored. Consumers will then have to process the resources according to their own requirements, e.g. by selecting the resources that they need (e.g. 'only resources about heritage created between year X and Y') or by mapping the data model of the resources to the data model of their platform.

## Example: Bodleian Libraries

This demonstration uses the [IIIF Change Discovery endpoint](https://iiif.bodleian.ox.ac.uk/iiif/activity/all-changes) of the [Bodleian Libraries](https://digital.bodleian.ox.ac.uk/). Please note that this data provider nor its data is a part of Colonial Collections - it's only used for demo purposes.
