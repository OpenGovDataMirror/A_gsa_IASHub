---
title: Getting started
tags: [getting_started]
layout: splash
---

<div id="search-demo-container-center" style="max-width:600px; margin: 50px auto 0px auto;"> 
    <div style="margin: 10px;">
        <h2 id="greeting" class="clearfix" style="font-weight:bolder;color: ghostwhite; margin-bottom:0px">Good afternoon</h2>
        <input type="search" id="search-input" style="" id="search-input-center" placeholder="Start here!" onfocus="this.placeholder = ''" onblur="this.placeholder = 'Start here!'">
        <ul id="results-container-center" style="clear: both;"></ul>
    </div>
</div>
<script src="{{ "/js/jekyll-search.js" | prepend: site.baseurl }}" type="text/javascript"></script>
<script type="text/javascript">
        SimpleJekyllSearch.init({
            searchInput: document.getElementById('search-input-center'),
            resultsContainer: document.getElementById('results-container-center'),
            dataSource: '{{ "/search.json" | prepend: site.baseurl }}',
            searchResultTemplate: '<li><a href="{url}" title="{{page.title | replace: "'", "\"}}">{title}</a>{{% if summary != "" and summary != nil %}}<br /><p style="font-size:12px;font-style: italic;">{summaryTrunc}</p>{{% endif %}}</li>',
noResultsText: '{{site.data.strings.search_no_results_text}}',
        limit: 10,
        fuzzy: true,
})
</script>
<!--end search-->