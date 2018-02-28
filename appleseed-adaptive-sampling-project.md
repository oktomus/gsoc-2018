# [appleseed](https://github.com/appleseedhq/appleseed): Adaptive image plane sampling

* **Required skills**: C++, reading and understanding scientific papers
* **Challenges**: None in particular
* **Primary mentor**: Franz
* **Secondary mentor**: Esteban

![Illustration by Yining Karl Li](http://blog.yiningkarlli.com/content/images/2015/Mar/adaptive_globe_baseline_vcm.png)
(Illustration from [Adaptive Sampling](http://blog.yiningkarlli.com/2015/03/adaptive-sampling.html) by Yining Karl Li.)

Like most renderers, appleseed has two types of "image plane sampler", i.e., it has two ways of allocating samples (which is the basic unit of work) to pixels:

- The *uniform* sampler allocates a fixed, equal number of samples to every pixel. This is simple and works well, but a lot of resources are wasted in "easy" areas that don't require many samples to get a smooth result, while "difficult" area remain noisy.
- The *adaptive* sampler tries to allocate more samples to difficult pixels and fewer samples to easy pixels. While it may work acceptably with a bit of patience, it's hard to adjust, and it can lead to flickering in animations.

The idea of this project is to replace the existing adaptive sampler by a new one based on a more rigorous theory. We settled for now on a technique described in [Adaptive Sampling](http://blog.yiningkarlli.com/2015/03/adaptive-sampling.html) by Yining Karl Li. However, the project should start with a quick survey of available techniques.

Tasks:

1. Survey available modern techniques to adaptively sample the image plane.
2. Implement the chosen adaptive sampling algorithm.
3. Make sure the new adaptive sampler works well in animation (absence of objectionable flickering).
4. Determine which settings should be used as default.
5. Expose adaptive sampler settings in appleseed.studio.
6. Compare quality and render times with the uniform image sampler.
7. Remove the old sampler, and add an automatic project migration step to maintain backward compatibility.

