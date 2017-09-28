Bootstrap Tab Collapse
======================

Small bootstrap plugin that switches bootstrap tabs component to collapse component for small screens.

**This version has been reworked to work with Bootstrap 4**


How it works
------------

The most obvious way: bootstrap tab collapse generates accordion markup and appends it right away after tabs component.
When accordion becomes (If accordion is) visible tabcollapse searchs for `.tab-pane` and detaches their content to appropriate
accordion groups keeping all attached js data.
Tabs component is given `hidden-xs`-class and accordion component is given `visible-xs`-class. That's it.

**Note:**
Since Bootstrap 4 no longer ships with those utility classes, I have re-created them from the `4.0.0-alpha.6`-version, and also added the `hidden-md-down` (and the like) that utilises breakpoints, for those of you who wants to write less code. They are "hidden" (pun intended) inside `dist/css/utilities.css` and I have also made the Sass available for anyone to look at in case you're bored.

**[Demo](http://tabcollapse.okendoken.com/example/example.html)** (Bootstrap v3.3.7)

Use
------------

Lets say you have your tabs component right from Bootstrap's documentation:

    <ul id="myTab" class="nav nav-tabs">
        <li class="nav-item active"><a class="nav-link" href="#home" data-toggle="tab">Home</a></li>
        <li class="nav-item"><a class="nav-link" href="#profile" data-toggle="tab">Profile</a></li>
        ...
    </ul>
    <div id="myTabContent" class="tab-content">
        <div class="tab-pane fade in active" id="home">
            <p>Raw denim you probably haven't...</p>
        </div>
        <div class="tab-pane fade" id="profile">
            <p>Food truck fixie locavore, accus...</p>
        </div>
        ...
    </div>

To activate tab collapse just include **bootstrap-tabcollapse.js** somewhere in your file and call:

    $('#myTab').tabCollapse();

If you want to specify the class that is given to accordion and tabs components you can do so by passing options to `tabCollapse`:

    $('#myTab').tabCollapse({
        tabsClass: 'hidden-sm',
        accordionClass: 'visible-sm'
    });

The default class is `hidden-xs`. So it means that tabs component will be switched to accordion for 767px and below. You can define your own classes and use them.
You can also use multiple Bootstrap classes in order to, for example, show accordion for mobile + tablets and tabs for desktop+:

    $('#myTab').tabCollapse({
        tabsClass: 'hidden-sm hidden-xs',
        accordionClass: 'visible-sm visible-xs'
    });

Events
------------

There are four events tabcollapse triggers (for **entire** component, not for single tabs or accordion groups!):
-   **show-tabs.bs.tabcollapse** - triggered before tabs component is shown
-   **shown-tabs.bs.tabcollapse** - triggered after tabs component is shown
-   **show-accordion.bs.tabcollapse** - triggered before accordion component is shown
-   **shown-accordion.bs.tabcollapse** - triggered after accordion component is shown

To attach event handler just call:

    $('#myTab').on('shown-accordion.bs.tabcollapse', function(){
        alert('accordion is shown now!');
    });

Attach an event handler when **either** tab or collapse is opened:
------------

    $(document).on("shown.bs.collapse shown.bs.tab", ".panel-collapse, a[data-toggle='tab']", function (e) {
        alert('either tab or collapse opened - check arguments to distinguish ' + e);
    });

Contributors
------------

Thanks to [bdaenen](https://github.com/bdaenen) for contributing.


To Do
-----------

Convert the script to work with the new `nav-tabs` layout where you use [simplified]:

    <nav class="nav nav-tabs">
        <a href="#home" class="nav-item nav-link">Home</a>
        <a href="#profile" class="nav-item nav-link">Profile</a>
        ...
    </nav>

Also, because of [one of my own suggestions](https://github.com/twbs/bootstrap/issues/22025) on the Bootstrap 4 issue-tracker, the accordions no longer have to bind on `.card`. That means you can use custom groups:

    <div id="accordion-group" data-children=".item">
        <div class="item">
            <a href="#example1" data-toggle="collapse" data-parent="#accordion-group">Toggle item</a>
            <div id="example1" class="collapse" role="tabpanel">
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
            </div>
        </div>
        <div class="item">
            <a href="#example2" data-toggle="collapse" data-parent="#accordion-group">Toggle item</a>
            <div id="example2" class="collapse" role="tabpanel">
                <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
            </div>
        </div>
    </div>

Thus, this library needs to take in an option that defines if it's either a card-based accordion, or a custom one like above.
