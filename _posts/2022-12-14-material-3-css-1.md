---
layout: post
parent: blog.html
title: Pure SCSS Material 3
image: /assets/blog-banners/material.png
category: tutorials
---
<!--desc.start-->
I love Material 3, but it's web implementation is in JavaScript - a slow and
bloated language, and one that isn't even needed for most UI components. So I
made my own Material 3 implementation - in pure SCSS.
<!--desc.end-->

# A Variable Start

To start off, we need to gather all of the Material 3 variables. These variables
store the colours, font weights, font sizes, etc. for our Material 3 app. I'll
walk through all of the steps for finding the variables here, but you can also
find their default values in the
[GitHub repo for my website](https://github.com/Bright-Shard/bright-shard.github.io).
They're in [_sass/variables.scss](https://github.com/Bright-Shard/bright-shard.github.io/blob/main/_sass/variables.scss).

## Colours

You can find all of the default Material 3 colours on the
[Material 3 Figma](https://www.figma.com/community/file/1035203688168086460).
I took everything from it and plugged them into a giant list of
variables (cropped here for brevity):

{% highlight scss linenos %}
// Surface colours
$surface: #1c1b1f;
$surface-1: #25232a;
// ...and all the other surfaces

// Variant colours
$surface-variant: #49454f;
$on-surface-variant: #cac4d0;
$outline: #938f99;
$outline-variant: #49454f;

// Themed colours
$primary: #d0bcff;
$on-primary: #381e72;
$primary-container: #4f378b;
$on-primary-container: #eaddff;

// Cropped here... you get the idea
{% endhighlight %}

These colours handle background colours at different elevations, as well as the
themed colours for buttons, outlines, etc. You should store all of the colours
for your theme (light or dark) - it's a lot of variables, but you'll use all of
them. You probably won't need the variables for both light and dark mode, unless
you plan on making that toggleable. I only used the dark theme colours.

## Fonts

Material 3 recommends the Roboto font, so I used Roboto Flex
(Roboto, but it's a flex font). In addition, Material 3 has 5 typing levels,
each with different font sizes and weights. From largest to smallest, they are:
Display, Headline, Title, Body, Label. Each typing level is designed for
different use cases; you can read more about that
[here](https://m3.material.io/styles/typography/type-scale-tokens). I added the
font weights and sizes for each typing level as variables as well:

{% highlight scss linenos %}
// Font sizes
$display-large: 57px;
$display-medium: 45px;
$display-small: 36px;
// Cropped again for brevity

// Font weights (it's all Roboto, so the font itself won't change)
$display-font: 475;
$headline-font: 400;
$title-font: 500;
$label-font: 500;
$body-font: 400;
{% endhighlight %}

## State Layer

Something introduced in Material 3 is the idea of a "state layer", a translucent,
coloured layer that lies in between a component's background and content. By
default, the state layer is completely transparent; however, when certain events
are triggered (hovering, clicking, etc), the state layer gains some opacity.
This changes the component's colour just enough to show the user that they are
interacting with the component. You can read more
[here](https://m3.material.io/foundations/interaction-states). I stored the
opacity level of the state layer for different events. It looks like this:

{% highlight scss linenos %}
// State layer opacities
$state-layer-opacity-hover: 8%;
$state-layer-opacity-focus: 12%;
$state-layer-opacity-press: 12%;
$state-layer-opacity-drag: 16%;
{% endhighlight %}

And that's it for variables! I also stored the margin size, width of the
navigation bar, and default shadow style for my site - but you might not need
those for your application.

# Making Components

Now that we have all our variables, we can start making some components. In this
tutorial, I'll just demo making Material 3's
[common buttons](https://m3.material.io/components/buttons/overview); however,
I'll show you what resources to use, so you can make your own, too. By the way,
you can view my whole common button implementation
[here](https://github.com/Bright-Shard/scss-m3/blob/main/components/buttons/common.scss).

## Understanding Material 3 Docs

First, let's explore the Material 3 docs. This is important for you to be able
to make your own components; if the docs don't make sense, you'll never make
them right!

![Material 3's Common Buttons Overview page](/assets/images/M3-buttons-overview-page.png)

First, the key features of the website. Obviously, on the left side of the
screen is the navigation bar. We'll spend most of our time in the 'Components'
tab, though the 'Foundations' tab and 'Styles' tab are also very useful - they
explain the why and how for many of Material's rules/designs.

On each component's page, you'll see that large, round bar under the title. It
always has 4 tabs: Overview, Specs, Guidelines, and Accessibility. Most of these
are pretty straightforward. The Overview tab gives an overview of the component.
The Specs tab (where we'll spend most our time) gives detailed... well, specs,
for the component's layout, text, and colours. The Guidelines tab gives more
information on the component's use case, and has suggestions for other
components that might work better in some cases. Finally, the Accessibility tab
has tips for making sure your UI remains accessible while using that component.

It's usually a good idea to read the Overview tab before using your component.
After that, you'll pretty much exclusively use the Specs tab to create the SCSS
rules for your component. This tab is *very* long. It walks through each variant
of the component (if applicable), and for each one, gives detailed rules for
every single state the component can be in.

## Common Buttons

All of the common buttons have a few things in common:

- (Optional) Icon before the button text
- Button text (size & font)
- Button shape, spacing, and border radius

I declared all of these properties for every kind of common button, like so:

{% highlight scss linenos %}

.button-elevated, .button-filled, .button-tonal, .button-outlined, .button-text {
    // Flexbox for displaying the text & icon side-by-side
    display: flex;
    flex-direction: row;
    column-gap: 8px;
    align-items: center;
    justify-content: flex-start;

    // Basic button shape
    height: 40px;
    width: fit-content;
    padding: 0px 24px;
    z-index: 0;
    // This rounds the corners (see below)
    @include round(20px);

    // Button text
    font-weight: $label-font;
    font-size: $label-large;
    text-decoration: none;

    // Button icon
    > .icon {
        margin-left: -8px;
        font-size: 18px;
    }
}

{% endhighlight %}

For the button's border radius, I used a mixin I made called 'round'.
Most Material3 components have round borders, so I simplified the rules with
that mixin. Here's the mixin's code:

{% highlight scss linenos %}

// Round corners without showing the border
@mixin round($radius) {
    border: 0px solid;
    border-radius: $radius;
}

{% endhighlight %}

It just makes an invisible border, and sets its radius to the provided radius.
I have several other mixins I'll use throughout this project; you can view them
[here](https://github.com/Bright-Shard/scss-m3/blob/main/material/mixins.scss).

# To be continued

Sorry to disappoint. Since this post is so long, I'm updating it in chunks. More will come soon!
