
404 ERROR REDIRECT CONFIGURATION

1.  ADD BANNER IMAGE to:
        [root] > templates > [template-name] > images > 404 > 404-background.png

2.  ADD 404.LESS FILE to folder:
        [root] > templates > [template-name] > less

3.  EDIT FILE:
        [root] > templates > [template-name] > less > template.less
    ————————————————————————————————
    ADD LINE: @import "404.less";

4.  ADD NEW ARTICLE
    Article title: 404
    ————————————————————————————————
    Article alias: 404
    ————————————————————————————————
    HTML content:
        <div class="banner">
            <div class="container">
                <h1>404</h1>
            </div>
        </div>
        <div class="content">
            <p class="whoops">Whoooops!</p>
            <p class="sorry">Sorry, the page you're looking for cannot be found.</p>
            <p class="links">Here are some useful links instead:</p>
            <ul class="options">
            <li><a class="hvr-shutter-out-horizontal" href=“/“>Home</a></li>
            <li><a class="hvr-shutter-out-horizontal" href=“/“>Button Two</a></li>
            <li><a class="hvr-shutter-out-horizontal" href=“/“>Button Three</a></li>
            <li><a class="hvr-shutter-out-horizontal" href=“/“>Button Four</a></li>
            </ul>
        </div>

    [Publishing] tab
    ————————————————————————————————
    Robots: No index, no follow
    ————————————————————————————————

5.  Joomla! Hidden Menu configuration

    LOCATE/CREATE A HIDDEN MENU
    ————————————————————————————————
    ADD NEW MENU ITEM:
    Menu Title: 404
    Menu Alias: error-404

    [Details] tab
    ————————————————————————————————
    Menu Item Type: Single Article
    Select Article: 404
    Menu (far right): Hidden
    Parent Item: Menu Item Root
    ————————————————————————————————

    [Options] tab
    ————————————————————————————————
    Show Title: Hide
    Show Category: Hide
    ————————————————

    [Page Display] tab
    ————————————————————————————————
    Page Class: error-404 (include a single space before error…)
    ————————————————————————————————

6.  Visit yourdomain.com/error-404 and test the 404 page layout thoroughly


7.  Configure CSS
    It will be invariably be necessary to configure the LESS/CSS file for the structure
    of the template it is applied to.


8.  IF NOT EXIST: [root] > templates > [template-name] > error.php
        COPY FILE: [root] > templates > system > error.php
	TO: [root] > templates > [template-name] > error.php
    EDIT FILE:
        [root] > templates > [template-name] > error.php
    ————————————————————————————————
    AFTER THE LINE:
        defined('_JEXEC') or die;
    ————————————————————————————————
    ADD THIS CODE:
        
        if (($this->error->getCode()) == '404') {
            header("HTTP/1.0 404 Not Found");
            echo file_get_contents(JURI::root().'error-404');
            exit;
        }

    FOR MULTI-LANGUAGE SITES, ADD (and ADAPT) THIS CODE:
	
        if (($this->error->getCode()) == '404') {
            header("HTTP/1.0 404 Not Found");
            switch ( strtolower($this->language) ) {
		case "es-es": echo file_get_contents(JURI::root().'/es/error-404'); break;
		case "pt-br": echo file_get_contents(JURI::root().'/pt/error-404'); break;
		     default: echo file_get_contents(JURI::root().'error-404'); break;
            }
            exit;
        }

9.  To test your 404 page, visit: yourdomain.com/[somerandomwordshere]

10. Confirm 404 page returns an HTTP 404 status code (i.e. not 200/301/302)
	
    Tip: Use this Chrome plugin: Redirect Path - https://chrome.google.com/webstore/detail/redirect-path/aomidfkchockcldhbkggjokdkkebmdll?hl=en
