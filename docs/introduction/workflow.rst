Step By Step Usage
=========================

Setup Scene
-------------

#. Create an empty Scene named ``SSF_Test``
#. Create a `ParticleSystem` and deactivate its ``Renderer`` function
#. Create an empty `Object` named ``Renderer``

The Inspector should looks like:
     .. image:: ../images/workflow_-1.PNG
        :scale: 50% 

Add ``SSF_LoadParticlesFromParticleSystem``.
   The Inspector should appears as follows:
   
   .. image:: ../images/workflow_0.PNG
      :scale: 50% 

#. Assign shader and the ParticleSystem just as follows:
   
   .. image:: ../images/workflow_1.PNG
     :scale: 50% 
#. Disable and then enable the Component to take effect.
#. Now Toggle on ``Visualize``, black spheres can be viewed in the `Scene` Window and `Game` Window.

.. note:: ``Visualize`` works only for debug purpose, it will not affect the proper workflow functionality.
  
Cofigure Renderer
---------------------
#. Move on to the `Inspector` of the ``Renderer`` in hierachy
#. Click Add Component, Add ``SSF_TextureGenerator``. This should be many missing values in the inpsector.
   Assign as follows:

   .. image:: ../images/workflow_2.PNG
     :scale: 50% 

#. Disable and then enable the Component to take effect.
   Component of type ``SSF_RenderSurface`` should be automatically added.

The meaning and effect of parameters can be checked in :doc:`../api/index` 

Congratulations!
------------------
From `Scene` View, fluid-like shape can already be viewed .

.. image:: ../images/workflow_3.PNG

It's not cool enough, right?

Check Other Cool Demos
------------------------
Now it's time too check other cool demos!