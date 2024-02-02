# Shopify Developer Challenge

I had a great time working on this challenge! 

On the very-off chance that something goes horribly wrong and my code doesn't render properly on your computer, I've made a quick demo video showing how things look on my end. It's likely not necessary, but I figure you can never bee too cautious. You can see that here:
[PREVIEW VIDEO](https://share.zight.com/L1uyOekj)

## To preview my PDP

- Git clone this repository onto your local machine
- navigate into the folder that you just cloned
- Change to my branch with `git checkout feature/pdp`
- Run `npm install`
- Run `npm run dev`
- Navigate to http://0.0.0.0:3000 in your browser to preview the PDP

## CHANGES I MADE

### IMAGES
- Added product image and product image gallery.
- Added ability to change the full-sized image by clicking on thumbnails.
- Added white background to any image containers, so the images would all look uniform in size. 
- Added box shadow to make product image pop.
- Added zoom on image hover.
- Added enlarged image modal on click.

### PRODUCT

- Added Montserrat font 
- Added sale badge that displays if the product price is lower than the product’s compare at price.
- Added css variables for often-reused values like font size, to ensure elements have a consistent look and that future font-size changes are simple to implement.
- Added JS logic to handle currency formatting. Usually I’d rely on the “money_with_currency” liquid filter to do this, but that didn’t work because this isn’t connected to an actual store. 
- Added variant selectors that are functional and update the variant ID that’s sent in the add to cart request.
- Added a quantity selector which is similarly functional and updates quantity value for the add to cart request.
- Added POST request to the AJAX api, following the cart request format outlined in [this Shopify doc](https://shopify.dev/docs/api/ajax/reference/cart)
- Added success and error messages that appear after clicking “Add to cart”. Success appears whenever our POST request receives a success message back from the fake cart API. Error message appears whenever a customer tries to add products to the cart without first selecting a variant.
- Added loading spinner to mimic actual API call, and show the user that their add to cart request is being processed.
- Pulled the product’s description to display below the add to cart form — On a real store I probably would have included an option to hide the description under a dropdown. But since the product was so basic and there’s no theme settings to interact with, I left the description fully displayed. 
- Styled for both mobile and desktop. One thing to note —  For some reason the media queries aren’t working when I view the site in Chrome’s responsive view. But these changes are working on every other browser, and work fine when I resize the Chrome window. Maybe it’s just on my end? But if things look iffy on mobile then viewing on a different browser might fix that. 



## WHAT I’D LIKE TO DO BETTER

I’ll be the first to admit that I’m not a natural web designer. I love doing front-end work and implementing a design, but when it comes to selecting the perfect font or layout, well, there’s people better suited to that than me. So the main thing I’d like to do better is give the page more of a “wow” factor. Right now it’s a very functional but pretty plain PDP, which is fine, but I know that by bouncing ideas off of other people or working with a designer we could get this site looking world-class. 

## WHAT WAS MY FAVOURITE PART  

I liked working from scratch and just building. It was fun to be given a totally blank slate and asked to turn it into a PDP. I’ve done a lot of work where I’m modifying a pre-built theme or working from a design and that’s a fun challenge in its own right, but it was nice to think “ok I want a clickable product gallery” and then have to fully design and implement that myself. Additionally, there were some Liquid features that I’m used to having in a Shopify store but they weren’t working here, and I found that added to the challenge in a positive way. It was good to think “here’s what I’d normally do, but that’s not going to work so let’s find a plan b” and then execute on that.


## WHAT I WOULD CHANGE IF THIS WERE ACTUALLY A SHOPIFY THEME

- I’d have separated css, js, and liquid files. I actually tried that but for some reason my imports weren’t working. So I threw all of the code in one file. I figure it’s easiest to see all the code I’d added that way anyway. But ideally I’d like to make this code more modular so that the product template file isn’t so dang lengthy.

- Developing for an actual Shopify theme would mean that every alterable feature would need to have an accompanying theme setting to go with it. Something I love about developing with Shopify is thinking about the person that we may be passing this off to, who might not necessarily have any tech skills themselves. In that situation, it’s paramount to ensure that everything they would ever want to do in modifying the theme is possible and intuitive. This requires developing with the user’s POV in mind at all times, and ensuring that the theme customizer is the driving force behind how your features are interacted with, modified, enabled, or disabled. So if this were actually Shopify, there would be a lot more references to theme and section settings, because I don’t ever want the user to feel like they need to know how to code in order to get their store looking right.  

- I’d have used Liquid’s {% form ‘product’ %} for the product form, because it manages a lot of data handling when sending info to the cart. But I got a 500 error when I tried to do that here so I implemented the functionality with an HTML form and JS instead.

- I'd have had more robust error handling for the cart API. There wasn't much to work around though since our API only returns "Success: true".

- Simirly, I'd have added more checks in the liquid code to see if certain theme settings are selected before rendering elements. EX: `{% if section.settngs.display_description == true %} {{ product.description }} {% endif %}`

- I’d have connected product images to the selected variant, so that the displayed product image changes as you select new variants, if those variants have a different featured image. But since our test product has the same images for all variants, that seemed like overkill here.

- I’d have leveraged to some existing liquid objects and filters that weren’t available to me here, like product.selected_or_first_available_variant. This was undefined on the app, but on an actual store I’d expect to be able to access that to make variant switching simpler. Instead, I made a JS workaround to send the correct variant id to the cart in my AJAX api request. However, ideally I’d use selected_or_first_available_variant within the product template itself for rendering things like the product price. That way, product price will be update if the user changes variants. 

- The “money_with_currency” liquid filter also wasn't working, so I added JS to format prices with currency. But I’d just use that liquid filter on an actual Shopify store. There are other examples of things I'd have done with liquid tools as well, but I think two is enough for here. This README is already pretty long.

- I’d have made the code more modular. A lot of what’s in the product.liquid file could be used in other places. EX: if we made a quick-view modal, we’d want to use the product image/gallery, variant selectors, etc. So likely I’d movee those into their own separate snippets and call those snippets as needed. 

- I’d have linked most text to the en.default.json file, instead of hardcoding it (things like “Add to cart”, “Sale”, etc), to ensure that the site is easy to translate.
