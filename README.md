# Custome-NER-SPACY-DECCONO

The Following are the steps for train the ner on our own dataset .

1. Annotate the dataset
2. Train model
3. Test



# ANNOTATION 
for annotation we are using DECCODO .
Doccano is an open source application designed to make the text annotation or text labeling process much quicker and easier for data scientists. It allows you to load up a dataset and then categorise or label it using a user-friendly web interface, and then output the results in a format that can be used in a range of NLP modeling platforms, such as Spacy.

Doccano can be used for a range of text annotation, text classification and labeling tasks for Natural Language Processing projects. These include sequence labeling for Named Entity Recognition (NER), part-of-speech (POS) tagging, and semantic role labeling; Sequence to Sequence tasks, such as string translation; Document Classification, for things like sentiment analysis, and even speech to text audio classification.

#To install doccano, simply run:
```
pip install doccano
```
After installation, run the following commands:

#Initialize database.
```
doccano init
```
#Create a super user.
```
doccano createuser --username admin --password pass
```
#Start a web server.
```
doccano webserver --port 8000
```
In another terminal, run the following command:
```
doccano task
```
and go to  [http://127.0.0.1:8000/](http://127.0.0.1:8000/ )
It open the doccano app . Follow the below steps for annotation
1)go to labels from the right side bar and add the label e.g skill,course
2)go to the dataset option from right side panel , action - import dataset -ingest - annotate
3)after annotating the text , go to dataset again and action-export-jsonl
4)it download the zip file having annotated data.

