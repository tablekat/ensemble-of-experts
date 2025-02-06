Initial prompt to Deep Research:

Help me write a publishable academic paper introducing and formalizing my idea of an extension to Autonomy of Experts and Mixture of Experts architectures, which i'm calling Ensemble of Experts (EoE). Distinguish it from previous research like "Hierarchical Mixture of Experts (HME) model introduced by Jordan and Jacobs" and "Nested Mixture of Experts (NMOE) proposed by Ahn et al. (2021)". Help me determine if its novel and distinct from google's "The Sparsely-Gated Mixture-of-Experts Layer" network. Below is my description of EoE:

EoE would build off of Autonomy of Experts, if you take a single expert as a building block, you would layer them in M x N rows and columns. The output from each expert in the first row would be fully connected to all of the inputs for each expert in the next row, but scaled by a weight which is provided by the activation the experts in the first row themselves give. Only the final row of experts would actually give a standard token embedding output (which, like regular AoE, would be weighted by the final layer's experts' own relevance activation). Effectively you would have N experts in the first row, feeding into N experts in the next row, feeding into N experts in the next row, etc. maybe "deep experts"?

In my suggestion of a nested version of this, you would effectively take the entire M x N network of layered experts, and then layer *that* once more, into a M' x N' "mixture of mixture of experts" or so.

Here's some notes on my motivations:
1. layered neural networks with fully connected neurons, treat an expert as a neuron  
2. relationship to the human brain, think about like an MRI scan where only certain parts of the brain are active at certain times 
3. for the same reasons deepseek used it, for the potential for optimization of network execution (but I would have to think about this more, if a expert self selects to have low weighting, is it possible to simply skip its evaluation completely?)
4. we contain multitudes, maybe that's part of the step towards consciousness
5. consider specialization: you have a reader expert for various languages, you have a physical logic expert or a chemistry expert in the middle, then you have a text output or c++ output or ASCII art output expert at the end 

Please write a document (of academic paper quality) introducing this concept, formalize it, distinguish it from previous literature (or tell me if it's not sufficiently novel), describe my motivations, describe challenges, assess feasibility, and describe a design.
