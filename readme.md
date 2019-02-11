Project Overview
The project is the Android version of AiyaSDK, which is a refactoring of the previous version of AiyaEffectsSDK. The initial version after refactoring is 4.0.0.
The project adopts modular design. On the C++ side, it is based on one module and contains authentication and basic interfaces. Other modules depend on the core modules. On the Java side, each functional module is encapsulated so that the Java side can be easily called.
Module description
There are five modules in the current project, and the core functions of each module are implemented in C++:

Aiyaeffectcore: The core module, which is dependent on other modules. The dynamic library libAyCoreSdk.so is dependent on the intermediate layer of the docked JNI. Aiyaeffectcore will compile libAyCoreSdkJni.so, which is dependent on all JNI layers in other modules.
Aiyatrack: face detection and feature point alignment module, relying on the core library. Contains libaftk.so and libsimd.so, compiled to produce libAyTrack.so, which is the JNI layer. In the aiyatrack library, the assets directory contains the config directory. The files in this directory are the necessary model files for face detection and alignment.
Aiyagift: face effects and gift effects library, relying on the core library, can be combined with the aiyatrack library. When not combined, only the gift special effects function is provided, and the combination of the functions for providing gift effects can also provide the face cute function. Contains libassimp.so, libgameplay.so, and libayeffects.so libraries, compiled to produce libAyGift.so, which is the JNI layer.
Shadereffect: A short video effects library that relies on the core library. Contains four libraries: libBaseEffects.so, libAiyaAe3dLib.so, libAiyaEffectLib.so, and libShortVideo.so. After compilation, libAyShaderEffects.so is generated, which is the JNI layer.
Beauty: Beauty library, relying on the core library. Contains libBaseEffects.so, libAiyaEffectLib.so, and libBeauty.so. After compilation, libAyBeauty.so is generated, which is the JNI library. In the beauty module only libBeauty.so prevents the demo compilation conflict from passing, you need to pay attention to this when exporting.
Maven integration
Add in app's build.gradle
    Allprojects {
        Repositories {
            Maven { url "https://dl.bintray.com/aiyaapp/sdk" }
        }
    }
Add a reference
    Compile 'com.aiyaapp.aiya:AyCore:v4.0.0'
    Compile 'com.aiyaapp.aiya:AyEffect:v4.0.0'
    Compile 'com.aiyaapp.aiya:AyBeauty:v4.0.0'
    Compile 'com.aiyaapp.aiya:AyFaceTrack:v4.0.0'
    Compile 'com.aiyaapp.aiya:AyShortVideoEffect:v4.0.0'
    Compile 'com.wuwang.aavt:aavt:a0.2.0'
In addition, aiyagift, shadereffect and beauty libraries rely on the aavt project (com.wuwang.aavt:aavt:a0.2.9, rendering framework) for rendering.

