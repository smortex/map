---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: map
---

<script language="javascript">
function linkTo(member, content) {
  return `<a href="${member.html_url}" target="_blank">${content}</a>`;
}
function renderMemberPopup(member) {
  return `
  <p>${linkTo(member, `<img src="${member.avatar_url}" width="72" class="avatar" />`)}</p>
  <p><strong class="login">${linkTo(member, member.login)}</strong> <span class="name">${linkTo(member, member.name)}</span></p>
  <p>${member.bio || ''}</p>
  `;
}
function memberPopup(layer) {
  member = layer.options.user_data;

  const el = document.createElement('div');
  el.className = 'member-popup';

  const popup = async (url) => {
    const response = await fetch(url);
    if (!response.ok) {
      alert(response.statusText);
    }

    const json = await response.json();
    el.innerHTML = renderMemberPopup(json);
  };

  popup('https://api.github.com/users/' + member.login);
  return el;
};
function callback(data) {
    var members = [];

    var member_icon = L.icon({
        iconSize:      [25, 41],
        iconAnchor:    [12, 41],
        popupAnchor:   [1, -34],
        tooltipAnchor: [16, -28],
        shadowSize:    [41, 41],
        iconUrl:       '{{ site.url }}/marker.png',
        shadowUrl:     '{{ site.url }}/marker-shadow.png',
    });

    data.forEach(m => {
      members.push(L.marker([m.lat, m.lng], { icon: member_icon, title: m.login, user_data: m }).bindPopup(memberPopup, {minWidth: 200}));
    });

    var common_attribution = 'Map data © <a href="https://www.openstreetmap.fr/">OpenStreetMap</a> | Tiles: ';
    var map_instructions = ' | <a href="{{ site.url }}/about.html">Manage your visibility on this map</a>';

    var neighbourhood = L.tileLayer('https://tile.thunderforest.com/neighbourhood/{z}/{x}/{y}.png?apikey={{ site.thunderforest_apikey }}', {attribution: common_attribution + 'Neighbourhood © <a href="https://thunderforest.com/">Thunderforest</a>' + map_instructions});

    var markers_layer = L.markerClusterGroup();

    var members_layer   = L.featureGroup.subGroup(markers_layer, members);

    markers_layer.addLayer(members_layer);

    var map = L.map('map', {layers: [neighbourhood, markers_layer, members_layer]});

    L.control.scale({maxWidth: 300}).addTo(map);

    map.fitWorld();
}

fetch("{{ site.url }}/data.json")
  .then(response => {
    if (!response.ok) {
      throw new Error(response.statusText);
    }
    return response.json();
  })
  .then(data => callback(data))
  .catch(error => alert('Error fetching data:', error));

</script>
