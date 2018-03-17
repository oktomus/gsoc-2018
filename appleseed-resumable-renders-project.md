# [appleseed](https://github.com/appleseedhq/appleseed): Resumable renders

* **Required skills**: C++
* **Challenges**: None in particular
* **Primary mentor**: Franz
* **Secondary mentor**: Esteban

Rendering a single image can take a very long time, depending on image resolution, scene complexity and desired level of quality.

It would be convenient to allow stopping a render and restarting it later. This would, for instance, enable the following typical workflow:

1. Render for a few seconds, or a few minutes, then interrupt the render.
2. Work with the low quality render as if it was high quality: apply tone mapping or other forms of post-processing, preview the entire animation, etc.
3. When time allows, resume rendering where it left off to get a smoother result.

Tasks:

1. Determine what needs to be persisted to disk to allow resuming an interrupted render.
2. Define a portable file format for interrupted renders. Can we reuse an existing format? For instance, could we store resume information as metadata in an [OpenEXR](http://www.openexr.com/) (*.exr) file?
3. When rendering is stopped, write an "interrupted render file".
4. Allow appleseed.cli (the command line client) to start rendering from a given "interrupted render file".

Possible follow-ups:

1. Expose the feature in appleseed.studio.
2. List and present all available interrupted renders when opening a project.
3. Identify when a render cannot be resumed, e.g., because the scene has changed in the meantime.
