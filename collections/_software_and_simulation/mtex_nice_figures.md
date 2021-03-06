---
title: Producing nice looking figures
author: Christopher Daniel
tags:
  - MTEX
  - MATLAB
  - EBSD
published: true
subcollection: MTEX
---

# Producing nice looking figures

To produce nice looking figures in MTEX the default settings need to be changed. Unfortunately, this needs to be done each time you download a new version of MTEX. The lines where these changes are located also change each version. The current changes apply to version 5.2.8

## Changes to mtex_settings.m

**Change the fontsize**

The default MTEX fontsize of the pole figures are too small for journal figures. The fontsize is a function of the figure size.

```matlab
fontSize = round(15 * ppi/100);
```

You can either increase this value, or we suggest commenting this line out (% means comment in MATLAB) and then setting the default font size in the line below.

```matlab
fontSize = 35;
```

**Remove the default annotations**

The default annotations in MTEX cover the pole figure data. We can remove these by uncommenting this line.

```matlab
pfAnnotations = @(varargin) [];
```

and then reapplying the annotations.

*Note, this is found in the section.*

```matlab
%% default global plotting options
```

**Change the spacing between plots**

To fit in the new annotations, we need to change the spacing of the pole figures. The value 30 works well to leave room between the individual pole figures. The value 50 is needed to leave enough room at the edge of the plot.

```matlab
setMTEXpref('outerPlotSpacing',50);
setMTEXpref('innerPlotSpacing',30);
```

**Set the defualt colour map**

The defualt colour map for MTEX is rainbow. This is not ideal since it is not perceptually uniform, which causes problems when printing figures in black and white, or for people who are colour blind. A much better option is the viridis colour (called 'parula' in MATLAB), but others are available if you're looking for something different.

```matlab
setMTEXpref('defaultColorMap','parula');
```

*Note, this is found in the section.*

```matlab
%% Default ColorMap
```

## Changes to phi2sections.m

The `phi2sections.m file` is located in `ODFSections` folder, in the `plotting` folder, within the MTEX package.

To remove the labels that cover the ODF contours and change the size of the values and fonts on the ODF slices, lines 110-113 need deleting.

```matlab
% plot data
h = plot(v,data{:},oS.sR,'TR',[int2str(oS.phi2(sec)./degree),'^\circ'],...
  'parent',ax,'projection','plain','xAxisDirection','east',...
  'xlabel','$\varphi_1$','ylabel','$\Phi$','dynamicMarkerSize',...
  'zAxisDirection','intoPlane',varargin{:},'doNotDraw');
```

And the following should be added.

```matlab
% plot data
h = plot(v,data{:},oS.sR,...
  'parent',ax,'projection','plain','xAxisDirection','east',...
  'xlabel','$\varphi_1$','ylabel','$\Phi$','dynamicMarkerSize',...
  'zAxisDirection','intoPlane',varargin{:},'doNotDraw');
set(ax,'FontSize',35,'LineWidth',1); % additional figure settings
```
