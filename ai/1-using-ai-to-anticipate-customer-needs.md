# Using Artificial Intelligence to Anticipate Customers' Needs

## Speaker: Tomi Poutanen (Layer 6)

- An image classifier (Dog vs. Cat) with neural networks: 
  - It loosely mirrors how the human brain works.
  - In the human brain, you have cells. Cells are stacked upon each other so you have multiple cells. Every layer adds an extra bit of insight, or abstraction to the data layer.
  - In the ANN, if the connections are correct, and the weights are correct, you'd have the pixels be fed in the model, and if the weights are proper then the DOG neuron will light up.
- Marvin Minski - considered the godfather of AI, however after trying for a long time claimed that neural networks were too opaque, too detailed, no closer to understanding human intellect.
- Geoff Hinton - developed the backproposition algorithm for training weights. Everything you hear about self-driving cars, etc, are based on this algorithm.
  - The basic idea is that if you can express what you're trying to achieve as an continuous function, you can use some calculus to get the integral of it, back-propogate the derivative down multiple layers and tweak those weights a tiny bit to get closer to the desired output.
  - After first, NNs struggled to do anything useful. By 2000, 20% of all US checks were processed by neural nets.
  - In mid 2000's a few things changed:
    1. Processing power finally caught up.
    2. Datasets became large enough to train ANNs in volume.
    3. Other thereotical breakthroughs.
  - In 2012, Geoff and his students submitted a neural-network based approach to the ImageNet challenge, which produced an error rate of 16%, compared to others of 25%.
    - The year after they dropped the error rate down to 11%.
  - Had to re-coin the term "Deep Learning" in lieu of "Neural Network".
  - In subsequent years, Google and Microsoft both adopted Neural Networks and added many layers.
    - Unlike humans, there are no biological limitations.
    - When they are trained, millions of input images are fed in, and you can have these ANNs with thousands of layers.