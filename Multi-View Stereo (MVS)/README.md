# <p align=center>`MVS` </p>

### Multi-view Stereo (MVS)

Multi-view Stereo (MVS) is the general term given to a group of techniques that use stereo correspondence as their main cue and use more than two images. **An MVS algorithm is only as good as the quality of the input images and camera parameters.** A generic MVS pipeline is；

- collect images,
- compute camera parameters for each image,
- reconstruct the 3D geometry of the scene from the set of images and corresponding camera parameters,
- optionally reconstruct the materials of the scene.

