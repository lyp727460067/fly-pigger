vins
=====================

vins 中的边缘化的一点记录

优化部分
--------------------


主要参考
1:`VINS-MONO边缘化策略接 <https://blog.csdn.net/weixin_41394379/article/details/89975386>`_
2:`OKVIS 笔记：边缘化实现 <https://fzheng.me/2018/03/23/okvis-marginalization/>`_
3:`IMU算姿态:相关代码和论文  <https://x-io.co.uk/open-source-imu-and-ahrs-algorithms/> `_

主要流程大致是:

* 通过边缘化操作之后，最后求解的方程为

.. math::
    :nowrap:

    \begin{equation}
    \label{mathjax-single}
    H\delta x  = b + H\Delta x
    \end{equation}

其中   

.. math::

    \begin{equation}
    H = \mathbf{J}^\mathrm{T} \mathbf{J}
    \end{equation}

然后可化解为一个一般的优化方程

.. math::
    :nowrap:

    \begin{equation}
    H\delta x  = -\mathbf{J}^\mathrm{T} ( \mathbf{J}^\mathrm{-T}b + \mathbf{J}\Delta x )
    \end{equation}

其中GN里面的err相当于

.. math::
    :nowrap:

    \begin{equation}
    \mathbf{J}^\mathrm{-T}b + \mathbf{J}\Delta x 
    \end{equation}

* 这个方程可以用ceres 去优化了  


estunatir主要残差函数
------------------------
* ProjectionTwoFrameOneCamFactor   i时刻和J时刻观测到的路标

* ProjectionTwoFrameTwoCamFactor 左相机I 和 右相机J 观察到的路标

* ProjectionOneFrameTwoCamFactor 左右相机I时刻观察到路标

代码部分
--------

.. code-block:: python
   :linenos:
   :emphasize-lines: 1,4-5
   :caption: A highlighted code-block example
   :name: 一个代码块示例

  