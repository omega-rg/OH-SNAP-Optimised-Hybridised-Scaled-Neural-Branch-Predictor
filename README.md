# **OH-SNAP**: Optimised Hybridised Scaled Neural Branch Predictor

## Branch Predictors
In computer architecture, branch predictors are a digital circuit component which try to guess the outcome of a branch before it is definitively known. A branch instruction has 2 possible outcomes: taken or not-taken. However, to know the definite outcome of the branch we need some clock cycles. A new instruction can't be fetched into the pipeline during this time as the address of the next instruction is dictated by the branch outcome. Branch predcictors predict the direction of the branch, thus allowing us to fetch instructions without any delays. However, we need to stall the pipeline in case the branch prediction is wrong. Thus an accurate branch predictor is a great boost for performance.

## My Work
I have implemented a branch predictor for the [Chamspsim Simulator Framework](https://github.com/ChampSim/ChampSim). The branch predictor has been written in the C++ language. 

Ideas for the branch predictor have majorly been taken from the following two research papers:
* [SNIP: Scaled Neural Indirect Predictor](https://www.jilp.org/jwac-2/program/cbp3_09_jimenez.pdf)
* [OH-SNAP: Optimized Hybrid Scaled Neural Analog Predictor](http://taco.cse.tamu.edu/pdfs/cbp3_02_jimenez.pdf)

## Usage details

1. Install [Champsim](https://github.com/ChampSim/ChampSim) on your PC. Refer to the instructions in the Champsim repository.
2. Add the `oh_snap.bpred` file to the `branch` folder in the Champsim directory.
3. Simulate the branch predictor according to the instructions provided in the [Champsim](https://github.com/ChampSim/ChampSim) repository

## Salient Features of the branch predictor

### Hybridisation
The predictor is a hybrid of the [SNIP](https://www.jilp.org/jwac-2/program/cbp3_09_jimenez.pdf) and the gshare low-level preedictor. As mentioned in the [Combining
Branch Predictors](https://www.hpl.hp.com/techreports/Compaq-DEC/WRL-TN-36.pdf), this hugely boosts performance

### Ragged Weight Array
Instead of using a single 2-D weight array, I have used multiple weight arrays having different rows based on the weight position. This has been done in accordance with the idea that recent weights have a larger correlation to the branch outcome. Different weight sizes have also been chosen for the different rows.

### Dynamic Weight Scaling
A weight scaling factor which is modified dynamically based on branch outcome is multiplied with the weights before making the prediction

### Adaptive Threshold Training
The threshold parameter which dictates the required confidence level in predcition to avoid training, is also modified dynamically based on ideas presented in [Analysis of the O-GEometric history length branch predictor](https://www.researchgate.net/publication/4144871_Analysis_of_the_O-GEometric_history_length_branch_predictor) research paper.

## Code Explanation
Minimal comments are present in the `oh_snap.cpp` file. For more explanation refer to this [Resources](https://drive.google.com/drive/folders/1Df5mPzWspYolPg2-PgZ45bb9V-5pqh9z?usp=sharing) folder. It contains powerpoint presentations and some other resources which cover every aspect of the code and the underlying ideas in detail.

