# Notes for ensemble_of_experts_v1_raw.md:

It hallucinated that it could make diagrams and refers to imagined figures... will need to fix that.

### Under "Introduction"
The introduction focuses on "routing" between laters, but the experts actually don't do any routing themselves. They will be fully connected to the next layer of experts. If there's a "french reading" expert on the first layer, it will route equally (proportional to its own self-selection activation) to all experts on the second layer, whether they're "design a program" experts or "begin analyzing literature" experts.

Another thought is this could be valuable for naturally sequential tasks, e.g. a "design" expert in a layer above a "write" expert in the next layer.

### Under "Related Work"

Relating to HME - It seems that the gating networks are scaled in a binary tree, but the actual leaves (the experts) are O(n). Here I would say regular MoE is also O(n). Effectively, EoE would be O(n^2)/O(mn) on number of experts.

"EoE can be seen as multiple levels of gating and experts" - I don't see EoE as having gating, except in that the experts gate themselves, as an extension of autonomy of experts. Therefore I would say its not true that EoE "could emulate an NMoE (if N=2 layers) or an HME (if structured as a tree)".

### Under "Formalization of the EoE Architecture"

"the pattern of which expert(s) become active in layer $\ell$ influences which experts are considered in layer $\ell+1$." - I don't think this is quite true. The activation of a layer only affects the weights of their own outputs. An expert on layer $\ell$ would determine its own activation, which would be the weight for *its own output*. Its output will be flatly scaled once, and that output will be combined (either linear combination or top-k of the highest activation), and then that one input will be provided to experts on layer $\ell+1$. There could be an additional weight trained for each expert on one row to each expert on the next, but this would be independent of the activation (e.g. french history expert could have strong weighting to a french literature analyzer in the next row, but low weighting to a robot arm controller expert).

"the choice of experts in layer 1 will constrain and inform the choice of experts in layer 2" - This is wrong, each layer will be fully connected to the next. The aformentioned aditional weight trained between layers of experts could be considered a "directed connection" that reduces the space of $\ell+1$ to activate I suppose.

"the experts in the final layer actually output to the external task – earlier layers produce intermediate representations" - Correct, the final layer in a EoE LLM would output an embedded token, but between higher layers the representation would be something different entirely.

Random thought - Train a deep EoE network with an expert that is *repeated* multiple layers in a row and only outputs to itself as a copy. The weights are locked between each version so it must learn to be effectively recursive, expecting input similar to its own output. In the limit of M -> infinity layers we would converge on an expert that could... something like maintain thought. Then, simply run that one expert on loop in inference and feed its output back into its own input, and take outputs into the rest of the network when output is necessary.

"Nested and Ensemble Structures" - This seems mostly like nonsense. Ensemble probably isn't the right name for this whole thing but I liked it.

I think it ignored one of the things I told it to compare against - the google thingy.

### Under "Theoretical Considerations"

Random thought I haven't even read the section yet, the benefits of sparse activation in regular MoE are improved by not only horizontal specialization but vertical specialization, getting even sparser activation.

"at each layer, only the top experts continue. This cascading sparsity means that an input quickly funnels down to a small set of possible paths" - hell yeah
