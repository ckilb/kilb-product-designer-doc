---
nav_order: 100
parent: FAQ
---

# Is it possible to show the preview images in the order confirmation mails?

When using Shopware 6 you may have recognized that the list of articles inside the order confirmation mails sent to your customers only shows
the article default images instead of the preview images generated by the designer.

The reason is that the designer will not automatically touch your mail templates.
You can easily edit your mail templates on your own in Shopware's administration area.

Shopware's article default image will usually be stored in
```twig
lineItem.cover.url
```

The image URL of the preview image generated by the designer will be placed in
```twig
lineItem.payload.productDesignBasketImageUrl
```

So if you want to show the preview image instead of the default cover image you have to add a condition for that.

If you did not yet touch the order confirmation template - so you are using the default one from Shopware - you can add the condition like this:

Find this piece of code:
```twig
{{ nestedItem.cover.url }}
```

and replace it with:
```twig
{{ nestedItem.payload.productDesignBasketImageUrl ?? nestedItem.cover.url }}
```

This will replace the image in case a preview image is existing. If there's no preview image existing - which may be the case if the product designer is not configured for the product - the default cover URL will be shown as a fallback.

Don't forget to save your changes by clicking the Save button.
Make sure you do these changes for all languages which are used in your shop.