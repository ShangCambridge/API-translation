
.. _cn_api_fluid_layers_array_read:

array_read
>>>>>>>>>>>>

.. py:class:: paddle.fluid.layers.array_read(array, i)

此函数用于读取LoD-Tensor类型的数据

::

	Given:

	array = [0.6, 0.1, 0.3, 0.1]

	And:

	i = 2

	Then:

	output = 0.3


参数:
	- array (Variable|list)：待读取的输入张量（Tensor）
	- i (Variable|list)：待读取的输入数据索引

返回：	张量（Tensor）类型的变量，储存事前写入的数据

返回类型:	变量（variable）


**代码示例**

..  code-block:: python

	tmp = fluid.layers.zeros(shape=[10], dtype='int32')
	i = fluid.layers.fill_constant(shape=[1], dtype='int64', value=10)
	arr = layers.array_read(tmp, i=i)


.. _cn_api_fluid_layers_Switch:

Switch
>>>>>>>>>>>>>>>>>>>>

.. py:class:: class paddle.fluid.layers.Switch (name=None)

Switch类实现的功能十分类似if-elif-else。它可以在学习率调度器(learning rate scheduler)中调整学习率。

::
 
	语义上，
	1. switch控制流挨个检查cases
	2. 各个case的条件是一个布尔值(boolean)，它是一个标量(scalar)变量
	3. 它将执行第一个匹配的case后面的分支，如果没有匹配的case，但若存在一个default case,则会执行default case后面的语句
	4. 一旦匹配了一个case,它降会执行这个case所对应的分支，且仅此分支。

**代码示例**

..  code-block:: python

	lr = fluid.layers.tensor.create_global_var(
	shape=[1],
	value=0.0,
	dtype='float32',
	persistable=True,
	name="learning_rate")
	one_var = tensor.fill_constant(
	shape=[1], dtype='float32', value=1.0)
	two_var = tensor.fill_constant(
	shape=[1], dtype='float32', value=2.0)

	with fluid.layers.control_flow.Switch() as switch:
	with switch.case(global_step == zero_var):
		fluid.layers.tensor.assign(input=one_var, output=lr)
	with switch.default():
		fluid.layers.tensor.assign(input=two_var, output=lr)

.. py:method:: case(condition)

为该condition（情况，条件）建立新的block（块）。

.. py:method:: default()

为该switch建立default case。
