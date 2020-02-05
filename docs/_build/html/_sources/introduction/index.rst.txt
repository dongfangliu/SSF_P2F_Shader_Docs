Introduction
================
This is a Unity shader plugin, not a fluid physics simulation plugin. It is used to render particle data into a smooth liquid surface.
It is suitable for rendering simulation systems that use particles as simulation units.

.. note:: The principle of this plugin is based on the paper ``Screen Space Rendering With Curvature Flow``.

Fluid simulation is generally based on grids or particles. In consideration of real-time performance, the SPH-based method (a particle-based method) is still used.

Unity does not have a very suitable fluid rendering plugin, which is the main reason for this plugin. I also noticed that there is indeed an implementation based on the same principle on the Asset Store.

In the process of using, I feel that I can do better, no matter from the efficiency or visual effects or ease of use and scalability, so this plugin was born.

.. note:: This plugin is developed on `Unity 2019.3.0f5 (64-bit)` version and supports `Unity Builtin Shader System` and `Unity URP System`. It runs more efficiently on the Unity Builtin Shader System and is not optimized for URP.

.. warning:: ``OnRenderObject`` needs to be supported. It cannot run on LWRP.


I prepared several demo scenarios:

.. figure:: ../images//DEMO_File.png
   :align: center
   
   [DEMO] Load particles from file

.. figure:: ../images//DEMO_Blood.png
   :align: center
   
   [DEMO] Blood

.. figure:: ../images//Demo_Single_ParticleSystem.png
   :align: center
   
   [DEMO] Single ParticleSystem

.. figure:: ../images//Demo_Multiple_ParticleSystem.png
   :align: center
   
   [DEMO] Multiple ParticleSystems

.. note ::
   By default, the Gameobject named ``Renderer`` is off on each demo, **enable it** to see the effects. If still not work, **reactive** the `ParticleSource` GameObject and `Renderer` Gameobject.


.. toctree::

   basic_setup.rst
   workflow.rst