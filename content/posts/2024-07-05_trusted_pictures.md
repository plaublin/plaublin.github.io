+++
title = "Toward Trusted Pictures to Combat Fake News"
date = "2024-07-05"

[taxonomies]
tags = ["Fake news", "Authenticity", "Provenance", "Images"]
+++

In Images we Trust!

<!-- more -->

# Introduction

Fake news, i.e. the forgery of news information, can have dramatic consequences,
from personal harm and legal issues to societal unrest, health risks, financial
losses, and threats to democratic processes, to the extent that governments are
considering new legislation to combat this threat, e.g.,
[here](https://www.msn.com/en-us/news/technology/over-300-global-experts-urge-governments-to-tackle-deepfake-threats/ar-BB1iFZPY)
or
[there](https://www.weforum.org/agenda/2024/02/ai-deepfakes-legislation-trust/).

Manipulated images are a particular potent medium, where an image is taken
out-of-context, with its original message altered to suit one agenda. Current
state-of-the-art methods rely on image processing techniques, which, as we will
show in this article, are unfortunately not sufficient to detect manipulations.

Fortunately, several actors are working on this problem. We will present two
such solutions: [CAI](https://contentauthenticity.org/) and
[Serelay](https://www.serelay.com/)

Before diving into the details, one might ask why an ISP such as IIJ should
care about these fake news. Internet actors are already filtering attacks over
the network such as spam, viruses, or Denial-of-Service. We believe they also
have some responsibility to stop the dissemination of fake news.

# The problem of detecting manipulated images

There exists a lot of tools to detect fake images:
[fake-inversion](https://fake-inversion.github.io/),
[fotoforensics](https://fotoforensics.com/), [invid
plugin](https://www.invid-project.eu/tools-and-services/invid-verification-plugin/),
[fakeimagedetector](https://www.fakeimagedetector.com/), etc.
They either rely on pixels analysis via machine learning, image processing
techniques, or search for similar images over the Internet to find the origin
of an image.

Unfortunately, these tools are not sufficient, as we show with the following
three images:
![WWF deforestation](https://raw.githubusercontent.com/plaublin/plaublin.github.io/main/static/images/2024-07-05_wwf)
![Kiss-in protest](https://raw.githubusercontent.com/plaublin/plaublin.github.io/main/static/images/2024-07-05_kissin)
![Rhein II](https://raw.githubusercontent.com/plaublin/plaublin.github.io/main/static/images/2024-07-05_rheinII)

The first image originates from a [WWF contest in
2019](https://twitter.com/climateconco/status/1087550447005646849/photo/1). It
shows the extent of deforestation in the Amazon forest by comparing the same
forest over a ten years period. The second image has been presented on some
social medias as an [anti-vaccine protest in Germany in
2021](https://www.dw.com/en/fact-check-no-anti-vaxxer-kiss-in-in-germany/a-60062668).
The third image, named ["Rhein
II"](https://www.theguardian.com/artanddesign/2011/nov/11/andreas-gursky-rhine-ii-photograph),
was taken by Andreas Gursky in 1999. The artist then edited the image to remove
unnecessary details to create this simple and abstract composition.

We ran these images on the
[fakeimagedetector](https://www.fakeimagedetector.com/) tool. This tool uses
[Error Level Analysis
(ELA)](https://en.wikipedia.org/wiki/Error_level_analysis) to detect pixel
manipulations. The results are quite surprising: the first image looks
authentic, while the second and third ones are deemed computer generated or
modified.

Actually, the first image does not show the same spot over a ten years period:
[both sides come from the same
image](https://www.huffpost.com/archive/qc/entry/10yearschallenge-defenseurs-environnement-defi_qc_5cccd7c5e4b089f526c7704c).
While deforestation is a real problem, such forgeries might make more harm than
good and damage the reputation of associations fighting for the climate.

Regarding the second image, it is authentic, but was taken in [Chile in 2011
during some students protest](https://actipedia.org/project/chilean-kiss), not
in Germany in 2021. It is easy to reuse an image for one's own agenda without
having access to additional metadata on the image, such as the time when this
image was taken or GPS coordinates.

The third image is also authentic, but was indeed slightly post-processed by
its author. The point we make in this third example is that the difference
between AI-generated and real images is now very thin, with [people believing
AI-generated images to be
real](https://scitechdaily.com/unmasking-the-illusion-ai-generated-faces-challenge-perceptions/).
Without any authenticity record it would be very easy to deceive someone by
pretending an image is AI-generated or not.

One may think the [Exif
metadata](https://archive.org/details/exif-specs-3.0-dc-008-translation-2023-e/mode/2up)
could help to detect these manipulations by showing detailed information to the
viewer about the situation in which they have been taken (camera model, GPS
location, time and date, etc.). Unfortunately, there are several problems.
First, there are no mandatory fields. Camera manufacturers can decide what
metadata will be (or not) embedded into the file, and users can modify some
settings prior to taking an image. Second, this metadata can be modified or
removed by any editing software. Third, image file formats are not secure: they
do not embed any signature or similar mechanism to prove their authenticity,
keep their integrity against unauthorized modifications, or store confidential
information that could prove the image authenticity (e.g., the GPS location of
an image taken during a conflict).

To summarize, image processing techniques can detect if the pixels of an image
have been manipulated (e.g., part of the image have been modified), but cannot
detect whether an image and its associated message are misleading the viewer,
for example by pretending an image has been taken at a different place or
different time. Part of the problem is the lack of any secure metadata (e.g.,
when and where the image has been taken) in current image formats: it is
relatively easy to remove or alter the Exif metadata.

# Existing solutions

We now present two existing solutions to build trusted images, that is to say
images whose provenance and history can be certified.

## Content Authenticity Initiative

The [Content Authenticity Initiative (CAI)](https://contentauthenticity.org/)
was co-founded by Adobe, The New York Times and Twitter in 2019. Its goal is to
promote an industry standard for provenance metadata. Since its inception, new
actors have joined this initiative, in particular the BBC, ARM, Qualcomm, or
even Nikon.

CAI proposes an end-to-end system that adds secure metadata to an image at
different stages of its creation, when it is taken by the camera and when it is
post-processed (see image below). This secure metadata contains additional
information regarding the provenance of the image: when it was taken, who took
it, who published it, how it was altered, etc.) This additional information is
then secured with hashes and digital signatures. When a user views the image,
he can then check the authenticity and provenance of the metadata, effectively
increasing his trust in the image.

![CAI file structure](https://raw.githubusercontent.com/plaublin/plaublin.github.io/main/static/images/2024-07-05_cai.png)

By embedding secure metadata into the image format instead of storing the
secure metadata in another place (a server or another file), this system is
transparent to users: they do not need to contact a remote server, thus not
needing an Internet connection to check for an image authenticity, and they do
not need to store or exchange another file alongside the image.

One downside of this approach is the need for a secure camera. If the image is
taken by a normal camera, its authenticity cannot be asserted. Fortunately,
smartphones and camera manufacturers are working on new devices compatible with
CAI, e.g.,
[Leica](https://leica-camera.com/en-US/photography/content-credentials#),
[Qualcomm](https://contentauthenticity.org/secure-mode-enabled), or
[Nikon](https://www.nikon.com/company/news/2022/1019_exhibition_01.html).

## Serelay

[Serelay](https://www.serelay.com/) proposes two phone applications to take
secure images and an SDK to verify the authenticity of an image. When taking an
image, Serelay application performs dozens of checks to make sure the photographer is not
trying to spoof the device location or time, by leveraging GPS coordinates,
nearby wifi networks, timezone, as well as analyzing the image to detect for
example whether the user is taking an image of another (two-dimensional)
image instead of a real scene.

The application then extracts and sends hundreds of datapoints from the image
to Serelay servers (which amount to 15kB only according to them). By leveraging
their SDK, other users can then check the image authenticity.
The figure below shows one such example.

![Serelay dashboard](https://raw.githubusercontent.com/plaublin/plaublin.github.io/main/static/images/2024-07-05_serelay.png)

Similarly to CAI, users need to take images with a special camera (in this
case, Serelay smartphones application). However, Serelay does not embed the
secure metadata with the image, but instead relies on its own servers.

# Summary

Existing image processing techniques are not sufficient to detect images
manipulated to alter their message. This is a problem in the fight against fake
news. Fortunately, several solutions are being developed. These solutions aim
at building trust into the image from the moment it is taken by the camera, and
then associate additional, secure metadata to the image to prove its
authenticity.
