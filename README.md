# Efficient-Code-Generation-with-E-Code


## How to Use

To use the E_code source code extremely fast: 

Download the Bert-tiny model weights file pytorch_model.bin from huggface and copy it to the Bert_tiny_Opened_expert_group_layer_Weights, Bert_tiny_Weights, Weights_Expert_Group _Integration_Layer in three folders.  Extract the ECG dataset to the E_code folder and change the file name to ECG. Run the train.py file. Implementation Train the model -> predict the generated code -> perform IO test on the generated code.

Set Command_line_parameters.task = 0 to train the E-code model.

Set Command_line_parameters.task = 0
and set Command_line_parameters.RELU = 1 to train a comparison experiment using the RELU activation function.

Set Command_line_parameters.task = 0, and set Command_line_parameters.
and set Command_line_parameters. heads = 8 to train a comparison experiment using 8 heads.

Set Command_line_parameters.task = 1 to train the No-expert-E-code model.
Set Command_line_parameters.task = 2 to train the GPT model.

Extremely fast use of Time_Predictor source code:  Extract the ECG dataset to the E_code folder and change the file name to ECG. Run the train.py file to train the model.
Put the code to be predicted into Code_to_be_predicted and run Prediction_generation_code to automatically predict the code runtime.


Since our experiments have one main model, two comparison experimental models and one runtime predictor. Therefore, we have placed the code for these four models separately.

First, you need to extract the ECG.rar zip file to the current folder.

The detailed code and usage for each of these four models are in the respective folders.

Here are the direct links to [E_code](https://github.com/CodeGeneration2/Efficient-Code-Generation-with-E-Code/tree/main/E_code),  
 [GPT_NEO 125M](https://github.com/CodeGeneration2/Efficient-Code-Generation-with-E-Code/tree/main/GPT_NEO%20125M),  
 [No expert group E-code 350M](https://github.com/CodeGeneration2/Efficient-Code-Generation-with-E-Code/tree/main/No%20expert%20group%20E-code%20350M),  
 and  [Run time predictor](https://github.com/CodeGeneration2/Efficient-Code-Generation-with-E-Code/tree/main/Run%20time%20predictor).


## DataSet
  Since efficient code generation is a new branch that is opened for code generation, we curate [a new dataset of efficient code generation programming problems called ECG](https://github.com/CodeGeneration2/ECG-dataset) for fine-tuning and evaluation. Accordingly, our model is fine-tuned on the ECG dataset. 
  
  The ECG draws on the APPS dataset (Hendrycks et al., 2021) and the CodeContests dataset (Li et al., 2022). We describe the dataset creation process and creative ideas in detail in Readme for DataSet folder.

  Although we developed the ECG dataset to perform efficient code generation, the ECG dataset is an exhaustive dataset that can be applied to different tasks. Therefore, we derived three datasets from this feature of the ECG dataset that can be applied to different specific code processing tasks to fill the gap of other code processing-oriented datasets.
  
Among the ECG datasets our model uses for efficient code generation, we derive three datasets from them: [ECG-CG](https://github.com/CodeGeneration2/ECG-CG-DataSet/tree/main/ECG-CG), [ECG-mini](https://github.com/CodeGeneration2/ECG-mini-DataSet), and [ECG-clone](https://github.com/CodeGeneration2/ECG-clone-DataSet). 
We present each dataset separately in the following.


### [ECG](https://github.com/CodeGeneration2/ECG-dataset)
  [The ECG dataset](https://github.com/CodeGeneration2/ECG-dataset) is divided into train, dev, and test in a ratio of 8:1:1. The train has 3021 folders, dev and test each have 377 folders, each folder corresponds to a problem, and the folders are sorted according to the difficulty of the problem from easy to challenging. We describe in detail what each problem folder covers in Appendix A. And the derived datasets ECG-CG, ECG-mini, and ECG-clone are divided into datasets in the same way as ECG.

The ECG dataset is divided into train, dev, and test in the ratio of 8:1:1. the train has 3021 folders, dev and test each have 377 folders, each folder corresponds to a problem, the folders are sorted according to the difficulty of the problem from easy to challenging, and each problem folder covers the following contents:

1.	acc_soltuions folder. It contains alternative better solution codes, which are grabbed at intervals based on the speed at which the code runs, covering all solution ideas as much as possible. The number of better solution codes is proportional to the number of timeout codes, with an upper limit of 5, sorted by running time from smallest to largest.

2.	acc_tle_soltuions folder. It contains inefficient timeout codes, grabbed by the slowest running time that can complete the problem in the specified time. The number of timeout codes is proportional to the number of better-solved codes, capped at 10, and sorted by runtime from smallest to largest.

3.	accepted.txt. We first select the optimal code with the shortest running time from all solutions to the current problem and again select the code with the smallest running space in the filtered results. It is the perfect solution code that we are trying to find to solve the current problem. This filtering method can optimize the code effectively without falling into the trap of trading space for time.

4.	accepted run time.txt. It contains the accepted code run time and required space information.

5.	tags.txt. It contains the problem tags, i.e., the corresponding classification tags for the problem. The problem tags indicate which methods may be needed to solve the problem (e.g., "greedy" or "recursive"). The last problem tag is a numerical rating of the problem's difficulty, from the most accessible 800 to the most challenging 3500.

6.	URL.txt. It is the file containing the URL of the problem description and solution code. The code generated by the model can be taken to the corresponding website, referring to the evaluation mechanism.

7.	question.txt This is the complete natural language description. The natural language description is divided into five parts: title, the body of the question description, input description, output description, I/O sample test, and note description, separated by two line breaks.

8.	Title.txt. This is one part of the split complete natural language description, that is, the title part.

9.	Problem Description Body.txt. This is one part of the split complete natural language description, which is the central part of the problem description.

10.	Input description.txt. This is one of the parts of the split complete natural language description, that is, the input description part.

11.	Output describing.txt. This is one of the parts of the split complete natural language description, that is, the output describing part.

12.	I/O sample testing and note description.txt. This is one part of the split complete natural language description, i.e., the I/O sample test and note description part.

All of the above files are in txt format. The better alternative solution code in the acc_soltuions folder and the inefficient code in the acc_tle_soltuions folder have similar naming rules: number,runtime,runspace.txt, for example, 0,77 ms,284 KB.txt.


### [ECG–CG](https://github.com/CodeGeneration2/ECG-CG-DataSet/tree/main/ECG-CG)
  Since applications that generate code directly from natural language descriptions are the most promising and relevant code generation datasets are too scarce, we derived [the code generation dataset ECG-CG](https://github.com/CodeGeneration2/ECG-CG-DataSet/tree/main/ECG-CG) from the ECG dataset. The ECG-CG dataset is similar to the APPS dataset (Hendrycks et al., 2021). We tried to extend the use of the ECG-CG dataset by dividing it into four versions based on whether it contains better alternate code and segmented problem text, and we present the specifics of the four versions in Table 1.

![_YAO9ES F)OGB CO2F81MB6](https://user-images.githubusercontent.com/95161813/175928204-82468069-36c2-4272-b4ee-b943756287e7.png)

Table 1: Four versions of ECG-CG dataset partitioning specifics.


### [ECG–mini](https://github.com/CodeGeneration2/ECG-mini-DataSet)
Since our dataset is intended to be exhaustive, many relevant descriptions will likely be annoying for some users who only use the critical data. 
Therefore, [the ECG-mini dataset](https://github.com/CodeGeneration2/ECG-mini-DataSet) is split from the ECG, keeping only the essential data. 
Each amount of data has a problem text, a low-efficiency code, and a high-efficiency code.
  
 
### [ECG–clone](https://github.com/CodeGeneration2/ECG-clone-DataSet)
  Although this paper is not a study of code cloning, many of our datasets have different codes that implement the same functionality. Therefore, we can derive [a semantic clone dataset](https://github.com/CodeGeneration2/ECG-clone-DataSet) from ECG. Each data in ECG-clone has two different implementations of the code.


## Diagrammatic figure
In the Efficient-Code-Generation-with-E-Code work, the diagrammatic figure is in the [Diagrammatic figure folder](https://github.com/CodeGeneration2/Diagrammatic-figure/tree/main/Diagrammatic%20figure).



## Generated code has been predicted
In the Efficient-Code-Generation-with-E-Code work, the authors use a fine-tuned pre-trained model to predict a range of codes to be generated. 
Due to the need for comparative experiments, three code generation models are available. 
The three code generation models are E-code 350M, GPT-Neo 125M, and No expert group E-code 350M. 
We use each of the three fine-tuned code generation models to generate codes. 
Below we have [the code generated by the three fine-tuned code generation models](https://github.com/CodeGeneration2/Generated-code-has-been-predicted/tree/main/Generated-code-has-been-predicted).


### E-code 350M
We give [the results of 3 times code generation in the E-code 350M model](https://github.com/CodeGeneration2/Generated-code-has-been-predicted/tree/main/Generated-code-has-been-predicted/E-code%20350M).


### GPT-Neo 125M
We give [the case results of one code generation for the GPT-Neo 125M model](https://github.com/CodeGeneration2/Generated-code-has-been-predicted/tree/main/Generated-code-has-been-predicted/GPT-Neo%20125M).


### No expert group E-code 350M
We give [the case results of one code generation for the no expert group E-code 350M model](https://github.com/CodeGeneration2/Generated-code-has-been-predicted/tree/main/Generated-code-has-been-predicted/No%20expert%20group%20E-code%20350M).

