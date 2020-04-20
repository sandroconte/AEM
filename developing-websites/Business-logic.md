# Business logic

1. Create a java file class in /apps/training/components/structure/site-topnav
2. Put this code

```java

package apps.training.components.structure.site_topnav;

import java.util.*;
import java.util.Iterator;
import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageFilter;

import com.adobe.cq.sightly.WCMUsePojo;

public class TopNav extends WCMUsePojo{
    private List<Page> items = new ArrayList<Page>();
    private Page rootPage;

    // Initializes the navigation
    @Override
    public void activate() throws Exception {
        rootPage = getCurrentPage().getAbsoluteParent(2);

        if (rootPage == null) {
        	rootPage = getCurrentPage();
        }
        
        Iterator<Page> childPages = rootPage.listChildren(new PageFilter(getRequest()));
	   	while (childPages.hasNext()) {
			items.add(childPages.next());
	   	}
    }

    // Returns the navigation items
    public List<Page> getItems() {
        return items;
    }
    // Returns the navigation root
    public Page getRoot() {
        return rootPage;
    }
}
```

3. Replace the code in /apps/training/components/structure/site-topnav/site-topnav.html by

```html
<!-- /* Add the business logic*/ -->
<div data-sly-use.topnav="TopNav" class="container we-Container--top-navbar">
    <nav class="navbar navbar-inverse navbar-absolute-top">
        <div class="navbar-header">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#we-example-navbar-collapse-inverse" aria-expanded="false">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span> <span class="icon-bar"></span>
            </button>
            <button type="button" class="navbar-toggle navbar-toggle-close collapsed" data-toggle="collapse" data-target="#we-example-navbar-collapse-inverse" aria-expanded="false">
                <span class="sr-only">Toggle navigation</span>
            </button>
            <a class="navbar-brand" href="${topnav.root.path}.html">we.<strong>train</strong></a>
            <div class="pull-right visible-xs"></div>
        </div>

        <!-- /.navbar-header -->
        <div class="collapse navbar-collapse width" id="we-example-navbar-collapse-inverse">
            <ul class="nav navbar-nav navbar-center">
                <li class="visible-xs"><a href="${topnav.root.path}.html">we.<strong class="text-primary">train</strong></a></li>

                <!-- /* Nav with business logic */ -->
                <li class="nav navbar-nav navbar-left" data-sly-repeat="${topnav.items}">
                    <a href="${item.path}.html">${item.title}</a>
                </li>

                <li class="visible-xs divider" role="separator"></li>
            </ul>
        </div>
        <span style="height: 0px;" class="navbar-shutter"></span>
    </nav>
    <!-- /.navbar -->
</div>
```

## Alternatively from js

4. Put this code

```javascript

// Server-side JavaScript for the topnav logic
use(function () {
    var items = [];
    var root = currentPage.getAbsoluteParent(2);

    //make sure that we always have a valid set of returned items
    //if navigation root is null, use the currentPage as the navigation root
    if(root == null){
    	root = currentPage;
    }


    var it = root.listChildren(new Packages.com.day.cq.wcm.api.PageFilter());
    while (it.hasNext()) {
        var page = it.next();
        items.push(page);
    }

    return {
        items: items,
        root: root
    };
});
```

in /apps/training/components/structure/site-topnav/topnav.js

5. Change ```data-sly-use.topnav="TopNav"```by ```data-sly-use.topnav="topnav.js"``` to modify the class use 