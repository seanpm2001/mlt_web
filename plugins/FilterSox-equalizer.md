---
layout: standard
title: Documentation
wrap_title: "Filter: equalizer"
category: plugin
---
{::options auto_ids="true" /}
{:toc}

## Plugin Information

title: equalizer  
media types:
Audio  
description: Process audio using a SoX effect.  
version: 1  
creator: Dan Dennedy  
copyright: Meltytech, LLC  
license: LGPL  
URL: [http://sox.sourceforge.net/](http://sox.sourceforge.net/)  

## Bugs

* Some effects are stereo only, but MLT processes each channel separately.
* Some effects have a temporal side-effect that do not work well.

## Parameters

### argument

title: Options    
type: string  
readonly: no  
required: no  
format: frequency width[q|o|h|k] gain  
