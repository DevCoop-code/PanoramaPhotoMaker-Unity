# Developer Guide, Hello World
This guide is intended for unity developers who want to use Stitching Function on Android.

## Using API - C# Code Level
You can easily learn to it from the PanoramaMaker Script File in SampleScene(SampleScene location: Assets/PanoramaMaker/Scenes/SampleScene)

### Creating PanoramaAndroid Instance & Initialization

```
using PanoramaMaker.Android;

// Create PanoramaAndroid Instance
PanoramaAndroid panoramaAndroid = new PanoramaAndroid();

// Initialization
panoramaAndroid.Init();
```

### Set Textures for make panorama picture
Set textures for make panorama picture
```
public Texture2D[] sourceTextures;

......

bool result = panoramaAndroid.SetSourceTextures(sourceTextures);
```
'SetSourceTextures' function returns the bool type variable. if the return value is the true, make panorama picture successfully but if not, fail to make panorama picture

### Get Panorama Texture
After the 'SetSourceTexture' function and the return type is true, you can get panorama picture call 'GetPanoramaTexture'
```
panoramaImg.texture = panoramaAndroid.GetPanoramaTexture();
```

### Release the Textures
After you finish making panorama picture, you must call release
```
panoramaAndroid.Release();
```

### Sample Source Code
```
using System;
using System.Collections;
using System.Collections.Generic;
using System.Runtime.InteropServices;
using UnityEngine;
using UnityEngine.UI;
using System.IO;

using PanoramaMaker.Android;

namespace PanoramaMaker
{
    public class PanoramaMaker : MonoBehaviour
    {
        public Texture2D[] sourceTextures;
        public RawImage panoramaImg;

        public void BuildPanorama()
        {
            if (Application.platform == RuntimePlatform.Android)
            {
                PanoramaAndroid panoramaAndroid = new PanoramaAndroid();
                panoramaAndroid.Init();
                bool result = panoramaAndroid.SetSourceTextures(sourceTextures);

                if (result)
                {
                    panoramaImg.texture = panoramaAndroid.GetPanoramaTexture();

                    // Release
                    panoramaAndroid.Release();
                }
            }
        }
    }
}

```