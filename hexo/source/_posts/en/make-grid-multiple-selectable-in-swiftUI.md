---
title: Make Grid multiple selectable in SwiftUI
date: 2022-05-23 07:53:48
indexing: false
tags:
- SwiftUI
- Grid
- Happy Hacky
---

SwiftUI, I love you, now.... please please please give me what I want :cry.

It's hard to belive that 3 years after launch, SwiftUI still don't have perfect solution to replace ***UICollectionView***, Grid components like **LazyVGrid** or **LazyHGrid** is the replacement I used most of time, when I only need a clasic flow-layouted collection view.

But these two boys come with a limitation, they do a pretty good job on layout, not thing to complain about, except that they don't have out-of-box selection capability, things like this need to be done manually:

![Grid-Selection](https://s2.loli.net/2022/05/23/1MoqscZtybSVpKJ.png)

It's totally do-able, and super easy with SwiftUI + some State management code.

## Now here is a hard one, user would expect pan to select gesture to be supported too:

![Pan-to-select](https://s2.loli.net/2022/05/23/2ZVnkKb6BHDczsS.gif)





As far as I know, we are unlucky, no open-sourced solution for that yet, don't count on Apple and don't start crying, let's get our hands dirty and sove this!



## Setup the Desk

Let's create a simple LazyVGrid as a start point.

````swift
struct GridView: View {
    @State var columns: [GridItem] = [
        GridItem(.adaptive(minimum: 150), spacing: 16),
    ]

    var body: some View {
        LazyVGrid(
                columns: columns,
                alignment: .center,
                spacing: 16,
                pinnedViews: .sectionHeaders
        ) {
            ForEach(Array(data.allBooksByGroupFiltered.enumerated()), id: \.element) { (groupIndex, group) in
                Section(header: LibrarySectionHeader(title: group.title)) {
                    ForEach(Array(group.items.enumerated()), id: \.element) { (itemIndex, content) in
                        Text(content.label)
                    }
                }
            }
        }
    }
}
````

## What we need?

Simply 3 steps:

1. A way to intercept the Pan gesture
2. Calculate the selection area base on that Pan gesture.
3. Select/un-select items under that selection area.

First step is super easy, we gonna use: https://github.com/siteline/SwiftUI-Introspect, it can help us get the scrolling container, then we can get the Pan gesture by `scrollView.panGesture`.



## Oh did I mention that you also need to auto scroll the container?
