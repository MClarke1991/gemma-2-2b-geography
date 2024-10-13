# Detecting Confident vs. Guessed Answers in Gemma-2-2b Using SAE Features: A Case Study with Geographic Distance Estimation

## **Instructions**

To recreate the experiments and figures, please run the notebooks in the root folder in order of their number, starting with 1_generate_location_ground_truth.ipynb

This project relies on the basic version of the US Cities database from https://simplemaps.com/data/us-cities, distributed under Creative Commons Attribution 4.0. 

## **Summary**

* To investigate how SAE features might be used to detect if a model knows, is extrapolating, or is guessing an answer to a factual question, I compared Gemma-2-2b estimations of the distances between cities to real world data.

* I expected that the ability to recall memorised distances, or extrapolate them from memorised pairs, would be related to e.g. population of the cities, or that errors would compound with distance.

* Instead, the predominant pattern was that answers would fall into groups with differing precision e.g. many answers would be simply '1000 miles' while others would be very precise e.g. '2,341.28 miles', but with no clear pattern relating to city size or location.

* This may be because the prompt was not eliciting a precise answer, or the model guessing when the pairwise distance was not memorised, or a mixture of the two.

* I find that these groups, which I term 'Guess' and 'Confident', can be detected by activation of features extracted by SAE trained on the residual stream, measured from the Gemma-Scope data set, when looking at activations on the final token at layer 21. 

* Features that clearly differ in activation, and are important in classification of 'Guess' and 'Confident', seem to fire on plain and scientific English respectively.

* This seems like a promising avenue of study for the ability to test for the confidence of an LLM in its answers, with applications to better detection of bad outputs in cases where LLM are being used for tasks where factual accuracy is key.
