Tracking in Connexions
======================

We supply educators with a publication mechanism for their work, and as such
those educators have an interest in tracking the usage of the published works.

At the moment the "legacy connexions" has two metadata fields (Google Analytics Tracking code field) in both the module and collections data.

When a module is viewed at its home page (say the `CCAP physics book <http://cnx.org/content/m42955/latest/>`_) we have included tracking javascript for account UA-7903479-1

Similarly a collection that `uses that module <cnx.org/content/m42955/latest/>`_
will have a tracking code.

By default we put tracking code  UA-7903479-1 (cnx) and UA-5033010-1 (hewlett) into everything.

Dealing with non-HTML downloads
-------------------------------

It is not clear if we do or do not track non-HTML use - for example so we fire a google-analytics API event when a pdf or ePub is downloaded.  This may well become a new story.

Glossary 
--------

gaq - google analytics (its the short form in _gaq.push in their own javascript)

Requirements for rewrite
------------------------

Ensure it is possible to replicate existing functionality
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This requires a gaq script snippet to be placed into every HTML document by
default (covering cnx and hewlett) It also requires a snippet to be placed in
the appropriate documnet should a googe analytics code exist in the module or
collections record.


We shall need to update the dbase, python code and the backbone model client side and ensure they are testable.

We shall also need to add gaq to the UI code for the MetaData tab 

Webview
-------

The webview will need to be able to inject the below code or similar 
into outgoing HTML documnets based on a lookup against the dbase fields refered to above.

If we see webview as sensible place to inject this then a sensible place to 
store tracking codes is at the user level - they just add once and it is applied always.  This impacts a number of assumptions about publication and ownership so may be needing deeper discussion. 

:discuss:`Do we inject on HTML serving or regularly update stored HTML and serve quicker`

:: 


        <script type="text/javascript">
                    var _gaq = _gaq || [];
                    function trackthisGoogleAnalytics(strCode) {
                      try {
                        _gaq.push(['user._setAccount', strCode]);
                        _gaq.push(['user._trackPageview']);
                      }
                      catch(err) {}
                    }
            </script>
        <script type="text/javascript">
                            var _gaq = _gaq || [];
                            _gaq.push(['_setAccount', 'UA-7903479-1']);
                            _gaq.push(['_setDomainName', '.cnx.org']);
                            _gaq.push(['_trackPageview']);
                            _gaq.push(['hewlett._setAccount', 'UA-5033010-1']);
                            _gaq.push(['hewlett._setDomainName', '.cnx.org']);
                            _gaq.push(['hewlett._trackPageview']);
            </script>
        <script type="text/javascript" id="user-google-analytics" user="UA-30227798-1"> 
                var thisElement;
                var codeGoogleAnalytics;
                thisElement = document.getElementById("user-google-analytics");
                if ( thisElement ) {
                  strGoogleAnalyticsTrackingCode = thisElement.getAttribute('user');
                  if ( strGoogleAnalyticsTrackingCode ) {
                    trackthisGoogleAnalytics(strGoogleAnalyticsTrackingCode);
                  }
                }
              </script>


bibliography
------------

http://cnx.org/help/reference/GoogleAnalyticsTrackingCode
