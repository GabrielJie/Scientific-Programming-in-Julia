# [Projects](@id projects)

The goal of the project should be to create something, which is actually useful. Therefore we offer a lot of freedom in how the project will look like with the condition that you should spent around 60 hours on it (this number was derived as follows: each credit is worth 30 hours minus 13 lectures + labs minus 10 homeworks 2 hours each) and you should demonstrate some skills in solving the project. In general, we can distinguish three types of project depending on the beneficiary:
 - **You benefit:** Use / try to solve a well known problem using Julia language,
 - **Our group:** work with your tutors on a topic researched in the AIC group, 
 - **Julia community:** choose an issue in a registered Julia project you like and fix it (documentation issues are possible but the resulting documentation should be very nice.).

The project should be of sufficient complexity that verify your skill of the language (to be agreed individually).

Below, we list some potential projects for inspiration.


## Improving documentation
Improve documentation of one of these projects
- [SymbolicPlanners.jl](https://github.com/JuliaPlanners/SymbolicPlanners.jl)
- [DaggerFlux.jl](https://github.com/FluxML/DaggerFlux.jl) for model-based parallelization of large Neural Networks (see [JuliaCon 2022 for exposition of the package](https://www.youtube.com/watch?v=176c4S6LqT8))
- [FluxDistributed.jl](https://github.com/DhairyaLGandhi/FluxDistributed.jl) for data-based parallelization of large Neural Networks (see [JuliaCon 2022 for exposition of the package](https://www.youtube.com/watch?v=176c4S6LqT8))

## Implementing new things

### The Equation Learner And Its Symbolic Representation

In many scientific and engineering one searches for interpretable (i.e.
human-understandable) models instead of the black-box function approximators
that neural networks provide.
The [*equation learner*](http://proceedings.mlr.press/v80/sahoo18a.html) (EQL)
is one approach that can identify concise equations that describe a given
dataset.

The EQL is essentially a neural network with different unary or binary
activation functions at each indiviual unit. The network weights are
regularized during training to obtain a sparse model which hopefully results in
a model that represents a simple equation.

The goal of this project is to implement the EQL, and if there is enough time
the [*improved equation learner*](https://arxiv.org/abs/2105.06331) (iEQL).
The equation learners should be tested on a few toy problems (possibly inspired
by the tasks in the papers).  Finally, you will implement functionality that
can transform the learned model into a symbolic, human readable, and exectuable
Julia expression.

### Planning algorithms
Extend [SymbolicPlanners.jl](https://github.com/JuliaPlanners/SymbolicPlanners.jl) with the mm-ϵ variant of the bi-directional search [MM: A bidirectional search algorithm that is guaranteed to meet in the middle](https://www.sciencedirect.com/science/article/pii/S0004370217300905). This [pull request](https://github.com/JuliaPlanners/SymbolicPlanners.jl/pull/8) might be very helpful in understanding better the library.

### Logging profiler
In our class, we have implemented a simple version of the profiler recording beggining and end of exection of function calls. This might be very useful for observing behavior of multi-threaded application. A sketch of logging profiler is implemented [here](https://github.com/pevnak/LoggingProfiler.jl). Your goal would to try to finish it into a workable lib or identify boundaries, why it cannot be implemented.

### A Rule Learning Algorithms
[Rule-based models](https://christophm.github.io/interpretable-ml-book/rules.html)
are simple and very interpretable models that have been around for a long time
and are gaining popularity again.
The goal of this project is to implement one of these algorithms
* [sequential covering](https://christophm.github.io/interpretable-ml-book/rules.html#sequential-covering)
algorithm called [`RIPPER`](http://www.cs.utsa.edu/~bylander/cs6243/cohen95ripper.pdf)
and evaluate it on a number of datasets.
* [Learning Certifiably Optimal Rule Lists for Categorical Data](https://arxiv.org/abs/1704.01701)
* [Boolean decision rules via column generation](https://proceedings.neurips.cc/paper/2018/file/743394beff4b1282ba735e5e3723ed74-Paper.pdf)
* [Learning Optimal Decision Trees with SAT](https://proceedings.neurips.cc/paper/2021/file/4e246a381baf2ce038b3b0f82c7d6fb4-Paper.pdf)
* [A SAT-based approach to learn explainable decision sets](www.t-news.cn/Floc2018/FLoC2018-pages/proceedings_paper_441.pdf)
To increase the impact of the project, consider interfacing it with [MLJ.jl](https://alan-turing-institute.github.io/MLJ.jl/dev/)

### Parallel optimization
Implement one of the following algorithms to train neural networks in parallel. Can be implemented in a separate package or consider extending [FluxDistributed.jl](https://github.com/DhairyaLGandhi/FluxDistributed.jl). Do not forget to verify that the method actually works!!!
* [Hogwild!](https://proceedings.neurips.cc/paper/2011/file/218a0aefd1d1a4be65601cc6ddc1520e-Paper.pdf)
* [Local sgd with periodic averaging: Tighter analysis and adaptive synchronization](https://proceedings.neurips.cc/paper/2019/file/c17028c9b6e0c5deaad29665d582284a-Paper.pdf)
* [Distributed optimization for deep learning with gossip exchange](Distributed optimization for deep learning with gossip exchange)

### Improving support for multi-threadding functions in NNLib
[NNlib.jl](https://github.com/FluxML/NNlib.jl) is a workhorse library for deep learning in Julia (it powers Flux.jl). Yet most of their functions are single-threaded. The task is to choose few of them (e.g. `logitcrossentropy` or application of non-linearity) and make them multi-threaded. Ideally, you should make a workable pull request that will be accepted by the community. **Warning: this will require interaction with the Flux community**


# Project requirements
The goal of the semestral project is to create a Julia pkg with **reusable, properly tested and documented** code. We have given you some options of topics, as well as the freedom to choose something that could be useful for your research or other subjects. In general we are looking for something where performance may be crucial such as data processing, optimization or equation solving.

In practice the project should follow roughly this tree structure
```julia
.
├── scripts
│	├── run_example.jl			# one or more examples showing the capabilities of the pkg
│	├── Project.toml 			# YOUR_PROJECT should be added here with develop command with rel path
│	└── Manifest.toml 			# should be committed as it allows to reconstruct the environment exactly
├── src
│	├── YOUR_PROJECT.jl 		# ideally only some top level code such as imports and exports, rest of the code included from other files
│	├── src1.jl 				# source files structured in some logical chunks
│	└── src2.jl
├── test
│	├── runtest.jl              # contains either all the tests or just includes them from other files
│	├── Project.toml  			# lists some additional test dependencies
│	└── Manifest.toml   		# usually not committed to git as it is generated on the fly
├── README.md 					# describes in short what the pkg does and how to install pkg (e.g. some external deps) and run the example
├── Project.toml  				# lists all the pkg dependencies
└── Manifest.toml  				# usually not committed to git as the requirements may be to restrictive
```

The first thing that we will look at is `README.md`, which should warn us if there are some special installation steps, that cannot be handled with Julia's Pkg system. For example if some 3rd party binary dependency with license is required. Secondly we will try to run tests in the `test` folder, which should run and not fail and should cover at least some functionality of the pkg. Thirdly and most importantly we will instantiate environment in `scripts` and test if the example runs correctly. Lastly we will focus on documentation in terms of code readability, docstrings and inline comments. 

Only after all this we may look at the extent of the project and it's difficulty, which may help us in deciding between grades. 

Nice to have things, which are not strictly required but obviously improves the score.
- Ideally the project should be hosted on GitHub, which could have the continuous integration/testing set up.
- Include some benchmark and profiling code in your examples, which can show us how well you have dealt with the question of performance.
- Some parallelization attempts either by multi-processing, multi-threadding, or CUDA. Do not forget to show the improvement.
- Documentation with a webpage using Documenter.jl.

Here are some examples of how the project could look like:

- [ImageInspector](https://github.com/JuliaTeachingCTU/ImageInspector.jl)
