3.2

fixed morea_theme_navbar_bg configuration in _plugins/MoreaGenerator.rb

fixed the navbar configuration in core.html
- deleted "fixed-top" in <div class="navbar navbar-expand-lg {{site.morea_theme_navbar_bg}}">
- with "fixed-top", the breadcrumb does not show