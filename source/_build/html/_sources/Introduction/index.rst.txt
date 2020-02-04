Introduction
===============
这是个Unity着色器插件而不是流体物理模拟插件，用于将粒子数据渲染成为平滑的液体表面。
它适用于渲染以粒子为模拟单元的仿真系统。

.. note::
    这个插件的原理是基于\ ``Screen Space Rendering With Curvature Flow``\ 这篇论文。

流体仿真一般都是基于网格或者粒子为单元的，考虑实时性通常依旧使用的是基于SPH的方法(一种基于粒子的方法)。

Unity并没有非常合适的流体渲染插件，这是这个插件出现的主要原因。我也注意到确实有一个基于同样原理的实现在Asset Store上。

在使用的过程中，我觉得自己可以做得更好，不管从效率还是视觉效果或者易用性以及扩展性上，因此这个插件诞生了。

.. note::
    这个插件在 `Unity 2019.3.0f5 (64-bit)` 版本上进行开发，支持 `Unity Builtin Shader System` 以及 `Unity URP System` 。在 `Unity Builtin Shader System` 上运行效率更好，并没有针对 `URP` 优化.

.. warning:: 
    ``OnRenderObject`` 需要被支持，在LWRP上应该是跑不起来的。

我准备了数个Demo 场景，以下是它们的简要介绍。

.. image::

.. image::

.. image::

.. image::
