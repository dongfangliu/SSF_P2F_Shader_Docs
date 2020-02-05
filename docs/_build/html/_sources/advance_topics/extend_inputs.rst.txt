Extend Particle Inputs
========================

Considering that users may have their own source of particle data, such as a particle solution system running in parallel with the GPU, or imported pre-made particle data, here we will explain how to extend the input of particle data.

In ``SSF Particle2Fluid ShaderUtil (SSF)`` ,the input of particles is implemented by the base class ``SSF_ParticleSource`` .

Particle Data Struct
----------------------
The structure of particle data in SSF is as follows:

.. code-block:: csharp

    public struct SSF_particle
    {
        public Vector3 position;
        public Color color;
        public float radius;
    }

.. note:: If you modify the particle's data structure, you need to pay attention to replacing 32 in ``particleBuffer = new ComputeBuffer (getParticleNum (), 32);`` in **SSF_ParticleSource.cs** with the number of bytes of particle data. At the same time, corresponding changes should be made in ``DepthColorThickness.shader`` and ``NoiseShader.shader``.

Explain SSF_ParticleSource
-------------------------------

The input and update of extended data is to create a new class inheriting from ``SSF_ParticleSource`` and implement the corresponding virtual function.

The following two member variables exist in ``SSF_ParticleSource``:

.. code-block:: csharp

        protected ComputeBuffer particleBuffer;// Buffer sent to GPU
        protected SSF_particle[] particlesData;// Particle Data for above buffer

Where ``particleBuffer`` is used to provide data to ``SSF_TextureGenerator`` to generate related textures for rendering.

You can notice that the following member function modifiers in ``SSF_ParticleSource`` are `public virtual`:

* setupParticleBufferData ()
* updateParticleBufferData ()

In ``setupParticleBufferData`` , ``particlesData`` needs to be created and assigned, and updated in ``updateParticleBufferData ()`` , neither of these operations need to involve ``particleBuffer``.

Example
----------
The simplest example is ``SSF_LoadParticlesFromFile.cs``.

.. code-block:: csharp

 public class SSF_LoadParticlesFromFile : SSF_ParticleSource
    {
        public UnityEngine.Object particleFile;
        public float particleRadius;
        public Color particleColor;
        [Range(0,2)]
        public int positionOrder_0=0;
        [Range(0,2)]
        public int positionOrder_1=2;
        [Range(0,2)]
        public int positionOrder_2=1;

        public override void setupParticleBufferData()
        {
            base.setupParticleBufferData();
            if (particleFile != null)
            {
                TextAsset asset = particleFile as TextAsset;
                string[] striparr = asset.text.Split(new string[] { "\r\n", " " }, StringSplitOptions.RemoveEmptyEntries);
                particle_num = striparr.Length / 3;
                print("Loaded particles : " + particle_num);
                particlesData = new SSF_particle[particle_num];
                for (int i = 0; i < particle_num; i++)
                {
                    particlesData[i].position = new Vector3(Convert.ToSingle(striparr[3 * i+positionOrder_0]),
                    Convert.ToSingle(striparr[3 * i + positionOrder_1]), Convert.ToSingle(striparr[3 * i + positionOrder_2]));
                    particlesData[i].radius = particleRadius;
                    particlesData[i].color = particleColor;
                }
            }
        }
        public override void updateParticleBufferData()
        {
            base.updateParticleBufferData();
        }

    }


You can also refer to ``SSF_LoadParticlesFromParticleSystem``, this is a bit complicated and tedious.