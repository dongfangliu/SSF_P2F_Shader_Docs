Debug Tips
=====================
The overall workflow of this plugin can be separated into 3 parts:

* Particles Data Input
* Texture Generating
* Surface Shading

Here are some useful tips for users when using this plugin:

#. On anything regarding Graphics Changes (e.g. Saving/Exiting Scene, Saving Shader...), the `ComputeBuffer` used to generate textures will be discarded.
#. Under all situations, the first step to debug is to check if ``ParticleSource`` was assigned on ``SSF_TextureGenerator``
#. If assigned, toggle On ``checkVisualize`` of ``SSF_TextureGenerator`` and check TextureOutputs.
#. If there's colored output on `EyeSpaceNormalTex`, then problems exist on the surface shading part.
#. If none, it could be two possible reasons during `Texture Generating`:
   
   1. ``ParticleSource`` is not providing data properly.
   2. ``ComputeBuffer`` is lost for some reasons (may due to scene saving and loading).

This first reason may due to users' buggy coding.

To tackle down the second reason, you have to first reactive ``ParticleSource``, then reactive ``SSF_TextureGenerator``.

.. note:: Here, **reactive** means exactly *Disable and then Enable*
