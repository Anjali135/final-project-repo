
# Garbage Classification

## Description
This project trains the resnet-18 network, to create a model that is better suited to classify different images of garbage. The classes are: white-glass, green-glass, brown-glass, battery, biological, cardboard, plastic, paper, trash, metal, shoes, and clothes. Based on the image that is provided, after completing the project, the given image is classified into one of these classes. 

Although this project does not have a huge impact, it is a useful project. It allows the user to upload a picture of an item they are unsure about, and in return they find out what it is classified as, so that they can then properly recycle that item. As global warming, climate change, and harm to the envirnment keep on happening, it is important for us to be aware of how we dispose of our belongings and objects that we use, therefore this can help people find out what and how to get rid of an item such as a can of coke, or even an old pair of shorts.

[example of the visual output when a picture of xyz is sent. ](direct image link here)

## The Algorithm

Model
The way this works, is that first, I chose to use Resnet-18, which is a pretrained model. Resnet-18 is already on downloaded onto the jetson, but it is not made to recognize different garbage categories, which is why it needs to be trained. 

Data and training
The data I used, was found on kaggle, specifically for data classification. I then categorized it myself, combining data from different sets. I had twelve categories: brown-glass, green-glass, white-glass, trash, paper, cardboard, plastic, biological, battery, plastic, clothes, shoes, and metal. I then made three folders: test, train, and validation. In my training set I had about 600 images per category, in the validation around 100, and in the test between 50-100 images. I also had a text file with all the labels, for when I trained the Resnet-18 model. The model was then trained using a pre written python file from the module, in order to train the network to recognize what these different items are. A lot of training had to be done to get correct values.

Once I trained the model, it was able to recognize the different types of garbage it was presented with. I then exported the model in the ONNX format, and saved it to the jetson.

Results
Now that the model was trained, and could classify different garbage images, I had to create a way to output the reuslts. Once the data was set, I wrote a python file to be able to output the data. 

## Running this project
Training:
1. Make sure you have resnet-18 already downloaded onto your jetson.
2. All of the files in the github should be downloaded onto the jetson, including all python scripts that will be used.
3. Change directories into jetson-inference/python/training/classification/data
4. Download the data from the "garbage-data-main" folder, and download that onto the jetson by getting the download link and typing "get" and then the link.
5. unzip the file, by running "unzip", and then the link we just did wget to.
6. Go to the jetson-inference folder and run: ./docker/run.sh
7. Go back to jetson-inference/python/training/classification
8. To train the data, run the following:
    python3 train.py--model-dir=models/garbage_classification data/garbage-data-main
9. Allow the resnet-18 model to train for at least 10 epochs, but the more training that is done, the better.

Exporting the model
10. Make sure the onnx_export.py file is on the jetson, if not do that first.
11. Stay in the jetson-inference/python/training/classification folder
12.  Run: python3 onnx_export.py --model-dir=models/garbage_classification
13. There should be a model named resnet18.onnx in jetson-inference/python/training/classification/models/garbage_classification

Outputting the data:
14. To see the overall accuracy of the trained model, go to the jetson-inference/python/training/classification, and type: python3 train.py -e --model-dir=models/final_project data/garbage-data-main
15. You should be able to see the accuracy from the validation data.
16. In order to get a visual representation of the data, in your home terminal, type: imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/image.jpg name.jpg
17. The image should now be saved on your laptop, with the label of what it is. 

## Results
Below are some images of what the output results look like, there are a few more examples in the "output examples" folder:
[Example of an image of a shoe given, and then the output being the result "shoes".](https://i.imgur.com/QJg6HNQ.jpg)

## Conclusion and next steps
Overall, I think that the project was successful to some extent. I was able to train the resnet18 model, and when I send images through the model, I seem to be getting correct results most of the time. However, there are many errors with this model, as can be seen in the output examples, where one of teh examples shows a picture of a glass bottle but the result says it is classified as plastic. Although this seems like a logcal error, because plastic and glass look similar, after 20 epochs of training it is an expected result. 

The accuracy is also relatively low, for acc@1 it being about 10, and for acc@5 it being around 40. This is not that bad, because with more training and more tweaking of the parameters and different settings, the model can be trained faster and for a longer time. 

The next steps would be to simply train the model for many more cycles, to get the accuracy percentage to be around 80%, and then to explore different ways of icorporating this trained resnet18 model into a proper real life scenario.

Currently, the user can go through the readme file and try this out, and it will help them classifcy different garbage pieces, but more realistically, with more refinement and time given to the project, this could be applied even to an application.

Overall, I think I really enjoyed this process, and although it was very challenging for me to understand how to actually train a model, I am happy with my final outcome, and i hope to further exapnd on this project on the future!

[This is a youtube video link of a demonstration of how my model works on two different examples](video link)
