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
and go to  [bh ](http://127.0.0.1:8000/ )
It open the doccano app . Follow the below steps for annotation
1)go to labels from the right side bar and add the label e.g skill,course
2)go to the dataset option from right side panel , action - import dataset -ingest - annotate
3)after annotating the text , go to dataset again and action-export-jsonl
4)it download the zip file having annotated data.

# Google Colab Steps
1) import json
import spacy

2)unzip the annoteted zip file
3)convert this data into spacy format by running the following function
import json

def convert_doccano_to_spacy(filepath):
  with open(filepath, 'rb') as fp:
    data = fp.readlines()
    training_data = []
    for record in data:
      entities = []
      read_record = json.loads(record)
      text = read_record['data']
      entities_record = read_record['label']
      for start, end, label in entities_record:
        entities.append((start, end, label))
        training_data.append((text, {"entities": entities}))
    return training_data
    
  4)data = convert_doccano_to_spacy('/content/ner-spacy-doccano/admin.jsonl')
  
  5) prepare an empty model to train
nlp = spacy.blank('en')
nlp.vocab.vectors.name = 'demo'
ner = nlp.create_pipe('ner')
nlp.add_pipe(ner, last = True)

if you want to train on pretained model then simply replace 'blank' with 'load'

6)class_list = ['person_name','city','course','skills'] #list of classes

  for label in class_list:
    nlp.entity.add_label(label)

7)# Train the model
optimizer = nlp.begin_training()

8)for i in range(170):  
  for text, annotations in data:  
      # print(text,annotations)  
      if len(text) > 0:  
          nlp.update([text], [annotations], sgd=optimizer)
          
          
9)text = '' #write text for testing

10)test the model     
doc = nlp(text)
for ent in doc.ents:
    print(ent.text,ent.label_)



