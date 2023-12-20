---
layout: post
title: How to make the footer stay at the bottom of the page
date: 2023-12-19 07:49:00-0800
description: just jotting down my thoughts1
tags: css
categories: programming
giscus_comments: true
related_posts: true
# related_publications: einstein1950meaning, einstein1905movement
---

<!-- #### I am just testing different kinds of features in my new blog:
---

d -->

Lately I have been working on my block site project using `nextjs` and I am having some issue with making the footer stay 
at the bottom of the page when the previous `div` renders an uncertain amount of items, the footer will go up and "chase" the 
previous `div`, for example, it looks like this:

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0 h-50">
        {% include figure.html path="assets/img/blog-2023-12-19/footer-up.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

so my first instinct would just be using some simple `css` tricks, for example:

```css
footer {
    bottom: 0 !important;
}
```

but the problem with this approach is that if previous `div`'s height is not fixed. This approach only guarantees to work if
you previous `div`'s height is at the perfect height of your screen size 

#### Enter Flexbox

so eventually I had to use flexbox to help me and here's the code to resolve my issue
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* Style for div1 */
        .div1 {
            display: flex;
            flex-direction: column;
            min-height: 100vh; /* Ensure div1 takes at least the full height of the viewport */
        }

        /* Style for div2 (adjust as needed) */
        .div2 {
            flex-grow: 1; /* Allow div2 to grow and push the footer to the bottom */
            /* Other styles for div2 */
        }

        /* Style for the footer */
        .footer {
            /* Footer styles, for example, background-color and padding */
        }
    </style>
</head>
<body>

    <div class="div1">
        <!-- Your other content, including div2 -->
        <div class="div2">
            <!-- Dynamically rendered items -->
            <!-- Adjust as needed -->
        </div>

        <!-- Footer -->
        <div class="footer">
            <!-- Your footer content -->
        </div>
    </div>

</body>
</html>


```

The main idea is to make a container like `div1` to have a fixed height, then use `flex-grow: 1;` to allow the previous `div` to grow 
relative to the other elements, in our case, the other element is the footer class.

after fixing the code, the footer is properly positioned in the bottom


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0 h-50">
        {% include figure.html path="assets/img/blog-2023-12-19/footer-fixed.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

I hope this tip is helpful to you! 😃 