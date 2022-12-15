---
layout: post
parent: blog.html
title: Pure CSS Material 3 (Part 2)
banner: material.png
categories: programming
---

<!--desc.start-->
I hate JavaScript. It's slow and annoying to use. So I made a pure-CSS implementation of the Material 3 components! That's actually what this website is using.
<!--desc.end-->

# A Variable Start
To start off, we need to gather all of the Material 3 variables. These variables store the colours, font weights, font sizes, etc. for our Material 3 app. I'll walk through all of the steps for finding the variables here, but you can also find their default values in the [GitHub repo for my website](https://github.com/Bright-Shard/bright-shard.github.io). They're in [_sass/variables.scss](https://github.com/Bright-Shard/bright-shard.github.io/blob/main/_sass/variables.scss).

## Colours
You can find all of the default Material 3 colours on the [Material 3 Figma](https://www.figma.com/community/file/1035203688168086460). I just took all of these variables and plugged them into a giant list of variables (cropped here for brevity):

{% highlight css linenos %}
:root {
    /* Surface colours */
    --surface: #1c1b1f;
    --surface-1: #25232a !important;
    --surface-2: #2a2831;
    --surface-3: #302d38;
    --surface-4: #322e3a;
    --surface-5: #35323e;
    --on-surface: #e6e1e5;
    /* Variant colours */
    --surface-variant: #49454f;
    --on-surface-variant: #cac4d0;
    --outline: #938f99;
    --outline-variant: #49454f;
    /* Themed colours */
    --primary: #d0bcff;
    --on-primary: #381e72;
    --primary-container: #4f378b;
    --on-primary-container: #eaddff;
    /* Cropped here, you get the idea */
}
{% endhighlight %}

These colours handle background colours at different elevations, as well as the themed colours for buttons, outlines, etc. You should store all of the colours for your theme (light or dark) - it's a lot of variables, but you'll use all of them. You probably won't need the variables for the other theme, unless you plan on making that toggleable. I stuck with the dark theme colours.

## Fonts
Material 3 recommends the Roboto font, so I used Roboto Flex (Roboto, but it's a flex font). In addition, Material 3 has 5 typing levels - from largest to smallest, they are: Display, Headline, Title, Body, Label. Each typing level is designed for different use cases, and they have different sizes and weights. You can find information about each level, their sizes, and their weights [here](https://m3.material.io/styles/typography/type-scale-tokens). I added the font weights and sizes for each typing level as variables as well:

{% highlight css linenos %}
:root {
    /* Colours above here */

    /* Font sizes */
    --display-large: 57px;
    --display-medium: 45px;
    --display-small: 36px;
    /* Cropped again for brevity */

    /* Font weights (it's all Roboto) */
    --display-font: 475;
    --headline-font: 400;
    --title-font: 500;
    --label-font: 500;
    --body-font: 400;
}
{% endhighlight %}

## State Layer
Something introduced in Material 3 is the idea of a "state layer" - effectively, a coloured layer that lies in between a component's background and content. By default, the state layer is completely invisible; however, when certain events are triggered (hovering, clicking, etc), the state layer gains some opacity. This changes the component's colour a little bit, visually showing the user that they are affecting the component. You can read more [here](https://m3.material.io/foundations/interaction-states), but for my purposes, I just stored the opacity level of the state layer for different events. It looks like this:

{% highlight css linenos %}
:root {
    /* Colours above here */
    /* Fonts above here */

    /* State layer opacities */
    --state-layer-opacity-hover: 8%;
    --state-layer-opacity-focus: 12%;
    --state-layer-opacity-press: 12%;
    --state-layer-opacity-drag: 16%;
}
{% endhighlight %}

And that's it for variables! I also stored the margin size, width of the navigation bar, and default shadow style for my site - but you might not need those for your application.



# Making Components
This post is already quite long, so I'm going to stop here. In Part 2, we'll start making some Material 3 components!
