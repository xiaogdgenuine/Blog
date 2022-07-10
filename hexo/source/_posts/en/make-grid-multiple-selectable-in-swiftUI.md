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

Let's create some data as a start point:

````swift
struct Group: Hashable {
    let title: String
    let items: [Item]
}

struct Item: Hashable {
    let title: String
}

let mockData = [
    Group(title: "Numbers",
          items: "0123456789"
                    .map{ Item(title: String($0)) }),
    Group(title: "Letters",
          items: "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
                    .map{ Item(title: String($0)) })
]
````

Then we create a LazyVGrid to render these data:

````swift
struct GridView: View {
    @State var columns: [GridItem] = [
        GridItem(.adaptive(minimum: 150), spacing: 16),
    ]

    var body: some View {
        ScrollView {
            LazyVGrid(
                    columns: columns,
                    alignment: .center,
                    spacing: 16,
                    pinnedViews: .sectionHeaders
            ) {
                ForEach(Array(mockData.enumerated()), id: \.element) { (groupIndex, group) in
                    Section(header: Text(group.title)) {
                        ForEach(Array(group.items.enumerated()), id: \.element) { (itemIndex, item) in
                            
                            // The cell
                            Text(item.title)
                                .padding()
                                .frame(maxWidth: .infinity, maxHeight: .infinity)
                                .background(Color.blue)
                            
                        }
                    }
                }
            }
        }
    }
}
````

This should give us a LazyVGrid with two sections:

![start-point](https://s2.loli.net/2022/05/23/tqaURvOgsfcwyTi.png)

## What we need?

Simply 3 steps:

1. A way to intercept the Pan gesture of scrollable container
2. Calculate the selection area base on that Pan gesture.
3. Select/un-select items under that selection area.

First step is super easy, we gonna use: https://github.com/siteline/SwiftUI-Introspect, it can help us get the scrolling container, once we did it, we can attach a new Pan gesture to the scrollable container.





## Oh did I mention that you also need to auto scroll the container?
