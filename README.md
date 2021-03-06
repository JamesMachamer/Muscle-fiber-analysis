# Muscle fiber analysis

  This macro will allow you to measure muscle fiber size with dystrophin staining and identify fiber types with staining of myosin heavy chain (MHC) isoforms.  This is accomplished in two parts, the second being dependent on the completion of the first:
  1) Identify muscle fibers based on dystrophin staining, exclude fibers based on measurement thresholding, directly delete erroneously detected fiber, and measure the cross-sectional areas of all detected fibers.
  2) Measure the intensity of staining in each other MHC channel, determine if a fiber is positive or negative for each MHC isoform based on a minimum intensity threshold, and count the number of fibers positive for each MHC isoform and combination of MHC isoform.

Requirements

ImageJ Requirements:  This macro was coded to run on FIJI v 2.0.0-rc-65/1.52i/Java 1.8_066 (64-bit).

Image requirements: This macro requires LSM files containing a dystrophin channel (or any other stain outlining muscle fibers) and MHC channels.  If no myosin channels are present, only the area will be measured. 


Starting analysis

  First, all of the images to be analyzed (in LSM format) need to be in a single folder. To analyze images, run the macro and select this folder when prompted.  Each LSM file will be loaded sequentially and after the analysis is completed the results for each LSM file will be saved in a separate folders with the same name as the LSM files.

Setting Channels

  For each channel in the image file, the staining identitiy has to be set as: “dystrophin”, “myosin 1”, “myosin 2”, “myosin 3”, or ”not analyzed” using the radio buttons..  The dystrophin channel will be used to identify individual fibers and measure cross-sectional area.  The myosin channels will be used identify the MHC isoforms present in each fiber.

Muscle fiber identification

1) A local thresholding algorithm will be applied to create a binary image of dystrophin stain.
2) A neurite tracing algorithm used the binary image to identify single pixel width skeletons of the binary dystrophin thresholding.  
3) Neurite end branches are pruned to eliminate false or incomplete dystrophin staining.
4) Areas completely surrounded by the skeletonized dystrophin staining are selected as muscle fibers.

Fiber area thresholding 

1) Muscle fibers are identified by outline in dystrophin image that have areas above the preset minimum threshold area, below the preset maximum threshold area and above the preset minimum roundnes.
2) The user may adjust the threshold values by sliding the bar or entering in values directly
3) Updating the analysis will generate a new set of fiber outlines reflecting the new threshold values.
4) Value adjustments and updating can be performed until the user is satisfied with the identified fibers
5) The user may proceed to the next step by selecting "finished" from the pull-down menu and pressing ok.

Direct elimination of fibers

1. Individual fibers may be selected by left clicking.
2. Press "Delete" to eliminate the fiber.
3. Make sure that you delete the fiber binary signal and not just the ROI that surrounds it.  
4. Press "OK" when satisfied with the remaining fibers.

Determining fiber MHC identity- processed for each channel identified as a myosin channel

1) The average signal intensity within each muscle fiber outline is measured.
1) Muscle fibers are identified by outline have intensities above the preset minimum threshold value.
2) The user may adjust the threshold values by sliding the bar or entering in values directly
3) Updating the analysis will generate a new set of fiber outlines reflecting the new threshold values.
4) Value adjustments and updating can be performed until the user is satisfied with the identified fibers
5) The user may proceed to the next step by selecting "finished" from the pull-down menu and pressing ok.

Saving the data

Two tables are created.  The first table consists of the ID of each muscle fiber identified, the area, the average intensity for each myosin channel and the identification of each channel as being positive (1) or negative (0).  The second table contains a count of all of the fibers that were positive in each myosin channel and that were positive for the various combinations of myosins.  Additionally the ROIs for the muscle fibers are saved.  
