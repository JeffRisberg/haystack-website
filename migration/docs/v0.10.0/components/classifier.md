# Classifier

The Classifier Node is a transformer based classification model used to create predictions that can be attached to retrieved documents as metadata.
For example, by using a sentiment model, you can label each document as being either positive or negative in sentiment.
Through a tight integration with the HuggingFace model hub, you can easily load any classification model by simply supplying the model name.

![image](/img/classifier.png)

<div className="max-w-xl bg-yellow-light-theme border-l-8 border-yellow-dark-theme px-6 pt-6 pb-4 my-4 rounded-md dark:bg-yellow-900">

Note that the Classifier is different from the Query Classifier.
While the Query Classifier categorizes incoming queries in order to route them to different parts of the pipeline,
the Classifier is used to create classification labels that can be attached to retrieved documents as metadata.

</div>

## Usage

Initialize it as follows:

``` python
from haystack.classifier import FARMClassifier

classifier_model = 'textattack/bert-base-uncased-imdb'
classifier = FARMClassifier(model_name_or_path=classifier_model)
```

It slotted into a pipeline as follows:

``` python
pipeline = Pipeline()
pipeline.add_node(component=retriever, name="Retriever", inputs=["Query"])
pipeline.add_node(component=classifier, name='Classifier', inputs=['Retriever'])
```

It can also be run in isolation:

``` python
documents = classifier.predict(
    query="",
    documents = [doc1, doc2, doc3, ...]
):
```