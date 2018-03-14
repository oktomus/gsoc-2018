# [Adaptive image plane sampling proposal](appleseed-adaptive-sampling-project.md)

## Contact Informations 

Kevin Masson
- Email:     *[contact.kevinmasson@gmail.com](contact.kevinmasson@gmail.com)*
- Slack:     *oktomus*
- Git:       *oktomus*

## Synopsis

Current implementation of adaptive sampling needs to be overwriten so that it is more efficient, easier to use for any user and more robust regarding animations. Up to now, appleseed's image plane adaptive sampler is based on a per-pixel variance analysis. To work correctly, it requires a large amount of initial samples, which is not convinient. Moreover, each pixel analysis isn't aware of its neighbours and this lead to an image still noisy.

## Benefits

After this project, rendered images would be less noisy compared to the same image renderer with the previous adaptive sampler and the same amount of user provided samples. Using the uniform sampler will not be a necessity anymore to obtain a fireflies-free sequence of image. 

## Deliverables

In the source code of appleseed, I will add and or edit the following:
- `src/appleseed/renderer/kernel/rendering/generic/...`
    - `tilejob.cpp`
    - `adaptivetilerenderer.cpp`
    - `uniformtilerenderer.cpp`
    - `tilerendererbase.cpp`
- `src/appleseed/renderer/kernel/rendering/final/...`
    - `adaptivepixelrenderer.cpp`
 
I will also write a wiki page to explain how it works and on what it was implemented.

## Project Details

See [appleseed-adaptive-sampling-project.md](appleseed-adaptive-sampling-project.md) for the original project description.

### 1. Survey

Adaptive image plane sampling can be done in various ways. We need to find what method can be implemented into appleseed. Up to know, *Dammertz and al.*'s method seems to be efficient and work fine on animations. It computes the variance across a block a pixel instead of doing it on each pixel. On each iteration, it samples and then compute each block's variance. If the block's variance is higher than a terminaison threshold, it will then be splitted in 2. The original block being the whole image.

*Yining Karl Li* propose a modification of this method to make it more efficient. He sets a lower bound on blocks' size to avoid undersampling of some pixels. Also, instead of reducing the number of sample when blocks are getting closer to the threshold, it simply keep the same amount of path and reallocate them to high-variance pixels. This reduce noise and fireflies in the final image.

### 2. Implementation / Refactoring

### 3. Tests / Optimization

- Test if the rendered images are correct
- Observe how pixels are sampled
- Reduce memory use if possible
- Port the implementation on multiple threads if originally implemented on a unique thread

## Project Schedule

I will have vacations from May 25 to August 31, which leaves a bit more time than planned. I will be able to work completly on this project during this period. I will also be available before May 25 because most of my units would have been finished by then. Here is an estimation of the project schedule:

#### Until May 14: Community Bonding

- Actively contribute
- Get familiar with appleseed's render pipeline
- Get familiar with blenderseed

#### Week of May 14

- List all methods that can be implemented directly into appleseed and the one that requires a fair amount of refactoring
- Compare methods between each other
- End of the week, along with maintainers: **Decide which solution will be implemented**

#### Week of May 21

- Get familiar with the choosen method 
- Schematize the algorithm
- Produce diagrams of what the final code structure would be
- Propose an interface for configuring the sampler
- Discuss of the structure with maintainers

#### Week of May 28

- Naive implementation of the algorithm
- Refactor appleseed if needed to fit the new sampler
- Create some test scenes
- Use diagnostic AOVs to observe the results

#### Week of June 4

- Continuing previous week tasks

#### Week of June 11: End of phase 1

- Evaluation of the Phase 1
- Preparation for Phase 2
- Work on the final report

#### Week of June 18

- Test the naive implementation
- Fix issues (there will be some :smile:)
- Improve previously create diagrams if needed
- Test the algorithm on animations

#### Week of June 25

- Optimize the algorithm
- Optimize memory managment

#### Week of July 2

- Better integration of the sampler inside source code
- Add the new sampler in appleseed.studio

#### Week of July 9: End of phase 2

- Evaluation of Pahse 2
- Preparation for Phase 3
- Work on the final report

#### Week of July 16

- Continuing last week work
- Test again with the same scenes as before

#### Week of July 23

- Compare results with the original adaptive sampler
- Benchmarking

#### Week of July 30

- Remove the original adaptive sampler
- Final fixes, tests and documentations

#### Week of August 6

- Final Evaluation
- Final report modifications

## Bio

I am 21 year old, studying *Compute Science and Image Science* at the University of Strasbourg, France, currently in first year of a Master's Degree. Computer graphics and especially rendering passionates me, I am doing my best for being ready to enter the industry. I have experience with NPR and real-time rendering, and I am learning about physically based renderers. I have professional experience with Python which I acquired by working in 2 different animation studios (one in Luxembourg named *La Fabrique d'Images* and one in Paris named *Ellipsanime*). Developping tools for artists was my principal task. Thanks to school and personnal projects, I have advanced knowledge of C++ and C. Also, I am starting to get confortable with Scientific Papers as I am using them to implement school projects.

## References

- [A Hierarchical Automatic Stopping Condition for Monte Carlo Global Illumination](https://jo.dreggn.org/home/2009_stopping.pdf)

## Links

- [Adaptive Sampling by Yining Karl Li](https://blog.yiningkarlli.com/2015/03/adaptive-sampling.html)
- [Final Project Report by Benedikt Bitterli](http://noobody.org/is-report/medium.html)
