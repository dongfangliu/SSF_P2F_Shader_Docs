SSF_TextureGenerator
========================

**SSF_TextureGenerator** forks ``particleBuffer`` from :doc:`ParticleSource </api/ParticleSource>` 
and then generate Textures for further  :doc:`surface reconstruction and shading </advance_topics/surface_shading>`.

Its working logic can be summarized as follow:

.. code-block:: csharp
   
    void OnEnable()
    {
        print("[SSF] Enabled TextureGenerator "+ gameObject.name);
        setupTextures();
        setupMaterials();
        // Add Surface Mesh and shading if not exists.
        if(GetComponent<SSF_RenderSurface>()==null){
            gameObject.AddComponent<SSF_RenderSurface>();
        }
        GetComponent<SSF_RenderSurface>().enabled = true;
        // Set shading's texsource from this
        GetComponent<SSF_RenderSurface>().tex_source = this;
    }
    void OnDisable()
    {
        print("[SSF] Disabled TextureGenerator "+ gameObject.name);
        releaseTextures();
        releaseBuffers();
        DestroyImmediate(material_depthColorThickness);
        DestroyImmediate(material_noise);
        //Disable Surface Shading
        if(GetComponent<SSF_RenderSurface>()!=null){
        GetComponent<SSF_RenderSurface>().enabled = false;            
        }
    }
    
Then  Draw Textures On Each Frame:

.. code-block:: csharp

    void OnRenderObject()
    {
        if (particleSource != null)
        {
            particleSource.updateParticleBuffer();
            setParams();
            check_debugVisualize();
            drawColorTexture();
            drawDepthTexture();
            drawThicknessTexture();
            smoothDepthTexture();
            drawNoiseTexture();
            drawNormalViewDirTexture();
        }
    }

Param Tuning
--------------------
smoothIterations
    Describes how many smoothing operations each frame, normally 50-120 is suitable
smothed_dt
    Describes the timestep dt for each smothing operation, normally 5e-4 is suitable
estimated_dz_t
    From some sense, it amplifies the smoothing effect of above params, normally 1000
thicknessAmplifier
    Controls `thicknessTexture`'s output magnitude 
basicNoiseTex
    Render each Particle with a basicNoiseTex, generate a `noiseTexture` for fluid shading
noiseAmplifier
    Controls `noiseTexture`'s output magnitude 
textureSize
    Controls the Texture Size of Texture ouput with ``textureSize*textureSize``
debug_visualize
    If toggle on, it will copy ``*Texture_ouput`` to ``*Texture_debug`` for debug purposes.
    This requires two kinds of textures share the same format and dimension.
fluid_surface_meshes
    Array of Plane meshes with different resolutions, corresponding to `surfaceQuality` in  ``SSF_RenderSurface``

