---
layout: layouts/post.njk
title: How to Display Additional Information on an Entity Form
date: 2021-06-28T08:55:15.793Z
---
```javascript
function popoverSwitcher() {
    var tieredRateValue = $('#pfc_tieredrate').val();
    var title;
    var content;
    switch (tieredRateValue) {
        case '229330000':
            title = 'Tier 1';
            content = 'Tier 1';
            break;
        case '229330001':
            title = 'Tier 2';
            content = 'Tier 2';
            break;
        case '229330002':
            title = 'Tier 3';
            content = 'Tier 3';
            break;
        case '229330003':
            title = 'Tier 4';
            content = 'Tier 4';
            break;
        default:
            title = 'Select a Tier';
            content = 'Select a tier from the optionset below in order to see further information';
    }

    $('#tiered-rate-popover')
        .popover({
            placement: 'top',
            html: false,
            title: `${title}`,
            content: `${content}`,
            trigger: 'manual',
        })
        .popover('show');
}
```

```javascript
tieredRateControl.on('change', function() {
    $('#tiered-rate-popover').popover('destroy');
    setTimeout(popoverSwitcher, 250);
});

tieredRateControl.on('blur', function () {
    $('#tiered-rate-popover').popover('destroy');
});
```

```javascript
$(document).on('click', '#tiered-rate-popover', function () {
    if ($('div.popover').length > 0) {
        $('div.popover').remove();
    } else {
        setTimeout(popoverSwitcher, 250);
    }
});

$('#tiered-rate-popover').on('blur', function () {
    $('#tiered-rate-popover').popover('destroy');
});
```



```javascript
$(document).on('click', '#tiered-rate-popover', function () {
    $('#tiered-rate-popover').popover('destroy');
    setTimeout(popoverSwitcher, 250);
});
```