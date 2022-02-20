# Project 1 Generative Text

Abraham Schaecher, aschaecher2@huskers.unl.edu

<!-- (Your teammate's contact info, if appropriate) -->

## Abstract

<!-- Include your abstract here. This should be one paragraph clearly describing your concept, method, and results. This should tell us what architecture/approach you used. Also describe your creative goals, and whether you were successful in achieving them. Also could describe future directions. -->

Within the history of exhibitions and galleries, museum labels are a vital piece of information to describe the name of an artist, the description of the artwork, and the inspiration behind certain pieces of creative media. The human thought process to add descriptions to an artwork is relatively based on the collaboration between the artist and perhaps a human "descriptor". I am interested in seeing whether or not a generative network can recreate the human thought process of creating museum labels of artworks. This project will be done by taking existing descriptions from the [Sheldon Museum of Art](https://sheldonartmuseum.org/) as data and creating generated descriptions from the dataset. Results will be evaluated based on descriptions, grammar, puncuation, and examining the comparisons between a original museum label and the generated label.

## Model/Data

<!--Briefly describe the files that are included with your repository:
- trained models
- training data (or link to training data). what is your corpus? -->

For this project, I have decided to use the [GPT-2](https://github.com/openai/gpt-2) text generation model for running this task. I did this becuase the GPT-2 Model allows the use of importing sample data to run results instead of the [GPT-3](https://github.com/openai/gpt-3) and how instead of the RNN model from the ml-art-code, this allows for a more refined model of text generation that is not determined one character at a time.

As for the data itself, I used the museum labels from the Sheldon Museum of Art as a way to gather existing descriptions of artworks as text data. I did so by taking pictures of the text descriptions of the artworks, convert the photos to text, refine the text data, and then add the data to the GPT-2 Model. 

Sample of Text Data of from the Museum: 
- `Edward Hopper's depictions of the everyday lives of city dwellers capture the anonymity and 
isolation of modern urban living. Some of his most compelling pictures, including Room in New York, 
are of figures seen through windows, seemingly unaware of being watched. In many paintings made 
between 1926 and 1932, Hopper included a single figure or couples in compositions that curator 
Judith Barter has described as "[evoking] a hermetically sealed world of emotion."`

Links to Data:
- Museum Description Initial Data as Photos: [Photos of Artwork Descriptions](https://github.com/unl-ml-art/generative-text-eher78/blob/master/Museum_Text.pdf)
- Museum Description Initial Data as Text: [Text of Artwork Descriptions](https://github.com/unl-ml-art/generative-text-eher78/blob/master/Museum_Text.txt)

## Code

<!--Your code for generating your project:
- training_code.py or training_code.ipynb - your training code
- generative_code.py or generative_code.ipynb - your generation code -->
The main code for the project is [gpt2-generate-finetune.ipynb](gpt2-generate-finetune.ipynb).

The oversimplified version of this code is that:
- Import the necessary packages such as the GPT2 Model, tensorflow, etc.
- Connect to a GPU.
- Download the 355M GPT-2 Model.
- Upload the `Museum_Text.txt` as initial textual data.
- Run the finetuning on the GPT-2 with the following parameters:
```
gpt2.finetune(sess,
              dataset=file_name,
              model_name=model_name,
              steps=400,
              restore_from='latest', # change to 'latest' to resume
              run_name='run1',
              print_every=10,
              learning_rate=1e-5,
              sample_every=100,
              save_every=100
              )
```
- Then generate the text with conditional or unconditional prompts. (See results)

## Results

- Documentation of your generative text in an effective form. A file with your generated text (.pdf, .doc, .txt). 

## Technical Notes

Any implementation details or notes we need to repeat your work. 
- Does this code require other pip packages, software, etc?
- Does it run on some other (non-datahub) platform? (CoLab, etc.)

## Reference

References to any papers, techniques, repositories you used:
- Papers
  - [This is a paper](this_is_the_link.pdf)
- Repositories
- Blog posts
