

1. Perceptrons
* Maps n-dimensional input to a single binary output.
* Function is y = f(w*x + b)
* f is lambda x: x > 0
* w*x is dot product, w is a vector, b a scalar bias
       
* Learning is supervised, i.e shown x, y examples (labelled data)
* w and b are updated iteratively to minimize error

* Unable to learn an XOR or equality function

2. Extension: Multiclass Perceptron
* Train an array of perceptrons
* w is now a matrix, b is a vector

  * For a small output set (e.g. digits 0-9,) use:
   * a 1-hot encoding for the target values
   * f is argmax, i.e. 1 if largest output value, else 0

* This should achieve about 91% on the MNIST dataset.

3. Extension: Multiple Layers of Multiclass Perceptrons
* Have the y values (hidden units) feed into a second perceptron layer
* Train the network using backpropagation (chain rule)
* Important f be a non-linear function, else we are no more powerful than a single layer
* F also needs to be effectively differentiable else chain rule won't help
     
* Possible f could be things like:
  *     x if x > 0 else 0
  *     sigmoid/tanh functions
  *     x + noise > 0

* A two-level network can learn XOR
    
* Deep networks are really slow to learn because the chaining results in vanishing gradients at the earlier levels
  * This seems wrong, like I'm trying to recognize cats vs dogs, and that drives (badly) my learning of vertical lines at the pixel level
      
4. Externsion: Unsupervised Learning
* Have the earlier layers, at least, learn a good representation of the input data without labelling
* Maybe define an two layer auto-encoder: x -> y -> x'
    *    If y is as big as x, it probably won't learn anything more than x == y == x'
	*    If y is smaller, may learn stuff like 8 bit one-hot vector -> 3 bit binary encoding -> 8 bit one-hot output
	*    Specially case of y == x' mapping being basically the transpose of the matrix from x == y is interesting
* Unfortunately, stacking these deep doesn't seem to do much: learning input reconstruction doesn't lead to deep knowledge
* Worse, classical methods do as well or better. See PCA, k-means, etc that can get to high 90s on MNIST
* Alternatives also include Kohonen type networks (essentially k-means to a low-dimensional space) that get 96%+ on MNIST
      
5 So that's the state of the art in the late 1980s
* Not very promising to scale deeply
*  Support Vector Machines started getting better results than ANNs

*  Lots of unsolved issues with rotational and scale invariance
*  Hyperparameter selection (learning rates, layer sizes, etc) was a black art
*  But still a lot of exploration going on with network topologies, relationship to biological neurons, related fields
*  Networks with memory (i.e. input to y is f(w*(x+y_old + b)) were also being looked at
*   But doing thousands of multiplications and sums with finely tuned weights just seems biologically implausible
   
* But, if you have intuition about the above, the recent advances are pretty easy to understand

* Here's a good overview of recent applications and various modern tricks:
https://www.udacity.com/course/deep-learning--ud730

* Here's the stuff on RBMs (Hinton) there's a lot of deep ideas here:
https://www.youtube.com/watch?v=AyzOUbkUf3M

