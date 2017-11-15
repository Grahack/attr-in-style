# attr-in-style

We are providing three functions `attr`, `style-id` and `style-class`.

They allow you to write in your [hiccup](https://github.com/weavejester/hiccup):

    [:div (attr :footer-wrapper [:inverted :small] {:on-click my-fn})
      "Lorem ipsum bla bla."]

Where `:footer-wrapper` in an `id`, the vector is a set of `class`es and the
map can contain additional attributes.

Beside, say in a `style.cljs` file (curly brackets could be at your prefered
position), you define the styles you want to apply:

    (style-id :footer-wrapper
      {:background-color "white"
       :color "black"})

    (style-class :inverted
      {:background-color "black"
       :color "white"})
      
    (style-class :small
      {:font-size "70%"})

The `attr` function then can do two different things, according to the way you
[require](http://clojuredocs.org/clojure.core/require) it:

1. insert id and classes in the elements and generate the CSS file, or
1. insert the style in the elements, ala no-CSS.

With the first way, you get this HTML:

    <div id="footer-wrapper" class="footer small" on-click="my-fn();">
      Lorem ipsum bla bla.
    </div>

and this CSS:

    #footer-wrapper {
      background-color: white;
      color: black;
    }

    .inverted {
      background-color: black;
      color: white;
    }
      
    .small {
      font-size: 70%;
    }

With the second way, you get this HTML:

    <div style="background-color: black; color: white; font-size: 70%;"
         on-click="my-fn();">
      Lorem ipsum bla bla.</div>

or if you need the `id` or `class`:

    <div id="footer-wrapper" class="footer small"
         style="background-color: black; color: white; font-size: 70%;"
         on-click="my-fn();">
      Lorem ipsum bla bla.</div>
