# Basic Usage

To use TensorFlow you need to understand how TensorFlow:

* Represents computations as graphs.
* Executes graphs in the context of `Sessions`.
* Represents data as tensors.
* Maintains state with `Variables`.
* Uses feeds and fetches to get data into and out of arbitrary operations.

## Overview

TensorFlow is a programming system in which you represent computations as
graphs.  Nodes in the graph are called *ops* (short for operations).  An op
takes zero or more `Tensors`, performs some computation, and produces zero or
more `Tensors`.  A `Tensor` is a typed multi-dimensional array. For example,
you can represent a  mini-batch of images as a 4-D array of floating point
numbers with dimensions `[batch, height, width, channels]`).

A TensorFlow graph is a *description* of computations.  To compute anything,
a graph must be launched in a `Session`.  A `Session` places the graph ops onto
`Devices`, such as CPUs or GPUs, and provides methods to execute them.  These
methods return tensors produced by ops as [numpy](http://www.numpy.org)
`ndarray` objects in Python, and as `tensorflow::Tensor` instances in C and
C++.

## The computation graph

TensorFlow programs are usually structured into a construction phase, that
assembles a graph, and an execution phase that uses a session to execute ops in
the graph.

For example, it is common to create a graph to represent and train a neural
network in the construction phase, and then repeatedly execute a set of
training ops in the graph in the execution phase.

TensorFlow can be used from C, C++, and Python programs.  It is presently much
easier to use the Python library to assemble graphs, as it provides a large set
of helper functions not available in the C and C++ libraries.

The session libraries have equivalent functionalities for the three languages.

### Building the graph

To build a graph start with ops that do not need any input (source ops), such as
`Constant`, and pass their output to other ops that do computation.

The ops constructors in the Python library return objects that stand for the
output of the constructed ops.  You can pass these to other ops constructors to
use as inputs.

The TensorFlow Python library has a *default graph* to which ops constructors
add nodes.  The default graph is sufficient for many applications.  See the
[Graph class](../api_docs/python/framework.md#Graph) documentation for how
to explicitly manage multiple graphs.

```python
import tensorflow as tf

# Create a Constant op that produces a 1x2 matrix.  The op is
# added as a node to the default graph.
#
# The value returned by the constructor represents the output
# of the Constant op.
matrix1 = tf.constant([[3., 3.]])

# Create another Constant that produces a 2x1 matrix.
matrix2 = tf.constant([[2.],[2.]])

# Create a Matmul op that takes 'matrix1' and 'matrix2' as inputs.
# The returned value, 'product', represents the result of the matrix
# multiplication.
product = tf.matmul(matrix1, matrix2)
```

The default graph now has three nodes: two `constant()` ops and one `matmul()`
op. To actually multiply the matrices, and get the result of the multiplication,
you must launch the graph in a session.

## Launching the graph in a Session

Launching follows construction.  To launch a graph, create a `Session` object.
Without arguments the session constructor launches the default graph.

See the [Session class](../api_docs/python/client.md#session-management) for
the complete session API.

```python
# Launch the default graph.
sess = tf.Session()

# To run the matmul op we call the session 'run()' method, passing 'product'
# which represents the output of the matmul op.  This indicates to the call
# that we want to get the output of the matmul op back.
#
# All inputs needed by the op are run automatically by the session.  They
# typically are run in parallel.
#
# The call 'run(product)' thus causes the execution of threes ops in the
# graph: the two constants and matmul.
#
# The output of the op is returned in 'result' as a numpy `ndarray` object.
result = sess.run(product)
print result

# Close the Session when we're done.
sess.close()


# Stdout output ==> [[ 12.]]
```

Sessions should be closed to release resources. You can also enter a `Session`
with a "with" block. The `Session` closes automatically at the end of the
`with` block.



```python
with tf.Session() as sess:
  result = sess.run([product])
  print result
```

The TensorFlow implementation translates the graph definition into executable
operations distributed across available compute resources, such as the CPU or
one of your computer's GPU cards. In general you do not have to specify CPUs
or GPUs explicitly. TensorFlow uses your first GPU, if you have one, for as
many operations as possible.

If you have more than one GPU available on your machine, to use a GPU beyond
the first you must assign ops to it explicitly. Use `with...Device` statements
to specify which CPU or GPU to use for operations:

```python
with tf.Session() as sess:
  with tf.device("/gpu:1"):
    matrix1 = tf.constant([[3., 3.]])
    matrix2 = tf.constant([[2.],[2.]])
    product = tf.matmul(matrix1, matrix2)
    ...
```

Devices are specified with strings.  The currently supported devices are:

*  `"/cpu:0"`: The CPU of your machine.
*  `"/gpu:0"`: The GPU of your machine, if you have one.
*  `"/gpu:1"`: The second GPU of your machine, etc.

See [Using GPUs](../how_tos/using_gpu/index.md) for more information about GPUs
and TensorFlow.

## Tensors

TensorFlow programs use a tensor data structure to represent all data -- only
tensors are passed between operations in the computation graph. You can think
of a TensorFlow tensor as an n-dimensional array or list. A tensor has a
static type a rank, and a shape.  To learn more about how TensorFlow handles
these concepts, see the [Rank, Shape, and Type](../resources/dims_types.md)
reference.


# output:
# [array([ 21.], dtype=float32), array([ 7.], dtype=float32)]





## Variables

Variables maintain state across executions of the graph. The following example
shows a variable serving as a simple counter.  See
[Variables](../how_tos/variables/index.md) for more details.

```python
# Create a Variable, that will be initialized to the scalar value 0.
var = tf.Variable(0, name="counter")

# Create an Op to add one to `var`.

one = tf.constant(1)
new_value = tf.add(state, one)
update = tf.assign(state, new_value)

# Variables must be initialized by running an `init` Op after having

# launched the graph.  We first have to add the `init` Op to the graph.
init_op = tf.initialize_all_variables()

# Launch the graph and run the ops.
with tf.Session() as sess:
    # Run the 'init' op
    sess.run(init_op)
    # Print the initial value of 'var'
    print sess.run(var)
    # Run the op that updates 'var' and print 'var'.
    for _ in range(3):
        sess.run(update)
        print sess.run(var)

# output:

# 0
# 1
# 2
# 3
```

The `assign()` operation in this code is a part of the expression graph just
like the `add()` operation, so it does not actually perform the assignment
until `run()` executes the expression.

You typically represent the parameters of a statistical model as a set of
Variables. For example, you would store the weights for a neural network as a
tensor in a Variable. During training you update this tensor by running a
training graph repeatedly.

## Fetches

To fetch the outputs of operations, execute the graph with a `run()` call on
the `Session` object and pass in the tensors to retrieve. In the previous
example we fetched the single node `var`, but you can also fetch multiple
tensors:

```python
input1 = tf.constant(3.0)
input2 = tf.constant(2.0)
input3 = tf.constant(5.0)
intermed = tf.add(input2, input3)
mul = tf.mul(input1, intermed)

with tf.Session():
  result = sess.run([mul, intermed])
  print result

# output:
# [array([ 21.], dtype=float32), array([ 7.], dtype=float32)]
```

All the ops needed to produce the values of the requested tensors are run once
(not once per requested tensor).

## Feeds

The examples above introduce tensors into the computation graph by storing them
in `Constants` and `Variables`. TensorFlow also provides a feed mechanism for
patching a tensor directly into any operation in the graph.

A feed temporarily replaces the output of an operation with a tensor value.
You supply feed data as an argument to a `run()` call. The feed is only used for
the run call to which it is passed. The most common use case involves
designating specific operations to be "feed" operations by using
tf.placeholder() to create them:

```python

input1 = tf.placeholder(tf.types.float32)
input2 = tf.placeholder(tf.types.float32)
output = tf.mul(input1, input2)

with tf.Session() as sess:
  print sess.run([output], feed_dict={input1:[7.], input2:[2.]})

# output:
# [array([ 14.], dtype=float32)]
```

A `placeholder()` operation generates an error if you do not supply a feed for
it. See the [MNIST fully-connected feed
tutorial](../tutorials/mnist/fully_connected_feed.py) for a larger-scale
example of feeds.

