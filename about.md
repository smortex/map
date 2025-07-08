---
layout: default
---
# {{ site.title }}

{{ site.description }}

[Back to the map]({{ site.url }})

## Who can appear on this map?

Members with write access to the [{{ site.github_project }}](https://github.com/{{ site.github_project }}) repository can manage their visibility on this map.

## Adding myself to the map

To appear on the map, run the [Add me to the map] GitHub action.  The action can be passed:
* **Nothing**, in which case it will geocode the location you setup in your GitHub profile;
* A **location/address** which will be geocoded.  Bear in mind that you probably don't need to be more specific than the country / city you live in and providing your exact address is not advised;
* A **latitude** and a **longitude**, which allow you to point to the exact location of your choice.

## Moving my location on the map

Proceed with the [Add me to the map] GitHub action.  It will update your location, there is no need to remove yourself before.

## Removing myself from the map

If you do not want to appear on the may anymore, run the [Remove me from the map] GitHub action.

## Dealing with other requests

Please open a pull request against [{{ site.github_project }}](https://github.com/{{ site.github_project }}) with your changes.
Do not forget to update the aggregated `data.json` if you change any file in the `_data` directory.
Check `.github/actions/aggregate-members-location/action.yml` to see how it's done.

[Add me to the map]:https://github.com/{{ site.github_project }}/actions/workflows/add_me_to_the_map.yml
[Remove me from the map]:https://github.com/{{ site.github_project }}/actions/workflows/remove_me_from_the_map.yml
