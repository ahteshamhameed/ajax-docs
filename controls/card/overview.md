---
title: Overview
page_title: RadCard Overview | UI for ASP.NET AJAX Documentation
description: Overview
slug: card/overview
tags: overview
published: True
position: 0
---

# Card Overview

RadCard is a UI component that incorporates a [set of classes](https://docs.telerik.com/kendo-ui/styles-and-layout/cards) from the [Kendo UI](https://www.telerik.com/kendo-ui) suite to create flexible containers.

A Card can consist of a single container or it could be a container with header, body, footer, actions and more.

### Table of content

- [Getting Started](#getting-started)
- [Card Components](#card-components)
- [Layout](#layout)
- [Orientation](#orientation)
- [Styles](#styles)
- [Skins](#skins)


## Getting Started

To create a Card, add a RadCard tag on the page and fill it with content.

````ASP.NET
<telerik:RadCard ID="RadCard1" runat="server" Width="285px">
    <telerik:CardImageComponent runat="server" src="https://demos.telerik.com/kendo-ui/content/web/cards/tulips.jpg"></telerik:CardImageComponent>

    <telerik:CardBodyComponent runat="server">
        <telerik:CardTitleComponent runat="server">
            Tulip time
        </telerik:CardTitleComponent>

        <p>The tulip season is just around the corner. If you still haven't decided on your spring destination, we have a suggestion- Holland, a.k.a the "flower shop of the world"!</p>
    </telerik:CardBodyComponent>

    <telerik:CardActionsContainerComponent runat="server" CardActionsAlignment="Stretched">
        <span class="k-button k-flat k-primary">Read more</span>
        <telerik:CardSeparatorComponent runat="server" Orientation="Vertical">
        </telerik:CardSeparatorComponent>
        <span class="k-button k-flat k-primary">Save for later</span>
    </telerik:CardActionsContainerComponent>

    <telerik:CardFooterComponent runat="server">
            <span class="k-icon k-i-heart-outline"></span>32
            <span class="k-icon k-i-comment"></span>2
            <span class="k-icon k-i-clock"></span>10 m
    </telerik:CardFooterComponent>
</telerik:RadCard>
````

## Card Components

- [Header]({%slug card/components%}#header)
- [Title]({%slug card/components%}#title)
- [Subtitle]({%slug card/components%}#subtitle)
- [Body]({%slug card/components%}#body)
- [Footer]({%slug card/components%}#footer)
- [Actions]({%slug card/components%}#actions)
- [Media]({%slug card/components%}#media)
- [Separators]({%slug card/components%}#separators)

![Card - Components](card-components.png)


## Layout

- [Read more]({%slug card/layout %})

![Card - Layout](layoutanimation.gif)

## Orientation

- [Read more]({%slug card/orientation %})

![Card - Orientation](card-orientation.png)

## Styles

- [Read more]({%slug card/styles %})

![Card Styles](card-styles.png)

## Skins

- [Read more]({%slug introduction/radcontrols-for-asp.net-ajax-fundamentals/controlling-visual-appearance/how-skins-work %})

 ![Card Skins](card-skins.gif)
   
