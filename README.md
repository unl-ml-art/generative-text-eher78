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
              steps=200,
              restore_from='fresh', # change to 'latest' to resume
              run_name='run1',
              print_every=10,
              learning_rate=1e-5,
              sample_every=100,
              save_every=200
              )
```
- Then generate the text with conditional or unconditional prompts. (See results)

## Results

<!-- - Documentation of your generative text in an effective form. A file with your generated text (.pdf, .doc, .txt). -->
The text generation results has produced a total of 4 sections from two categories: unconditional or conditional (with prompts) generation.

Here are a section of the sample results from each of the sections. Before moving on, it should be noted that the following parameters are the same for each section:
- Steps = 200
- Learning Rate = 1e-5

#### Conditional Generation, Prefix "Machine"
```
In these muted, charcoal paintings made from fibreglass and iron, Houdini
engaged the subconscious mind of the viewer, evoking both his psychological
and physical states. As the viewer focuses on a particular color, the fibrous
form shifts dramatically—from a solid block wall into a soft, muted waft;
from a dark room into a warm one.
```

#### Conditional Generation, Prefix "Abstract"
```
The photos were taken of a cat in a cage, and one of the photos is shown below. 
It's lit from below up to reveal a close-up of the cat's eyes—brightly pigmented and infused with violet. 
The other photos, however, are from a higher perch, and reveal the cat from below down.
```

#### Conditional Generation, Prefix "Untitled"
```
This photograph, by Italian artist Giulietta Bensi, provides a rare 
view of an eye. the artist is wearing a complete face view camera, allowing 
agnostic reading of a picture to the naked eye. out of focus details such as 
the tinge of brown around the irises and the thick black of the iris allow us to see 
closely the thought processes involved in the drawing.
```

#### Unconditional Generation
```
In many of his earliest studies, Hinton relied upon cadaveries as a basic repository for 
body parts such as feet and hands, which he used to make paintings. For 2002's I Live in Drowns, 
he visited six cemeteries in the Shenandoah Valley in Maryland to display hundreds of handmade pieces of his artwork: 
cotton embroidered hoodeds, brocaded vestments, embroidered gloves, and block print button-down shirts.all
brooded on the commodification of corpses and the deaths they exert in the diaspora.
```

## Evaluating the Results
The generated results should fit within the theme of museum artwork descriptions to ensure the text is relevant to a piece of art and the creative process behind the work. As such, I decided the best way to evaluate the results is to implement a classification score to each block of text and get the average accuracy from each section.

Scoring Guidelines:
- 1.0 = Description of Generated Text that looks like it is from a museum
` ex: In the 1950s, after 
spending two decades teaching himself to paint, he executed a number of major works, including this 
one, and was beginning to make a name for himself. `

- 0.5 = Quote from Artist
`ex: "But really, my interest in painting lies in the fact of the painting. And I think that's why 
sometimes people find the big paintings uncomfortable."`

- 0.0 = Indecipherable Text or Irrelevant to Topic of Museum Descriptions
`ex: Her grave lacks the pomp and circumstance of our past honors.`

The basic template for evalutating the scores is:
<img src="https://latex.codecogs.com/svg.latex?\Large&space;x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" title="\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" />


#### Conditional Generation, Prefix "Machine"


#### Conditional Generation, Prefix "Abstract"


#### Conditional Generation, Prefix "Untitled"


#### Unconditional Generation

## Conclusions

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
