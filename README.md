# ArguMentor

An automated text segmentation and classifier tool for argumentative essays.


## Project Overview

Argumentative writing is an essential skill for academic and professional success. However, a significant portion of underprivileged high school students struggle with proficient writing. One effective way to address this issue is by building and deploying an automated, instant feedback tool capable of evaluating students’ writing and providing personalized feedback. This project aims to implement the foundation of such tool to enhances the quality of automated writing evaluation, making it more accessible to educators and students.

To that end, we built a tool that is capable of segmenting students' essays into argumentative components, and providing a visual breakdown of their essays on demand.

## Implementation Details

We decided to approach the issue as a token classification problem - like NER (Named Entity Recognition) or POS (Part-of-Speech tagging). Then, as this is a fairly developed subset of NLP methods, we leveraged an existing, pre-trained token classification model ([BigBird](https://huggingface.co/google/bigbird-roberta-base)) and fine-tuned it to the task of argumentative component classification for automated essay feedback. 

We preprocessed and restructured our [original dataset](https://www.kaggle.com/competitions/feedback-prize-2021/data) to better fit the training loop needs of our particular fine-tuning [Trainer code](./notebooks/trainer.ipynb). Then, we make extensive use of HuggingFace's token classification, transfer-learning, and transformer training infrastructure to perform our fine-tuning, where we obtained a >90% accuracy in training.

All the code can be found under `notebooks/`. The preprocessing code is located in [`preprocessing.ipynb`](./notebooks/preprocessing.ipynb), the trainer code is located in [`trainer.ipynb`](./notebooks/trainer.ipynb), and the visualization tool's code can be found in [`argumentor.ipynb`](./notebooks/argumentor.ipynb).

With respect to the model, since training took +6 hours on a 3080 Ti, we recommend downloading the model we trained from [Box](https://uofi.box.com/s/r0uerujvsq2z25odnmtga5gcdlrs1pd4), which we've made publicly available. The [`argumentor.ipynb`](./notebooks/argumentor.ipynb), which can be run on Google Colab [here](https://colab.research.google.com/drive/1EHaqudzFlCt7zOUDq-Cw-QbBDpbMF4Hw?usp=sharing#scrollTo=N6rB_r7Wu8g0), downloads and extracts the weights from Box, so the notebook can also be used as a reference on how to use the model for inference.

```Note: For in-depth implementation details, please navigate to each notebook, where all major steps are documented and design choices explained.```

## Usage

1. To open our Interactive ArguMentor Tool, either navigate inside the notebooks folder, find [argumentor.ipynb](notebooks/argumentor.ipynb), and click the "Open in Colab" button, or open it here directly: [Interactive Tool](https://colab.research.google.com/drive/1EHaqudzFlCt7zOUDq-Cw-QbBDpbMF4Hw?usp=sharing)

![image](https://github.com/fzassumpcao/ArguMentor/assets/36646488/ef97d280-428c-44c7-8496-001efc5ef27b)
\
&nbsp;

2. On the top-left, click on Runtime and then Run All. Once all cells are done running, you should see the Interactive Tool if you scroll all the way to the bottom.

![image](https://github.com/fzassumpcao/ArguMentor/assets/36646488/542b697f-f754-4aa5-8ab2-4c711d49c7d6)
\
&nbsp;

3. Paste your text/essay in the essay box and run the cell. The tool will call the trained model to infer on the input text, which will output a list of labels that it will use to appropriately highlight different segments and elements in the text. There is a legend showing what arugmentative element each color represents and the element name will also be displayed when you hover over any segment.
   
![image](https://github.com/fzassumpcao/ArguMentor/assets/36646488/7a95319d-d837-4a70-866d-45360858f576)
\
&nbsp;

## Presentation

[YouTube Link](https://youtu.be/a7W2KMcyKBk)

[Slides Link](https://docs.google.com/presentation/d/1zOMqR2grHXHj_SGosKBUKWW62ps-3E26CLlUTzd1Mcc/edit?usp=sharing)
