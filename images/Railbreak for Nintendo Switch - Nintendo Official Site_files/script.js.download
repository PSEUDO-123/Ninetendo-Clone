(function () {
    var psConfig = PriceSpider.widgetConfigs["5dc435df8b867f001f540866"];
    PS_$ = PriceSpider.$;

    psConfig.on("redirect", function(widget, productSeller) {
        // Analytics Tagging - LT - 01/09/2020 - DEL-28869
        // Client: "User clicked on an online seller"
        window.dispatchEvent(new CustomEvent('PriceSpiderInteraction', {
            detail: {
                type: 'REDIRECT_TO_SELLER',
                product: {
                    sku: widget.skuKey,
                    name: widget.data.product.title,
                    price: productSeller.price
                },
                seller: productSeller.seller.name
            }
        }));
    });
    psConfig.on("getDirections", function(widget, productSeller) {
        // Analytics Tagging - LT - 01/09/2020 - DEL-28869
        // Client: User clicked on Get Directions and entered a starting address
        window.dispatchEvent(new CustomEvent('PriceSpiderInteraction', {
            detail: {
                type: 'GET_DIRECTIONS',
                product: {
                    sku: widget.skuKey,
                    name: widget.data.product.title
                },
                seller: productSeller.seller.name,
                postalCode: productSeller.postalCode,
                distanceAway: productSeller.distance
            }
        }));
    });
    psConfig.on("skuChanged", function(widget, productSeller) {
        // Analytics Tagging - LT - 01/09/2020 - DEL-28869
        // Client: User selected a different product from the dropdown in a WTB modal
        window.dispatchEvent(new CustomEvent('PriceSpiderInteraction', {
            detail: {
                type: 'PRODUCT_LOOKUP',
                product: {
                    sku: widget.skuKey
                }
            }
        }));
    });

    psConfig.on("data", function(widget) {
        for (var i = 0; i < widget.data.localSellers.length; i++) {
            widget.data.localSellers[i].store.city = widget.data.localSellers[i].store.city.trim();
        }
    });

    psConfig.on("update", function(widget) {
        for (var i = 0; i < widget.data.onlineSellers.length; i++) {
            if (widget.data.onlineSellers[i].hiddenPrice) {
                document.querySelector(`.ps-online-seller-select > div > div[data-seller='${widget.data.onlineSellers[i].seller.id}'] > div:nth-child(2) > span > span.ps-price`).innerText = "See price in cart"
            }
        }
    });
})();