---
layout: standard
title: Documentation
wrap_title: "Filter: avfilter.colorcorrect"
category: plugin
---
* TOC
{:toc}

## Plugin Information

title: colorcorrect  
media types:
Video  
description: Adjust color white balance selectively for blacks and whites.  
version: Lavfi7.110.100  
creator: libavfilter maintainers  

## Parameters

### av.rl

  
description:
set the red shadow spot  
type: float  
readonly: no  
required: no  
minimum: -1  
maximum: 1  
default: 0  

### av.bl

  
description:
set the blue shadow spot  
type: float  
readonly: no  
required: no  
minimum: -1  
maximum: 1  
default: 0  

### av.rh

  
description:
set the red highlight spot  
type: float  
readonly: no  
required: no  
minimum: -1  
maximum: 1  
default: 0  

### av.bh

  
description:
set the blue highlight spot  
type: float  
readonly: no  
required: no  
minimum: -1  
maximum: 1  
default: 0  

### av.saturation

  
description:
set the amount of saturation  
type: float  
readonly: no  
required: no  
minimum: -3  
maximum: 3  
default: 1  

### av.threads

  
description:
Maximum number of threads  
type: integer  
readonly: no  
required: no  
minimum: 0  
default: 0  

### position

  
description:
The MLT position value to set on avfilter frames  
type: string  
readonly: no  
required: no  
default: frame  
values:  

* frame
* filter
* source
* producer
