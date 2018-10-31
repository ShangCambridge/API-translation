.. cn_api_fluid_layers_array_read

array_read
>>>>>>>>>>>>

paddle.fluid.layers.array_read(array, i)
""""""""""""""""""""""""""""""""""""""""""

此函数用于读取LoD-Tensor类型的数据

::
	
	Given:

	array = [0.6, 0.1, 0.3, 0.1]

	And:

	i = 2

	Then:

	output = 0.3
	

参数：  
		- array (Variable|list)：待读取的输入张量（Tensor）
		- i (Variable|list)：待读取的输入数据索引

返回：	张量（Tensor）类型的变量，储存事前写入的数据

返回类型:	变量（variable）


**代码示例**

..  code-block:: python

	tmp = fluid.layers.zeros(shape=[10], dtype='int32')
	i = fluid.layers.fill_constant(shape=[1], dtype='int64', value=10)
	arr = layers.array_read(tmp, i=i)
