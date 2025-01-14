---
layout: standard
title: Documentation
wrap_title: "Filter: rescale"
category: plugin
---
* TOC
{:toc}

## Plugin Information

title: Rescale  
media types:
Video  Hidden  
description: Scale the producer video frame size to match the consumer. This filter is designed for use as a normaliser for the loader producer.  
version: 1  
creator: Dan Dennedy <dan@dennedy.org>  
copyright: Meltytech, LLC  
license: LGPLv2.1  

## Notes

If a property &quot;consumer_aspect_ratio&quot; exists on the frame, then rescaler normalises the producer&#39;s aspect ratio and maximises the size of the frame, but may not produce the consumer&#39;s requested dimension. Therefore, this option works best in conjunction with the resize filter. This behavior can be disabled by another service by either removing the property, setting it to zero, or setting frame property &quot;distort&quot; to 1.

## Bugs

* It only implements a nearest neighbour scaling - it is used as the base class for the gtkrescale and swscale filters.

