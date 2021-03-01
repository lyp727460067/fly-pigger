vins
=====================

vins 中的边缘化的一点记录

优化部分
--------------------


主要参考
1:`VINS-MONO边缘化策略接 <https://blog.csdn.net/weixin_41394379/article/details/89975386>`_
2:`OKVIS 笔记：边缘化实现 <https://fzheng.me/2018/03/23/okvis-marginalization/>`_

* `这个的rst 的格式参考 <(https://self-contained.github.io/reStructuredText/index.html>`_

主要流程大致是 主要求解  方程： 

.. math::
    :nowrap:

    \begin{equation}
    \label{mathjax-single}
    H\delta x  = b + H\Delta x
    \end{equation}

通过舒尔补求出H 

代码部分
--------

.. code-block:: python
   :linenos:
   :emphasize-lines: 1,4-5
   :caption: A highlighted code-block example
   :name: 一个代码块示例

  