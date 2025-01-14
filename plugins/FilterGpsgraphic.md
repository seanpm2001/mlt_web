---
layout: standard
title: Documentation
wrap_title: "Filter: gpsgraphic"
category: plugin
---
* TOC
{:toc}

## Plugin Information

title: GPS Graphic  
media types:
Video  
description: Overlay GPS-related graphics onto the video  
version: 1  
creator: Daniel F  
copyright: Meltytech, LLC  
license: LGPLv2.1  

## Parameters

### resource

title: GPS File/URL    
description:
The fullpath of file containing location (GPS) data. Supported extensions: .gpx, .tcx.  
type: string  
readonly: no  
required: yes  
widget: fileopen  

### time_offset

title: Time offset    
description:
An offset (in seconds) to be added to the video file to match it to the GPS track. Most of the time this will at least need to be set to the timezone difference between the 2 files plus some seconds if the video recording device isn&#39;t precisely set to correct time. GPS time is always exact and in UTC. Use positive values if GPS is ahead of video and negative otherwise.  
type: integer  
readonly: no  
required: no  
default: 0  
widget: text  

### smoothing_value

title: Smoothing level    
description:
How many GPS points to smooth in order to eliminate GPS errors. A value of 1 does not smooth locations, it only calculates the extra fields (speed, distance, etc) it also interpolates missing values for heart rate and altitude.  
type: integer  
readonly: no  
required: no  
minimum: 1  
default: 5  
widget: text  

### speed_multiplier

title: Speed multiplier    
description:
If the video file is a timelapse (or slow motion), use this value to set the speed up/slow down ratio. Sample values: 30 for 30x timelapse, 0.25 for 4x slow motion footage.  
type: float  
readonly: no  
required: no  
default: 1  
widget: text  

### graph_data_source

title: Graph data source    
description:
<pre>
What data from the GPS file is used for drawing:
0 = GPS location/track
1 = altitude (if available)
2 = heart rate (if available)
3 = speed (always available, computed from location)
</pre>
type: integer  
readonly: no  
required: no  
minimum: 0  
maximum: 3  
default: 0  
widget: combo  

### graph_type

title: Graph type    
description:
<pre>
How to draw the selected data:
0 = a basic 2D map line (for location) or 1D graph per time (others)
1 = zooms in onto the map/graph and centers around the current location
2 = draws a speedometer (available for all data sources but recommended only for speed;
for the map type it represents the "percentage done" from trimmed start - end)
Note: for type 1 (follow centered dot):
* crop values are only valid as a percentage and only the bottom (resp left) values
will be taken into consideration as both values (ie: bot/top) will need to be equal to
keep the dot centered)
* if data source is not GPS location, the centering will only be done for horizontal axis
(time), vertical axis crop will behave just like for the type 0 (it will statically keep
the same min/max limit allowing the now_dot to move up and down).
</pre>
type: integer  
readonly: no  
required: no  
minimum: 0  
maximum: 2  
default: 0  
widget: combo  

### trim_start_p

title: Trim start    
description:
Trim data from the start of the gps file (as a percentage of total). Note: both trim_start_p and trim_end_p are computed from the total file so trimming 50% start and 50% end will result in trimming the entire file.  
type: float  
readonly: no  
required: no  
minimum: 0  
maximum: 100  
default: 0  
widget: spinner  

### trim_end_p

title: Trim end    
description:
Trim data from the end of the gps file (as a *reversed* percentage of total, ie: 100 means no trim, 50 means half of total file, 5 means trim 95% of the file). Note: both trim_start_p and trim_end_p are computed from the total file so trimming 50% start and 50% end will result in trimming the entire file.  
type: float  
readonly: no  
required: no  
minimum: 0  
maximum: 100  
default: 100  
widget: spinner  

### crop_mode_h

title: Crop mode horizontal    
description:
<pre>
Decides how to interpret the crop_left_p and crop_right_p values:
0 = a percentage from min..max
1 = an absolute value (ie: it can crop between 22.2 and 22.3 degrees of longitude)
Note: for the horizontal type, absolute values are the longitude (for the location
source type) and time (in miliseconds since epoch) for the rest of the data source types)
</pre>
type: integer  
readonly: no  
required: no  
minimum: 0  
maximum: 1  
default: 0  
widget: combo  

### crop_left_p

title: Crop left    
description:
Crops data from the left side of the graph (effectively zooming in). The value is interpreted either as a percentage of total or an absolute value depending on crop_mode_h. In percentage mode the values are not restricted to 0-100 to allow for &quot;zoom out&quot; behaviour (ie: cropping -50 left will add an extra half of the total horizontal distance). Values over 100 (in % mode) will effectively not display anything. If graph_type is speedometer, all crop left/right values are ignored.  
type: float  
readonly: no  
required: no  
default: 0  
widget: spinner  

### crop_right_p

title: Crop left    
description:
Same as crop_left_p but for the right side and percentage type is interpreted as an inverse percentage (ie: 100 = do not crop anything). Values under 0 will effectively not display anything.  
type: float  
readonly: no  
required: no  
default: 100  
widget: spinner  

### crop_mode_v

title: Crop mode vertical    
description:
<pre>
Decides how to interpret the crop_bot_p and crop_top_p values:
0 = a percentage from min..max
1 = an absolute value (ie: it can zoom in to between 100 and 150m of altitude to show
small changes in altitude between those 2 values better)
Note: for the vertical type, absolute values are latitude degrees (for the location
source type) and altitude, heart rate, speed for the others interpreted as the legend_unit
type where applicable (ie: a value of 10 for altitude will be considered meters by default
but if changing legend_unit to feet it will mean 10 feet).
</pre>
type: integer  
readonly: no  
required: no  
minimum: 0  
maximum: 1  
default: 0  
widget: combo  

### crop_bot_p

title: Crop left    
description:
Crops data from the bottom side of the graph (effectively zooming in). The value is interpreted either as a percentage of total or an absolute value depending on crop_mode_v. In percentage mode the values are not restricted to 0-100 to allow for &quot;zoom out&quot; behaviour (ie: cropping -50 bot will add an extra half of the total vertical distance to the bottom). Values over 100 (in % mode) will effectively not display anything. If graph_type is speedometer, this will set the minimum needle position which will clamp all values that are lower.  
type: float  
readonly: no  
required: no  
default: 0  
widget: spinner  

### crop_top_p

title: Crop left    
description:
Same as crop_bot_p but for the top side and percentage type is interpreted as an inverse percentage (ie: 100 = do not crop anything). Values under 0 will effectively not display anything.  
type: float  
readonly: no  
required: no  
default: 100  
widget: spinner  

### color_style

title: Graph color style    
description:
<pre>
Chooses one of the 9 styles to draw the graph line:
0 = one color -> same color and size for the entire graph
1 = two colors -> same as 2 and 3 but the entire line is the same thickness
2 = solid past, thin future -> from the begining of the graph to the current position (="past")
it will be drawn using the 1st color and chosen thickness, but for the "future" part of the
graph it will use the 2nd color and thickness will be 2px (or 1px if main thickness is below 3)
3 = solid future, thin past
4 = vertical gradient -> the line will be coloured as a vertical gradient relative to the entire
rect area
5 = horizontal gradient
6 = color by duration -> the selected colors will be used as a gradient, in chronological time
(except for location source, this will effectively be a left to right gradient for 1D graphs)
7 = color by altitude -> the selected colors will be used as a gradient from the minimum altitude
value from file to the maximum one, not affected by crops or trim
8 = color by heart rate
9 = color by speed -> same as above but gradient is affected by smoothing
</pre>
type: integer  
readonly: no  
required: no  
minimum: 0  
maximum: 9  
default: 1  
widget: combo  

### color.*

title: Colours    
description:
<pre>
Sets the colours of the graph line.
Multiple colours can be specified with incrementing suffixes to cause the
line to be drawn in a specific way (ie: gradient or past/future).
By default, the filter has 5 colors (blue, green, yellow, orange, red):
color.1 = #ff00aaff
color.2 = #ff00e000
color.3 = #ffffff00
color.4 = #ffff8c00
color.5 = #ffff0000
A color value is a hexadecimal representation of RGB plus alpha channel
as 0xrrggbbaa. Colors can also be the words: white, black, red, green,
or blue. You can also use a HTML-style color values #rrggbb or #aarrggbb.
</pre>
type: color  
readonly: no  
required: no  
animation: yes  
widget: color  

### show_now_dot

title: Show now dot    
description:
Enable it to draw a disc at the current location/time over the graph line. If graph type is speedometer, this affects the needle.  
type: boolean  
readonly: no  
required: no  
default: 0  
widget: checkbox  

### now_dot_color

title: Now dot colour    
description:
Choose the outer circle color of the now_dot disc. The size of this circle is the same as the line thickness. The inside of the disc is always white. If the alpha value of the color is 0 (default) this will use the same colour as the nearby (or past) line (including for gradient types) thus effectively making it change color in time. A color value is a hexadecimal representation of RGB plus alpha channel as 0xrrggbbaa. Colors can also be the words: white, black, red, green, or blue. You can also use a HTML-style color values #rrggbb or #aarrggbb.  
type: color  
readonly: no  
required: no  
animation: yes  
widget: color  

### show_now_text

title: Show now text    
description:
Enable it to draw the current value in big white bold letters on the bottom right side of the rect. The legend_unit value will be appended at the end and it will be used as the current unit (if a valid unit is found ie: kilometers if &quot;km&quot; is found anywhere in the legend_unit string).  
type: boolean  
readonly: no  
required: no  
default: 0  
widget: checkbox  

### angle

title: Rotation    
description:
Rotate the entire graph rect. For speedometer type the text stays horizontal.  
type: float  
readonly: no  
required: no  
default: 0  

### thickness

title: Thickness    
description:
Sets the thickness of the line graph in px.  
type: integer  
readonly: no  
required: no  
minimum: 1  
default: 5  

### show_grid

title: Draw legend    
description:
If enabled it will draw 5 horizontal (and vertical for map type) lines with small values each corresponding to the current data source value at 0%, 25%, 50%, 75% and 100% of current graph shown, affected by the legend_unit type if applicable and with the string appended to the value. For speedometer type this shows division values (but without appending unit).  
type: boolean  
readonly: no  
required: no  
default: 0  
widget: checkbox  

### legend_unit

title: Legend unit    
description:
Sets the unit to be used for displaying values of type altitude and speed. Default is meters and km/h respectively. The unit is matched anywhere in the string so extra spaces can be used to tweak displaying. Supported formats, distance: m|meter, km|kilometer*, mi|mile*, ft|feet, nm|nautical*; speed: ms|m/s|meter, km|km/h|kilometer, mi|mi/h|mile, ft|ft/s|feet, kn|nm/h|knots.  
type: string  
readonly: no  
required: no  
default: m  

### draw_individual_dots

title: Show gots only    
description:
If enabled the graph will be drawn using individual dots instead of lines. This will effectively show the individual data points as affected by smoothing (ie: for location data it will display each GPS fix if smoothing is 1) and can either be used as a cool effect when zoomed in enough or to debug unexpected line jumps.  
type: boolean  
readonly: no  
required: no  
default: 0  
widget: checkbox  

### rect

title: Rectangle    
description:
Defines the rectangle that the graph should be drawn in. Format is: &quot;X Y W H&quot;. X, Y, W, H are assumed to be pixel units unless they have the suffix &#39;%&#39;.  
type: rect  
readonly: no  
required: no  
default: 0 0 100% 100%  

### bg_img_path

title: Background image    
description:
If a valid image file is selected it will be used as a background for the rect area. Paths starting with the &quot;!&quot; character are ignored. TIP: use a map image to add context to the gps track.  
type: string  
readonly: no  
required: no  
widget: fileopen  

### bg_scale_w

title: Background scale    
description:
Scale the background image (relative to center) to match it to the above gps track. Values smaller than 1 zoom into the image, values larger than 1 zoom out. 0 hides it.  
type: float  
readonly: no  
required: no  
minimum: 0  
maximum: 2  
default: 1  

### bg_opacity

title: Background opacity    
description:
Sets the opacity of the background image.  
type: float  
readonly: no  
required: no  
minimum: 0  
maximum: 1  
default: 1  

### gps_start_text

title: GPS start time    
description:
Date and time of the first valid GPS point.  
type:   
readonly: yes  
required: no  

### video_start_text

title: Video start time    
description:
Date and time of the video file.  
type:   
readonly: yes  
required: no  

### auto_gps_offset_start

title: Auto offset start    
description:
Provides a helper offset to guarantee start of video file syncs with the start of gps file. Correctly sets the offset if video file and gps recording was started at the same time.  
type:   
readonly: yes  
required: no  

### auto_gps_offset_now

title: Auto offset now    
description:
Provides a helper offset to sync the first gps point to current video time (it is updated every second). Correctly sets the offset if you video record the moment gps starts.  
type:   
readonly: yes  
required: no  

### map_coords_hint

title: Map hint    
description:
Returns the middle lat, lon coordonates of the gps file.  
type:   
readonly: yes  
required: no  

