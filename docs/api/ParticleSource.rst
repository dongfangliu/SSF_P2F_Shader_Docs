SSF_ParticleSource
====================
This class has been explained clearly in :doc:`/advance_topics/extend_inputs` 

This class provides data to ``SSF_TextureGenerator`` for generating textures.

.. note:: 
    ``SSF_TextureGenerator`` uses the transform of ``SSF_ParticleSource`` as **the model matrix** for particles, please ensure it's your expected model matrix. 

.. note:: Thus, if using multiple particleSystem, 
    the ``simulationSpace`` should be setted to ``World`` and
    this script should be attached to a gameObject with Identity transform.
    