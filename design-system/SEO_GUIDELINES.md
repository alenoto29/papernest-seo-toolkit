# Design System SEO Guidelines

> Source: Notion export dal design team Papernest. Regole ufficiali per il SEO team.

> Now that the storybook components are slightly redesigned, the next step would be to redesign the HTML components following the CAT design system rules.

## Goal

The goal of the guidelines is to leave some room for the SEO team to modify components while staying true to best UX/UI practices and allow pages to have visual cohesiveness and good readability. The guidelines will follow a simple structure of Do's and Don'ts ranging different categories.

In the General rules sections these categories will be explained in more details and you can have a look at the Figma file where all these informations are listed.

---

## General Rules

### Colors

The colors that are used in the components, as well as eventual color changes at the team's discretion, have to be part of papernest's color palette. Otherwise components run the risk of clashing with one another and undermine the visual cohesiveness of the page. This also aligns with the greater goal of having a unified visual identity across all sites. While font color could be placed in this category, it is talked about within the typography section.

Figma reference: [Core Colors](https://www.figma.com/design/3t2bjqWp5FPMk7IcOknP88/Design-system---CAT?node-id=1158-502)

### Typography

While font sizes, weight, and color can be changed to a certain extent, it is important to follow the typography hierarchy established in the storybook. This will allow the team to have freedom in modifying certain typographic elements while ensuring clear readability and cohesiveness within pages and elements.

Figma reference: [Typography](https://www.figma.com/design/3t2bjqWp5FPMk7IcOknP88/Design-system---CAT?node-id=0-1)

### Icons

Because the storybook did not provide an icon library, the icons used come from the CAT design system which uses the **Lucide icon library**. This means that there are **no filled versions** of the icons since the Lucide library does not have them.

Figma reference: [Icons](https://www.figma.com/design/3t2bjqWp5FPMk7IcOknP88/Design-system---CAT?node-id=905-1304)

### Shape and Radius

If possible, it is best to keep the shapes and radiuses of the components as they were presented in the HTML code. If the team wants to modify them, they can be allowed to in a **5 pixel interval**. The storybook has radiuses that work in a 5 pixel logic (except the ppn shape which has **18 pixels on top left and bottom right**).

Figma reference: [Radius](https://www.figma.com/design/3t2bjqWp5FPMk7IcOknP88/Design-system---CAT?node-id=443-2684)

### Spacing (Padding and Gap)

It would be best to **not modify the padding and gap** of the components until the design team redesigns them. Padding and gaps are chosen according to the scale used in the design system (usually **8 pixel grid** although the storybook had a 5 pixel grid logic). It also uses principles from **Gestalt's theory** to create a visual hierarchy within components that ensure readability and visual cohesiveness.

Figma reference: [Spacing](https://www.figma.com/design/3t2bjqWp5FPMk7IcOknP88/Design-system---CAT?node-id=1157-436)

---

## Storybook Components (Redesigned)

Components that have been redesigned following the new design system:

- Buttons
- Button group
- ppn-block-double
- ppn-deals-list
- ppn-callout
- ppn-cta-block-single (Lugia + Kamino)
- ppn-cta-fullwidth

---

## Custom HTML Components

Components marked with the "HTML custom" tag on the [component mapping spreadsheet](https://docs.google.com/spreadsheets/d/13fMz-3CS3ccfigdl60HEO1LOucGcZkRLNgw3Uo-_isQ/edit?gid=1232086971#gid=1232086971):

- Navigation buttons
- CTA promotion
- HTML callout
- Main steps
- Expert card
- Comparation cards
- Step by step
- HTML deal list
- Multiple cards
- Main providers
- Color block
- Related news module
- Related articles without images
- 3 time sections
- Our service
- Reviews
- HTML card
- Card offer version 1
- Card offer version 2
- Offer table
- Podiums
